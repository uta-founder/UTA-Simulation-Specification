# Military Analyst - Technical Assignment

## Role
Formalize military constraints and scenarios for UTA simulation. Define permissible military actions, economic consequences, and escalation thresholds within realistic bounds.

## Core Assumptions (Require Validation)
- Full-scale war with USA is systemically prohibited
- USA retains naval supremacy in open oceans
- Regional conflicts between mid-tier powers are possible
- Economic warfare is primary tool; kinetic actions are localized and limited

## Core Deliverables

### 1. Military Action Registry
**Format**: CSV with fields
- action_id, description, scope (local/regional/global)
- probability [0-1], preconditions, duration (min/max days)

**Permissible actions** (examples):
- NAV_INTERCEPT: Ship interception and inspection
- PORT_BLOCKADE: Single port blockade
- PIPELINE_SABOTAGE: Pipeline infrastructure disruption
- CYBER_INFRA: Port/logistics cyberattack
- STRAIT_MINING: Chokepoint mining
- CONVOY_ESCORT: Armed protection of commercial shipping
- AIR_EXCLUSION: Limited no-fly zone over waters

**Prohibited actions** (automatic rejection):
- WMD use of any kind
- Strategic strikes on nuclear powers
- Total maritime blockade of great powers
- Attacks on civilian population centers

### 2. Red Lines Matrix
**For each actor pair** (US-CN, RU-EU, CN-IN, etc.):

**Thresholds**:
- **Soft red line**: Diplomatic warning, sanctions threat
- **Hard red line**: Limited military response, local confrontation
- **Critical**: Regional escalation, alliance activation

**Quantitative triggers**:
- Shipping losses >X% of total tonnage
- Port blockade duration >N days
- Naval force displacement >Z% from regional waters
- Critical infrastructure destruction (pipelines, cables)

**Format**: JSON matrix with justification and historical precedents

### 3. Operational Parameters
**For each operation type**, specify economic impacts:

```json
{
  "operation": "NAV_INTERCEPT",
  "logistics_impact": 0.02,
  "insurance_rise_bps": 120,
  "port_throughput_drop": 0,
  "duration_days": {"mean": 1, "sd": 0.5},
  "detectability": 1.0,
  "attribution_certainty": 0.9,
  "retaliation_probability": 0.3
}
```

**Parameters**:
- Trade flow disruption (% reduction)
- Insurance premium increase (basis points)
- Port/infrastructure throughput impact
- Duration distributions
- Detection and attribution probabilities

### 4. Escalation Ladder
**Rules and mechanisms**:

**Retaliation matrix**: action → probable responses with probabilities
**Escalation factors**:
- Alliance commitments (automatic involvement triggers)
- Economic dependency (higher stakes → higher escalation risk)
- Domestic political pressure (election cycles, nationalist sentiment)

**De-escalation mechanisms**:
- Third-party mediation
- Graduated concessions and face-saving
- Cooling-off periods

**Format**: State machine with transition probabilities

### 5. Economic Impact Formulas
**Specify quantitatively**:
- Export/import reduction through affected port: % per day of disruption
- Freight/insurance cost increases: basis points or % over baseline
- Commodity shortage development: % deficit after T days
- Recovery time: probability distribution (mean, sd)

**Calibration**: Historical cases
- Strait of Hormuz tensions (1987-1988)
- Suez Canal blockage (Ever Given, 2021)
- Red Sea Houthi attacks (2023-2024)

### 6. Scenario Packages
**Minimum**: 8 fully specified scenarios

**Examples**:
1. **Ship interception** (1-2 days): Insurance spike, temporary rerouting
2. **Regional port blockade** (7-14 days): Supply chain disruption, price increases
3. **Cyberattack on logistics** (3-5 days): Throughput reduction, backlog
4. **Chokepoint mining** (30+ days): Major rerouting, cost escalation
5. **Oil platform seizure**: Production disruption, regional tension
6. **Convoy operations under threat**: Deterrence costs, insurance

**For each**:
- Timeline with phases
- Parameter values (disruption %, cost increases)
- Economic propagation (which sectors, countries affected)
- Escalation probabilities
- Resolution conditions

### 7. Realism Constraints
**Capacity limits**:
- Maximum simultaneous blockades: 2-3 (even for major powers)
- Full military mobilization required for >5 concurrent operations
- Fog of war: 10-20% deviation from intended outcomes

**Temporal dynamics**:
- Instantaneous (cyberattacks, electronic warfare)
- Short-term (1-7 days: interceptions, inspections)
- Extended (weeks-months: blockades, minefields)

### 8. Detection and Attribution
**Data sources**:
- AIS (Automatic Identification System) for ship tracking
- Satellite reconnaissance (commercial and military)
- SIGINT intercepts
- Commercial shipping reports

**Attribution rules**:
- State actor vs proxy/non-state actor
- Confidence levels [0-1]: conclusive, probable, suspected
- Time to attribution: hours (overt) to days (covert)

**UTA enforcement triggers**: Thresholds for automatic flagging and credit penalties

### 9. Ethical Constraints
**Prohibited in all circumstances**:
- WMD employment
- Intentional civilian targeting
- Large-scale environmental terrorism (dam destruction, nuclear plant attacks)

**Validation mechanism**: Automatic action legality checks before execution

## Integration with Other Modules

### With Energy Analyst
- Energy infrastructure vulnerability mapping
- Tanker/pipeline disruption impacts on supply

### With Geopolitical Strategists
- Military actions as policy continuation (Clausewitz)
- Conditions for force employment by archetype

### With Economists
- Supply chain shock multipliers through I-O tables
- Trade flow rerouting costs and delays

## Technical Requirements
- All estimates with confidence intervals
- Data sources: Historical cases, RAND studies, war games, naval exercises
- Logic reproducible in pseudo-code
- Machine-readable formats (CSV/JSON/YAML)

## Delivery Format
1. Red Lines Matrix (CSV/JSON)
2. Action Catalog with parameters (JSON schema)
3. Scenario Packs × 8 (YAML/JSON)
4. Escalation Engine Specification (pseudo-code + formulas)
5. Economic Impact Coefficients (table with sources)
6. Detection/Attribution Methodology (document)

## Validation Criteria
- Consistency with historical precedents
- Plausible economic consequences (calibrated to real disruptions)
- Realistic escalation thresholds (avoid both triviality and apocalypse)
- No runaway escalation to global war under standard scenarios
