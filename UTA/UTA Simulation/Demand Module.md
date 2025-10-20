# Demand Module

## Purpose & Scope

The Demand Module models consumption patterns, preferences, and demand elasticities for all products across countries. It captures both domestic demand (internal consumption) and import demand, incorporating substitution effects between domestic production and imports, as well as between different import sources. The module provides the demand-side equations for market equilibrium and drives import requirements that feed into trade flow decisions.

This module implements nested demand structures that reflect real-world consumption hierarchies: consumers first decide total consumption levels, then allocate between domestic and imported varieties, and finally choose among import sources based on price and preference.

## Key Components

### 1. Demand Function System
- **Aggregate Demand**: Total consumption demand by country and product
- **Armington Aggregator**: CES nesting of domestic vs import varieties
- **Import Source Allocation**: Second-stage CES across import origins
- **Price Responsiveness**: Own-price and cross-price elasticities

### 2. Utility Maximization Framework
- Representative consumer optimization
- Budget constraint enforcement
- Nested CES utility structure
- Corner solutions for zero consumption

### 3. Demand Shifters
- Income effects (GDP per capita changes)
- Population dynamics
- Preference shocks (policy-induced or exogenous)
- Seasonal and cyclical factors

### 4. Substitution Mechanics
- Domestic-import substitution (first nest)
- Import-import substitution (second nest)
- Cross-product substitution (for close substitutes)
- Quality-adjusted preferences

## Data Structures

### Input Data
```python
class DemandInputs:
    # Economic Fundamentals
    gdp_per_capita: dict[country] -> float                    # Income level
    population: dict[country] -> float                        # Market size
    price_indices: dict[country] -> float                     # General price level

    # Product Prices
    domestic_prices: dict[country][product] -> float          # Local production price
    import_prices: dict[country][product][source] -> float    # CIF prices by source

    # From Trade Flow Module
    available_suppliers: dict[country][product] -> list[supplier]
    supply_reliability: dict[supplier][product] -> float      # 0-1 score

    # Policy Variables
    consumption_taxes: dict[country][product] -> float        # VAT, excise
    consumption_subsidies: dict[country][product] -> float    # Food, energy subsidies
```

### Internal Parameters
```python
class DemandParameters:
    # Elasticity Parameters (calibrated)
    income_elasticity: dict[product] -> float                 # ε_income
    price_elasticity_own: dict[product] -> float             # ε_own
    armington_elasticity: dict[product] -> float             # σ_domestic/import
    import_substitution_elasticity: dict[product] -> float    # σ_between_sources

    # Preference Parameters
    consumption_shares: dict[country][product] -> float       # α in utility
    domestic_preference_bias: dict[country][product] -> float # Home bias parameter
    import_source_preferences: dict[country][product][source] -> float

    # Subsistence Consumption
    minimum_consumption: dict[country][product] -> float      # Stone-Geary LES

    # Dynamic Adjustment
    adjustment_speed: dict[product] -> float                  # Partial adjustment
```

### Output Data
```python
class DemandOutputs:
    # Consumption Quantities
    total_demand: dict[country][product] -> float
    domestic_demand: dict[country][product] -> float
    import_demand: dict[country][product] -> float
    import_by_source: dict[country][product][source] -> float

    # Derived Metrics
    import_penetration: dict[country][product] -> float       # Import share
    demand_elasticity_realized: dict[country][product] -> float
    consumer_surplus: dict[country] -> float

    # Market Signals
    excess_demand: dict[country][product] -> float           # Shortage signal
    substitution_pressure: dict[country][product] -> float    # Switch incentive

    # For Welfare Analysis
    utility_level: dict[country] -> float
    equivalent_variation: dict[country] -> float              # Welfare change
```

## Economic Logic

### 1. Nested CES Demand Structure

**First Stage - Total Consumption**:
```
Q[c,p] = α[c,p] * (Y[c]/POP[c])^ε_y[p] * P_composite[c,p]^ε_p[p]

Where:
- Q[c,p] = Total quantity demanded of product p in country c
- α[c,p] = Preference parameter
- Y[c]/POP[c] = Per capita income
- ε_y[p] = Income elasticity
- P_composite[c,p] = Composite price index
- ε_p[p] = Price elasticity
```

**Second Stage - Armington Aggregation**:
```
Q[c,p] = (δ_d[c,p] * Q_d[c,p]^((σ-1)/σ) + δ_m[c,p] * Q_m[c,p]^((σ-1)/σ))^(σ/(σ-1))

Where:
- Q_d[c,p] = Domestic variety consumption
- Q_m[c,p] = Import variety consumption
- δ_d, δ_m = Share parameters (sum to 1)
- σ = Armington elasticity of substitution
```

**Third Stage - Import Source Allocation**:
```
Q_m[c,p] = (Σ[s] β[c,p,s] * Q[c,p,s]^((ρ-1)/ρ))^(ρ/(ρ-1))

Where:
- Q[c,p,s] = Imports from source country s
- β[c,p,s] = Source preference parameter
- ρ = Elasticity of substitution between import sources
```

### 2. Optimal Allocation Conditions

**Domestic vs Import Share**:
```python
def calculate_domestic_import_shares(prices, params):
    # Relative price
    price_ratio = prices['import'] / prices['domestic']

    # Apply home bias
    adjusted_ratio = price_ratio * (1 + params['home_bias'])

    # CES allocation
    import_share = 1 / (1 + (adjusted_ratio)**params['armington_elasticity'])
    domestic_share = 1 - import_share

    return domestic_share, import_share
```

**Import Source Selection**:
```python
def allocate_import_sources(import_demand, source_prices, params):
    # Calculate price index
    price_index = sum([
        params['source_preference'][s] * price**(1-params['rho'])
        for s, price in source_prices.items()
    ])**(1/(1-params['rho']))

    # Allocate by relative prices
    shares = {}
    for source, price in source_prices.items():
        relative_price = price / price_index
        shares[source] = params['source_preference'][source] * \
                        (relative_price)**(-params['rho'])

    # Normalize and apply to total import demand
    total_share = sum(shares.values())
    quantities = {s: import_demand * share/total_share
                 for s, share in shares.items()}

    return quantities
```

### 3. Income and Substitution Effects

**Slutsky Decomposition**:
```python
def calculate_demand_response(price_change, income_change, params):
    # Marshallian demand change
    total_effect = params['own_price_elasticity'] * price_change + \
                   params['income_elasticity'] * income_change

    # Decompose into substitution and income effects
    substitution_effect = params['compensated_elasticity'] * price_change
    income_effect = total_effect - substitution_effect

    return {
        'total': total_effect,
        'substitution': substitution_effect,
        'income': income_effect
    }
```

### 4. Dynamic Adjustment Process

**Partial Adjustment Model**:
```
Q[t] = Q[t-1] + λ * (Q_desired[t] - Q[t-1]) + ε[t]

Where:
- λ = Adjustment speed parameter (0 < λ ≤ 1)
- Q_desired = Long-run equilibrium demand
- ε = Stochastic shock
```

### 5. Welfare Calculations

**Consumer Surplus**:
```python
def calculate_consumer_surplus(demand_curve, price_before, price_after, quantity):
    # For linear demand
    if demand_curve['type'] == 'linear':
        cs_change = 0.5 * (price_before - price_after) * \
                    (quantity_before + quantity_after)

    # For CES demand
    elif demand_curve['type'] == 'ces':
        # Use expenditure function
        cs_change = expenditure(price_after, utility_before) - \
                   expenditure(price_before, utility_before)

    return cs_change
```

## Integration Points

### Inputs From Other Modules

1. **From Trade Flow Module**:
   - Available import sources and reliability
   - Delivered prices (CIF + tariff)
   - Supply constraints and quotas

2. **From Pricing & Equilibrium Module**:
   - Equilibrium prices for all products
   - Price indices and inflation rates
   - Market clearing signals

3. **From Country Agents**:
   - GDP and population data
   - Domestic production volumes
   - Policy stance (protectionist vs open)

4. **From Subsidy & Industrial Policy Module**:
   - Consumption subsidies (food, fuel)
   - VAT and excise tax rates
   - Public procurement demand

5. **From Sanctions & Geopolitics Module**:
   - Import bans and restrictions
   - Preference shifts from political tensions
   - Strategic stockpiling requirements

### Outputs To Other Modules

1. **To Trade Flow Module**:
   - Import demand by product and preferred sources
   - Demand elasticities for trade modeling
   - Maximum willingness to pay

2. **To Pricing & Equilibrium Module**:
   - Total demand quantities for market clearing
   - Demand curves and elasticities
   - Excess demand signals

3. **To Country Agents**:
   - Consumer welfare metrics
   - Import dependence ratios
   - Demand satisfaction levels

4. **To Compliance & Detection Module**:
   - Unusual demand spikes (hoarding signals)
   - Substitution patterns (circumvention indicator)

## Implementation Guidance

### Algorithm Flow

```python
def update_demand(world_state):
    """Main demand calculation cycle"""

    for country in world_state.countries:
        # Step 1: Calculate income-driven demand
        base_demand = calculate_base_demand(
            country.gdp_per_capita,
            country.population,
            country.preferences
        )

        # Step 2: Apply price effects
        for product in world_state.products:
            # Get all prices
            prices = get_price_structure(country, product)

            # First nest: domestic vs import
            domestic_share, import_share = armington_allocation(
                prices['domestic'],
                prices['import_composite'],
                params['armington_elasticity'][product]
            )

            # Second nest: allocate among import sources
            if import_share > 0:
                import_allocation = allocate_imports(
                    import_share * base_demand[product],
                    prices['import_by_source'],
                    params['source_substitution'][product]
                )

            # Step 3: Check constraints
            final_demand = apply_constraints(
                base_demand[product],
                country.budget_constraint,
                world_state.supply_limits
            )

            # Step 4: Calculate welfare
            welfare_change = calculate_welfare_impact(
                prices, quantities, country.utility_function
            )

        # Step 5: Update state
        country.demand_state.update(final_demand, welfare_change)

    return aggregate_demand_signals(world_state)
```

### Computational Considerations

1. **CES Function Evaluation**:
   - Pre-compute elasticity transformations
   - Use log-linear approximations for small changes
   - Cache price indices for repeated calculations

2. **Nested Structure**:
   - Solve recursively from bottom up
   - Maintain consistency between nesting levels
   - Handle corner solutions explicitly

3. **Convergence Issues**:
   - Implement dampening for oscillations
   - Set maximum iterations
   - Use adaptive step sizes

4. **Memory Optimization**:
   - Store only active trade relationships
   - Aggregate minor suppliers
   - Use sparse matrices for preferences

## Calibration Requirements

### Required Data Sources

1. **Consumption Data**:
   - UN National Accounts (final consumption)
   - OECD Input-Output tables (intermediate demand)
   - Household expenditure surveys

2. **Trade Data for Calibration**:
   - Import penetration ratios from WTO
   - Bilateral trade flows from UN Comtrade
   - Product-level import data

3. **Elasticity Estimates**:
   - Academic literature meta-analyses
   - GTAP elasticity database
   - Econometric estimates from time series

4. **Preference Parameters**:
   - Revealed preference from trade data
   - Home bias estimates from gravity models
   - Quality ladders from unit value data

### Key Parameters to Calibrate

```python
DEMAND_CALIBRATION = {
    # Income elasticities by product category
    'income_elasticity': {
        'food_staples': 0.3,           # Necessity
        'food_luxury': 1.2,            # Luxury food
        'energy': 0.8,                 # Normal good
        'manufacturing': 1.0,          # Unitary
        'services': 1.3,               # Superior good
        'raw_materials': 0.7           # Input demand
    },

    # Price elasticities (own-price, Marshallian)
    'price_elasticity': {
        'food_staples': -0.3,          # Inelastic
        'energy': -0.4,                # Inelastic
        'manufacturing': -1.2,         # Elastic
        'luxury_goods': -1.5,          # Very elastic
        'commodities': -0.8            # Moderately elastic
    },

    # Armington elasticities (domestic vs import)
    'armington_elasticity': {
        'homogeneous': 5.0,            # Perfect substitutes
        'differentiated': 2.0,         # Imperfect substitutes
        'unique': 0.5                  # Poor substitutes
    },

    # Import source substitution
    'import_substitution': {
        'commodities': 10.0,           # Very high
        'intermediate': 4.0,           # High
        'consumer_goods': 2.5,         # Moderate
        'specialized': 1.5             # Low
    },

    # Home bias parameters
    'home_bias': {
        'default': 0.2,                # 20% preference for domestic
        'food': 0.4,                   # 40% for food security
        'strategic': 0.6               # 60% for critical goods
    },

    # Dynamic adjustment speeds
    'adjustment_speed': {
        'immediate': 1.0,              # Full adjustment
        'fast': 0.7,                   # Within period
        'normal': 0.4,                 # Gradual
        'slow': 0.2                    # Sticky
    }
}
```

### Validation Metrics

1. **Demand Prediction Accuracy**: MAPE < 10% on out-of-sample
2. **Elasticity Consistency**: Match econometric estimates ±20%
3. **Budget Constraint**: Total expenditure = Income (Walras' Law)
4. **Import Share Stability**: Historical fit R² > 0.8
5. **Welfare Measures**: Consistent with revealed preference axioms