# Demand Engine

## Purpose & Scope

The Demand Engine formalizes how countries and consumers demand goods and services, both domestically produced and imported. It models substitution between domestic and foreign varieties (Armington assumption), price and income elasticities, and compositional demand across sectors. This Engine is foundational to the CGE system: without properly specified demand, equilibrium prices cannot be determined and trade flows cannot be computed.

Demand in the UTA simulation operates at two levels:
1. **Final Demand:** Households, government, and investment demand for finished goods
2. **Intermediate Demand:** Firms demanding inputs for production (handled via input-output linkages)

This specification focuses primarily on final demand, with integration points for intermediate demand via MRIO tables.

---

## Economic Foundation

### 1. Armington Aggregation

Products are differentiated by country of origin. A country j consuming product p sources it from multiple origins i (including domestic production). These varieties are imperfect substitutes aggregated via a CES (Constant Elasticity of Substitution) function:

```
Q[j,p] = A[j,p] * (Σ[i] α[i,j,p]^(1/σ[p]) * q[i,j,p]^((σ[p]-1)/σ[p]))^(σ[p]/(σ[p]-1))

Where:
- Q[j,p] = Composite good p consumed in country j (Armington aggregate)
- q[i,j,p] = Quantity of product p sourced from country i and consumed in country j
- α[i,j,p] = Share parameter (preference for origin i in country j for product p)
- σ[p] = Elasticity of substitution between origins for product p
- A[j,p] = Efficiency parameter (calibrated scale factor)
```

**Economic Intuition:**
- σ[p] > 1: Varieties are substitutes (higher σ means easier substitution)
- Commodities (oil, wheat): σ ≈ 5-8 (highly substitutable)
- Differentiated products (cars, pharmaceuticals): σ ≈ 2-3 (less substitutable)
- Strategic goods (semiconductors): σ ≈ 1.2-1.5 (very difficult to substitute)

### 2. Demand for Composite Good

The quantity of composite good Q[j,p] demanded in country j depends on:
- Price of the composite good P[j,p]
- Consumer income/expenditure Y[j]
- Population N[j]
- Preferences and subsistence requirements

We use a **Linear Expenditure System (LES)** to capture subsistence consumption and income effects:

```
Q[j,p] = γ[j,p] + (β[j,p] / P[j,p]) * (Y[j] - Σ[k] P[j,k] * γ[j,k])

Where:
- γ[j,p] = Subsistence quantity (minimum consumption of p in country j)
- β[j,p] = Marginal budget share (fraction of supernumerary income spent on p)
- Y[j] = Total expenditure (income) in country j
- Σ[k] P[j,k] * γ[j,k] = Expenditure on subsistence consumption

Constraint: Σ[p] β[j,p] = 1 (budget shares sum to one)
```

**Alternative Formulation (Cobb-Douglas for MVP):**
For simplicity in early implementation, Cobb-Douglas demand is acceptable:

```
Q[j,p] = (β[j,p] * Y[j]) / P[j,p]

Where β[j,p] is the expenditure share on product p.
```

### 3. Source-Specific Demand (Import Composition)

Given total demand Q[j,p] for the composite good, demand for each origin i is derived from cost minimization:

```
q[i,j,p] = α[i,j,p] * (P[i,j,p] / P[j,p])^(-σ[p]) * Q[j,p]

Where:
- P[i,j,p] = Delivered price from origin i to destination j for product p (CIF + tariff)
- P[j,p] = Price index of the composite good (Armington price index)
```

**Armington Price Index:**
```
P[j,p] = (Σ[i] α[i,j,p] * P[i,j,p]^(1-σ[p]))^(1/(1-σ[p]))
```

### 4. Price Elasticities

**Own-Price Elasticity:**
```
ε[j,p] = ∂Q[j,p]/∂P[j,p] * P[j,p]/Q[j,p]

For LES: ε[j,p] = -1 + (γ[j,p] * P[j,p]) / Q[j,p]  (more inelastic for necessities)
For Cobb-Douglas: ε[j,p] = -1  (unitary elastic)
```

**Substitution Elasticity (between origins):**
```
ε[i,j,p] = ∂(q[i,j,p]/q[k,j,p])/∂(P[i,j,p]/P[k,j,p]) * (P[i,j,p]/P[k,j,p])/(q[i,j,p]/q[k,j,p])

For Armington CES: ε[i,j,p] = σ[p]
```

### 5. Income Elasticity

**Income Elasticity:**
```
η[j,p] = ∂Q[j,p]/∂Y[j] * Y[j]/Q[j,p]

For LES: η[j,p] = β[j,p] * Y[j] / (P[j,p] * Q[j,p])  (varies by income level)
For Cobb-Douglas: η[j,p] = 1  (proportional to income)

Empirical ranges:
- Necessities (food, energy): 0.3 - 0.7
- Normal goods (manufactures): 0.8 - 1.2
- Luxuries (high-tech, services): 1.3 - 2.0
```

---

## Data Structures

### Input Data

```python
class DemandInputs:
    # Country Characteristics
    gdp: dict[country] -> float  # Total GDP (or total expenditure)
    population: dict[country] -> float  # Population size
    per_capita_income: dict[country] -> float  # GDP / Population

    # Prices (from Pricing Engine)
    composite_prices: dict[country][product] -> float  # P[j,p]
    bilateral_prices: dict[origin][dest][product] -> float  # P[i,j,p] (CIF + tariff)

    # Preference Parameters (calibrated)
    expenditure_shares: dict[country][product] -> float  # β[j,p]
    subsistence_quantities: dict[country][product] -> float  # γ[j,p]
    armington_shares: dict[origin][dest][product] -> float  # α[i,j,p]
    substitution_elasticities: dict[product] -> float  # σ[p]

    # Policy Shocks (from Policy Engines)
    demand_shocks: dict[country][product] -> float  # Exogenous demand changes
```

### Internal State

```python
class DemandState:
    # Composite Demand
    total_demand: dict[country][product] -> float  # Q[j,p]

    # Bilateral Demand (Import Composition)
    bilateral_demand: np.array[n_countries, n_countries, n_products]  # q[i,j,p]
    domestic_demand: dict[country][product] -> float  # q[j,j,p]
    import_demand: dict[dest][product] -> dict[origin -> float]  # Σ[i≠j] q[i,j,p]

    # Price Indices
    armington_price_index: dict[country][product] -> float  # P[j,p]

    # Elasticity Tracking (for diagnostics)
    realized_price_elasticity: dict[country][product] -> float
    realized_income_elasticity: dict[country][product] -> float
```

### Output Data

```python
class DemandOutputs:
    # For Equilibrium Solver
    total_quantity_demanded: dict[country][product] -> float  # Q[j,p]
    excess_demand: dict[country][product] -> float  # Q[j,p] - Supply[j,p]

    # For Trade Flow Engine
    import_demand_by_source: dict[dest][product][origin] -> float  # q[i,j,p]
    import_value_by_source: dict[dest][product][origin] -> float  # P[i,j,p] * q[i,j,p]

    # For Country Agents
    consumer_surplus: dict[country][product] -> float
    expenditure_by_product: dict[country][product] -> float
    import_penetration_rate: dict[country][product] -> float  # Import / Total Demand

    # For Pricing Engine
    marginal_willingness_to_pay: dict[country][product] -> float
    demand_sensitivity: dict[country][product] -> float  # ∂Q/∂P
```

---

## Implementation Specification

### Algorithm Flow

```python
def update_demand(world_state):
    """
    Main demand update cycle

    Called each simulation step after prices are updated
    """

    # Step 1: Calculate Armington price indices
    armington_prices = calculate_armington_price_indices(
        world_state.bilateral_prices,
        world_state.armington_shares,
        world_state.substitution_elasticities
    )

    # Step 2: Calculate total composite demand (LES or Cobb-Douglas)
    total_demand = calculate_composite_demand(
        armington_prices,
        world_state.gdp,
        world_state.expenditure_shares,
        world_state.subsistence_quantities,
        demand_system='LES'  # or 'cobb_douglas' for MVP
    )

    # Step 3: Decompose into bilateral demands (import composition)
    bilateral_demand = decompose_to_bilateral_demand(
        total_demand,
        world_state.bilateral_prices,
        armington_prices,
        world_state.armington_shares,
        world_state.substitution_elasticities
    )

    # Step 4: Calculate demand-side metrics
    import_penetration = calculate_import_penetration(bilateral_demand)
    consumer_surplus = calculate_consumer_surplus(total_demand, armington_prices)

    # Step 5: Update state and return outputs
    world_state.demand_state.update(
        total_demand=total_demand,
        bilateral_demand=bilateral_demand,
        armington_price_index=armington_prices
    )

    return DemandOutputs(
        total_quantity_demanded=total_demand,
        import_demand_by_source=bilateral_demand,
        import_penetration_rate=import_penetration,
        consumer_surplus=consumer_surplus
    )
```

### Detailed Function Specifications

#### 1. Armington Price Index Calculation

```python
def calculate_armington_price_indices(bilateral_prices, armington_shares, sigma):
    """
    Calculate price index for composite goods under Armington aggregation

    P[j,p] = (Σ[i] α[i,j,p] * P[i,j,p]^(1-σ[p]))^(1/(1-σ[p]))

    Parameters:
    - bilateral_prices: dict[origin][dest][product] -> float
    - armington_shares: dict[origin][dest][product] -> float (α[i,j,p])
    - sigma: dict[product] -> float (σ[p])

    Returns:
    - armington_prices: dict[dest][product] -> float
    """
    armington_prices = {}

    for dest in countries:
        armington_prices[dest] = {}
        for product in products:
            sigma_p = sigma[product]
            sum_term = 0

            for origin in countries:
                alpha_ijp = armington_shares[origin][dest][product]
                price_ijp = bilateral_prices[origin][dest][product]
                sum_term += alpha_ijp * (price_ijp ** (1 - sigma_p))

            armington_prices[dest][product] = sum_term ** (1 / (1 - sigma_p))

    return armington_prices
```

#### 2. Composite Demand Calculation (LES)

```python
def calculate_composite_demand_LES(armington_prices, gdp, beta, gamma):
    """
    Calculate total demand for composite goods using Linear Expenditure System

    Q[j,p] = γ[j,p] + (β[j,p] / P[j,p]) * (Y[j] - Σ[k] P[j,k] * γ[j,k])

    Parameters:
    - armington_prices: dict[country][product] -> float (P[j,p])
    - gdp: dict[country] -> float (Y[j])
    - beta: dict[country][product] -> float (marginal budget shares)
    - gamma: dict[country][product] -> float (subsistence quantities)

    Returns:
    - total_demand: dict[country][product] -> float (Q[j,p])
    """
    total_demand = {}

    for country in countries:
        # Calculate subsistence expenditure
        subsistence_expenditure = sum(
            armington_prices[country][p] * gamma[country][p]
            for p in products
        )

        # Supernumerary income
        supernumerary_income = gdp[country] - subsistence_expenditure

        # Ensure non-negative supernumerary income
        supernumerary_income = max(supernumerary_income, 0)

        total_demand[country] = {}
        for product in products:
            subsistence = gamma[country][product]
            discretionary = (beta[country][product] / armington_prices[country][product]) * supernumerary_income
            total_demand[country][product] = subsistence + discretionary

    return total_demand
```

#### 3. Composite Demand Calculation (Cobb-Douglas - MVP)

```python
def calculate_composite_demand_cobb_douglas(armington_prices, gdp, beta):
    """
    Simplified Cobb-Douglas demand for MVP implementation

    Q[j,p] = (β[j,p] * Y[j]) / P[j,p]

    Parameters:
    - armington_prices: dict[country][product] -> float
    - gdp: dict[country] -> float
    - beta: dict[country][product] -> float (expenditure shares)

    Returns:
    - total_demand: dict[country][product] -> float
    """
    total_demand = {}

    for country in countries:
        total_demand[country] = {}
        for product in products:
            total_demand[country][product] = (
                beta[country][product] * gdp[country] / armington_prices[country][product]
            )

    return total_demand
```

#### 4. Bilateral Demand Decomposition

```python
def decompose_to_bilateral_demand(total_demand, bilateral_prices, armington_prices,
                                   armington_shares, sigma):
    """
    Decompose composite demand into demands for each origin

    q[i,j,p] = α[i,j,p] * (P[i,j,p] / P[j,p])^(-σ[p]) * Q[j,p]

    Parameters:
    - total_demand: dict[dest][product] -> float (Q[j,p])
    - bilateral_prices: dict[origin][dest][product] -> float (P[i,j,p])
    - armington_prices: dict[dest][product] -> float (P[j,p])
    - armington_shares: dict[origin][dest][product] -> float (α[i,j,p])
    - sigma: dict[product] -> float (σ[p])

    Returns:
    - bilateral_demand: dict[origin][dest][product] -> float (q[i,j,p])
    """
    bilateral_demand = {}

    for origin in countries:
        bilateral_demand[origin] = {}
        for dest in countries:
            bilateral_demand[origin][dest] = {}
            for product in products:
                alpha_ijp = armington_shares[origin][dest][product]
                price_ratio = bilateral_prices[origin][dest][product] / armington_prices[dest][product]
                sigma_p = sigma[product]
                Q_jp = total_demand[dest][product]

                bilateral_demand[origin][dest][product] = (
                    alpha_ijp * (price_ratio ** (-sigma_p)) * Q_jp
                )

    return bilateral_demand
```

---

## Integration Points

### Inputs From Other Engines

1. **From Pricing & Market Equilibrium Engine:**
   - Composite good prices P[j,p] (Armington price indices)
   - Bilateral delivered prices P[i,j,p] (CIF + tariff)
   - Price update signals

2. **From Country Agents:**
   - GDP / Total expenditure Y[j]
   - Population N[j]
   - Policy-induced demand shocks (e.g., government procurement)

3. **From Trade Flow Engine:**
   - Delivered prices including transport costs and tariffs
   - Route availability (affects which origins are accessible)

4. **From Sanctions & Geopolitics Engine:**
   - Trade bans (set bilateral demand to zero for sanctioned flows)
   - Preferential access (modify armington shares for allies)

### Outputs To Other Engines

1. **To Pricing & Market Equilibrium Engine:**
   - Total quantity demanded Q[j,p] for market clearing
   - Excess demand signals (Q[j,p] - S[j,p])
   - Demand elasticities for price adjustment algorithms

2. **To Trade Flow Engine:**
   - Import demand by source q[i,j,p]
   - Import value by source P[i,j,p] * q[i,j,p]
   - Source substitution patterns (which origins are preferred)

3. **To Country Agents:**
   - Consumer surplus by product
   - Import penetration rates (domestic vs foreign consumption)
   - Expenditure breakdown

4. **To Subsidy & Industrial Policy Engine:**
   - Demand sensitivity to price changes (informs subsidy effectiveness)
   - Import competition metrics

---

## Calibration Requirements

### Required Data Sources

1. **Expenditure Shares (β[j,p]):**
   - Source: Household consumption surveys, national accounts
   - Database: OECD National Accounts, World Bank Household Surveys
   - Method: Calculate as (Expenditure on p) / (Total Expenditure)

2. **Substitution Elasticities (σ[p]):**
   - Source: Empirical trade literature
   - Typical values:
     - GTAP database: σ ranges from 1.9 (agriculture) to 5.6 (services)
     - Broda & Weinstein (2006): median σ = 4.0 across products
     - Strategic goods: Set lower (1.2-1.5) to reflect dependency
   - Method: Use literature estimates or calibrate to match trade flow responses to tariff changes

3. **Armington Share Parameters (α[i,j,p]):**
   - Source: Observed trade shares
   - Method: Calibrate using initial trade flows:
     ```
     α[i,j,p] = (q[i,j,p]^((σ[p]-1)/σ[p])) / (Σ[k] q[k,j,p]^((σ[p]-1)/σ[p]))
     ```
   - Database: WIOD, OECD ICIO, UN Comtrade

4. **Subsistence Quantities (γ[j,p]) - LES only:**
   - Source: Nutritional requirements (food), minimum energy needs, essential services
   - Method: Set γ[j,p] as percentage of observed consumption in low-income countries
   - Typical values: 40-60% of baseline consumption for necessities, 0% for luxuries

5. **GDP and Population:**
   - Source: World Bank, IMF, OECD
   - Database: World Development Indicators, OECD.Stat

### Calibration Procedure

**Step 1: Collect Baseline Data**
- Obtain initial trade flows T0[i,j,p] from WIOD or OECD ICIO
- Collect GDP, population, and expenditure data
- Gather price data or assume baseline prices = 1 (numeraire)

**Step 2: Calculate Expenditure Shares**
```python
beta[j,p] = sum(T0[i,j,p] * P0[i,j,p] for i in countries) / GDP[j]
```
Normalize: Σ[p] beta[j,p] = 1

**Step 3: Set Substitution Elasticities**
- Use literature values from GTAP or Broda & Weinstein
- Adjust for strategic products (lower σ for semiconductors, rare earths)

**Step 4: Calibrate Armington Shares**
```python
# Calculate total composite consumption
Q0[j,p] = sum(T0[i,j,p] for i in countries)

# Calculate Armington price index
P0[j,p] = (sum(alpha_placeholder * P0[i,j,p]^(1-sigma[p]) for i in countries))^(1/(1-sigma[p]))

# Initial guess: equal shares
alpha_initial[i,j,p] = 1 / n_countries

# Iteratively adjust alpha to match observed trade shares
for iteration in range(max_iter):
    predicted_q[i,j,p] = alpha[i,j,p] * (P0[i,j,p] / P0[j,p])^(-sigma[p]) * Q0[j,p]
    alpha[i,j,p] *= (T0[i,j,p] / predicted_q[i,j,p])^adjustment_rate
    normalize(alpha, axis=origins)
```

**Step 5: Validate**
- Check that predicted demand matches observed consumption
- Verify that expenditure shares sum to one
- Test sensitivity to price changes

### Key Parameters and Typical Ranges

```python
CALIBRATION_PARAMS = {
    # Substitution elasticities by product category
    'sigma': {
        'agriculture': 3.0,       # Moderately substitutable
        'mining': 5.0,            # Highly substitutable (commodities)
        'energy': 4.0,            # Substitutable with some constraints
        'manufacturing': 3.5,     # Differentiated products
        'high_tech': 2.0,         # Low substitutability
        'strategic': 1.3,         # Very low (semiconductors, rare earths)
        'services': 2.5           # Moderate differentiation
    },

    # Income elasticities (for reference, not directly used in Cobb-Douglas)
    'income_elasticity': {
        'food': 0.5,
        'energy': 0.7,
        'manufactures': 1.0,
        'high_tech': 1.5,
        'luxury_services': 1.8
    },

    # Subsistence shares (for LES) - fraction of consumption that is subsistence
    'subsistence_share': {
        'food': 0.5,              # 50% of food consumption is subsistence
        'energy': 0.3,            # 30% for energy
        'basic_manufactures': 0.2,
        'high_tech': 0.0,         # No subsistence for luxuries
        'services': 0.1
    }
}
```

---

## Validation Metrics

1. **Expenditure Conservation:**
   - Check: Σ[p] P[j,p] * Q[j,p] ≈ GDP[j] (within 1% tolerance)

2. **Trade Share Replication:**
   - Check: Baseline bilateral demands match observed trade flows
   - Metric: R² > 0.90 for q[i,j,p] vs observed T[i,j,p]

3. **Elasticity Plausibility:**
   - Check: Own-price elasticity ε[j,p] < 0 (downward sloping demand)
   - Check: Substitution elasticity σ[p] > 1 (substitutes, not complements)

4. **Price Response Test:**
   - Scenario: Increase P[i,j,p] by 10%
   - Expected: q[i,j,p] decreases, q[k,j,p] increases for k≠i
   - Check: Elasticity of substitution equals σ[p]

5. **Income Response Test:**
   - Scenario: Increase GDP[j] by 10%
   - Expected: All Q[j,p] increase proportionally (Cobb-Douglas) or according to income elasticity (LES)
   - Check: Σ[p] P[j,p] * ΔQ[j,p] ≈ ΔY[j]

---

## Strategic Gameplay

### Player-Facing Elements

1. **Demand Forecasts:**
   - Players see projected demand for their exports in each market
   - Sensitivity analysis: How demand changes with price adjustments

2. **Market Share Opportunities:**
   - Identify markets where substitution elasticity is high (easier to capture share)
   - Highlight markets where the player's country has low Armington share (growth potential)

3. **Import Vulnerability:**
   - Display import penetration rates (% of domestic demand satisfied by imports)
   - Flag products with high import dependency and low supplier diversity

4. **Demand Shocks:**
   - Simulate exogenous demand changes (e.g., pandemic shifts, technological obsolescence)
   - Players can respond with production adjustments or trade diversification

### Strategic Trade-Offs

1. **Price vs Volume:**
   - Lower export prices → higher demand (elastic goods)
   - But: Lower revenue per unit
   - Optimal: Maximize (P[i,j,p] - MC[i,p]) * q[i,j,p]

2. **Market Diversification:**
   - High Armington share in one market → vulnerable to policy changes
   - Diversify across markets with different demand characteristics

3. **Product Mix:**
   - Necessities (low σ) → stable demand, less price-sensitive
   - Luxuries (high σ) → volatile demand, high price competition

---

## Example Scenarios

### Example 1: Tariff Impact on Import Demand

**Setup:**
- Country J imports Steel from Country I
- Initial bilateral price: P[I,J,steel] = 500 USD/ton
- Initial quantity: q[I,J,steel] = 1000 tons
- Armington share: α[I,J,steel] = 0.6
- Substitution elasticity: σ[steel] = 4.0
- Composite price: P[J,steel] = 480 USD/ton
- Total demand: Q[J,steel] = 2000 tons

**Scenario:** Country J imposes 25% tariff on imports from Country I

**Step 1: New Bilateral Price**
```
P[I,J,steel]_new = 500 * 1.25 = 625 USD/ton
```

**Step 2: New Composite Price (Armington Index)**
Assume Country K (alternative supplier) has:
- P[K,J,steel] = 510 USD/ton (unchanged)
- α[K,J,steel] = 0.4

```
P[J,steel]_new = (0.6 * 625^(1-4) + 0.4 * 510^(1-4))^(1/(1-4))
               = (0.6 * 625^(-3) + 0.4 * 510^(-3))^(-1/3)
               = (0.6 * 3.90E-9 + 0.4 * 7.53E-9)^(-1/3)
               = (5.35E-9)^(-1/3)
               = 584 USD/ton
```

**Step 3: New Total Demand (Cobb-Douglas)**
Assume β[J,steel] = 0.1, GDP[J] = 10,000,000 USD
```
Q[J,steel]_new = (0.1 * 10,000,000) / 584
                = 1712 tons (down from 2000 due to higher price)
```

**Step 4: New Import from Country I**
```
q[I,J,steel]_new = 0.6 * (625 / 584)^(-4) * 1712
                  = 0.6 * (1.07)^(-4) * 1712
                  = 0.6 * 0.746 * 1712
                  = 767 tons (down from 1000)
```

**Step 5: New Import from Country K**
```
q[K,J,steel]_new = 0.4 * (510 / 584)^(-4) * 1712
                  = 0.4 * (0.873)^(-4) * 1712
                  = 0.4 * 1.715 * 1712
                  = 1173 tons (up from 800)
```

**Result:**
- Country I loses 233 tons of exports (23% decline)
- Country K gains 373 tons (47% increase)
- Total imports decrease to 1940 tons
- Country J experiences slight domestic substitution (60 tons)

---

### Example 2: Income Shock and Demand Adjustment

**Setup:**
- Country C experiences 10% GDP growth
- Initial GDP: Y[C] = 1,000,000 USD
- Products: Food, Manufactures, Luxuries
- Expenditure shares: β[C,food] = 0.3, β[C,mfg] = 0.5, β[C,lux] = 0.2
- Prices: P[C,food] = 10, P[C,mfg] = 50, P[C,lux] = 200

**Initial Demand (Cobb-Douglas):**
```
Q[C,food] = (0.3 * 1,000,000) / 10 = 30,000 units
Q[C,mfg] = (0.5 * 1,000,000) / 50 = 10,000 units
Q[C,lux] = (0.2 * 1,000,000) / 200 = 1,000 units
```

**After 10% GDP Increase:**
```
Y[C]_new = 1,100,000 USD

Q[C,food]_new = (0.3 * 1,100,000) / 10 = 33,000 units (+10%)
Q[C,mfg]_new = (0.5 * 1,100,000) / 50 = 11,000 units (+10%)
Q[C,lux]_new = (0.2 * 1,100,000) / 200 = 1,100 units (+10%)
```

**Interpretation:**
- With Cobb-Douglas, all demands increase proportionally (unitary income elasticity)
- With LES, necessities (food) would increase less than 10%, luxuries more than 10%

---

## Computational Considerations

1. **Armington Price Index Calculation:**
   - CES aggregation can be numerically unstable for extreme σ values
   - Use logarithmic formulation for σ ≠ 1:
     ```
     log(P[j,p]) = (1/(1-σ[p])) * log(Σ[i] α[i,j,p] * exp((1-σ[p]) * log(P[i,j,p])))
     ```

2. **Budget Share Normalization:**
   - Ensure Σ[p] β[j,p] = 1 after calibration
   - Renormalize if parameters are adjusted:
     ```
     β[j,p] = β[j,p] / Σ[k] β[j,k]
     ```

3. **Handling Zero Flows:**
   - If q[i,j,p] = 0 in baseline, set α[i,j,p] = small_epsilon (e.g., 1e-6)
   - Prevents division by zero in calibration
   - Allows potential trade to emerge under policy changes

4. **Convergence in Iterative Calibration:**
   - Use damped updates: α_new = λ * α_calculated + (1-λ) * α_old
   - Typical damping: λ = 0.3
   - Convergence criterion: max|α_new - α_old| < 1e-5

---

## Extensions and Future Enhancements

1. **Non-Homothetic Preferences:**
   - Implement full LES to capture income-dependent expenditure patterns
   - Important for modeling development and inequality

2. **Intermediate Demand:**
   - Integrate with MRIO tables for input-output linkages
   - Firms demand inputs based on production technology

3. **Demand for Varieties:**
   - Model demand for firm-level varieties (Dixit-Stiglitz)
   - Allows for entry/exit of firms and product differentiation

4. **Dynamic Demand:**
   - Habit formation and durability
   - Intertemporal substitution (savings vs consumption)

5. **Quality Differentiation:**
   - Extend Armington to include quality ladders
   - Higher prices may signal higher quality, not just tariffs

---

## References and Data Sources

**Theoretical Foundation:**
- Armington, P. S. (1969). "A Theory of Demand for Products Distinguished by Place of Production."
- Hertel, T. W. (1997). "Global Trade Analysis: Modeling and Applications." GTAP Book.
- Deaton, A., & Muellbauer, J. (1980). "Economics and Consumer Behavior."

**Empirical Elasticities:**
- Broda, C., & Weinstein, D. E. (2006). "Globalization and the Gains from Variety." QJE.
- GTAP Database: https://www.gtap.agecon.purdue.edu/
- Imbs, J., & Mejean, I. (2015). "Elasticity Optimism." AEJ: Macro.

**Data Sources:**
- WIOD (World Input-Output Database): http://www.wiod.org/
- OECD ICIO (Inter-Country Input-Output): https://www.oecd.org/sti/ind/inter-country-input-output-tables.htm
- UN Comtrade: https://comtrade.un.org/
- World Bank Household Surveys: https://microdata.worldbank.org/

---

**End of Demand Engine Specification**
