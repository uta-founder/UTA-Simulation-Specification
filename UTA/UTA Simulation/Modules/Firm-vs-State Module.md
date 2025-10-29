# Firm-vs-State Module

## The Two-Level Game: States Set Rules, Firms Execute

This module governs the critical relationship between government policy and business reality. While countries (you, the player) set tariffs, subsidies, and regulations, the actual economic outcomes depend on how firms respond to these incentives. Your steel subsidy might boost production—or firms might pocket it as profit. Your export ban might halt trade—or clever companies might find workarounds through third countries. Your procurement mandates might reshape markets—or trigger creative compliance that undermines your goals.

The module models firms as profit-maximizing agents operating within state-imposed constraints, creating a principal-agent dynamic where government intentions don't always translate into desired outcomes. This realism is essential: most trade cheating, subsidy gaming, and sanction evasion happens at the firm level, not through official government channels. Understanding and managing this firm-state interaction determines whether your policies succeed or fail.

## Core Game Mechanics: Who Decides What

### The State-Firm Decision Hierarchy

**You (the State) Control:**
- **Policy Framework**: Tariffs, quotas, subsidies, regulations, standards
- **Incentive Design**: Tax rates, R&D support, export credits, procurement prices
- **Enforcement Intensity**: Inspection rates, audit frequency, penalty severity
- **Strategic Direction**: Which sectors to support, which markets to target
- **SOE Mandates**: Direct commands to state-owned enterprises

**Firms (Autonomous Agents) Decide:**
- **Production Levels**: How much to produce given costs and prices
- **Pricing Strategy**: Markup over costs, price discrimination, transfer pricing
- **Market Allocation**: Domestic vs export sales, which countries to target
- **Capacity Investment**: Whether to expand, timing, technology choice
- **Compliance vs Cheating**: Follow rules or exploit loopholes for profit

**The Critical Gap:**
Your policies create incentives, but firms interpret them through their profit lens. A 20% production subsidy doesn't guarantee 20% more output—firms might increase production by 10% and take 10% as extra margin. This gap between policy intent and firm behavior drives the module's strategic depth.

### Turn Sequence: Policy → Response → Detection → Equilibrium

Each simulation turn follows a four-phase structure:

**Phase 1: State Policy Phase (You Decide)**
- Set subsidy rates by sector
- Adjust regulatory requirements
- Define export controls and sanctions
- Establish procurement programs
- Allocate enforcement resources

**Phase 2: Firm Response Phase (Agents Calculate)**
- Firms observe new policies and market conditions
- Calculate profit-maximizing strategies
- Decide production, pricing, and routing
- Evaluate cheating opportunities vs risks
- Execute decisions (with some randomness)

**Phase 3: Detection Phase (Enforcement Checks)**
- Automated monitoring flags anomalies
- Audit mechanisms trigger investigations
- Cheating detection algorithms run
- Violations identified and recorded
- Penalties assessed

**Phase 4: Market Equilibrium Phase (Outcomes Resolve)**
- Supply and demand balance through prices
- Trade flows adjust to new patterns
- Market shares shift based on competitiveness
- Reputation scores update
- Economic indicators calculate

## Player-Facing Strategic Options

### State Policy Tools: Your Arsenal

**1. Production Incentives**
- **Direct Subsidies**: Pay $X per unit produced (visible, challengeable)
- **Tax Credits**: Reduce firm tax burden (less visible)
- **Soft Loans**: Below-market interest rates (hard to detect)
- **Input Subsidies**: Cheaper energy, materials, land (very opaque)
- **R&D Support**: Long-term productivity improvements

Each tool has different visibility to competitors and enforcement agencies. Direct subsidies are transparent but trigger countervailing duties. Hidden support through SOE purchases or soft loans is harder to detect but risks reputation damage if discovered.

**2. Market Shaping**
- **Procurement Mandates**: Government buys domestic at premium prices
- **Local Content Requirements**: Force use of domestic inputs
- **Export Quotas**: Limit foreign sales to boost domestic supply
- **Technical Standards**: Create non-tariff barriers to imports
- **State Trading Monopolies**: Control key commodity flows

**3. Firm Directives (SOE Control)**
For state-owned enterprises, you have direct command:
- **Output Targets**: Produce X tons regardless of profitability
- **Pricing Orders**: Sell below cost to gain market share
- **Market Allocation**: Prioritize strategic partners
- **Technology Sharing**: Transfer knowledge to domestic private firms
- **Loss Tolerance**: Accept negative margins for strategic goals

Private firms ignore directives but respond to incentives. SOEs follow orders but at efficiency costs (20-40% productivity penalty vs private firms).

**4. Enforcement Calibration**
- **Inspection Intensity**: Higher rates catch more cheating but cost more
- **Audit Triggers**: Set sensitivity of anomaly detection
- **Penalty Severity**: Harsh punishments deter but may drive activity underground
- **Transparency Requirements**: Stricter reporting reduces opacity but increases compliance costs
- **Whistleblower Rewards**: Incentivize reporting of violations

### Firm Strategic Behaviors: How Companies Respond

**1. Production Optimization**
Firms continuously adjust output based on:
- **Marginal Cost vs Price**: Produce while Price > MC + regulatory costs
- **Capacity Constraints**: Can't exceed installed capacity
- **Input Availability**: Need materials, energy, labor
- **Lead Times**: Steel furnaces take 6 months to build
- **Subsidy Capture**: Maximize government support per unit effort

**Example Calculation:**
```
Steel firm with capacity 1000 tons/month
Cost: $400/ton, Market price: $500/ton, Margin: $100/ton
Government offers $50/ton subsidy
Firm decision:
- Option A: Keep production at 1000 tons, pocket $50/ton extra profit
- Option B: Increase production to 1200 tons (overtime), margin drops to $80/ton
- Chooses A if demand is weak, B if demand is strong
```

**2. Price Discrimination**
Firms exploit price differences across markets:
- **Domestic Premium**: Charge locals more if protected by tariffs
- **Export Dumping**: Sell abroad below cost to gain market share
- **Transfer Pricing**: Manipulate internal prices to shift profits
- **Bundling**: Hide true prices through package deals

**3. Routing and Origin Games**
When facing trade restrictions, firms get creative:
- **Triangulation**: Ship through third countries to obscure origin
- **Minimal Processing**: Add token value to change classification
- **Paper Shuffling**: Forge certificates of origin
- **Subsidiary Networks**: Use affiliates to disguise ownership

**Risk-Return Calculation:**
```
Direct export banned, loses $10M market
Triangulation route: $8M revenue - $1M extra cost - $2M expected penalty
Expected value: $8M - $1M - ($2M × 60% detection rate) = $5.8M
Firm triangulates if $5.8M > $0 (no export)
```

**4. Capacity Investment Timing**
Firms time expansions strategically:
- **Subsidy Harvesting**: Expand when government support peaks
- **Cycle Timing**: Build during downturns, operate in upturns
- **Competitor Response**: Preempt or follow rivals
- **Policy Uncertainty**: Delay if rules might change

### Cheating Mechanics: The Underground Economy

**Detection Probability Formula:**
```
P(detection) = Base Rate × (1 + Enforcement Intensity) × (1 + Anomaly Score) × (1 - Opacity Index)

Where:
- Base Rate: 20% (inherent detection chance)
- Enforcement Intensity: 0 to 2 (government setting)
- Anomaly Score: 0 to 3 (based on red flags)
- Opacity Index: 0 to 0.8 (sector characteristic)
```

**Common Cheating Methods and Detection Rates:**

**1. Origin Laundering (Triangulation)**
- **Method**: Ship sanctioned goods through complicit third country
- **Detection Triggers**:
  - Sudden spike in third country re-exports (>50% increase)
  - Re-export value exceeds domestic production
  - Minimal value-add despite "processing" claims
- **Base Detection Rate**: 60%
- **Penalty**: -100 UTA credits, trade suspension

**2. Transfer Pricing Manipulation**
- **Method**: Artificial prices between related companies
- **Detection Triggers**:
  - Prices deviate >25% from arm's length benchmarks
  - Consistent losses in high-tax jurisdictions
  - Profit margins inversely correlated with tax rates
- **Base Detection Rate**: 40%
- **Penalty**: -75 UTA credits, back-taxes

**3. Subsidy Concealment**
- **Method**: Hidden support through SOEs, land deals, soft loans
- **Detection Triggers**:
  - Below-cost pricing sustained >3 periods
  - Unusual profitability of "private" firms
  - Capacity expansion without visible financing
- **Base Detection Rate**: 30%
- **Penalty**: -80 UTA credits, countervailing duties

**4. Phantom Trade**
- **Method**: Fake invoices to claim export subsidies
- **Detection Triggers**:
  - Export volumes exceed production capacity
  - No corresponding import records in partner countries
  - Unusual shipping patterns (circular routes)
- **Base Detection Rate**: 70%
- **Penalty**: -50 UTA credits, subsidy clawback

## Implementation Specification

### Two-Level Agent Architecture

The module uses a hierarchical agent structure:

**Level 1: State Strategic Agents (Players)**
- Make policy decisions each turn
- Set enforcement parameters
- Allocate resources across sectors
- Respond to international pressures
- Manage UTA credit balance

**Level 2: Firm Micro-Agents**
- **Representative Firms**: One per sector in most industries
- **Sentinel Firms**: Individual major companies in strategic sectors
- Autonomous profit-maximization within state constraints
- Stochastic decision-making with bounded rationality

### Firm Data Structure

Each firm (representative or sentinel) has:

```python
class Firm:
    # Identity
    sector: str              # Industry classification
    country: str            # Headquarters location
    ownership: str          # "private", "state", "foreign"

    # Production Parameters
    capacity: float         # Maximum output per period
    utilization: float      # Current capacity usage (0-1)
    technology_level: float # Productivity multiplier

    # Economic Parameters
    marginal_cost: float    # Cost per additional unit
    fixed_costs: float      # Period overhead
    margin_target: float    # Desired profit margin

    # Behavioral Parameters
    risk_tolerance: float   # Willingness to cheat (0-1)
    state_loyalty: float    # Compliance with directives (0-1)
    opacity_score: float    # Ability to hide activities (0-1)

    # Market Position
    domestic_share: float   # Share of home market
    export_share: float     # Share of production exported
    market_power: float     # Ability to set prices (0-1)

    # Elasticities
    supply_elasticity_short: float  # Output response to price (short-run)
    supply_elasticity_long: float   # Output response to price (long-run)
    capex_lead_time: int    # Periods to build new capacity
```

### Firm Decision Algorithm

Each firm follows this decision process:

```
1. OBSERVE market conditions and policies
   - Current prices (domestic and international)
   - Government subsidies and regulations
   - Competitor actions
   - Demand forecasts

2. CALCULATE profit under different strategies
   For each feasible production level:
   - Revenue = Price × Quantity
   - Costs = (Marginal Cost × Quantity) + Fixed Costs - Subsidies
   - Profit = Revenue - Costs - Expected Penalties

3. EVALUATE special opportunities
   - Can triangulation increase profits?
   - Would transfer pricing reduce tax burden?
   - Is subsidy fraud detection risk acceptable?

4. OPTIMIZE production and pricing
   - Set quantity where Marginal Revenue = Marginal Cost (adjusted)
   - Set price based on demand elasticity and competition

5. DECIDE on compliance vs cheating
   If (Profit from Cheating - Expected Penalty) > Profit from Compliance:
       And Random() < Risk Tolerance:
           Execute cheating strategy
   Else:
       Comply with regulations

6. INVEST in capacity if profitable
   If Expected Future Profit > Investment Cost:
       And Government signals stable policy:
           Begin capacity expansion
```

### Detection Engine Specifications

The detection system runs automated checks each turn:

**1. Anomaly Scoring Algorithm**
```python
def calculate_anomaly_score(firm, sector_average):
    score = 0

    # Export growth anomaly
    if firm.export_growth > sector_average.export_growth * 1.5:
        score += 0.5
    if firm.export_growth > sector_average.export_growth * 2.0:
        score += 1.0

    # Margin anomaly
    if firm.margin < 0 and firm.duration_negative > 2:
        score += 0.8  # Sustained losses suggest hidden support

    # Capacity anomaly
    if firm.capacity_growth > 0.2 and firm.visible_investment < firm.capacity_cost * 0.5:
        score += 1.0  # Expansion without visible financing

    # Trade pattern anomaly
    if firm.export_concentration > 0.8 and firm.primary_destination in sanctioned_countries:
        score += 1.5  # Suspicious routing

    # Input-output anomaly
    if firm.output_value > firm.input_value * sector.max_value_add * 1.2:
        score += 0.7  # Creating value from thin air

    return min(score, 3.0)  # Cap at 3.0
```

**2. Audit Trigger Rules**
```python
def should_audit(firm, enforcement_intensity):
    # Automatic triggers
    if firm.anomaly_score > 2.0:
        return True

    # Probabilistic triggers
    audit_probability = 0.1 * enforcement_intensity * (1 + firm.anomaly_score)

    # Previous violations increase scrutiny
    if firm.violation_history > 0:
        audit_probability *= 1.5

    # High-risk sectors get more attention
    if firm.sector in ['chemicals', 'steel', 'semiconductors']:
        audit_probability *= 1.3

    return random() < audit_probability
```

**3. Investigation Resolution**
```python
def investigate_firm(firm, enforcement_resources):
    detection_probability = calculate_detection_probability(firm)

    if random() < detection_probability:
        violation_type = identify_violation(firm)
        penalty = assess_penalty(violation_type)

        # Apply consequences
        firm.country.uta_credits -= penalty.credit_cost
        firm.pay_fine(penalty.monetary_fine)
        firm.violation_history += 1

        # Public disclosure affects reputation
        if penalty.public_disclosure:
            firm.reputation -= 0.2
            firm.country.transparency_score -= 0.1

        return violation_type

    return None
```

## Economic Parameters & Calibration

### Sectoral Supply Elasticities

Based on empirical literature (source: GTAP, World Bank):

| Sector | Short-Run | Medium-Run | Long-Run | Capex Lead Time |
|--------|-----------|------------|----------|-----------------|
| Agriculture | 0.3 | 0.8 | 1.5 | 1-2 periods |
| Oil & Gas | 0.1 | 0.3 | 0.8 | 8-12 periods |
| Steel | 0.2 | 0.5 | 1.2 | 4-6 periods |
| Chemicals | 0.4 | 0.7 | 1.3 | 3-5 periods |
| Electronics | 0.6 | 1.2 | 2.0 | 2-3 periods |
| Textiles | 0.8 | 1.5 | 2.5 | 1-2 periods |
| Machinery | 0.3 | 0.6 | 1.1 | 3-4 periods |
| Services | 1.0 | 1.8 | 2.8 | 0-1 periods |

**Interpretation**: A short-run elasticity of 0.3 means a 10% price increase yields 3% output increase immediately.

### Opacity Index by Sector

How easily can activities be hidden? (0 = transparent, 1 = opaque)

| Sector | Opacity | Reasoning |
|--------|---------|-----------|
| Agriculture | 0.1 | Satellite monitoring, seasonal patterns |
| Oil & Gas | 0.3 | Physical infrastructure, metered flows |
| Mining | 0.2 | Geological constraints, visible extraction |
| Steel | 0.4 | Large facilities but complex supply chains |
| Chemicals | 0.7 | Dual-use, easy relabeling, complex products |
| Electronics | 0.6 | Small, high-value, complex supply chains |
| Financial Services | 0.8 | Digital, encrypted, offshore capabilities |
| Logistics | 0.5 | Physical tracking but complex networks |

### Detection Thresholds

Red flags that trigger automatic investigation:

| Indicator | Yellow Flag | Red Flag | Automatic Audit |
|-----------|------------|----------|-----------------|
| Export Growth Rate | >30% | >50% | >100% |
| Re-export Ratio | >40% | >60% | >80% |
| Margin Deviation | <-10% | <-20% | <-30% |
| Price vs Benchmark | ±15% | ±25% | ±40% |
| Capacity Utilization | >95% | >100% | >110% |
| Input-Output Ratio | <0.7 | <0.5 | <0.3 |

### Pass-Through Rates

How much of subsidies/tariffs affect prices vs quantities:

| Market Structure | Price Pass-Through | Quantity Pass-Through |
|-----------------|-------------------|----------------------|
| Perfect Competition | 90-100% | 0-10% |
| Monopolistic Competition | 60-80% | 20-40% |
| Oligopoly | 40-60% | 40-60% |
| Monopoly/Monopsony | 20-40% | 60-80% |

**Example**: In oligopolistic steel markets, a $100/ton subsidy leads to $50 price reduction and $50 expanded margin/output.

### Cheating Payoff Matrix

Expected value calculation for different violation types:

| Cheating Method | Gross Benefit | Detection Rate | Expected Penalty | Net Expected Value |
|-----------------|---------------|----------------|------------------|-------------------|
| Triangulation | 20% of blocked trade | 60% | -100 credits + fine | Positive if trade > $10M |
| Transfer Pricing | 15% tax savings | 40% | -75 credits + backtax | Positive if volume > $25M |
| Subsidy Hiding | 30% cost advantage | 30% | -80 credits + duties | Usually positive |
| Origin Falsification | Tariff differential | 70% | -50 credits + seizure | Rarely positive |
| Phantom Exports | Subsidy value | 70% | -50 credits + clawback | Negative expected value |

## Integration with Other Modules

### Inputs FROM Other Modules

**From Subsidy & Industrial Policy Module:**
- Subsidy rates by sector
- R&D investment levels
- Procurement program parameters
- Capital support programs

**From Sanctions & Geopolitics Module:**
- Embargo lists
- Export control regimes
- Coalition penalties for violations
- Secondary sanction risks

**From Pricing & Market Equilibrium Module:**
- Current market prices (domestic and international)
- Demand elasticities
- Market clearing conditions
- Excess demand/supply signals

**From Compliance & Cheating Detection Module:**
- Enforcement intensity settings
- Detection algorithm parameters
- UTA credit penalties
- Investigation triggers

**From Trade Flow Module:**
- Bilateral trade volumes
- Transport costs
- Route availability
- Partner country import data

### Outputs TO Other Modules

**To Trade Flow Module:**
- Actual production quantities
- Export allocations by destination
- Triangulation attempts
- Modified origin certificates

**To Pricing & Market Equilibrium Module:**
- Firm supply schedules
- Marginal cost curves
- Capacity constraints
- Production responses to price

**To Compliance & Cheating Detection Module:**
- Cheating flags by firm
- Anomaly scores
- Investigation evidence
- Violation records

**To Demand Module:**
- Available supply by location
- Quality-adjusted quantities
- Product differentiation parameters

**To Subsidy & Industrial Policy Module:**
- Subsidy uptake rates
- Capacity expansion reports
- R&D investment responses
- Policy effectiveness metrics

### Feedback Loops

**Policy Effectiveness Loop:**
State sets subsidy → Firms respond partially → Market outcomes differ from intent → State adjusts policy → Firms adapt behavior

**Detection-Evasion Arms Race:**
Enforcement increases → Detection rates rise → Firms develop new cheating methods → Detection algorithms update → Opacity increases → Investment in enforcement technology

**Reputation Spiral:**
Firm cheats → Gets caught → Reputation falls → Higher monitoring → More likely to get caught → Reputation trap

**Capacity Investment Cycle:**
High prices → Firms invest → Capacity increases (with lag) → Prices fall → Investment stops → Capacity depreciates → Prices rise

## Strategic Gameplay Scenarios

### Scenario 1: The Subsidy Game - Steel Wars

**Setup:** China subsidizes steel production by $100/ton. USA considers response.

**Turn 1 - China's Move:**
- Implements $100/ton steel production subsidy
- Cost: $5 billion annually (50M tons production)
- Enforcement: Medium (catches obvious fraud)

**Turn 2 - Firm Responses:**
Chinese steel firms face choice:
- **Expand Aggressively**: Build new capacity (6-month lag), gain global share
- **Profit Harvest**: Keep production flat, pocket subsidy as margin
- **Mixed Strategy**: Moderate expansion + some profit taking

Firm calculation:
```
Aggressive Expansion Path:
- Investment: $2B for 10M ton capacity
- ROI period: 3 years at current prices
- Risk: Overcapacity if others expand too
- Decision: 3 firms expand, 2 harvest profit

Result: Production +15% over 6 months, prices -8%
```

**Turn 3 - USA Response Options:**

Option A: **Countervailing Duties**
- Impose $100/ton duty on Chinese steel
- Immediate protection for domestic industry
- But: Raises costs for steel-using industries
- China may retaliate on other products

Option B: **Match Subsidies**
- Subsidize US steel by $100/ton
- Cost: $2 billion annually
- Triggers subsidy war, both lose money
- But maintains market share

Option C: **WTO Case + Targeted Response**
- File formal complaint (takes 8-12 turns)
- Meanwhile: Strategic procurement, quality standards
- Longer-term but avoids escalation

**Turn 4 - Detection Phase:**
- Audit reveals 2 Chinese firms claiming phantom production
- 500,000 tons of fake capacity for subsidy harvesting
- China loses 50 UTA credits
- USA gains propaganda victory

**Outcome Variables:**
- Chinese steel global market share: +8%
- US steel employment: -5,000 jobs
- Chinese fiscal cost: $5B - $0.5B (fraud) = $4.5B
- Steel prices: -12% globally
- Downstream industry benefits: +$8B globally

### Scenario 2: Sanctions Evasion - The Oil Triangle

**Setup:** USA/EU ban Russian oil imports. Russia seeks alternatives.

**Turn 1 - Sanctions Imposed:**
- EU bans Russian oil (30M barrels/month)
- Price cap at $60/barrel
- Insurance ban for violations

**Turn 2 - Russian Firm Adaptation:**

Russian oil firms evaluate options:
1. **Comply**: Sell to Asia at discount (-$20/barrel)
2. **Triangulate**: Route through Turkey/India
3. **Shadow Fleet**: Use uninsured tankers

**Triangulation Mechanics:**
```
Direct to EU: Banned ($0 revenue)
To India direct: $50/barrel (discount + transport)
To India → Refined → To EU: $75/barrel

India's take: $5/barrel facilitation fee
Russia nets: $70/barrel vs $50 direct to Asia
Risk: 60% detection probability
Penalty if caught: -100 UTA credits, secondary sanctions on India
```

**Turn 3 - Execution:**
- 40% goes through shadow fleet (uninsured tankers)
- 30% through India triangulation
- 30% legitimate to China at discount

**Turn 4 - Detection Triggers:**
- India's petroleum product exports spike 200%
- India importing 150% of refinery capacity
- Satellite imagery shows ship-to-ship transfers
- Investigation launched

**Turn 5 - Investigation Results:**
- Triangulation confirmed via shipping data
- India faces choice: Stop facilitating or face secondary sanctions
- Russia loses 100 UTA credits
- Insurance companies fined for violations

**Market Impact:**
- Russian oil revenue: -30% from pre-sanction
- EU energy costs: +15%
- India refining margins: +200%
- Global oil price: +$8/barrel
- Tanker rates: +50% on shadow routes

### Scenario 3: SOE Mandates vs Market Reality

**Setup:** China mandates SOE semiconductor production surge despite losses.

**Turn 1 - State Directive:**
- Target: Double semiconductor output in 2 years
- SOEs ordered to expand regardless of profitability
- Private firms offered subsidies but not mandated

**Turn 2 - Firm Divergence:**

**SOE Response:**
- Immediate capacity investment ($20B)
- Hire aggressively, wages +30%
- Accept -20% margins to gain scale
- Technology remains 2 generations behind

**Private Firm Response:**
- Cherry-pick profitable segments only
- Focus on specialized chips
- Maintain 15% margins
- Slower expansion but sustainable

**Turn 3 - Market Distortions:**
```
SOE behavior:
- Production: +80% (approaching target)
- Losses: $8B annually
- Quality: 60% yield rate
- Market share: Gained in low-end

Private firms:
- Production: +20%
- Profit: $2B
- Quality: 85% yield
- Market share: Stable in high-end
```

**Turn 4 - International Response:**
- USA invokes anti-dumping measures
- Japan/Korea coordinate technology restrictions
- WTO case filed on subsidies

**Turn 5 - Sustainability Crisis:**
- SOE losses unsustainable
- State must either:
  - Continue funding (fiscal stress)
  - Allow consolidation (job losses)
  - Pivot to quality over quantity

**Lessons Learned:**
- Mandates can force rapid capacity growth
- But efficiency penalty is severe (20-40%)
- Private firms outperform even with less support
- International backlash costs may exceed benefits

## Decision Trees and Probability Calculations

### Firm Cheating Decision Tree

```
Market Opportunity Detected
├─ Calculate Legal Profit: $10M
├─ Calculate Illegal Profit: $15M
└─ Assess Risk
   ├─ Detection Probability: 60%
   ├─ Penalty if Caught: $8M + reputation
   └─ Expected Value Calculation
      ├─ EV(Cheat) = 0.4 × $15M + 0.6 × ($15M - $8M) = $10.2M
      ├─ EV(Comply) = $10M
      └─ Decision: CHEAT (EV difference = $0.2M)
         ├─ If risk_tolerance > threshold
         │  └─ Execute cheating strategy
         └─ If risk_tolerance < threshold
            └─ Comply despite EV advantage
```

### State Enforcement Investment Decision

```
Observed Cheating Signals
├─ Current Detection Rate: 40%
├─ Cheating Cost to Economy: $100M/year
└─ Enforcement Options
   ├─ Status Quo
   │  ├─ Cost: $10M/year
   │  ├─ Detection: 40%
   │  └─ Expected Loss: $60M
   ├─ Enhanced Monitoring
   │  ├─ Cost: $25M/year
   │  ├─ Detection: 65%
   │  └─ Expected Loss: $35M
   └─ Maximum Enforcement
      ├─ Cost: $50M/year
      ├─ Detection: 85%
      ├─ Expected Loss: $15M
      └─ OPTIMAL if Marginal Benefit > Marginal Cost
```

### Triangulation Route Optimization

```
Sanctioned Trade Worth $100M
├─ Direct Route: Blocked ($0)
├─ Option 1: Turkey Triangle
│  ├─ Markup: 5%
│  ├─ Detection: 70%
│  ├─ Net EV: $28.5M
│  └─ Risk: High
├─ Option 2: UAE-India Chain
│  ├─ Markup: 12%
│  ├─ Detection: 45%
│  ├─ Net EV: $48.4M
│  └─ Risk: Medium
└─ Option 3: Complex Multi-hop
   ├─ Markup: 20%
   ├─ Detection: 25%
   ├─ Net EV: $60M
   ├─ Risk: Low
   └─ SELECT if risk-adjusted returns highest
```

## Sentinel Firm Approach for High-Risk Sectors

### When to Use Sentinel Firms

Instead of representative firms, model specific companies when:
- Sector has high concentration (top 3 firms > 60% market share)
- Cheating risk is extreme (chemicals, dual-use, luxury goods)
- Strategic importance is critical (semiconductors, energy, food)
- Existing evasion networks are known

### Sentinel Firm Examples

**Russian Oil Majors (Rosneft, Lukoil, Gazprom Neft)**
- Each modeled individually with specific tanker fleets
- Ownership trees include trading subsidiaries
- Historical sanctions evasion patterns encoded
- Relationships with specific transit countries

**Chinese Steel Giants (Baosteel, HBIS, Shagang)**
- Capacity and technology precisely specified
- State influence parameters vary by firm
- Export market specialization tracked
- Subsidy receipt individually monitored

**Semiconductor Titans (TSMC, Samsung, Intel)**
- Technology generation precisely modeled
- Customer concentration risk included
- Input dependencies explicitly mapped
- Export control compliance individually tracked

### Ownership Graph Specification

For sentinel firms, track full ownership networks:

```python
class OwnershipNetwork:
    nodes: Dict[str, Firm]  # Company ID → Firm object
    edges: Dict[Tuple[str, str], float]  # (Parent, Child) → ownership %

    def get_ultimate_owner(firm_id):
        # Traverse up to find ultimate beneficial owner

    def aggregate_group_trade():
        # Sum all related party transactions

    def detect_circular_trading():
        # Flag suspicious within-group trades

    def calculate_opacity():
        # More subsidiaries = harder to track
```

This allows modeling of:
- Transfer pricing within corporate groups
- Regulatory arbitrage across jurisdictions
- Hidden beneficial ownership
- Coordinated evasion strategies

## Key Implementation Notes

### For Developers

1. **Agent Architecture**: Implement firms as Mesa agents with profit-maximization objectives and bounded rationality (not perfect foresight)

2. **Decision Timing**: Firms decide simultaneously each turn, not sequentially, to prevent gaming

3. **Stochasticity**: Add 10-20% random variation to firm decisions to simulate real-world uncertainty

4. **Learning**: Firms should update their beliefs about detection probabilities based on experience

5. **Performance**: Use representative firms for most sectors, sentinel firms only where strategically critical

### For Game Balance

1. **Calibration**: Start with conservative parameters, then tune based on historical validation (2018 US-China tariffs, 2022 Russia sanctions)

2. **Feedback Intensity**: Ensure no single strategy dominates; both compliance and cheating should be viable under different conditions

3. **Detection Balance**: Neither perfect enforcement nor complete opacity; maintain 40-70% detection rates for interesting gameplay

4. **Computational Limits**: Cap at ~1000 firm agents for reasonable performance, use representative firms to aggregate

### For Economic Realism

1. **No Magic**: Firms can't create value from nothing; input-output balance must hold

2. **Time Consistency**: Capacity takes time to build; elasticities increase over time

3. **Market Power**: Large firms have more pricing power but also attract more scrutiny

4. **Sectoral Variation**: Don't use uniform parameters; sectors differ fundamentally

## Summary: Why This Module Matters

The Firm-vs-State Module transforms the UTA simulation from abstract country-level policy into realistic economic gameplay. By modeling how firms actually respond to government policies—partially, strategically, sometimes defiantly—it captures the messy reality of international trade.

Players must think beyond simple policy levers to consider:
- How will firms interpret my incentives?
- What loopholes might they exploit?
- How can I align firm profits with national goals?
- When should I crack down vs turn a blind eye?
- How do I compete when others are cheating?

This creates rich, emergent gameplay where unintended consequences are common, enforcement is costly, and the gap between policy intent and economic outcome drives strategic depth. The module ensures that success requires not just good policies but effective implementation—just like the real world.