# Sanctions & Geopolitics Module

## Purpose & Scope

The Sanctions & Geopolitics Module models the strategic layer of international economic relations, including trade restrictions, alliance dynamics, retaliatory measures, and geopolitical constraints. It captures how countries use economic tools for political objectives, form coalitions, and navigate the tension between economic interdependence and strategic autonomy. The module generates policy decisions based on game-theoretic reasoning and tracks reputation, credibility, and escalation dynamics.

This module bridges economic simulation with strategic behavior, ensuring that trade policies reflect not just economic optimization but also security concerns, alliance obligations, and power projection. It models both unilateral actions (sanctions, tariffs) and multilateral coordination (trade blocs, collective sanctions).

## Key Components

### 1. Sanctions Engine
- **Sanction Types**: Sectoral, entity-specific, financial, technology transfer
- **Implementation Mechanisms**: Full embargo, partial restrictions, licensing requirements
- **Enforcement Levels**: Strict, moderate, symbolic
- **Secondary Sanctions**: Pressure on third parties

### 2. Alliance & Bloc Management
- **Coalition Formation**: Economic blocs, security alliances, sanctions coalitions
- **Burden Sharing**: Cost distribution among allies
- **Free Riding Detection**: Monitoring compliance within coalitions
- **Preference Alignment**: Measuring policy convergence

### 3. Retaliation Framework
- **Tit-for-Tat Logic**: Proportional response mechanisms
- **Escalation Ladders**: Graduated response options
- **De-escalation Pathways**: Face-saving exits and negotiations
- **Asymmetric Responses**: Non-reciprocal countermeasures

### 4. Geopolitical Constraints
- **Red Lines**: Non-negotiable security interests
- **Sphere of Influence**: Regional hegemony dynamics
- **Strategic Dependencies**: Critical supply vulnerabilities
- **Reputation Management**: Credibility and deterrence

## Data Structures

### Input Data
```python
class GeopoliticsInputs:
    # Bilateral Relations
    diplomatic_distance: dict[country_i][country_j] -> float  # 0=allied, 1=hostile
    security_alliances: list[set[countries]]                  # NATO, CSTO, etc.
    economic_blocs: list[set[countries]]                      # EU, ASEAN, etc.
    historical_conflicts: dict[(country_i, country_j)] -> list[dispute]

    # Strategic Interests
    red_lines: dict[country] -> list[issue]                   # Non-negotiable positions
    strategic_resources: dict[country][product] -> float      # Dependency level
    military_capability: dict[country] -> float               # Power projection

    # Economic Leverage
    trade_dependence: dict[country_i][country_j] -> float     # Trade/GDP ratio
    financial_exposure: dict[country_i][country_j] -> float   # Investment stocks
    technology_dependence: dict[country][tech_provider] -> float

    # From Economic Modules
    trade_flows: dict[exporter][importer][product] -> float
    market_share: dict[country][market][product] -> float
    gdp: dict[country] -> float
```

### Internal State
```python
class GeopoliticsState:
    # Active Sanctions
    sanctions_registry: list[Sanction]  where Sanction = {
        'sender': country,
        'target': country,
        'type': enum[SECTORAL, FINANCIAL, TECHNOLOGY, COMPREHENSIVE],
        'scope': list[products/sectors],
        'severity': float,  # 0-1
        'start_date': int,
        'effectiveness': float,  # Actual impact vs intended
        'coalition': set[countries]  # Supporting countries
    }

    # Alliance Dynamics
    bloc_cohesion: dict[bloc] -> float  # 0-1, unity level
    alliance_commitments: dict[country][alliance] -> float  # Commitment strength

    # Reputation & Credibility
    reputation_score: dict[country] -> float  # Reliability as partner
    deterrence_credibility: dict[country] -> float  # Threat credibility
    sanction_effectiveness_history: dict[country] -> list[float]

    # Escalation Tracking
    tension_matrix: dict[country_i][country_j] -> float  # Current tension level
    escalation_stage: dict[(country_i, country_j)] -> int  # Ladder position
    recent_actions: list[GeopoliticalAction]  # For retaliation calculation

    # Strategic Positioning
    influence_score: dict[country][region] -> float
    alignment_matrix: dict[country_i][country_j] -> float  # Policy similarity
```

### Output Data
```python
class GeopoliticsOutputs:
    # Policy Decisions
    new_sanctions: list[Sanction]
    lifted_sanctions: list[Sanction]
    tariff_changes: dict[country][partner][product] -> float
    trade_agreements: list[Agreement]

    # Strategic Signals
    escalation_risk: dict[(country_i, country_j)] -> float
    coalition_stability: dict[bloc] -> float
    retaliation_probability: dict[country][action] -> float

    # Economic Impacts
    sanction_costs: dict[sender] -> float  # Cost to sender
    sanction_damage: dict[target] -> float  # Damage to target
    third_party_effects: dict[country] -> float  # Collateral damage

    # For Other Modules
    trade_restrictions: dict[importer][exporter][product] -> bool
    tariff_schedule: dict[importer][exporter][product] -> float
    risk_premiums: dict[country] -> float  # Political risk markup
```

## Economic Logic

### 1. Sanction Decision Calculus

**Expected Utility Framework**:
```python
def evaluate_sanction_decision(sender, target, sanction_type, params):
    # Benefits
    political_gain = calculate_political_value(
        sender.objectives,
        target.behavior_change_probability,
        sender.domestic_support
    )

    # Costs
    economic_cost = calculate_economic_damage(
        sender.trade_exposure[target],
        sanction_type.trade_impact,
        sender.substitution_capacity
    )

    reputation_cost = calculate_reputation_impact(
        sanction_type.legitimacy,
        international_support,
        sender.past_sanctions
    )

    # Probability of success
    success_probability = estimate_success_rate(
        sender.economic_leverage[target],
        target.resilience,
        coalition_size,
        sanction_type.severity
    )

    expected_utility = (political_gain * success_probability -
                       economic_cost - reputation_cost)

    return expected_utility > sender.sanction_threshold
```

### 2. Coalition Formation Game

**Coalition Stability Condition (Core)**:
```
V(C) ≥ Σ[i∈C] V({i})  # Coalition value exceeds sum of individual values

Where:
- V(C) = Total value of coalition C
- V({i}) = Value country i can achieve alone

Shapley Value allocation:
φ[i] = Σ[S⊆N\{i}] [|S|!(|N|-|S|-1)!/|N|!] * [V(S∪{i}) - V(S)]
```

### 3. Retaliation Game Theory

**Tit-for-Tat with Forgiveness**:
```python
def determine_retaliation(action_against_us, our_strategy, history):
    if our_strategy == 'tit_for_tat':
        # Match opponent's action
        retaliation_level = action_against_us.severity

        # Add noise/forgiveness to prevent spirals
        if random.random() < params['forgiveness_probability']:
            retaliation_level *= params['de_escalation_factor']

    elif our_strategy == 'massive_retaliation':
        # Disproportionate response for deterrence
        retaliation_level = min(
            action_against_us.severity * params['escalation_multiplier'],
            our_maximum_damage_capability
        )

    elif our_strategy == 'graduated_response':
        # Incremental escalation
        previous_level = history.get_last_retaliation_level()
        retaliation_level = previous_level + params['escalation_step']

    return select_retaliation_action(retaliation_level)
```

### 4. Alliance Burden Sharing

**Olson-Zeckhauser Model**:
```python
def calculate_burden_sharing(alliance, threat_level):
    total_contribution = 0
    contributions = {}

    for member in alliance.members:
        # Larger members contribute disproportionately
        optimal_contribution = (member.gdp / alliance.total_gdp) ** params['power_factor']

        # Adjust for free-riding incentive
        free_riding_factor = 1 - params['free_riding_rate'] * (1 - member.vulnerability)

        contributions[member] = optimal_contribution * free_riding_factor * threat_level
        total_contribution += contributions[member]

    # Check if alliance holds
    alliance_stability = total_contribution >= alliance.minimum_deterrence

    return contributions, alliance_stability
```

### 5. Reputation Dynamics

**Reputation Update Function**:
```python
def update_reputation(country, action, outcome):
    # Base reputation decay
    country.reputation *= params['reputation_decay']

    # Action-based update
    if action.type == 'impose_sanction':
        if outcome == 'success':
            country.reputation += params['successful_enforcement_bonus']
            country.deterrence_credibility += params['credibility_gain']
        else:
            country.reputation -= params['failed_enforcement_penalty']
            country.deterrence_credibility -= params['credibility_loss']

    elif action.type == 'violate_agreement':
        country.reputation -= params['violation_penalty']
        country.trustworthiness *= params['trust_damage_multiplier']

    elif action.type == 'honor_commitment':
        country.reputation += params['reliability_bonus']

    # Bound reputation
    country.reputation = max(0, min(1, country.reputation))
```

### 6. Strategic Resource Dependencies

**Vulnerability Assessment**:
```python
def assess_strategic_vulnerability(country, product):
    # Import dependence
    import_share = imports[country][product] / total_consumption[country][product]

    # Concentration risk
    herfindahl_index = sum([
        (imports_from[supplier] / total_imports) ** 2
        for supplier in suppliers
    ])

    # Substitutability
    substitution_difficulty = 1 / product.elasticity_of_substitution

    # Strategic importance
    criticality = product.strategic_importance * product.defense_relevance

    vulnerability_score = (import_share * herfindahl_index *
                          substitution_difficulty * criticality)

    return vulnerability_score
```

## Integration Points

### Inputs From Other Modules

1. **From Trade Flow Module**:
   - Current bilateral trade volumes
   - Trade route dependencies
   - Alternative suppliers availability

2. **From Country Agents**:
   - National objectives and priorities
   - Risk tolerance parameters
   - Domestic political constraints

3. **From Pricing & Equilibrium Module**:
   - Economic impact of trade restrictions
   - Market share changes from sanctions
   - Price effects of supply disruptions

4. **From Energy & Logistics Module**:
   - Critical infrastructure vulnerabilities
   - Energy supply dependencies
   - Transportation chokepoints

5. **From Compliance Module**:
   - Sanction violation detection
   - Circumvention evidence
   - Enforcement effectiveness

### Outputs To Other Modules

1. **To Trade Flow Module**:
   - Prohibited trade flows (sanctions)
   - Tariff rates by country-pair-product
   - Quota restrictions

2. **To Country Agents**:
   - Available policy actions
   - Reputation scores
   - Alliance obligations

3. **To Pricing & Equilibrium Module**:
   - Supply shocks from sanctions
   - Risk premiums for political instability
   - Trade policy uncertainty effects

4. **To Compliance & Detection Module**:
   - Sanctions to monitor
   - Coalition enforcement priorities
   - Legitimacy scores for enforcement

## Implementation Guidance

### Algorithm Flow

```python
def update_geopolitics(world_state):
    """Main geopolitical dynamics update"""

    # Step 1: Assess current situation
    for country in world_state.countries:
        country.threat_assessment = evaluate_threats(
            country,
            world_state.tension_matrix,
            world_state.recent_actions
        )

        country.opportunity_assessment = identify_opportunities(
            country,
            world_state.alliance_dynamics,
            world_state.economic_leverage
        )

    # Step 2: Generate policy options
    policy_options = {}
    for country in world_state.countries:
        options = []

        # Sanction decisions
        if country.threat_assessment.requires_response:
            options.extend(generate_sanction_options(
                country,
                country.threat_assessment.source,
                world_state.coalition_possibilities
            ))

        # Alliance decisions
        if country.opportunity_assessment.alliance_beneficial:
            options.extend(generate_alliance_options(
                country,
                world_state.potential_partners
            ))

        # Retaliation decisions
        if country in world_state.recent_targets:
            options.extend(generate_retaliation_options(
                country,
                world_state.recent_actions_against[country]
            ))

        policy_options[country] = options

    # Step 3: Strategic decision making
    decisions = {}
    for country in world_state.countries:
        # Game-theoretic evaluation
        best_response = find_nash_equilibrium(
            country,
            policy_options[country],
            expected_responses(world_state.countries, country)
        )

        decisions[country] = best_response

    # Step 4: Implement decisions
    for country, decision in decisions.items():
        if decision.type == 'impose_sanction':
            implement_sanction(decision, world_state)
        elif decision.type == 'form_alliance':
            form_alliance(decision, world_state)
        elif decision.type == 'retaliate':
            execute_retaliation(decision, world_state)

    # Step 5: Update reputation and relationships
    update_reputation_scores(world_state, decisions)
    update_bilateral_relations(world_state, decisions)
    update_tension_matrix(world_state)

    # Step 6: Check for escalation/de-escalation
    manage_escalation_dynamics(world_state)

    return world_state.geopolitics_state
```

### Computational Considerations

1. **Game Theory Solvers**:
   - Use backward induction for sequential games
   - Implement iterative best response for simultaneous games
   - Cache equilibrium solutions for common scenarios

2. **Coalition Formation**:
   - Use cooperative game theory algorithms
   - Implement Shapley value for fair allocation
   - Check core conditions for stability

3. **Belief Updates**:
   - Bayesian updating for reputation
   - Kalman filters for continuous variables
   - Decay functions for historical memory

4. **Scenario Generation**:
   - Monte Carlo for uncertainty
   - Minimax for worst-case planning
   - Robust optimization for strategic decisions

## Calibration Requirements

### Required Data Sources

1. **Diplomatic Relations**:
   - UN voting similarity indices
   - Alliance membership data (NATO, CSTO, etc.)
   - Bilateral trade agreements database
   - Historical conflict data (GDELT, ICEWS)

2. **Sanctions Data**:
   - Global Sanctions Database (GSDB)
   - US Treasury OFAC sanctions
   - EU consolidated sanctions list
   - UN Security Council sanctions

3. **Economic Interdependence**:
   - Bilateral trade from UN Comtrade
   - FDI stocks from UNCTAD
   - Technology trade from OECD

4. **Strategic Resources**:
   - Critical minerals assessments
   - Energy trade from IEA
   - Food security from FAO
   - Defense industrial base reports

### Key Parameters to Calibrate

```python
GEOPOLITICS_CALIBRATION = {
    # Sanction Effectiveness
    'sanction_success_rate': {
        'comprehensive': 0.35,         # Full embargo success rate
        'targeted': 0.25,              # Smart sanctions success
        'sectoral': 0.30,              # Sector-specific success
        'symbolic': 0.10               # Minimal actual impact
    },

    # Coalition Parameters
    'coalition_bonus': 1.5,            # Effectiveness multiplier
    'free_riding_rate': 0.3,          # Typical free-riding level
    'coalition_fragmentation': 0.2,    # Probability of defection

    # Retaliation Parameters
    'retaliation_probability': 0.7,    # Base retaliation chance
    'escalation_ladder_steps': 5,      # Levels before war
    'de_escalation_probability': 0.3,  # Chance to step back
    'tit_for_tat_noise': 0.1,         # Forgiveness factor

    # Reputation Dynamics
    'reputation_decay': 0.95,          # Per period decay
    'credibility_half_life': 10,       # Periods to halve
    'violation_penalty': 0.3,          # Reputation loss
    'compliance_bonus': 0.1,           # Reputation gain

    # Strategic Thresholds
    'red_line_sensitivity': 0.9,       # Trigger probability
    'vulnerability_threshold': 0.6,     # When to diversify
    'alliance_threshold': 0.4,         # Minimum benefit to join

    # Economic Costs
    'sanction_deadweight_loss': 0.15,  # Economic efficiency loss
    'trade_diversion_cost': 0.25,      # Cost of new suppliers
    'reputation_economic_value': 0.05   # GDP impact of reputation
}
```

### Validation Metrics

1. **Sanction Prediction**: F1 score > 0.7 on historical sanctions
2. **Alliance Stability**: Predict alliance duration within 20%
3. **Escalation Dynamics**: Match historical escalation patterns
4. **Retaliation Timing**: Correct prediction rate > 65%
5. **Economic Impact**: Sanction costs within 30% of empirical estimates