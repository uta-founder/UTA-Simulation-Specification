# Trade Flow Module

## Purpose & Scope

The Trade Flow Module manages bilateral trade volumes between countries across all products/sectors, incorporating transport costs, tariffs, and trade routing decisions. It serves as the primary data structure for tracking actual goods movement in the simulation, updating dynamically based on production changes, policy interventions, and market equilibrium outcomes.

This module bridges the gap between production decisions (supply) and consumption needs (demand), accounting for physical and regulatory constraints on trade. It handles both legitimate trade flows and potential circumvention routes (triangulation, re-exporting).

## Key Components

### 1. Trade Matrix Structure
- **Bilateral Trade Tensor**: 3D array `T[i,j,p]` representing trade volume from country i to country j for product p
- **Price Matrix**: `P[i,j,p]` - delivered price including transport and tariffs
- **Route Registry**: Graph structure tracking actual vs declared trade routes
- **Transit Trade Tracker**: Flows through third countries for re-export

### 2. Transport Cost Calculator
- Distance-based costs using great circle calculations
- Modal choice optimization (sea, air, rail, road, pipeline)
- Chokepoint premiums (Suez, Panama, Malacca)
- Insurance and freight (CIF) adjustments

### 3. Tariff Engine
- Ad valorem tariffs: percentage of product value
- Specific tariffs: fixed amount per unit
- Compound tariffs: combination of ad valorem and specific
- Preferential rates from trade agreements
- Retaliatory tariff escalation logic

### 4. Trade Flow Optimizer
- Gravity model base calculation
- Route selection under constraints
- Triangulation opportunity identification
- Capacity constraint enforcement

## Data Structures

### Input Data
```python
class TradeFlowInputs:
    # From Country Agents
    production_capacity: dict[country][product] -> float  # Maximum production
    domestic_demand: dict[country][product] -> float      # Internal consumption
    export_supply: dict[country][product] -> float        # Available for export
    import_demand: dict[country][product] -> float        # Required imports

    # From Policy Module
    tariff_schedule: dict[importer][exporter][product] -> float  # Tariff rates
    trade_bans: set[(importer, exporter, product)]              # Prohibited flows
    quotas: dict[importer][exporter][product] -> float          # Volume limits

    # From Transport/Logistics Module
    transport_cost_matrix: dict[origin][destination][mode] -> float
    route_availability: dict[(origin, destination)] -> list[routes]
    chokepoint_status: dict[chokepoint] -> float  # 0=blocked, 1=normal
```

### Internal State
```python
class TradeFlowState:
    # Core Trade Data
    bilateral_trade: np.array[n_countries, n_countries, n_products]  # Volume
    trade_prices: np.array[n_countries, n_countries, n_products]     # CIF price

    # Route Information
    trade_routes: dict[(i,j,p)] -> list[country_sequence]  # Actual path
    transit_volumes: dict[country][product] -> float       # Re-export volumes

    # Trade Balance Accounting
    exports_total: dict[country][product] -> float
    imports_total: dict[country][product] -> float
    trade_balance: dict[country] -> float  # Exports - Imports value

    # Compliance Tracking
    declared_routes: dict[(i,j,p)] -> list[country_sequence]
    actual_routes: dict[(i,j,p)] -> list[country_sequence]
    triangulation_flags: set[(exporter, importer, product, transit_country)]
```

### Output Data
```python
class TradeFlowOutputs:
    # For Equilibrium Solver
    effective_supply: dict[country][product] -> float  # Production + Imports
    effective_demand: dict[country][product] -> float  # Domestic + Export demand
    market_access: dict[country][product] -> list[accessible_markets]

    # For Pricing Module
    landed_costs: dict[importer][product][source] -> float  # CIF + tariff
    competitive_suppliers: dict[importer][product] -> list[(supplier, price)]

    # For Compliance Module
    anomaly_flags: list[TradeAnomaly]  # Suspicious patterns
    trade_asymmetries: dict[(reporter, partner)] -> float  # Reporting gaps

    # For Country Agents
    market_share: dict[exporter][importer][product] -> float
    revenue_by_destination: dict[exporter][destination] -> float
```

## Economic Logic

### 1. Gravity Model Foundation
Trade flows follow modified gravity equation:
```
T[i,j,p] = A * (Y[i]^α * Y[j]^β * P[i,p]^γ) / (D[i,j]^δ * (1 + τ[i,j,p])^ε)

Where:
- T[i,j,p] = Trade flow from i to j for product p
- Y[i], Y[j] = GDP of exporter and importer
- P[i,p] = Production capacity of i for product p
- D[i,j] = Effective distance (geographic * infrastructure quality)
- τ[i,j,p] = Tariff rate
- A, α, β, γ, δ, ε = Calibrated parameters
```

### 2. Armington Assumption
Products differentiated by origin using CES aggregation:
```
Q[j,p] = (Σ[i] a[i,j,p] * T[i,j,p]^((σ-1)/σ))^(σ/(σ-1))

Where:
- Q[j,p] = Composite good p consumed in country j
- a[i,j,p] = Share parameter (preference for origin i)
- σ = Elasticity of substitution between origins
```

### 3. Transport Cost Function
```python
def calculate_transport_cost(origin, destination, product, volume):
    base_distance = great_circle_distance(origin, destination)

    # Modal optimization
    if product.is_pipeline_good:
        mode = "pipeline"
        unit_cost = PIPELINE_COST_PER_KM
    elif product.is_perishable:
        mode = "air" if distance > AIR_THRESHOLD else "road"
        unit_cost = AIR_COST_PER_KM if mode == "air" else ROAD_COST_PER_KM
    else:
        mode = "sea"
        unit_cost = SEA_COST_PER_TON_KM

    # Volume discounts (economies of scale)
    volume_factor = 1 - 0.2 * min(volume / VOLUME_THRESHOLD, 1)

    # Chokepoint premiums
    route = find_optimal_route(origin, destination, mode)
    chokepoint_premium = sum([CHOKEPOINT_COSTS[cp] for cp in route.chokepoints])

    total_cost = base_distance * unit_cost * volume_factor + chokepoint_premium
    return total_cost, mode, route
```

### 4. Triangulation Detection
```python
def detect_triangulation(trade_flows, threshold=0.8):
    anomalies = []

    for transit in countries:
        for product in products:
            imports = trade_flows.imports_total[transit][product]
            exports = trade_flows.exports_total[transit][product]
            domestic_production = production[transit][product]

            # High re-export ratio without production
            if domestic_production < 0.1 * exports and exports > threshold * imports:
                # Check if avoiding sanctions/tariffs
                for source in trade_flows.import_sources[transit][product]:
                    for dest in trade_flows.export_destinations[transit][product]:
                        if is_sanctioned(source, dest, product):
                            anomalies.append({
                                'type': 'triangulation',
                                'transit': transit,
                                'true_source': source,
                                'declared_source': transit,
                                'destination': dest,
                                'product': product,
                                'volume': min(imports[source], exports[dest])
                            })

    return anomalies
```

## Integration Points

### Inputs From Other Modules

1. **From Demand Module**:
   - Domestic consumption requirements
   - Import demand by product and preferred sources
   - Elasticity of substitution between suppliers

2. **From Supply Module** (Country/Firm Agents):
   - Production volumes available for export
   - Minimum price requirements
   - Capacity constraints

3. **From Pricing & Equilibrium Module**:
   - Market-clearing prices
   - Excess supply/demand signals
   - Price signals for route optimization

4. **From Sanctions & Geopolitics Module**:
   - Trade restrictions and embargoes
   - Tariff schedules and trade agreements
   - Retaliation triggers

5. **From Energy & Logistics Module**:
   - Transport cost matrices by mode
   - Infrastructure capacity and chokepoints
   - Energy costs affecting transport

### Outputs To Other Modules

1. **To Pricing & Equilibrium Module**:
   - Realized trade volumes for market clearing
   - Effective supply/demand by location
   - Trade-weighted average prices

2. **To Compliance & Detection Module**:
   - Trade asymmetries and anomalies
   - Triangulation candidates
   - Sudden flow changes

3. **To Country Agents**:
   - Market share achievements
   - Revenue by product and destination
   - Trade balance position

4. **To Subsidy & Industrial Policy Module**:
   - Export performance metrics
   - Import penetration rates
   - Competitiveness indicators

## Implementation Guidance

### Algorithm Flow

```python
def update_trade_flows(world_state):
    """Main trade flow update cycle"""

    # Step 1: Calculate base trade potential (gravity model)
    trade_potential = calculate_gravity_flows(
        world_state.gdp,
        world_state.production,
        world_state.distance_matrix
    )

    # Step 2: Apply policy constraints
    constrained_flows = apply_trade_policies(
        trade_potential,
        world_state.tariffs,
        world_state.quotas,
        world_state.sanctions
    )

    # Step 3: Calculate transport costs and optimal routes
    routed_flows = optimize_trade_routes(
        constrained_flows,
        world_state.transport_costs,
        world_state.infrastructure
    )

    # Step 4: Check market clearing conditions
    balanced_flows = balance_supply_demand(
        routed_flows,
        world_state.production,
        world_state.consumption,
        convergence_threshold=0.001
    )

    # Step 5: Detect anomalies and circumvention
    anomalies = detect_trade_anomalies(
        balanced_flows,
        world_state.historical_flows
    )

    # Step 6: Update state and calculate metrics
    update_trade_state(balanced_flows, anomalies)
    calculate_trade_metrics()

    return balanced_flows, anomalies
```

### Computational Considerations

1. **Matrix Sparsity**: Most country pairs don't trade all products
   - Use sparse matrix representations
   - Index only active trade relationships

2. **Equilibrium Convergence**: Trade flows must balance
   - Use iterative proportional fitting (RAS algorithm)
   - Set maximum iterations and convergence tolerance

3. **Route Optimization**: NP-hard for multi-hop routes
   - Pre-compute common routes
   - Use heuristics for complex triangulation

4. **Parallelization Opportunities**:
   - Trade flow calculations by product (independent)
   - Route optimization by country-pair
   - Anomaly detection by trade corridor

## Calibration Requirements

### Required Data Sources

1. **Trade Volumes**:
   - UN Comtrade database
   - OECD ICIO tables
   - WIOD inter-country input-output tables

2. **Trade Costs**:
   - OECD Trade Facilitation Indicators
   - World Bank Trade Costs Database
   - UNCTAD transport cost estimates

3. **Tariff Data**:
   - WTO Tariff Database
   - UNCTAD TRAINS
   - Regional trade agreement texts

4. **Distance and Geography**:
   - CEPII GeoDist database
   - Sea route distances from MarineTraffic
   - Infrastructure quality from WEF

### Key Parameters to Calibrate

```python
CALIBRATION_PARAMS = {
    # Gravity model
    'gdp_elasticity_export': 0.8,      # α in gravity equation
    'gdp_elasticity_import': 0.7,      # β in gravity equation
    'distance_elasticity': -1.2,       # δ in gravity equation
    'tariff_elasticity': -2.5,         # ε in gravity equation

    # Armington elasticities by product type
    'substitution_elasticity': {
        'commodities': 5.0,            # High substitutability
        'differentiated': 2.0,          # Low substitutability
        'strategic': 1.2               # Very low substitutability
    },

    # Transport costs (USD per ton-km)
    'sea_freight_rate': 0.05,
    'air_freight_rate': 2.00,
    'rail_freight_rate': 0.10,
    'road_freight_rate': 0.15,
    'pipeline_rate': 0.03,

    # Chokepoint premiums (% markup)
    'chokepoint_premiums': {
        'suez_canal': 0.15,
        'panama_canal': 0.10,
        'malacca_strait': 0.12,
        'hormuz_strait': 0.20
    },

    # Triangulation thresholds
    're_export_threshold': 0.8,        # Re-exports > 80% of imports
    'margin_threshold': 0.05,          # Markup < 5% suggests pass-through
    'volume_spike_threshold': 2.0      # 2x normal volume
}
```

### Validation Metrics

1. **Bilateral Trade Accuracy**: R² > 0.7 vs actual trade data
2. **Gravity Model Fit**: Standard gravity coefficients
3. **Trade Balance Consistency**: Σ exports = Σ imports globally
4. **Price Pass-through**: Tariff changes affect prices correctly
5. **Triangulation Detection Rate**: Catch known circumvention cases