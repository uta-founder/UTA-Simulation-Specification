# Geopolitical Strategist - Technical Assignment

## Role
Transform country objective functions and actions into realistic strategic behavior patterns. Define motivations, archetypes, and transition logic between strategic states.

## Core Deliverables

### 1. Strategic Archetypes
Define 5 primary country archetypes with formal specifications:

#### 1.1 Hegemon
**Examples**: USA, historical UK
**Motivation**: Preserve global dominance through system control
**Imperatives**:
- Prevent emergence of peer competitor
- Control key resources (reserve currency, energy, tech standards)
- Sanctions as coercion tool
**Deliverable**: Utility function + action set + reaction thresholds

#### 1.2 Rising Power
**Examples**: China, India
**Motivation**: Disrupt old order, create new institutions
**Imperatives**:
- Build alternative institutions (BRICS, AIIB, CIPS)
- Capture value chain positions (upstream critical materials, downstream tech)
- Aggressive industrial policy and subsidies
**Deliverable**: Challenge strategy + escalation conditions

#### 1.3 Resource Emperor
**Examples**: Russia, Saudi Arabia
**Motivation**: Leverage resources for geopolitical influence
**Imperatives**:
- Price manipulation (OPEC+, gas supply management)
- Energy dependency as leverage tool
- Bilateral energy pacts for political alignment
**Deliverable**: Resource coercion mechanics

#### 1.4 Normative Leader
**Examples**: EU, Japan, Singapore
**Motivation**: Lead through standards and norms
**Imperatives**:
- ESG, human rights, climate as influence tools
- Institutional dominance (WTO, IMF, standards bodies)
- Rules club membership benefits
**Deliverable**: Normative influence instruments

#### 1.5 Survival State
**Examples**: Turkey, Argentina, Pakistan
**Motivation**: Avoid crisis at any cost
**Imperatives**:
- Balance between competing blocs
- Maximize short-term aid and concessions
- Abrupt strategy shifts for survival
**Deliverable**: Loyalty switching conditions

### 2. Strategic Decision Matrix
**Minimum**: 20 strategic actions fully specified

**Table format**:
| Strategy | Description | Objective | Trigger | Economic Effect | Detection |
|----------|-------------|-----------|---------|----------------|-----------|
| Tariff war | Import tariff increase | Market protection | Market share loss >10% | +X% domestic prices, -Y% imports | Immediate |
| Export subsidies | Hidden state support | Market capture | Excess capacity | -Z% export prices | Medium |
| Currency manipulation | Competitive devaluation | Export boost | Trade deficit | +A% exports, -B% import power | Variable |
| Industrial policy | Targeted sector support | Tech leadership | Strategic threat | Capacity +C% in T years | Low-Medium |

### 3. Strategy Transition Conditions
**Threshold matrix**:

**Economic triggers**:
- GDP growth < X% for Y quarters → shift to protectionist
- Trade deficit > Z% GDP → aggressive export push
- Unemployment > A% → industrial policy activation

**Geopolitical triggers**:
- Military threat level > threshold → security over growth
- Alliance isolation score > threshold → survival mode

**Internal triggers**:
- Social unrest index > threshold → populist policies
- Fiscal crisis → austerity + bailout-seeking

**Format**: Decision tree with transition probabilities

### 4. Reaction Functions
**For each archetype pair** (5x5 matrix):
- Action by country A → Probable responses by country B
- Escalation ladder (5-7 steps from diplomatic to severe)
- De-escalation conditions and off-ramps

**Deliverable**: Interaction matrix (JSON) with probabilities and payoffs

### 5. Archetype Evolution Mechanism
**Transition rules**:
- Resource → Industrial: Conditions (investment in manufacturing, education), timeline
- Rising → Hegemon: Requirements (military parity, currency acceptance, institutional control)
- Stable → Survival: Crisis triggers (debt default, currency collapse, political instability)

**Format**: State machine with transition probabilities and time horizons

### 6. Alliance and Bloc Mechanics
**Coalition game specification**:

**Formation conditions**:
- Economic complementarity index > threshold
- Security threat alignment
- Ideological proximity (democracy index, governance similarity)

**Benefit distribution**:
- Trade gains split by bargaining power
- Security burden sharing rules
- Technology transfer within bloc

**Exit and defection**:
- Triggers for leaving alliance
- Punishment mechanisms for defection
- Reputation costs and recovery time

**Deliverable**: Game-theoretic model of coalition formation and stability

### 7. Global Shock Catalog
**Minimum**: 8 shock types with specifications

**Examples**:
- Energy crisis (supply disruption, price spike)
- Financial contagion (sovereign default, banking crisis)
- Pandemic/climate (supply chain disruption, demand collapse)
- Military conflict (trade route blockade, infrastructure destruction)
- Tech breakthrough (AI, quantum, fusion)

**For each**:
- Probability (annual)
- Propagation channels (trade, finance, confidence)
- Vulnerability matrix by archetype
- Response strategies by archetype

### 8. Success/Failure Metrics
**Dominance indicators**:
- Economic influence: % world trade, reserve currency share
- Technological leadership: patent share, critical tech production
- Military projection: force projection index, alliance network
- Normative influence: standard-setting power, institutional voting weight

**Victory conditions** (archetype-specific):
- Hegemon: Maintain >40% influence composite index
- Rising: Achieve parity with hegemon in 2+ dimensions
- Resource: Control >30% global supply of critical resource
- Normative: Set standards adopted by >50% global GDP
- Survival: Avoid sovereign default, maintain >2% growth

## Integration with Other Modules

### With Economists
- Translate strategic imperatives to economic parameters
- Calibrate utility functions for each archetype
- Map strategic actions to CGE impacts

### With Military Analysts
- Define red lines and escalation thresholds
- Integrate military threats into economic decision-making

### With Behavioral Analysts
- Strategic learning and adaptation
- Reputation formation and signaling
- Belief updating about adversary intentions

## Technical Requirements
- All decisions formalized as rules (pseudo-code acceptable)
- Transition probabilities with empirical justification
- Historical validation cases for each archetype
- Mesa framework compatibility (agent decision logic)

## Delivery Format
1. Strategic archetypes document (40-50 pages)
2. Decision and reaction matrices (CSV/JSON)
3. Scenario library (minimum 15 scenarios with outcomes)
4. State machines for archetype evolution (pseudo-code)
5. Historical calibration cases
6. Integration specification with economic and behavioral modules

## Success Criteria
- Realistic behavior in historical scenarios
- No dominant strategies (strategic diversity preserved)
- Emergent outcomes vary across runs
- Consistency with geopolitical theory (realism, liberalism, constructivism)
