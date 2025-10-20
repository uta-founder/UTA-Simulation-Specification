# Energy Analyst - Technical Assignment

## Role
Formalize energy flows, dependencies, and vulnerabilities in global trade system. Model energy as strategic resource with unique transport, storage, and substitutability characteristics.

## Core Deliverables

### 1. Energy Commodity Classification
**Categories with characteristics** (CSV matrix):

**Types**:
- **Pipeline** (gas, oil): Fixed infrastructure, high dependency
- **Marine tanker** (LNG, crude): Flexible logistics, moderate lead times
- **Electricity**: Instantaneous transmission, no storage
- **Solid fuel** (coal, uranium): Easy storage, lower value density
- **Renewable capacity**: Intermittent generation, local production

**Attributes per type**:
- transport_mode, storage_cost, delivery_time, infrastructure_dependency
- substitutability_matrix (cross-fuel substitution elasticities)
- conversion_losses (efficiency when switching energy forms)

### 2. Infrastructure Network Map
**Components** (JSON topology):

**Critical nodes**:
```json
{
  "node_id": "Hormuz_Strait",
  "capacity_mbpd": 21,
  "current_flow": 18,
  "alternatives": ["Cape_Route"],
  "switching_time_days": 14,
  "switching_cost_multiplier": 1.4,
  "disruption_impact": 0.20
}
```

**Include**:
- Major pipelines (Nord Stream, Power of Siberia, TAP, etc.)
- Chokepoints (Hormuz, Malacca, Suez, Bosporus, Panama)
- LNG terminals (regasification capacity, expansion timelines)
- Alternative routes and switching costs

### 3. Strategic Reserves and Buffers
**Parameters per country**:
- Minimum strategic reserves (days of consumption)
- Storage costs by energy type (USD/barrel/month, USD/MWh)
- Mobilization speed (% per day release rate)
- Market impact when reserves deployed (price elasticity)

**Deliverable**: Table + formulas for reserve dynamics and price impacts

### 4. Energy Weaponization Mechanics
**Scenarios**:
- **Export embargo**: Complete supply cutoff
- **Infrastructure disconnection**: Pipeline/grid isolation
- **Price dumping**: Below-cost exports to destroy competitors
- **Artificial scarcity**: Production restrictions to drive prices up

**For each scenario specify**:
- Applicability conditions (who can do what to whom)
- Effectiveness vs different target types
- Countermeasures and costs
- Long-term reputational consequences
- Detection probability and attribution certainty

### 5. Energy Dependency Metrics
**Formulas**:
- **Import dependency ratio** = energy_imports / total_consumption (by fuel type)
- **Supplier concentration** = HHI index of import sources
- **Critical threshold** = % import dependency where vulnerability becomes severe
- **Switching costs** = cost and time to change suppliers

**Deliverable**: Formulas + threshold values triggering risk flags

### 6. Pricing and Elasticity Model
**Specify**:
- **Short-run vs long-run** demand elasticity by fuel and sector
- **Supply elasticity** (production response to price changes)
- **Regional price contagion** (how price shocks spread geographically)
- **Futures market influence** (speculation effects on spot prices)

**Deliverable**: System of equations with calibrated parameters from IEA, EIA data

### 7. Energy Transition Dynamics
**Components**:
- Substitution rates: Fossil → renewable timelines by country type
- Capex requirements for transition
- Geopolitical balance shifts (winners/losers from decarbonization)
- Stranded asset impacts on resource-dependent economies

**Format**: Transition scenarios with temporal profiles (2025-2050)

### 8. Manipulation Detection
**Indicators**:
- Anomalous flow changes (reported vs observed via satellite/AIS)
- Reporting discrepancies (export vs import data mismatches)
- Shadow fleet operations (dark tankers, flag switching)
- Reserve manipulation for price control (coordinated releases/builds)

**Deliverable**: Detection rules + confidence scores + data sources

## Integration with Other Modules

### With Military Analyst
- Infrastructure vulnerability assessments
- Blockade scenarios and economic impacts
- Critical node protection priorities

### With Currency Strategist
- Petrodollar flows and FX impacts
- Energy trade invoicing (USD vs local currency)

### With Economists
- Energy intensity by production sector
- Multipliers for energy price shocks through input-output tables

## Technical Requirements
- **Temporal resolution**: Daily for crises, monthly for normal operations
- **Data calibration**: IEA, EIA, JODI, BP Statistical Review
- **Seasonality**: Heating/cooling demand patterns
- **Extreme events**: Weather shocks, production disruptions
- **Storage dynamics**: Inventory equations with costs and constraints

## Delivery Format
1. Technical specification document (30-40 pages)
2. Parameter tables (CSV/JSON): elasticities, costs, capacities
3. Network topology (JSON/graph format)
4. Scenario library (minimum 10 scenarios)
5. Calibration notebook with historical validation
6. Integration specification with trade and economic modules

## Validation Criteria
- Reproduce historical energy crises (1973 oil shock, 2022 gas crisis)
- Realistic price dynamics matching historical volatility
- Plausible diversification strategies
- Correct modeling of infrastructure bottlenecks
