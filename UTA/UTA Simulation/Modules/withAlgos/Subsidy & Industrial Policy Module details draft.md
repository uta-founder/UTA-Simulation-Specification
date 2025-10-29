# Subsidy & Industrial Policy Module

## Purpose & Scope

The Subsidy & Industrial Policy Module models government interventions in production and trade, including production subsidies, export subsidies, R&D support, capital subsidies, preferential procurement, and strategic industrial targeting. It calculates how these policies affect cost structures, competitiveness, market shares, and overall economic welfare. This module also tracks the fiscal costs of policies, their effectiveness in achieving strategic objectives, and their detection by the Compliance Module.

Industrial policy is a core strategic tool in the UTA framework—countries use subsidies to build strategic industries, gain market share, or retaliate against competitors. The module must capture both the direct cost-reduction effects and the indirect equilibrium impacts through price changes and trade flows.

## Key Components

### 1. Subsidy Types
- **Production Subsidies**: Per-unit or ad valorem support for domestic production
- **Export Subsidies**: Support conditional on exporting (WTO-restricted)
- **R&D Subsidies**: Support for innovation and technology development
- **Capital Subsidies**: Reduced cost of capital investment (tax credits, low-interest loans)
- **Input Subsidies**: Reduced prices for key inputs (energy, materials)

### 2. Policy Instruments
- **Direct Transfers**: Cash payments to producers
- **Tax Incentives**: Corporate tax reductions, accelerated depreciation
- **Preferential Loans**: Below-market interest rates
- **Public Procurement**: Government purchases at premium prices
- **State Ownership**: Direct production by government entities

### 3. Competitiveness Metrics
- **Unit Cost Index**: Cost relative to global benchmark
- **Revealed Comparative Advantage (RCA)**: Export share relative to world average
- **Market Share**: Domestic and export market penetration
- **Productivity Growth**: TFP changes from policy support

### 4. Detection and Compliance
- **Subsidy Transparency**: Reporting requirements
- **Hidden Subsidy Detection**: Finding concealed state support
- **Countervailing Duty Logic**: Tariffs offsetting subsidies
- **WTO Compliance** (if relevant to UTA framework)

## Data Structures

### Input Data
```python
class SubsidyPolicyInputs:
    # From Country Agents
    policy_budget: dict[country] -> float                    # Fiscal space for subsidies
    strategic_priorities: dict[country] -> list[product]     # Targeted industries
    subsidy_rates: dict[country][product] -> float           # Current subsidy levels

    # From Production/Firm Agents
    production_costs: dict[country][product] -> float        # Baseline marginal cost
    production_volumes: dict[country][product] -> float      # Output levels
    input_requirements: dict[country][product] -> dict[input -> float]

    # From Trade Flow Module
    export_volumes: dict[exporter][product] -> float
    import_volumes: dict[importer][product] -> float
    market_share: dict[country][market][product] -> float

    # From Pricing Module
    domestic_prices: dict[country][product] -> float
    world_prices: dict[product] -> float                     # Benchmark prices

    # Historical Data
    subsidy_history: dict[country][product] -> list[float]   # Past subsidy levels
    effectiveness_history: dict[country][product] -> list[float]
```

### Internal State
```python
class SubsidyPolicyState:
    # Active Policies
    production_subsidies: dict[country][product] -> {
        'rate': float,                                       # Per-unit or % subsidy
        'type': enum[PER_UNIT, AD_VALOREM],
        'start_date': int,
        'duration': int or None,
        'budget_allocated': float,
        'budget_spent': float
    }

    export_subsidies: dict[country][product] -> {
        'rate': float,
        'conditionality': str,                               # e.g., "exports > threshold"
        'budget': float
    }

    r_and_d_support: dict[country][sector] -> {
        'annual_funding': float,
        'productivity_boost': float,                         # TFP multiplier
        'lead_time': int                                     # Periods until effect
    }

    capital_support: dict[country][product] -> {
        'interest_rate_subsidy': float,                      # Basis points reduction
        'depreciation_acceleration': float,
        'investment_tax_credit': float
    }

    # Derived Effects
    effective_marginal_costs: dict[country][product] -> float    # MC after subsidies
    competitiveness_index: dict[country][product] -> float       # Relative to world
    fiscal_cost: dict[country] -> float                         # Total subsidy spending

    # Detection State
    declared_subsidies: dict[country][product] -> float
    estimated_hidden_subsidies: dict[country][product] -> float
    transparency_score: dict[country] -> float                   # 0-1 reporting quality
```

### Output Data
```python
class SubsidyPolicyOutputs:
    # For Pricing Module
    cost_adjustments: dict[country][product] -> float        # Subsidy-induced cost reduction
    effective_marginal_costs: dict[country][product] -> float

    # For Trade Flow Module
    competitiveness_changes: dict[country][product] -> float
    export_incentive_effects: dict[country][product] -> float

    # For Country Agents
    fiscal_burden: dict[country] -> float                    # Budget spent on subsidies
    industrial_strength: dict[country][sector] -> float      # Strategic capacity
    roi_on_subsidies: dict[country][product] -> float        # Benefit / Cost

    # For Compliance Module
    subsidy_registry: dict[country][product] -> {
        'amount': float,
        'type': str,
        'transparency': float,
        'detection_likelihood': float
    }

    # Welfare Metrics
    producer_surplus_gain: dict[country][product] -> float
    consumer_surplus_impact: dict[country] -> float          # From price changes
    deadweight_loss: dict[country] -> float                  # Inefficiency cost
```

## Economic Logic

### 1. Production Subsidy Impact

**Per-Unit Subsidy**:
```python
def apply_production_subsidy_per_unit(marginal_cost, subsidy_per_unit):
    """
    Reduce marginal cost by fixed amount per unit

    MC_effective = MC_baseline - s

    Where:
    - MC_baseline = Original marginal cost
    - s = Per-unit subsidy
    - MC_effective = New marginal cost faced by producer
    """
    effective_mc = marginal_cost - subsidy_per_unit

    # Ensure non-negative cost
    effective_mc = max(effective_mc, 0.01)

    return effective_mc
```

**Ad Valorem Subsidy**:
```python
def apply_production_subsidy_ad_valorem(marginal_cost, subsidy_rate):
    """
    Reduce marginal cost by percentage

    MC_effective = MC_baseline * (1 - σ)

    Where:
    - σ = Ad valorem subsidy rate (e.g., 0.20 for 20% subsidy)
    """
    effective_mc = marginal_cost * (1 - subsidy_rate)

    return effective_mc
```

### 2. Competitiveness Index Calculation

```python
def calculate_competitiveness_index(country, product, world_state):
    """
    Measure competitiveness relative to global benchmark

    CI[j,p] = MC_world[p] / MC[j,p]

    Where:
    - CI > 1: Country j is more competitive than world average
    - CI < 1: Country j is less competitive
    - CI = 1: Equal to world average
    """
    # Calculate world average marginal cost (production-weighted)
    world_production = sum([
        world_state.production[c][product]
        for c in world_state.countries
    ])

    world_avg_mc = sum([
        (world_state.production[c][product] / world_production) *
        world_state.marginal_costs[c][product]
        for c in world_state.countries
    ])

    # Country-specific marginal cost
    country_mc = world_state.effective_marginal_costs[country][product]

    # Competitiveness index
    competitiveness = world_avg_mc / country_mc

    return competitiveness
```

### 3. Market Share Impact

**Subsidy Pass-Through to Market Share**:
```python
def estimate_market_share_impact(country, product, subsidy_rate, elasticity, world_state):
    """
    Estimate how subsidy translates to market share gain

    Theory: Lower cost → lower price → higher demand → higher market share

    ΔMS[j,p] = MS_0[j,p] * (ΔP/P) * η

    Where:
    - MS_0 = Initial market share
    - ΔP/P = Price reduction from subsidy
    - η = Market share elasticity with respect to price
    """
    # Initial market share
    initial_share = world_state.market_share[country][product]

    # Price reduction from subsidy (assuming full pass-through)
    price_reduction_pct = subsidy_rate

    # Market share elasticity (typically 2-4)
    market_share_elasticity = elasticity

    # Estimated market share gain
    market_share_change = initial_share * price_reduction_pct * market_share_elasticity

    # New market share (bounded by [0,1])
    new_market_share = min(initial_share + market_share_change, 1.0)

    return new_market_share
```

### 4. Fiscal Cost Calculation

```python
def calculate_fiscal_cost(country, subsidy_policies, production, exports):
    """
    Total government spending on subsidies

    Fiscal Cost = Σ[p] (s[p] * X[p]) + Σ[p] (s_export[p] * Exports[p])

    Where:
    - s[p] = Production subsidy per unit
    - s_export[p] = Export subsidy per unit
    - X[p] = Production volume
    """
    total_cost = 0

    # Production subsidies
    for product in products:
        subsidy_rate = subsidy_policies.production_subsidies[country][product]['rate']
        subsidy_type = subsidy_policies.production_subsidies[country][product]['type']
        production_volume = production[country][product]

        if subsidy_type == 'PER_UNIT':
            cost = subsidy_rate * production_volume
        elif subsidy_type == 'AD_VALOREM':
            marginal_cost = world_state.marginal_costs[country][product]
            cost = subsidy_rate * marginal_cost * production_volume

        total_cost += cost

    # Export subsidies
    for product in products:
        if country in subsidy_policies.export_subsidies:
            export_subsidy = subsidy_policies.export_subsidies[country][product]['rate']
            export_volume = exports[country][product]
            total_cost += export_subsidy * export_volume

    return total_cost
```

### 5. Return on Investment (ROI) Metrics

```python
def calculate_subsidy_roi(country, product, subsidy_cost, benefits):
    """
    Measure effectiveness of subsidy spending

    ROI = (Market Share Gain + Producer Surplus Gain + Strategic Value) / Fiscal Cost

    High ROI (> 2): Effective subsidy
    Low ROI (< 0.5): Wasteful subsidy
    """
    # Market share value (increased export revenue)
    market_share_gain_value = benefits['market_share_gain'] * benefits['average_price'] * benefits['market_size']

    # Producer surplus (profit increase for domestic firms)
    producer_surplus_gain = benefits['producer_surplus']

    # Strategic value (non-monetary benefits)
    strategic_value = benefits['strategic_importance'] * benefits['capacity_built']

    # Total benefits
    total_benefits = market_share_gain_value + producer_surplus_gain + strategic_value

    # ROI
    roi = total_benefits / max(subsidy_cost, 1e-6)

    return roi
```

### 6. Hidden Subsidy Detection

```python
def detect_hidden_subsidies(country, product, world_state):
    """
    Identify undeclared subsidies through cost-price anomalies

    Detection signals:
    1. Price < Marginal Cost (sustained losses impossible without subsidy)
    2. Rapid capacity expansion without commensurate investment
    3. Export prices < domestic prices (dumping signal)
    4. Input costs anomalously low
    """
    flags = []

    # Signal 1: Below-cost pricing
    price = world_state.prices[country][product]
    declared_mc = world_state.declared_marginal_costs[country][product]

    if price < declared_mc * 0.95:  # Sustained 5%+ loss
        implied_subsidy = declared_mc - price
        flags.append({
            'type': 'below_cost_pricing',
            'estimated_subsidy': implied_subsidy,
            'confidence': 0.7
        })

    # Signal 2: Capacity expansion without investment
    capacity_growth = world_state.capacity_growth[country][product]
    capex = world_state.capital_expenditure[country][product]
    typical_capex_ratio = world_state.industry_benchmarks['capex_per_capacity'][product]

    if capacity_growth > 0.1 and capex < capacity_growth * typical_capex_ratio * 0.5:
        implied_capital_subsidy = (capacity_growth * typical_capex_ratio - capex)
        flags.append({
            'type': 'hidden_capital_subsidy',
            'estimated_subsidy': implied_capital_subsidy,
            'confidence': 0.6
        })

    # Signal 3: Export dumping
    export_price = world_state.export_prices[country][product]
    domestic_price = world_state.domestic_prices[country][product]

    if export_price < domestic_price * 0.95:
        implied_export_subsidy = domestic_price - export_price
        flags.append({
            'type': 'export_dumping',
            'estimated_subsidy': implied_export_subsidy,
            'confidence': 0.8
        })

    return flags
```

### 7. Countervailing Duty Calculation

```python
def calculate_countervailing_duty(exporter, importer, product, estimated_subsidy, world_state):
    """
    Calculate offsetting tariff to neutralize subsidy advantage

    CVD = s[exporter, product] / P[exporter, product]

    Where:
    - s = Estimated subsidy per unit
    - P = Export price
    - CVD = Countervailing duty rate (ad valorem)
    """
    export_price = world_state.export_prices[exporter][product]
    subsidy_per_unit = estimated_subsidy

    # Ad valorem equivalent
    cvd_rate = subsidy_per_unit / export_price

    # Apply with cap (typically 25-50% maximum)
    cvd_rate_capped = min(cvd_rate, world_state.params['max_cvd_rate'])

    return cvd_rate_capped
```

## Integration Points

### Inputs From Other Modules

1. **From Country Agents**:
   - Fiscal budget available for subsidies
   - Strategic priorities (which industries to support)
   - Political constraints on subsidy visibility

2. **From Production/Firm Agents**:
   - Baseline production costs
   - Production volumes
   - Capacity expansion plans

3. **From Trade Flow Module**:
   - Export volumes and destinations
   - Market shares by destination
   - Import competition levels

4. **From Pricing & Equilibrium Module**:
   - Market prices
   - Marginal costs
   - Equilibrium quantities

5. **From Compliance Module**:
   - Detection of hidden subsidies
   - Transparency requirements
   - Penalty risks

### Outputs To Other Modules

1. **To Pricing & Equilibrium Module**:
   - Adjusted marginal costs (MC - subsidy)
   - Cost shocks from policy changes
   - Supply shifts from subsidies

2. **To Trade Flow Module**:
   - Competitiveness changes affecting trade
   - Export subsidy effects
   - Market share targets

3. **To Country Agents**:
   - Fiscal costs of policies
   - ROI metrics for subsidy decisions
   - Strategic industry development status

4. **To Compliance Module**:
   - Declared subsidy registry
   - Transparency scores
   - Detection signals for hidden support

5. **To Sanctions & Geopolitics Module**:
   - Subsidy disputes (trigger for retaliation)
   - WTO violation signals
   - Countervailing duty justifications

## Implementation Guidance

### Algorithm Flow

```python
def update_subsidy_policies(world_state):
    """Main subsidy and industrial policy update cycle"""

    # Step 1: Process policy decisions from country agents
    for country in world_state.countries:
        new_policies = country.policy_decisions.subsidies

        for policy in new_policies:
            if policy.type == 'production_subsidy':
                implement_production_subsidy(country, policy, world_state)
            elif policy.type == 'export_subsidy':
                implement_export_subsidy(country, policy, world_state)
            elif policy.type == 'r_and_d':
                implement_r_and_d_support(country, policy, world_state)

    # Step 2: Calculate effective marginal costs
    for country in world_state.countries:
        for product in world_state.products:
            baseline_mc = world_state.baseline_marginal_costs[country][product]

            # Apply production subsidy
            if country in world_state.subsidy_state.production_subsidies:
                subsidy = world_state.subsidy_state.production_subsidies[country][product]
                if subsidy['type'] == 'PER_UNIT':
                    effective_mc = baseline_mc - subsidy['rate']
                elif subsidy['type'] == 'AD_VALOREM':
                    effective_mc = baseline_mc * (1 - subsidy['rate'])
            else:
                effective_mc = baseline_mc

            world_state.effective_marginal_costs[country][product] = max(effective_mc, 0.01)

    # Step 3: Calculate competitiveness indices
    competitiveness = {}
    for country in world_state.countries:
        competitiveness[country] = {}
        for product in world_state.products:
            competitiveness[country][product] = calculate_competitiveness_index(
                country, product, world_state
            )

    # Step 4: Estimate market share impacts
    market_share_changes = {}
    for country in world_state.countries:
        for product in world_state.products:
            if country in world_state.subsidy_state.production_subsidies:
                subsidy_rate = world_state.subsidy_state.production_subsidies[country][product]['rate']
                market_share_changes[country][product] = estimate_market_share_impact(
                    country, product, subsidy_rate,
                    world_state.params['market_share_elasticity'][product],
                    world_state
                )

    # Step 5: Calculate fiscal costs
    fiscal_costs = {}
    for country in world_state.countries:
        fiscal_costs[country] = calculate_fiscal_cost(
            country,
            world_state.subsidy_state,
            world_state.production,
            world_state.exports
        )

    # Step 6: Detect hidden subsidies
    hidden_subsidy_flags = {}
    for country in world_state.countries:
        hidden_subsidy_flags[country] = {}
        for product in world_state.products:
            flags = detect_hidden_subsidies(country, product, world_state)
            if flags:
                hidden_subsidy_flags[country][product] = flags

    # Step 7: Calculate ROI for active subsidies
    subsidy_roi = {}
    for country in world_state.countries:
        subsidy_roi[country] = {}
        for product in world_state.products:
            if country in world_state.subsidy_state.production_subsidies:
                subsidy_cost = fiscal_costs[country] # (allocate to product)
                benefits = calculate_subsidy_benefits(country, product, world_state)
                subsidy_roi[country][product] = calculate_subsidy_roi(
                    country, product, subsidy_cost, benefits
                )

    # Step 8: Update state
    world_state.subsidy_state.effective_marginal_costs = world_state.effective_marginal_costs
    world_state.subsidy_state.competitiveness_index = competitiveness
    world_state.subsidy_state.fiscal_cost = fiscal_costs

    return SubsidyPolicyOutputs(
        cost_adjustments=world_state.effective_marginal_costs,
        competitiveness_changes=competitiveness,
        fiscal_burden=fiscal_costs,
        subsidy_registry=world_state.subsidy_state.production_subsidies,
        hidden_subsidy_flags=hidden_subsidy_flags,
        roi_metrics=subsidy_roi
    )
```

### Computational Considerations

1. **Subsidy Pass-Through**:
   - Not all subsidies reduce prices (some go to profits)
   - Model pass-through rate empirically (typically 50-80%)

2. **Dynamic Effects**:
   - R&D subsidies have lag before productivity boost
   - Capital subsidies affect future capacity

3. **Equilibrium Feedback**:
   - Subsidies shift supply, which changes equilibrium prices
   - This changes everyone's competitiveness (general equilibrium effect)

4. **Fiscal Constraints**:
   - Subsidy spending limited by budget
   - Opportunity cost of subsidies (foregone spending elsewhere)

## Calibration Requirements

### Required Data Sources

1. **Subsidy Data**:
   - OECD Producer Support Estimates
   - WTO subsidy notifications
   - IMF fiscal monitor (government support programs)
   - Academic studies on industrial policy effectiveness

2. **Cost Structure**:
   - Firm-level production costs from industry surveys
   - Input-output tables for intermediate costs
   - Energy prices and factor costs

3. **Effectiveness Parameters**:
   - Elasticity of market share to cost changes
   - Pass-through rates of subsidies to prices
   - ROI estimates from policy evaluations

### Key Parameters to Calibrate

```python
SUBSIDY_POLICY_CALIBRATION = {
    # Pass-through rates (how much subsidy reduces price)
    'subsidy_pass_through': {
        'competitive_sector': 0.80,      # 80% passes to consumers
        'oligopoly': 0.50,               # 50% retained as profit
        'monopoly': 0.20                 # 20% passes through
    },

    # Market share elasticity
    'market_share_elasticity': {
        'commodities': 4.0,              # Very responsive
        'differentiated': 2.0,           # Moderate
        'strategic': 1.0                 # Less responsive
    },

    # R&D effectiveness
    'r_and_d_productivity_boost': {
        'low_effectiveness': 0.05,       # 5% TFP gain per $100M
        'medium_effectiveness': 0.10,
        'high_effectiveness': 0.20
    },
    'r_and_d_lag': 3,                    # Periods before effect

    # Detection parameters
    'hidden_subsidy_detection_threshold': {
        'below_cost_pricing': 0.05,      # 5% sustained loss triggers flag
        'capacity_expansion': 0.5,       # 50% below normal capex ratio
        'export_dumping': 0.05          # 5% below domestic price
    },

    # Countervailing duty caps
    'max_cvd_rate': 0.50,                # 50% maximum tariff

    # Fiscal limits
    'max_subsidy_gdp_share': 0.03       # 3% of GDP maximum
}
```

### Validation Metrics

1. **Cost Impact**: Subsidies reduce effective MC by declared amount
2. **Market Share Consistency**: Predicted vs actual market share changes R² > 0.6
3. **Fiscal Accounting**: Total subsidy spending = Σ (subsidy rate × volume)
4. **Detection Accuracy**: Hidden subsidy detection rate > 60%
5. **ROI Plausibility**: Average ROI between 0.5 and 3.0 (reasonable range)