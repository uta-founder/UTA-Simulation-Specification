# Energy & Logistics Module

## Purpose & Scope

The Energy & Logistics Module models the physical infrastructure and energy systems that enable global trade, capturing transport costs, energy pricing, infrastructure capacity constraints, and critical chokepoint vulnerabilities. It provides the cost structure for trade flows and identifies strategic bottlenecks that can become targets or leverage points in geopolitical conflicts. The module also models energy as both a tradable commodity and a critical input to production and transportation.

This module links physical geography to economic activity, ensuring that trade flows respect real-world constraints: ships need fuel, pipelines have capacity limits, chokepoints can be blocked, and infrastructure requires maintenance. It captures the "physics" layer underlying the economic simulation.

## Key Components

### 1. Energy Pricing System
- **Crude Oil Market**: Global benchmark pricing with regional differentials
- **Natural Gas Markets**: Regional markets with limited arbitrage (LNG linkage)
- **Electricity Grids**: National/regional pricing with interconnection
- **Renewable Energy**: Capacity factors and marginal cost pricing
- **Energy Derivatives**: Futures markets for hedging

### 2. Transportation Network
- **Maritime Shipping**: Container, bulk, tanker routes with fuel costs
- **Rail Systems**: Continental freight networks
- **Road Transport**: Last-mile and regional distribution
- **Pipeline Networks**: Oil, gas, chemical pipelines
- **Air Cargo**: High-value, time-sensitive goods

### 3. Chokepoint Registry
- **Maritime Straits**: Suez, Panama, Malacca, Hormuz, Bab el-Mandeb
- **Land Borders**: Critical crossing points
- **Pipeline Junctions**: Concentration nodes
- **Port Infrastructure**: Container terminals, LNG terminals
- **Digital Infrastructure**: Subsea cables, satellite networks

### 4. Infrastructure Capacity
- **Port Throughput**: Container handling, bulk loading capacity
- **Pipeline Capacity**: Maximum flow rates
- **Storage Facilities**: Strategic reserves, commercial stocks
- **Refining Capacity**: Processing bottlenecks
- **Grid Capacity**: Transmission constraints

## Data Structures

### Input Data
```python
class EnergyLogisticsInputs:
    # Energy Fundamentals
    oil_production: dict[country] -> float                    # Barrels/day
    gas_production: dict[country] -> float                    # BCM/year
    coal_production: dict[country] -> float                   # Tonnes/year
    renewable_capacity: dict[country][type] -> float          # MW installed

    # Energy Consumption
    energy_intensity: dict[country][sector] -> float          # Energy/output
    transport_fuel_demand: dict[mode] -> float                # Derived demand

    # Infrastructure Assets
    pipeline_network: dict[(origin, destination)] -> {
        'capacity': float,                                    # Max flow
        'current_utilization': float,                         # % of capacity
        'fuel_type': enum[OIL, GAS, CHEMICAL],
        'ownership': country,
        'vulnerability': float                                # 0-1 risk score
    }

    port_registry: dict[port] -> {
        'country': country,
        'throughput_capacity': float,                         # TEU/year or tonnes
        'utilization': float,
        'chokepoint_exposure': float,                         # Dependency on straits
        'infrastructure_quality': float                       # 0-1 score
    }

    chokepoint_status: dict[chokepoint] -> {
        'location': (lat, lon),
        'type': enum[STRAIT, CANAL, BORDER, PIPELINE],
        'daily_throughput': float,
        'alternative_routes': list[route],
        'control': country,
        'blockade_probability': float
    }

    # From Trade Module
    trade_volumes: dict[origin][destination][product] -> float
    trade_value: dict[origin][destination] -> float

    # From Geopolitics Module
    sanctions: list[Sanction]
    conflict_zones: list[region]
```

### Internal State
```python
class EnergyLogisticsState:
    # Energy Prices
    oil_price: dict[benchmark] -> float                       # Brent, WTI, Dubai
    gas_price: dict[market] -> float                          # Henry Hub, TTF, JKM
    coal_price: dict[type] -> float                           # Thermal, coking
    electricity_price: dict[country] -> float

    # Transport Cost Matrix
    sea_freight_cost: dict[route][vessel_type] -> float       # USD/ton or TEU
    rail_freight_cost: dict[route] -> float
    road_freight_cost: dict[route] -> float
    pipeline_tariff: dict[pipeline] -> float
    air_freight_cost: dict[route] -> float

    # Route Optimization
    optimal_routes: dict[(origin, destination, cargo_type)] -> {
        'primary_route': list[waypoints],
        'alternative_routes': list[list[waypoints]],
        'cost': float,
        'time': float,
        'risk': float
    }

    # Capacity Utilization
    infrastructure_stress: dict[facility] -> float            # 0-1 congestion
    bottleneck_registry: list[{
        'location': facility,
        'severity': float,
        'duration': int,
        'affected_flows': list[trade_flow]
    }]

    # Energy Security
    strategic_reserves: dict[country][fuel_type] -> float     # Days of consumption
    import_dependency: dict[country][fuel_type] -> float      # Import/consumption
    supplier_concentration: dict[country][fuel_type] -> float  # HHI
```

### Output Data
```python
class EnergyLogisticsOutputs:
    # For Trade Flow Module
    transport_cost_matrix: dict[origin][destination][mode] -> float
    route_availability: dict[(origin, destination)] -> list[feasible_routes]
    delivery_time: dict[origin][destination][mode] -> int     # Days

    # For Pricing Module
    energy_cost_shock: dict[country][sector] -> float         # Input cost change
    transport_inflation: float                                # Fuel pass-through

    # For Country Agents
    energy_security_score: dict[country] -> float             # 0-1 vulnerability
    chokepoint_exposure: dict[country] -> list[(chokepoint, impact)]
    logistics_competitiveness: dict[country] -> float         # Infrastructure quality

    # For Geopolitics Module
    strategic_chokepoints: list[{
        'chokepoint': location,
        'throughput_value': float,                            # USD/day
        'affected_countries': list[country],
        'control': country,
        'disruption_impact': dict[country] -> float
    }]

    # For Compliance Module
    unusual_routing: list[{
        'flow': (origin, destination, product),
        'expected_route': route,
        'actual_route': route,
        'cost_difference': float,
        'sanction_avoidance_flag': bool
    }]
```

## Economic Logic

### 1. Energy Price Formation

**Oil Price Model (Hotelling + Supply-Demand)**:
```python
def calculate_oil_price(supply, demand, inventories, expectations):
    # Short-run price (demand-driven)
    excess_demand = demand - supply
    price_pressure = excess_demand / demand  # Percentage gap

    # Inventory buffer effect
    inventory_cushion = inventories / (demand * DAYS_OF_COVER_TARGET)
    inventory_factor = 1 - 0.3 * (inventory_cushion - 1)  # Price falls if high inventory

    # Base price with elasticity
    base_price = REFERENCE_PRICE * (1 + price_pressure * PRICE_ELASTICITY)

    # Apply inventory adjustment
    adjusted_price = base_price * inventory_factor

    # Forward curve (Hotelling rule: price growth = interest rate)
    forward_prices = [
        adjusted_price * (1 + DISCOUNT_RATE) ** t
        for t in range(FORECAST_HORIZON)
    ]

    return adjusted_price, forward_prices
```

**Gas Price Regionalization**:
```python
def calculate_gas_prices(production, demand, lng_capacity):
    prices = {}

    # Regional markets with limited arbitrage
    for region in ['north_america', 'europe', 'asia']:
        local_supply = production[region] + imports[region]
        local_demand = demand[region]

        # Market clearing
        prices[region] = clear_market(local_supply, local_demand, params[region])

    # LNG arbitrage (limited by shipping capacity)
    arbitrage_potential = max(prices.values()) - min(prices.values())
    lng_cost = LNG_LIQUEFACTION_COST + LNG_SHIPPING_COST + LNG_REGASIFICATION_COST

    if arbitrage_potential > lng_cost and lng_capacity.available > 0:
        # Partial convergence
        avg_price = sum(prices.values()) / len(prices)
        for region in prices:
            prices[region] = 0.7 * prices[region] + 0.3 * avg_price

    return prices
```

### 2. Transport Cost Calculation

**Mode Selection Optimization**:
```python
def select_optimal_transport(origin, destination, cargo, params):
    modes = []

    # Sea freight (if both have ports)
    if has_port(origin) and has_port(destination):
        sea_route = find_sea_route(origin, destination)
        sea_cost = calculate_sea_freight(
            distance=sea_route.distance,
            cargo_weight=cargo.weight,
            cargo_value=cargo.value,
            fuel_price=fuel_price,
            vessel_type=select_vessel(cargo)
        )
        modes.append({'mode': 'sea', 'cost': sea_cost, 'time': sea_route.days})

    # Rail freight (if connected)
    if has_rail_connection(origin, destination):
        rail_cost = calculate_rail_freight(
            distance=rail_distance(origin, destination),
            cargo_weight=cargo.weight,
            tariff=rail_tariff(origin, destination)
        )
        modes.append({'mode': 'rail', 'cost': rail_cost, 'time': rail_days})

    # Road freight (always available)
    road_cost = calculate_road_freight(
        distance=road_distance(origin, destination),
        cargo_weight=cargo.weight,
        fuel_price=diesel_price
    )
    modes.append({'mode': 'road', 'cost': road_cost, 'time': road_days})

    # Air freight (for high-value or perishable)
    if cargo.value_density > AIR_THRESHOLD or cargo.is_perishable:
        air_cost = calculate_air_freight(
            distance=great_circle_distance(origin, destination),
            cargo_weight=cargo.weight,
            fuel_price=jet_fuel_price
        )
        modes.append({'mode': 'air', 'cost': air_cost, 'time': air_hours/24})

    # Select mode minimizing total cost (transport + inventory + risk)
    total_costs = [
        m['cost'] + cargo.value * INVENTORY_COST_RATE * m['time'] + cargo.value * m.get('risk', 0)
        for m in modes
    ]

    optimal_mode = modes[total_costs.index(min(total_costs))]
    return optimal_mode
```

**Sea Freight Cost Function**:
```python
def calculate_sea_freight(distance, cargo_weight, fuel_price, vessel_type):
    # Base cost components
    vessel_params = VESSEL_CHARACTERISTICS[vessel_type]

    # Fuel consumption (proportional to distance and weight)
    fuel_consumption = (vessel_params['fuel_consumption_rate'] *
                       distance / vessel_params['speed'] *
                       (1 + 0.3 * cargo_weight / vessel_params['capacity']))

    fuel_cost = fuel_consumption * fuel_price

    # Operating costs
    daily_operating_cost = vessel_params['crew_cost'] + vessel_params['maintenance']
    voyage_days = distance / vessel_params['speed'] / 24
    operating_cost = daily_operating_cost * voyage_days

    # Port fees
    port_costs = PORT_ENTRY_FEE[origin] + PORT_ENTRY_FEE[destination]

    # Canal fees if applicable
    canal_costs = 0
    if route.crosses_suez:
        canal_costs += SUEZ_CANAL_FEE
    if route.crosses_panama:
        canal_costs += PANAMA_CANAL_FEE

    # Insurance premium (risk-based)
    insurance_premium = cargo_weight * INSURANCE_RATE * (1 + route.piracy_risk)

    total_cost = fuel_cost + operating_cost + port_costs + canal_costs + insurance_premium

    # Per-unit cost
    unit_cost = total_cost / cargo_weight

    return unit_cost
```

### 3. Chokepoint Vulnerability Assessment

```python
def assess_chokepoint_risk(country, chokepoint, trade_flows):
    # Direct exposure
    flows_through_chokepoint = [
        flow for flow in trade_flows[country]
        if flow.route.passes_through(chokepoint)
    ]

    exposure_value = sum([flow.value for flow in flows_through_chokepoint])
    exposure_share = exposure_value / country.total_trade_value

    # Alternative route analysis
    alternative_costs = []
    for flow in flows_through_chokepoint:
        alt_route = find_alternative_route(
            flow.origin, flow.destination,
            avoid=[chokepoint]
        )

        if alt_route:
            additional_cost = alt_route.cost - flow.route.cost
            additional_time = alt_route.time - flow.route.time
            alternative_costs.append({
                'cost_increase': additional_cost / flow.value,
                'time_increase': additional_time,
                'feasible': additional_cost < flow.value * DISRUPTION_TOLERANCE
            })
        else:
            alternative_costs.append({
                'cost_increase': float('inf'),
                'feasible': False
            })

    # Risk score
    feasible_alternatives = sum([1 for ac in alternative_costs if ac['feasible']])
    alternative_ratio = feasible_alternatives / len(alternative_costs)

    vulnerability_score = exposure_share * (1 - alternative_ratio) * chokepoint.blockade_probability

    return {
        'exposure_value': exposure_value,
        'exposure_share': exposure_share,
        'vulnerable_flows': len([ac for ac in alternative_costs if not ac['feasible']]),
        'vulnerability_score': vulnerability_score,
        'mitigation_cost': sum([ac['cost_increase'] for ac in alternative_costs if ac['feasible']])
    }
```

### 4. Energy Security Metrics

```python
def calculate_energy_security(country):
    scores = {}

    for fuel_type in ['oil', 'gas', 'coal']:
        # Import dependency
        imports = country.energy_imports[fuel_type]
        consumption = country.energy_consumption[fuel_type]
        import_dependency = imports / consumption if consumption > 0 else 0

        # Supplier concentration (HHI)
        import_shares = [
            (imports_from[supplier] / imports) ** 2
            for supplier in country.import_sources[fuel_type]
        ]
        hhi = sum(import_shares)

        # Reserve adequacy
        reserves = country.strategic_reserves[fuel_type]
        days_of_cover = reserves / (consumption / 365)

        # Geopolitical risk of suppliers
        supplier_risk = sum([
            (imports_from[supplier] / imports) * geopolitical_risk[supplier]
            for supplier in country.import_sources[fuel_type]
        ])

        # Composite score (0 = secure, 1 = vulnerable)
        security_score = (
            0.3 * import_dependency +
            0.3 * hhi +
            0.2 * max(0, 1 - days_of_cover / TARGET_DAYS_OF_COVER) +
            0.2 * supplier_risk
        )

        scores[fuel_type] = 1 - security_score  # Invert so higher = more secure

    # Overall energy security
    weights = {'oil': 0.4, 'gas': 0.4, 'coal': 0.2}
    overall_security = sum([scores[ft] * weights[ft] for ft in scores])

    return overall_security, scores
```

## Integration Points

### Inputs From Other Modules

1. **From Trade Flow Module**:
   - Bilateral trade volumes by product
   - Actual routes selected
   - Trade flow changes over time

2. **From Demand Module**:
   - Energy consumption requirements
   - Derived demand for transport services

3. **From Country Agents**:
   - Production volumes (energy intensity)
   - Infrastructure investment decisions
   - Strategic reserve policies

4. **From Sanctions & Geopolitics Module**:
   - Energy embargoes and restrictions
   - Chokepoint control and threats
   - Alliance access to infrastructure

5. **From Pricing Module**:
   - Energy price signals
   - Transport cost pass-through
   - Inflation transmission

### Outputs To Other Modules

1. **To Trade Flow Module**:
   - Transport cost matrix by mode and route
   - Route availability and capacity constraints
   - Delivery time estimates

2. **To Pricing & Equilibrium Module**:
   - Energy input costs by country and sector
   - Transport cost inflation
   - Supply shock propagation

3. **To Country Agents**:
   - Energy security scores and vulnerabilities
   - Infrastructure bottleneck warnings
   - Investment opportunities

4. **To Geopolitics Module**:
   - Chokepoint strategic value
   - Energy leverage metrics
   - Infrastructure vulnerability assessment

5. **To Compliance Module**:
   - Unusual route selections (circumvention signal)
   - Energy trade anomalies
   - Infrastructure misuse detection

## Implementation Guidance

### Algorithm Flow

```python
def update_energy_logistics(world_state):
    """Main energy and logistics update cycle"""

    # Step 1: Update energy prices
    energy_markets = update_energy_markets(
        world_state.production,
        world_state.consumption,
        world_state.inventories
    )

    # Step 2: Calculate transport costs
    transport_costs = {}
    for origin in world_state.countries:
        for destination in world_state.countries:
            for mode in TRANSPORT_MODES:
                transport_costs[origin][destination][mode] = calculate_transport_cost(
                    origin, destination, mode,
                    fuel_prices=energy_markets.fuel_prices,
                    infrastructure=world_state.infrastructure
                )

    # Step 3: Optimize routes for active trade flows
    optimized_routes = {}
    for flow in world_state.active_trade_flows:
        route_options = generate_route_options(
            flow.origin, flow.destination,
            flow.cargo_type,
            avoid_regions=world_state.conflict_zones,
            respect_sanctions=world_state.sanctions
        )

        best_route = select_optimal_route(
            route_options,
            transport_costs,
            flow.value,
            flow.time_sensitivity
        )

        optimized_routes[flow.id] = best_route

    # Step 4: Check capacity constraints
    infrastructure_utilization = calculate_utilization(
        optimized_routes,
        world_state.infrastructure_capacity
    )

    bottlenecks = identify_bottlenecks(
        infrastructure_utilization,
        threshold=CONGESTION_THRESHOLD
    )

    # Step 5: Assess chokepoint vulnerabilities
    chokepoint_risks = {}
    for country in world_state.countries:
        for chokepoint in CRITICAL_CHOKEPOINTS:
            risk = assess_chokepoint_risk(
                country, chokepoint,
                optimized_routes, world_state
            )
            chokepoint_risks[country][chokepoint] = risk

    # Step 6: Calculate energy security
    energy_security_scores = {
        country: calculate_energy_security(country, world_state)
        for country in world_state.countries
    }

    # Step 7: Detect anomalies
    anomalies = detect_logistics_anomalies(
        optimized_routes,
        historical_routes=world_state.route_history,
        sanctions=world_state.sanctions
    )

    # Step 8: Update state
    world_state.energy_prices = energy_markets.prices
    world_state.transport_costs = transport_costs
    world_state.optimal_routes = optimized_routes
    world_state.infrastructure_stress = infrastructure_utilization
    world_state.chokepoint_vulnerabilities = chokepoint_risks

    return {
        'energy_markets': energy_markets,
        'transport_costs': transport_costs,
        'routes': optimized_routes,
        'bottlenecks': bottlenecks,
        'anomalies': anomalies
    }
```

### Computational Considerations

1. **Route Optimization**:
   - Use Dijkstra's algorithm for shortest path
   - Pre-compute common routes and cache
   - Limit alternative route search depth
   - Parallelize by trade flow

2. **Energy Market Clearing**:
   - Use iterative solvers for market equilibrium
   - Handle regional markets separately
   - Implement LNG arbitrage as secondary optimization

3. **Network Analysis**:
   - Represent infrastructure as directed graph
   - Use flow algorithms for capacity checking
   - Identify critical nodes with betweenness centrality

4. **Spatial Calculations**:
   - Pre-compute distance matrices
   - Use spatial indexing for geographic queries
   - Cache route segments

## Calibration Requirements

### Required Data Sources

1. **Energy Data**:
   - IEA World Energy Statistics
   - BP Statistical Review of World Energy
   - EIA International Energy Statistics
   - OPEC Monthly Oil Market Report

2. **Transport Data**:
   - World Bank Logistics Performance Index
   - UNCTAD Review of Maritime Transport
   - IMF Connectivity Platform
   - SeaRoutes API for shipping distances

3. **Infrastructure**:
   - Global Energy Monitor databases
   - Port Economics, Technology and Development
   - Pipeline & Gas Journal annual surveys
   - Airport Council International statistics

4. **Cost Data**:
   - Drewry Maritime Advisors freight rates
   - Baltic Exchange indices
   - Platts price assessments
   - World Bank commodity prices

### Key Parameters to Calibrate

```python
ENERGY_LOGISTICS_CALIBRATION = {
    # Energy price elasticities
    'oil_demand_elasticity': -0.3,              # Short-run inelastic
    'gas_demand_elasticity': -0.5,              # Moderate
    'oil_supply_elasticity': 0.1,               # Very inelastic short-run

    # Transport cost parameters
    'sea_freight_fuel_share': 0.50,             # Fuel as % of cost
    'rail_freight_cost_per_tkm': 0.03,          # USD per tonne-km
    'road_freight_cost_per_tkm': 0.12,          # USD per tonne-km
    'air_freight_cost_per_tkm': 1.80,           # USD per tonne-km
    'pipeline_cost_per_tkm': 0.01,              # USD per tonne-km

    # Vessel characteristics
    'container_ship': {
        'capacity': 14000,                       # TEU
        'fuel_consumption': 225,                 # tonnes/day
        'speed': 22,                             # knots
        'daily_operating_cost': 15000            # USD/day
    },

    'bulk_carrier': {
        'capacity': 180000,                      # DWT
        'fuel_consumption': 50,                  # tonnes/day
        'speed': 14,                             # knots
        'daily_operating_cost': 8000             # USD/day
    },

    'tanker': {
        'capacity': 320000,                      # DWT (VLCC)
        'fuel_consumption': 80,                  # tonnes/day
        'speed': 15,                             # knots
        'daily_operating_cost': 12000            # USD/day
    },

    # Chokepoint costs
    'suez_canal_fee': 700000,                   # USD per transit
    'panama_canal_fee': 450000,                 # USD per transit
    'alternative_route_cost': {
        'suez_via_cape': 1.8,                   # Cost multiplier
        'panama_via_cape': 1.5                  # Cost multiplier
    },

    # Strategic reserves
    'target_oil_reserves_days': 90,             # IEA standard
    'target_gas_reserves_days': 30,             # Typical
    'reserve_drawdown_cost': 1.2                # Premium over market

}
```

### Validation Metrics

1. **Transport Cost Accuracy**: Within 15% of actual freight rates
2. **Energy Price Correlation**: R² > 0.85 vs benchmark prices
3. **Route Selection**: 80% match with observed trade routes
4. **Infrastructure Utilization**: Capacity factors within 10% of reported
5. **Chokepoint Value**: Disruption costs match historical events ±25%