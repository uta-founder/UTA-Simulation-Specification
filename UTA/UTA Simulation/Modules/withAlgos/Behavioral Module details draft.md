# Behavioral Module

## Purpose & Scope

The Behavioral Module governs how country agents learn, adapt, and make strategic decisions in the UTA simulation. It formalizes game-theoretic interactions, reputation dynamics, belief formation, and contagion effects that drive geopolitical and economic behavior. This module ensures agents don't just optimize static utility functions but exhibit realistic strategic behavior including learning from history, responding to reputation incentives, and coordinating or competing with other nations.

The module operates at three levels:
1. **Strategic Interaction**: Game-theoretic framework for multi-agent decisions
2. **Learning & Adaptation**: How agents update beliefs and strategies over time
3. **System Dynamics**: Network effects, contagion, and stability mechanisms

## Economic & Game-Theoretic Foundation

### 1. Strategic Interaction Framework

#### Core Game Matrices

The module models key strategic interactions as formal games with well-defined payoff structures:

**Trade War Game** (2-player, simultaneous move):
```
                Country B
                Free Trade    Protectionist
Country A:
Free Trade      (100, 100)   (60, 140)
Protectionist   (140, 60)    (80, 80)

Nash Equilibria:
- Pure strategy: (Protectionist, Protectionist) with payoff (80, 80)
- Mixed strategy: p(Free Trade) = 0.5 for symmetric players
- Pareto optimal: (Free Trade, Free Trade) with payoff (100, 100)

Prisoner's Dilemma structure → Suboptimal equilibrium without cooperation
```

**Currency War Game** (n-player, sequential move):
```
Strategy space: δ[i] ∈ [-0.2, 0.2] (devaluation rate)

Payoff function:
π[i] = Export_Gain[i](δ[i], δ[-i]) - Inflation_Cost[i](δ[i]) - Retaliation_Cost[i](δ[-i])

Where:
Export_Gain[i] = α * (δ[i] - mean(δ[-i])) * Export_Volume[i]
Inflation_Cost[i] = β * δ[i]^2 * GDP[i]
Retaliation_Cost[i] = γ * max(0, δ[i] - threshold) * Σ[j≠i] δ[j]

Parameters:
α = 0.3 (export competitiveness sensitivity)
β = 0.5 (inflation pass-through)
γ = 0.2 (retaliation intensity)
threshold = 0.05 (tolerance before retaliation)
```

**Sanctions Escalation Game** (2-player, extensive form):
```
Stage 1: Country A chooses sanction level s[A] ∈ [0, 1]
Stage 2: Country B observes s[A], chooses response s[B] ∈ [0, 1]
Stage 3: Both observe (s[A], s[B]), choose escalate/de-escalate

Payoff at stage t:
π[i,t] = -Economic_Cost[i](s[i,t]) - Damage_to_Target[i](s[j,t]) + Political_Gain[i](s[i,t])

Where:
Economic_Cost[i] = s[i,t]^2 * Trade_Exposure[i,j] * GDP[i]
Damage_to_Target[i] = s[j,t] * Vulnerability[j] * Effectiveness[i,j]
Political_Gain[i] = log(1 + s[i,t]) * Domestic_Support[i]

Subgame Perfect Equilibrium: Backward induction from terminal nodes
```

**Alliance Formation Game** (n-player, coalition game):
```
Value function for coalition S:
v(S) = Trade_Benefits(S) + Security_Benefits(S) - Coordination_Costs(S)

Where:
Trade_Benefits(S) = Σ[i,j∈S] Bilateral_Trade[i,j] * (1 + preferential_rate)
Security_Benefits(S) = sqrt(Σ[i∈S] Military_Power[i]) * threat_level
Coordination_Costs(S) = |S|^2 * heterogeneity(S) * coordination_friction

Shapley value for player i in coalition S:
φ[i] = Σ[T⊆S\{i}] (|T|!(|S|-|T|-1)!/|S|!) * (v(T∪{i}) - v(T))

Stability: Coalition S is stable if φ[i] ≥ v({i}) for all i ∈ S
```

### 2. Reputation System

Reputation affects future interaction costs and cooperation probability:

```
Reputation[i,t+1] = ρ * Reputation[i,t] + (1-ρ) * Observed_Behavior[i,t]

Where:
ρ = 0.85 (reputation persistence parameter)

Observed_Behavior[i,t] = weighted average of:
- Compliance_Rate[i,t] (weight: 0.4)
- Retaliation_Restraint[i,t] (weight: 0.2)
- Alliance_Loyalty[i,t] (weight: 0.2)
- Transparency_Score[i,t] (weight: 0.2)

Reputation ∈ [0, 100] with:
0-20: Pariah state (high transaction costs, limited cooperation)
20-40: Unreliable partner (risk premiums, conditional engagement)
40-60: Normal standing (standard interactions)
60-80: Trusted partner (preferential treatment, alliance invitations)
80-100: Exemplary leader (first-mover advantages, coalition leadership)
```

**Reputation Impact on Interactions**:
```
Effective_Tariff[i,j] = Base_Tariff[i,j] * (1 + max(0, (50 - Reputation[j])/100))
Alliance_Probability[i,j] = logistic((Reputation[i] + Reputation[j] - 80)/20)
Enforcement_Detection_Rate[i] = Base_Detection * (1 + (100 - Reputation[i])/200)
Credit_Cost_Multiplier[i] = 2 - Reputation[i]/100
```

### 3. Learning & Belief Formation

#### Fictitious Play for Strategy Selection
```
Belief[i,t](strategy[j]) = Count[t](j played strategy) / t

Best_Response[i,t+1] = argmax[s[i]] Σ[s[j]] Belief[i,t](s[j]) * Payoff[i](s[i], s[j])

With inertia:
P(play s[i] at t+1) = (1-ε) * 1{s[i] = Best_Response} + ε * P[t](s[i])
Where ε = 0.1 (exploration rate)
```

#### Q-Learning for Policy Optimization
```
State: s = (GDP_growth, Trade_balance, Reputation, Geopolitical_tension)
Action: a ∈ {Free_Trade, Moderate_Protection, High_Protection, Sanctions}

Q-value update:
Q[t+1](s,a) = Q[t](s,a) + α * (Reward + γ * max[a'] Q[t](s',a') - Q[t](s,a))

Where:
α = 0.1 (learning rate)
γ = 0.95 (discount factor)
Reward = ΔWelfare + Reputation_Change + Strategic_Objective_Progress
```

#### Adaptive Expectations
```
Expected_Price[i,t+1,p] = λ * Actual_Price[i,t,p] + (1-λ) * Expected_Price[i,t,p]
Where λ = 0.3 (adaptive parameter, higher = faster adaptation)

Expected_Retaliation[i,j,t+1] = Historical_Average[j] + β * Recent_Deviation[j,t]
Where β = 0.5 (recency bias parameter)
```

### 4. Behavioral Heuristics Library

Countries can adopt different behavioral strategies:

**Tit-for-Tat** (Reciprocal):
```
If partner[j] imposed tariff[t] = x%, then impose tariff[t+1] = x% on partner[j]
If partner[j] removed sanctions[t], then reduce sanctions[t+1] proportionally
Memory: 1 period
Reputation bonus: +5 per turn (seen as predictable/fair)
```

**Grim Trigger** (Punitive):
```
If partner[j] ever defects (tariff > threshold or sanctions), then:
  Permanent maximum retaliation (tariff = 100%, full embargo)
  No forgiveness regardless of partner behavior
Memory: Infinite
Reputation penalty: -2 per turn in punishment mode
```

**Tit-for-Two-Tats** (Forgiving):
```
Only retaliate after two consecutive defections
Forgive after one cooperation
Memory: 2 periods
Reputation bonus: +3 per turn (seen as patient/reasonable)
```

**Gradual** (Escalating):
```
Defection[n] triggers n periods of retaliation, then 2 periods of cooperation
Escalation: Linear in number of defections
Memory: Full history with decay
Reputation: Neutral
```

**Bandwagon** (Conformist):
```
If majority (>50%) of trade partners adopt policy X, adopt policy X
Threshold can be adjusted: Conservative (70%), Moderate (50%), Eager (30%)
Reputation: Follows group reputation trends
```

**Contrarian** (Strategic differentiation):
```
Deliberately choose opposite of majority strategy
Exploit market gaps when others converge
Risk: High variance in outcomes
Reputation: Volatile (+10 if successful, -10 if fails)
```

## Player-Facing Game Mechanics

### Turn Options for Behavioral Strategy

Each turn, players can select:

#### 1. Strategic Doctrine Selection
- **Choose primary behavioral strategy**: Tit-for-Tat, Grim Trigger, Gradual, etc.
- **Set trigger thresholds**: When to consider action as "defection"
- **Define response intensity**: Proportional, escalatory, or de-escalatory
- **Memory setting**: How long to remember past interactions (1 turn to infinite)

#### 2. Reputation Management
- **Transparency level**: Full disclosure, selective reporting, or opacity
- **Compliance signaling**: Publicly commit to rules (reputation investment)
- **Reputation repair actions**: Apologies, reparations, policy reversals
- **Strategic reputation damage**: Controlled reputation sacrifice for gains

#### 3. Learning Mode Configuration
- **Exploration vs exploitation**: Balance between trying new strategies vs optimizing known ones
- **Learning speed**: Fast adaptation (volatile) vs slow learning (stable)
- **Information sources**: Learn from own experience only vs observe all countries
- **Forecast horizon**: Short-term optimization vs long-term strategic planning

#### 4. Coalition & Alliance Behavior
- **Coalition formation strategy**: Lead, follow, or remain independent
- **Loyalty commitment level**: Binding agreements vs flexible alignment
- **Burden sharing rules**: Equal contribution vs capability-based
- **Exit conditions**: Define when to leave coalitions

#### 5. Escalation Management
- **Escalation ladder position**: De-escalate, maintain, controlled escalation, or rapid escalation
- **Red lines**: Define automatic response triggers
- **Off-ramps**: Conditions for backing down
- **Signaling intensity**: Clarity of threats and promises

## Implementation Specification

### Agent Decision Architecture

```python
class BehavioralAgent:
    def __init__(self, country_id, initial_strategy="tit_for_tat"):
        self.country_id = country_id
        self.strategy = initial_strategy
        self.reputation = 50.0  # Start neutral
        self.memory = {}  # History of interactions
        self.beliefs = {}  # Beliefs about other agents
        self.q_table = {}  # Q-learning values
        self.learning_rate = 0.1
        self.exploration_rate = 0.1

    def decide_action(self, state, available_actions):
        # Step 1: Update beliefs based on observations
        self.update_beliefs(state.observed_actions)

        # Step 2: Apply behavioral strategy
        if self.strategy == "tit_for_tat":
            action = self.tit_for_tat_logic(state.last_opponent_action)
        elif self.strategy == "grim_trigger":
            action = self.grim_trigger_logic(state.history)
        elif self.strategy == "q_learning":
            action = self.q_learning_select(state, available_actions)
        elif self.strategy == "fictitious_play":
            action = self.fictitious_play_select(state)

        # Step 3: Add exploration noise
        if random.random() < self.exploration_rate:
            action = random.choice(available_actions)

        # Step 4: Record decision
        self.memory[state.turn] = action

        return action

    def update_beliefs(self, observations):
        for country, action in observations.items():
            if country not in self.beliefs:
                self.beliefs[country] = {"action_history": [], "predicted_type": None}
            self.beliefs[country]["action_history"].append(action)
            self.beliefs[country]["predicted_type"] = self.infer_strategy_type(
                self.beliefs[country]["action_history"]
            )

    def update_reputation(self, behavior_scores):
        # Weighted average of behavior components
        compliance_score = behavior_scores["compliance_rate"] * 0.4
        restraint_score = behavior_scores["retaliation_restraint"] * 0.2
        loyalty_score = behavior_scores["alliance_loyalty"] * 0.2
        transparency_score = behavior_scores["transparency"] * 0.2

        observed_behavior = (compliance_score + restraint_score +
                           loyalty_score + transparency_score)

        # Exponential moving average update
        self.reputation = 0.85 * self.reputation + 0.15 * observed_behavior
        self.reputation = max(0, min(100, self.reputation))  # Bound [0,100]
```

### Network Propagation Mechanics

```python
class NetworkContagion:
    def __init__(self, adjacency_matrix, transmission_prob=0.3):
        self.network = adjacency_matrix  # Trade network connections
        self.transmission_prob = transmission_prob
        self.threshold = 0.5  # Activation threshold for adopting behavior

    def propagate_crisis(self, initial_shock, shock_type="financial"):
        affected = initial_shock.copy()
        iteration = 0

        while iteration < 10:  # Max 10 rounds of contagion
            new_affected = affected.copy()

            for country in range(len(self.network)):
                if affected[country] > 0:
                    continue  # Already affected

                # Calculate pressure from neighbors
                neighbor_pressure = 0
                for neighbor in range(len(self.network)):
                    if self.network[country][neighbor] > 0:  # Connected
                        weight = self.network[country][neighbor]  # Trade intensity
                        neighbor_pressure += affected[neighbor] * weight

                # Check if pressure exceeds threshold
                if neighbor_pressure > self.threshold:
                    contagion_strength = neighbor_pressure * self.transmission_prob

                    # Dampening based on country resilience
                    resilience = self.calculate_resilience(country, shock_type)
                    new_affected[country] = contagion_strength * (1 - resilience)

            # Check for convergence
            if sum(abs(new_affected[i] - affected[i]) for i in range(len(affected))) < 0.01:
                break

            affected = new_affected
            iteration += 1

        return affected

    def calculate_resilience(self, country, shock_type):
        if shock_type == "financial":
            return 0.3 + 0.5 * (country_reserves[country] / country_gdp[country])
        elif shock_type == "trade":
            return 0.2 + 0.3 * (1 - trade_openness[country])
        elif shock_type == "reputation":
            return 0.4 + 0.4 * (country_reputation[country] / 100)
```

### Stability Mechanisms

```python
class StabilityController:
    def __init__(self):
        self.warning_thresholds = {
            "price_volatility": 0.3,  # 30% price swing
            "trade_collapse": 0.5,     # 50% trade reduction
            "reputation_crisis": 20,    # Reputation below 20
            "cascade_size": 0.4        # 40% of countries affected
        }
        self.dampening_active = False

    def check_stability(self, state):
        warnings = []

        # Check price volatility
        price_volatility = self.calculate_volatility(state.price_history)
        if price_volatility > self.warning_thresholds["price_volatility"]:
            warnings.append(("price_instability", price_volatility))

        # Check trade volume
        trade_change = (state.current_trade - state.baseline_trade) / state.baseline_trade
        if trade_change < -self.warning_thresholds["trade_collapse"]:
            warnings.append(("trade_collapse", trade_change))

        # Check reputation crisis
        crisis_countries = sum(1 for r in state.reputations if r < 20)
        crisis_fraction = crisis_countries / len(state.reputations)
        if crisis_fraction > self.warning_thresholds["cascade_size"]:
            warnings.append(("reputation_crisis", crisis_fraction))

        return warnings

    def apply_dampening(self, state, warnings):
        for warning_type, severity in warnings:
            if warning_type == "price_instability":
                # Reduce price adjustment speed
                state.price_adjustment_rate *= 0.5
                # Add friction to arbitrage
                state.transaction_costs *= 1.5

            elif warning_type == "trade_collapse":
                # Inject liquidity through reduced tariffs
                state.emergency_tariff_reduction = 0.5
                # Relax quota constraints
                state.quota_flexibility = 2.0

            elif warning_type == "reputation_crisis":
                # Slow reputation decay
                state.reputation_decay_rate *= 0.5
                # Increase forgiveness rate
                state.reputation_recovery_rate *= 2.0

        self.dampening_active = True
        return state

    def calculate_volatility(self, price_history, window=10):
        if len(price_history) < window:
            return 0
        recent = price_history[-window:]
        mean = sum(recent) / len(recent)
        variance = sum((x - mean)**2 for x in recent) / len(recent)
        return (variance ** 0.5) / mean  # Coefficient of variation
```

## Calibration & Parameters

### Learning Parameters (from behavioral economics literature)

| Parameter | Value | Source | Rationale |
|-----------|-------|---------|-----------|
| Learning rate (α) | 0.1 | Camerer & Ho (1999) | Balance between stability and adaptation |
| Discount factor (γ) | 0.95 | Standard in trade models | Reflects ~5% annual discount rate |
| Exploration rate (ε) | 0.1 | Sutton & Barto (2018) | 10% experimentation maintains learning |
| Reputation decay (ρ) | 0.85 | Similar to credit ratings | ~15% quarterly depreciation |
| Adaptive expectations (λ) | 0.3 | Empirical inflation expectations | Moderate adaptation speed |

### Game-Theoretic Parameters (from empirical trade conflicts)

| Interaction | Cooperation Payoff | Defection Temptation | Punishment Payoff | Source |
|------------|-------------------|---------------------|------------------|---------|
| Trade War | 100 | 140 | 80 | US-China trade war (2018-2020) |
| Currency War | 0 (baseline) | +20% exports | -15% welfare | Plaza Accord (1985) |
| Sanctions | 0 (baseline) | Political gain +30 | -25% trade | Russia sanctions (2014-) |

### Contagion Parameters (from financial crisis literature)

| Parameter | Value | Calibration | Historical Example |
|-----------|-------|-------------|-------------------|
| Transmission probability | 0.3 | Asian Financial Crisis (1997) | Thailand → Indonesia: ~30% GDP shock transmission |
| Trade network threshold | 0.5 | Lehman Brothers (2008) | 50% exposure triggered defaults |
| Resilience factor | 0.2-0.8 | Varies by reserves/GDP | Singapore (0.8) vs Argentina (0.2) |
| Maximum cascade depth | 10 turns | Prevent infinite loops | Most crises stabilize within 2-3 quarters |

### Reputation Thresholds (from sovereign ratings)

| Reputation Range | Real-World Equivalent | Trade Cost Impact | Example Countries |
|-----------------|---------------------|------------------|------------------|
| 0-20 | Default/Pariah | +100% costs | North Korea, Venezuela (crisis) |
| 20-40 | Junk/High Risk | +50% costs | Argentina, Turkey (stressed) |
| 40-60 | Investment Grade | Baseline | Brazil, India, South Africa |
| 60-80 | Strong/Stable | -20% costs | South Korea, Chile |
| 80-100 | AAA/Reserve Currency | -40% costs | Switzerland, Singapore |

## Integration Points

### With Economic Modules

**Pricing & Market Equilibrium Module**:
- Behavioral expectations → Expected_Prices[t+1]
- Strategic withholding → Supply_Adjustment
- Reputation → Transaction_Costs

**Trade Flow Module**:
- Coalition membership → Preferential_Tariffs
- Retaliation triggers → Bilateral_Trade_Restrictions
- Trust level → Shipment_Insurance_Costs

**Demand Module**:
- Consumer confidence (f(reputation)) → Demand_Elasticity
- Expectations → Precautionary_Inventory
- Panic/Herding → Demand_Shocks

### With Policy Modules

**Sanctions & Geopolitics Module**:
- Game outcomes → Sanction_Decisions
- Reputation → Coalition_Formation_Probability
- Escalation ladder → Sanction_Intensity

**Compliance & Cheating Detection Module**:
- Reputation history → Prior_Probability_Cheating
- Learning → Detection_Algorithm_Updates
- Strategic deception → False_Signal_Generation

**Subsidy & Industrial Policy Module**:
- Strategic rivalry → Subsidy_Wars
- Learning → Optimal_Subsidy_Discovery
- Reputation → WTO_Compliance_Pressure

### With Agent Intelligence

**Strategy Generation**:
- Q-values → Suggested_Actions
- Belief state → Situation_Assessment
- Behavioral mode → Strategy_Constraints

**Performance Evaluation**:
- Reputation trajectory → Strategy_Success_Metric
- Learning progress → Adaptation_Quality
- Stability contribution → Systemic_Impact_Score

## Strategic Gameplay Examples

### Example 1: Trade War Escalation and Learning

**Initial Conditions**:
- USA and China both start with Tit-for-Tat strategy
- Initial tariffs: 0% (free trade)
- Reputation: Both at 60 (good standing)
- Trade volume: $500B annually

**Turn 1**: USA imposes 10% tariff on steel (domestic pressure)
```
USA action: Tariff_Steel = 10%
China observes: Defection detected
China TfT response: Tariff_Agriculture = 10%
Reputation impact: USA -5 (initiator), China -2 (retaliation)
```

**Turn 2**: Escalation
```
USA observes retaliation, updates beliefs:
- P(China = Tit-for-Tat) = 0.7
- P(China = Grim Trigger) = 0.3
USA decision: Expand tariffs to 25% on $200B goods
China response: Match with 25% on $200B US goods
Reputation: USA = 50, China = 53
Trade volume: Decreased to $400B (-20%)
```

**Turn 3**: Learning and Adaptation
```
USA Q-learning update:
State = (Growth: -0.5%, Trade_deficit: improved, Reputation: 50)
Reward = -10 (negative growth outweighs trade improvement)
Q(escalation) decreases from 0.6 to 0.45

China Fictitious Play update:
Observed: USA escalated after retaliation
Belief: USA not pure Tit-for-Tat, possibly Gradual or Hawkish
Best Response: Switch to "Gradual" strategy
```

**Turn 4**: De-escalation Attempt
```
USA: Freeze tariffs (no new increases)
China (Gradual strategy): Maintains current tariffs for 2 turns, then reduce by 5%
Market response: Positive, uncertainty decreases
Reputation recovery: USA +2, China +3
Trade volume: Stabilizes at $420B
```

**Outcome**: Both learned that escalation is costly, shifted to more cooperative strategies

### Example 2: Reputation Crisis and Contagion

**Initial Setup**:
- Turkey faces currency crisis, reputation = 35
- Trading partners: EU (40% of trade), Russia (20%), Middle East (40%)
- Network density: High interconnection through supply chains

**Shock Event**: Turkey defaults on debt, reputation crashes to 15

**Turn 1**: Immediate Effects
```
Turkey reputation: 35 → 15 (pariah status)
Trade cost increase: +100% for all partners
Credit access: Frozen
Behavioral response: Switch to "Desperate" mode (aggressive devaluation)
```

**Turn 2**: First-Order Contagion
```
Contagion calculation for Greece (high exposure):
- Trade exposure to Turkey: 15% of GDP
- Financial exposure: 8% of banking assets
- Network pressure = 0.15 * 0.6 (trade weight) + 0.08 * 0.4 (financial weight) = 0.122
- Exceeds threshold (0.1) → Greece affected

Greece impact:
- Reputation: 45 → 38 (contagion penalty)
- Trade costs: +20%
- Behavioral shift: Adopt "Cautious" strategy (reduce exposure)
```

**Turn 3**: Second-Order Cascade
```
Italy (exposed to Greece):
- Network pressure from Greece = 0.08
- Below threshold, but precautionary response
- Reduces trade with affected countries by 10%
- Reputation: Stable at 52 (shows resilience)

Dampening mechanism activates:
- Reputation decay slowed by 50%
- Emergency IMF-style support available
- Trade finance guarantees introduced
```

**Turn 4**: Stabilization
```
Turkey: Implements reforms, reputation recovery begins (15 → 20)
Greece: Stabilizes at reputation = 35
Contagion halted: Network pressure below thresholds
Total affected: 2 countries directly, 4 countries minor impacts
```

**Outcome**: Crisis contained through dampening mechanisms, limited cascade

### Example 3: Coalition Formation Game

**Scenario**: Formation of trade alliance against China

**Players**: USA, EU, Japan, Australia, India
**Target**: China (outside coalition)
**Objective**: Coordinated tariff and technology restrictions

**Initial Coalition Calculation**:
```
Coalition {USA, EU, Japan}:
- Trade benefits: $2.5T * 1.1 (preferential) = $2.75T
- Security benefits: sqrt(45 + 20 + 8) * 0.8 = 6.8
- Coordination costs: 3^2 * 0.3 = 2.7
- Net value: $2.75T + 6.8 - 2.7 = $2.75T + 4.1

Shapley values:
- USA: 45% of net value (largest economy)
- EU: 35% of net value (second largest)
- Japan: 20% of net value (technology leader)
```

**Turn 1**: Coalition Invitation
```
USA (leader) invites: EU, Japan, Australia, India
Acceptance probability (based on reputation and interests):
- EU: 0.75 (high, but concerns about costs)
- Japan: 0.85 (strong security alignment)
- Australia: 0.90 (high dependence on USA)
- India: 0.40 (balancing with China trade)
```

**Turn 2**: Negotiation
```
EU demands: Technology sharing, market access
Japan demands: Security guarantees
Australia: Accepts baseline terms
India: Requests exemptions for pharmaceuticals

Coalition adjusts terms:
- Technology sharing: Limited to non-dual use
- Security: Extended deterrence commitment
- Exemptions: Case-by-case review process
```

**Turn 3**: Formation
```
Final coalition: {USA, EU, Japan, Australia}
India: Remains observer (hedging strategy)

Behavioral strategies within coalition:
- USA: "Leader" - sets agenda, bears higher costs
- EU: "Conditional cooperator" - comply if others do
- Japan: "Loyal ally" - full compliance
- Australia: "Follower" - matches coalition average
```

**Turn 4**: Coordinated Action
```
Coalition implements:
- Synchronized 15% tariffs on Chinese tech
- Investment screening (block acquisitions)
- Technology export controls

China response:
- Reputation damage for coalition: -5 each (seen as protectionist)
- Retaliation: Rare earth export restrictions
- Counter-coalition attempt with Russia, Iran

Market impact:
- Tech prices increase 8%
- Supply chain reorganization begins
- Coalition trade increases 12% (trade diversion)
```

**Outcome**: Successful coalition with internal stability, managed retaliation

## System Stability Analysis

### Critical Thresholds

| Metric | Safe Zone | Warning Zone | Crisis Zone | Automatic Dampening |
|--------|-----------|--------------|-------------|---------------------|
| Average Reputation | >40 | 30-40 | <30 | Reputation floor at 10 |
| Trade Volume Change | ±20% | ±20-40% | >±40% | Emergency trade finance |
| Price Volatility | <15% | 15-30% | >30% | Transaction cost increase |
| Coalition Size | <50% | 50-70% | >70% | Antitrust-style breakup |
| Retaliation Chains | <3 deep | 3-5 deep | >5 deep | Forced cooling period |

### Early Warning Indicators

```python
class EarlyWarningSystem:
    def calculate_indicators(self, state):
        indicators = {}

        # Polarization Index (0-1, higher = more polarized)
        reputation_groups = self.cluster_reputations(state.reputations)
        indicators["polarization"] = self.calculate_polarization(reputation_groups)

        # Fragmentation Coefficient (0-1, higher = more fragmented)
        trade_network = state.trade_adjacency_matrix
        indicators["fragmentation"] = 1 - self.calculate_connectivity(trade_network)

        # Systemic Stress Index (composite measure)
        indicators["systemic_stress"] = (
            0.3 * indicators["polarization"] +
            0.3 * indicators["fragmentation"] +
            0.2 * state.average_tariff_rate / 50 +  # Normalized by 50% max
            0.2 * (100 - state.average_reputation) / 100
        )

        # Cascade Risk Score
        indicators["cascade_risk"] = self.calculate_cascade_probability(state)

        return indicators

    def trigger_alerts(self, indicators):
        alerts = []
        if indicators["polarization"] > 0.7:
            alerts.append("WARNING: High polarization - bloc formation likely")
        if indicators["fragmentation"] > 0.6:
            alerts.append("WARNING: Trade network fragmenting - efficiency loss")
        if indicators["systemic_stress"] > 0.8:
            alerts.append("CRITICAL: System under severe stress - intervention needed")
        if indicators["cascade_risk"] > 0.5:
            alerts.append("WARNING: High contagion risk - monitor closely")
        return alerts
```

## Module Configuration

### Default Parameters

```json
{
  "behavioral_module": {
    "learning": {
      "q_learning_rate": 0.1,
      "discount_factor": 0.95,
      "exploration_rate": 0.1,
      "fictitious_play_weight": 0.7,
      "adaptive_expectations_lambda": 0.3
    },
    "reputation": {
      "persistence_rate": 0.85,
      "initial_value": 50,
      "compliance_weight": 0.4,
      "restraint_weight": 0.2,
      "loyalty_weight": 0.2,
      "transparency_weight": 0.2
    },
    "strategies": {
      "available": ["tit_for_tat", "grim_trigger", "gradual",
                    "tit_for_two_tats", "bandwagon", "contrarian"],
      "default": "tit_for_tat",
      "switching_cost": 5
    },
    "contagion": {
      "transmission_probability": 0.3,
      "activation_threshold": 0.5,
      "max_cascade_depth": 10,
      "network_type": "trade_weighted"
    },
    "stability": {
      "price_volatility_threshold": 0.3,
      "trade_collapse_threshold": 0.5,
      "reputation_crisis_threshold": 20,
      "cascade_size_threshold": 0.4,
      "dampening_intensity": 0.5
    },
    "game_parameters": {
      "trade_war_payoffs": [[100, 100], [60, 140], [140, 60], [80, 80]],
      "currency_war_alpha": 0.3,
      "currency_war_beta": 0.5,
      "sanctions_escalation_cost": 0.2,
      "alliance_coordination_friction": 0.1
    }
  }
}
```

### Scenario-Specific Overrides

```json
{
  "cold_war_scenario": {
    "reputation.persistence_rate": 0.95,
    "strategies.default": "grim_trigger",
    "stability.cascade_size_threshold": 0.6
  },
  "cooperation_scenario": {
    "reputation.compliance_weight": 0.6,
    "strategies.default": "tit_for_two_tats",
    "contagion.transmission_probability": 0.1
  },
  "crisis_scenario": {
    "learning.exploration_rate": 0.2,
    "contagion.transmission_probability": 0.5,
    "stability.dampening_intensity": 0.8
  }
}
```

## Validation & Testing

### Theoretical Validation

1. **Nash Equilibrium Convergence**: Verify strategies converge to theoretical equilibria
2. **Reputation Dynamics**: Check reputation evolves consistent with repeated game theory
3. **Learning Convergence**: Confirm Q-learning converges to optimal policies
4. **Coalition Stability**: Validate Shapley values ensure stable coalitions

### Empirical Calibration Targets

| Historical Event | Model Prediction Target | Tolerance |
|-----------------|------------------------|-----------|
| 2018 US-China Trade War | Tit-for-tat escalation for 4-6 rounds | ±2 rounds |
| 1997 Asian Financial Crisis | Contagion to 5-7 countries | ±2 countries |
| EU Formation (1990s) | Stable coalition of 12-15 members | ±3 members |
| Plaza Accord (1985) | Currency coordination among 5 powers | Exact match |
| 2014 Russia Sanctions | Reputation drop of 30-40 points | ±10 points |

### Stress Testing

1. **Cascade Prevention**: No more than 50% of countries affected in worst-case
2. **Convergence Speed**: Equilibrium within 20 turns for standard scenarios
3. **Reputation Recovery**: Possible to recover from 20 to 60 within 10 turns
4. **Strategy Diversity**: At least 3 different strategies viable in equilibrium
5. **Coalition Limits**: No coalition should exceed 70% of global GDP

## Summary

The Behavioral Module transforms the UTA simulation from a static economic model into a dynamic strategic environment where countries learn, adapt, build reputations, and engage in complex multi-agent interactions. By grounding agent behavior in game theory and behavioral economics, the module ensures realistic strategic dynamics while maintaining computational tractability and economic consistency.

Key innovations:
- **Strategic Depth**: Rich game-theoretic framework for all major interactions
- **Adaptive Intelligence**: Countries learn optimal strategies through experience
- **Reputation Matters**: Long-term consequences for short-term opportunism
- **Systemic Realism**: Network effects and contagion capture interdependence
- **Stability Assured**: Automatic dampening prevents unrealistic collapse

The module provides players with meaningful strategic choices while ensuring the simulation remains grounded in empirical patterns observed in real-world trade conflicts, financial crises, and geopolitical competition.