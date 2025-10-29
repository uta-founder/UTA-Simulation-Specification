# Pricing & Market Equilibrium Engine

## Purpose & Scope

The Pricing & Market Equilibrium Engine is the computational core of the UTA simulation's economic engine. It determines market-clearing prices across all products and countries, ensuring that supply equals demand in every market while respecting budget constraints, zero-profit conditions, and macroeconomic accounting identities. This Engine transforms the UTA simulation from a partial equilibrium trade model into a fully-fledged Computable General Equilibrium (CGE) system.

**Core Responsibility:** Given production capacities, consumption needs, trade policies, and behavioral rules from all other Engines, this Engine computes the price vector that clears all markets simultaneously.

**Key Outputs:**
- Equilibrium prices for all products in all locations
- Realized quantities produced and consumed
- Factor prices (wages, capital returns)
- Exchange rates and trade balances

---

## Economic Foundation

### 1. Market Clearing Conditions

For each product p in each country j, the fundamental equilibrium condition is:

```
Supply[j,p] = Demand[j,p]

Where:
Supply[j,p] = Domestic Production[j,p] + Σ[i] Imports[i,j,p]
Demand[j,p] = Domestic Consumption[j,p] + Σ[k] Exports[j,k,p] + Intermediate Use[j,p]
```

**Excess Demand Function:**
```
Z[j,p] = Demand[j,p] - Supply[j,p]

Equilibrium condition: Z[j,p] = 0 for all j, p
```

### 2. Walras' Law

The sum of values of excess demands equals zero (one market clears automatically if all others clear):

```
Σ[j,p] P[j,p] * Z[j,p] = 0

Implication: We can drop one price equation and set it as numeraire (typically P[reference_country, reference_product] = 1)
```

### 3. Zero-Profit Conditions

In perfect competition with constant returns to scale, firms earn zero economic profit:

```
P[j,p] = Σ[i] a[i,j,p] * P[j,i] + w[j] * L[j,p] + r[j] * K[j,p]

Where:
- a[i,j,p] = Input-output coefficient (units of input i per unit of output p in country j)
- w[j] = Wage rate in country j
- L[j,p] = Labor per unit of output p
- r[j] = Capital rental rate in country j
- K[j,p] = Capital per unit of output p
```

**Implication:** Prices are determined by costs, which are themselves prices of inputs.

### 4. Armington Price Linkage

The composite price index (from Demand Engine) links bilateral prices:

```
P[j,p] = (Σ[i] α[i,j,p] * P[i,j,p]^(1-σ[p]))^(1/(1-σ[p]))

Where:
- P[j,p] = Armington composite price (price of aggregate good p in country j)
- P[i,j,p] = Delivered price from origin i to destination j for product p
- P[i,j,p] = P[i,p] * (1 + τ[i,j,p]) * (1 + t[i,j,p])
  - P[i,p] = Producer price in country i
  - τ[i,j,p] = Ad valorem tariff rate
  - t[i,j,p] = Iceberg transport cost rate
```

### 5. Factor Market Clearing

Labor and capital markets must clear within each country:

```
Labor Market: Σ[p] L[j,p] * X[j,p] = L_endowment[j]
Capital Market: Σ[p] K[j,p] * X[j,p] = K_endowment[j]

Where:
- X[j,p] = Total production of product p in country j
- L_endowment[j] = Labor supply in country j
- K_endowment[j] = Capital stock in country j
```

### 6. Income-Expenditure Balance

For each country, total income equals total expenditure:

```
Income[j] = w[j] * L_endowment[j] + r[j] * K_endowment[j] + Net_Transfers[j]

Expenditure[j] = Σ[p] P[j,p] * Q[j,p]

Budget Balance: Income[j] = Expenditure[j]
```

### 7. Trade Balance (Closure Rule)

The trade balance can be:
- **Fixed:** Trade deficit/surplus predetermined
- **Flexible:** Exchange rate adjusts to clear
- **Endogenous:** Determined by savings-investment balance

```
Trade Balance[j] = Σ[i,p] (P[j,p] * Exports[j,i,p] - P[i,j,p] * Imports[i,j,p])

Global Consistency: Σ[j] Trade Balance[j] = 0 (world trade balances)
```

---

## Data Structures

### Input Data

```python
class PricingEquilibriumInputs:
    # From Demand Engine
    demand_functions: dict[country][product] -> callable  # Q[j,p](P[j,p], Y[j])
    substitution_elasticities: dict[product] -> float  # σ[p]
    armington_shares: dict[origin][dest][product] -> float  # α[i,j,p]

    # From Production/Supply
    production_capacities: dict[country][product] -> float  # Max X[j,p]
    marginal_costs: dict[country][product] -> float  # MC[j,p]
    input_output_coefficients: dict[country][product][input] -> float  # a[i,j,p]

    # From Trade Flow Engine
    transport_costs: dict[origin][dest][product] -> float  # t[i,j,p]
    tariff_rates: dict[importer][exporter][product] -> float  # τ[i,j,p]
    trade_bans: set[(importer, exporter, product)]  # Prohibited flows

    # From Policy Engines
    subsidies: dict[country][product] -> float  # s[j,p] (per-unit subsidy)
    production_quotas: dict[country][product] -> float  # Max production constraints

    # Factor Endowments
    labor_supply: dict[country] -> float  # L_endowment[j]
    capital_stock: dict[country] -> float  # K_endowment[j]
    labor_productivity: dict[country][product] -> float  # L[j,p]
    capital_intensity: dict[country][product] -> float  # K[j,p]

    # Macroeconomic Closures
    fixed_trade_balances: dict[country] -> float  # If using fixed TB closure
    numeraire_product: (country, product)  # Price fixed to 1.0
```

### Internal State

```python
class PricingEquilibriumState:
    # Prices (endogenous variables)
    producer_prices: dict[country][product] -> float  # P[j,p]
    composite_prices: dict[country][product] -> float  # Armington index
    bilateral_prices: dict[origin][dest][product] -> float  # P[i,j,p]
    factor_prices_wage: dict[country] -> float  # w[j]
    factor_prices_capital: dict[country] -> float  # r[j]

    # Quantities (endogenous)
    production: dict[country][product] -> float  # X[j,p]
    consumption: dict[country][product] -> float  # Q[j,p]
    trade_flows: dict[origin][dest][product] -> float  # T[i,j,p]

    # Excess Demands (for convergence checking)
    excess_demand_goods: dict[country][product] -> float  # Z[j,p]
    excess_demand_labor: dict[country] -> float  # Labor market slack
    excess_demand_capital: dict[country] -> float  # Capital market slack

    # Income and Expenditure
    total_income: dict[country] -> float  # Income[j]
    total_expenditure: dict[country] -> float  # Expenditure[j]
    trade_balance: dict[country] -> float  # TB[j]

    # Convergence Metrics
    max_excess_demand: float
    iterations: int
    converged: bool
```

### Output Data

```python
class PricingEquilibriumOutputs:
    # Equilibrium Prices (to all Engines)
    equilibrium_prices: dict[country][product] -> float
    equilibrium_composite_prices: dict[country][product] -> float
    equilibrium_bilateral_prices: dict[origin][dest][product] -> float
    factor_prices: dict[country] -> dict[factor -> float]

    # Equilibrium Quantities
    equilibrium_production: dict[country][product] -> float
    equilibrium_consumption: dict[country][product] -> float
    equilibrium_trade_flows: dict[origin][dest][product] -> float

    # Welfare Metrics
    real_gdp: dict[country] -> float
    consumer_welfare: dict[country] -> float  # Hicksian equivalent variation
    producer_surplus: dict[country][product] -> float

    # Market Diagnostics
    convergence_status: str  # "CONVERGED" or "DIVERGED"
    max_market_imbalance: float
    iterations_to_convergence: int
    computational_warnings: list[str]
```

---

## Implementation Specification

### Algorithm Selection

Three approaches, in order of complexity:

#### **MVP Approach: Simple Tâtonnement (Walrasian Adjustment)**

Iterative price adjustment based on excess demand:

```python
P[j,p]^(t+1) = P[j,p]^(t) * (1 + λ * (Z[j,p]^(t) / Q[j,p]^(t)))

Where:
- λ = Adjustment speed parameter (0.1 - 0.3 typical)
- Z[j,p]^(t) = Excess demand at iteration t
- Prices increase when Z > 0 (excess demand), decrease when Z < 0 (excess supply)
```

**Pros:** Simple, intuitive, stable for well-behaved demand
**Cons:** Slow convergence, may not converge with strong complementarities

---

#### **Intermediate Approach: Newton-Raphson with Jacobian**

Solve the system F(P) = 0 where F[j,p] = Z[j,p] using Newton's method:

```python
P^(t+1) = P^(t) - J^(-1) * F(P^(t))

Where:
- J = Jacobian matrix of partial derivatives ∂Z[j,p]/∂P[k,q]
- F(P) = Vector of excess demands
```

**Pros:** Fast quadratic convergence near solution
**Cons:** Requires Jacobian calculation (expensive), can diverge if far from solution

---

#### **Advanced Approach: PATH Solver (Mixed Complementarity Problem)**

Formulate as MCP with complementarity slackness:

```
0 ≤ P[j,p] ⊥ Z[j,p] ≤ 0  (price non-negative, excess demand non-positive)
0 ≤ X[j,p] ⊥ (P[j,p] - MC[j,p]) ≤ 0  (production non-negative, zero profit)
```

**Pros:** Handles corner solutions (zero production), guaranteed convergence
**Cons:** Requires external solver (PATH, GAMS), complex setup

---

### Recommended: Hybrid Tâtonnement + Gauss-Seidel

For UTA simulation, use **Gauss-Seidel decomposition** with **damped tâtonnement**:

1. **Decompose** into subproblems: Solve for each country's production given others' prices
2. **Iterate** through countries updating production and prices
3. **Damp** price adjustments to ensure stability
4. **Check convergence** across all markets

---

## Main Algorithm Flow

```python
def solve_equilibrium(world_state, max_iterations=1000, tolerance=1e-6):
    """
    Solve for market-clearing prices using Gauss-Seidel + Tâtonnement

    Parameters:
    - world_state: Complete simulation state
    - max_iterations: Maximum solver iterations
    - tolerance: Convergence criterion (max relative excess demand)

    Returns:
    - equilibrium_state: Converged prices, quantities, and diagnostics
    """

    # Step 1: Initialize prices
    if world_state.has_previous_prices():
        prices = world_state.previous_prices  # Warm start
    else:
        prices = initialize_prices(world_state)  # Marginal costs

    # Step 2: Set numeraire
    prices[NUMERAIRE_COUNTRY][NUMERAIRE_PRODUCT] = 1.0

    # Iteration loop
    for iteration in range(max_iterations):

        # Step 3: Update composite prices (Armington indices)
        composite_prices = calculate_armington_price_indices(
            prices, world_state.transport_costs, world_state.tariffs,
            world_state.armington_shares, world_state.sigma
        )

        # Step 4: Update factor prices (solve factor market clearing)
        wage, rent = solve_factor_markets(
            prices, world_state.production, world_state.io_coefficients,
            world_state.labor_supply, world_state.capital_stock
        )

        # Step 5: Calculate demands (from Demand Engine)
        total_income = calculate_income(wage, rent, world_state.endowments)
        quantities_demanded = calculate_demand(
            composite_prices, total_income, world_state.demand_params
        )

        # Step 6: Calculate supplies (from Production Engine)
        quantities_supplied = calculate_supply(
            prices, wage, rent, world_state.production_capacities,
            world_state.io_coefficients, world_state.subsidies
        )

        # Step 7: Decompose demand into bilateral flows
        bilateral_demands = decompose_bilateral_demand(
            quantities_demanded, prices, composite_prices,
            world_state.armington_shares, world_state.sigma
        )

        # Step 8: Aggregate to market-level supply/demand
        market_demand, market_supply = aggregate_market_flows(
            bilateral_demands, quantities_supplied
        )

        # Step 9: Calculate excess demands
        excess_demands = {
            (j, p): market_demand[j][p] - market_supply[j][p]
            for j in countries for p in products
        }

        # Step 10: Check convergence
        max_excess = max(
            abs(Z) / max(market_demand[j][p], 1e-6)
            for (j, p), Z in excess_demands.items()
        )

        if max_excess < tolerance:
            return EquilibriumState(
                prices=prices,
                composite_prices=composite_prices,
                quantities_demanded=quantities_demanded,
                quantities_supplied=quantities_supplied,
                converged=True,
                iterations=iteration,
                max_excess_demand=max_excess
            )

        # Step 11: Adjust prices (Tâtonnement)
        prices = adjust_prices(
            prices, excess_demands, market_demand,
            adjustment_speed=0.2, damping_factor=0.95^iteration
        )

        # Step 12: Enforce numeraire
        prices[NUMERAIRE_COUNTRY][NUMERAIRE_PRODUCT] = 1.0

    # Failed to converge
    return EquilibriumState(
        prices=prices,
        converged=False,
        iterations=max_iterations,
        max_excess_demand=max_excess,
        warnings=["Failed to converge within max iterations"]
    )
```

---

## Detailed Function Specifications

### 1. Price Initialization

```python
def initialize_prices(world_state):
    """
    Initialize prices as marginal costs plus markup

    Cold start: Use cost-based pricing
    """
    prices = {}

    for country in countries:
        prices[country] = {}
        for product in products:
            # Marginal cost = input costs + factor costs
            input_cost = sum(
                world_state.io_coefficients[country][product][inp] * INITIAL_PRICE[inp]
                for inp in inputs
            )
            labor_cost = world_state.labor_productivity[country][product] * INITIAL_WAGE
            capital_cost = world_state.capital_intensity[country][product] * INITIAL_RENT

            marginal_cost = input_cost + labor_cost + capital_cost

            # Apply markup (10% typical)
            prices[country][product] = marginal_cost * 1.10

    return prices
```

### 2. Factor Market Clearing

```python
def solve_factor_markets(prices, production, io_coefficients, labor_supply, capital_stock):
    """
    Solve for factor prices (wages and rents) that clear factor markets

    Approach: Iterate until factor demands equal factor supplies
    """
    wages = {country: 1.0 for country in countries}  # Initialize
    rents = {country: 1.0 for country in countries}

    for country in countries:
        # Calculate factor demands
        labor_demand = sum(
            production[country][p] * labor_productivity[country][p]
            for p in products
        )
        capital_demand = sum(
            production[country][p] * capital_intensity[country][p]
            for p in products
        )

        # Adjust factor prices
        if labor_demand > 0:
            wages[country] = wages[country] * (labor_supply[country] / labor_demand)
        if capital_demand > 0:
            rents[country] = rents[country] * (capital_stock[country] / capital_demand)

    return wages, rents
```

### 3. Supply Calculation

```python
def calculate_supply(prices, wages, rents, capacities, io_coefficients, subsidies):
    """
    Calculate profit-maximizing supply given prices and costs

    Firm optimization: Produce up to capacity if P >= MC
    """
    supply = {}

    for country in countries:
        supply[country] = {}
        for product in products:
            # Calculate marginal cost
            input_cost = sum(
                io_coefficients[country][product][inp] * prices[country][inp]
                for inp in inputs
            )
            labor_cost = labor_productivity[country][product] * wages[country]
            capital_cost = capital_intensity[country][product] * rents[country]

            marginal_cost = input_cost + labor_cost + capital_cost - subsidies[country][product]

            # Supply decision
            price = prices[country][product]
            if price >= marginal_cost:
                supply[country][product] = capacities[country][product]  # Full production
            else:
                supply[country][product] = 0  # Shut down (corner solution)

    return supply
```

### 4. Price Adjustment (Tâtonnement)

```python
def adjust_prices(prices, excess_demands, quantities_demanded, adjustment_speed=0.2, damping=1.0):
    """
    Adjust prices based on excess demand (Walrasian tâtonnement)

    P_new[j,p] = P_old[j,p] * (1 + λ * damping * (Z[j,p] / Q[j,p]))
    """
    new_prices = {}

    for country in countries:
        new_prices[country] = {}
        for product in products:
            Z = excess_demands[(country, product)]
            Q = max(quantities_demanded[country][product], 1e-6)  # Avoid division by zero
            P_old = prices[country][product]

            # Proportional adjustment
            relative_excess = Z / Q
            adjustment = adjustment_speed * damping * relative_excess

            # Apply adjustment with bounds (prevent negative prices)
            P_new = P_old * (1 + adjustment)
            P_new = max(P_new, 0.01 * P_old)  # No more than 99% price drop per iteration

            new_prices[country][product] = P_new

    return new_prices
```

### 5. Convergence Checking

```python
def check_convergence(excess_demands, quantities_demanded, tolerance=1e-6):
    """
    Check if all markets have cleared within tolerance

    Criterion: max|Z[j,p] / Q[j,p]| < tolerance
    """
    max_relative_excess = 0

    for (country, product), Z in excess_demands.items():
        Q = max(quantities_demanded[country][product], 1e-6)
        relative_excess = abs(Z / Q)
        max_relative_excess = max(max_relative_excess, relative_excess)

    converged = (max_relative_excess < tolerance)
    return converged, max_relative_excess
```

---

## Integration Points

### Inputs From Other Engines

1. **From Demand Engine:**
   - Demand functions Q[j,p](P[j,p], Y[j])
   - Armington parameters (α, σ)
   - Expenditure shares (β)

2. **From Trade Flow Engine:**
   - Transport costs t[i,j,p]
   - Bilateral accessibility (which routes are viable)

3. **From Sanctions & Geopolitics Engine:**
   - Tariff rates τ[i,j,p]
   - Trade bans (set bilateral flows to zero)

4. **From Subsidy & Industrial Policy Engine:**
   - Production subsidies s[j,p]
   - Cost adjustments from industrial policy

5. **From Country/Firm Agents:**
   - Production capacities
   - Factor endowments

### Outputs To Other Engines

1. **To Demand Engine:**
   - Equilibrium prices (for demand calculation next period)
   - Consumer prices (composite Armington prices)

2. **To Trade Flow Engine:**
   - Bilateral prices P[i,j,p]
   - Realized trade flows

3. **To Country Agents:**
   - Real GDP and welfare metrics
   - Factor income (wages, capital returns)
   - Trade balance position

4. **To All Engines:**
   - Market-clearing prices (foundation for all decisions)

---

## Calibration Requirements

### Required Data Sources

1. **Input-Output Coefficients (a[i,j,p]):**
   - Source: WIOD, OECD ICIO
   - Method: Derive from MRIO tables (intermediate use / gross output)

2. **Factor Productivity:**
   - Labor: OECD Productivity Statistics, ILO
   - Capital: Penn World Tables (capital stocks)

3. **Initial Prices:**
   - If available: Actual producer prices from statistical agencies
   - Otherwise: Set all prices = 1.0 (numeraire) and calibrate shares

4. **Baseline Trade Flows:**
   - Source: UN Comtrade, WIOD
   - Use to validate that equilibrium replicates observed flows

### Calibration Procedure

**Step 1: Calibrate Input-Output Structure**
```python
# From MRIO table
intermediate_use[j][p][i] = MRIO_intermediate[j][p][i]  # Value
gross_output[j][p] = MRIO_output[j][p]  # Total production value

# Calculate coefficient
io_coefficient[j][p][i] = intermediate_use[j][p][i] / gross_output[j][p]
```

**Step 2: Calibrate Factor Shares**
```python
# Value added = Gross Output - Intermediate Inputs
value_added[j][p] = gross_output[j][p] - sum(intermediate_use[j][p])

# Labor share (from national accounts)
labor_share[j][p] = compensation_employees[j][p] / value_added[j][p]
capital_share[j][p] = 1 - labor_share[j][p]

# Implied factor productivities
labor_productivity[j][p] = labor_share[j][p] * gross_output[j][p] / employment[j][p]
capital_intensity[j][p] = capital_share[j][p] * gross_output[j][p] / capital_stock[j]
```

**Step 3: Solve for Baseline Equilibrium**
- Use observed quantities as initial guess
- Solve for prices that rationalize observed flows
- Adjust parameters if model cannot replicate baseline

### Key Parameters and Typical Ranges

```python
CALIBRATION_PARAMS = {
    # Solver parameters
    'max_iterations': 1000,
    'convergence_tolerance': 1e-6,  # 0.0001% relative excess demand
    'adjustment_speed': 0.2,        # Tâtonnement step size
    'damping_factor': 0.95,         # Exponential damping per iteration

    # Factor shares (typical values)
    'labor_share': {
        'agriculture': 0.6,
        'manufacturing': 0.5,
        'services': 0.7,
        'high_tech': 0.4  # Capital intensive
    },

    # Markup over marginal cost (for initialization)
    'initial_markup': 1.10,  # 10% markup

    # Bounds
    'min_price': 0.01,  # Prevent negative or zero prices
    'max_price_change': 0.50,  # Maximum 50% price change per iteration
}
```

---

## Validation Metrics

1. **Market Clearing:**
   - Check: |Z[j,p]| / Q[j,p] < 0.0001 for all markets
   - Metric: Maximum relative excess demand

2. **Walras' Law:**
   - Check: |Σ[j,p] P[j,p] * Z[j,p]| < 0.001 * Σ[j] GDP[j]
   - Implication: Budget constraints satisfied

3. **Zero Profit:**
   - Check: P[j,p] ≈ MC[j,p] for all j, p with positive production
   - Tolerance: ±1% deviation

4. **Factor Market Clearing:**
   - Check: Σ[p] L[j,p] * X[j,p] ≈ L_endowment[j]
   - Check: Σ[p] K[j,p] * X[j,p] ≈ K_endowment[j]
   - Tolerance: ±0.1%

5. **Trade Balance Consistency:**
   - Check: Σ[j] TradeBalance[j] ≈ 0 (global trade balances)
   - Tolerance: ±0.001% of world GDP

6. **Baseline Replication:**
   - Check: Model replicates observed trade flows
   - Metric: R² > 0.95 for predicted vs actual trade

---

## Strategic Gameplay

### Player-Facing Elements

1. **Price Signals:**
   - Display equilibrium prices for all products
   - Highlight price changes from previous period
   - Show price gaps between markets (arbitrage opportunities)

2. **Profitability Analysis:**
   - Show P[j,p] - MC[j,p] for each product
   - Identify high-margin opportunities
   - Warning when P < MC (unprofitable production)

3. **Market Tightness Indicators:**
   - Excess demand/supply by market
   - Capacity utilization rates
   - Price pressure indices (how fast prices are changing)

4. **Welfare Impacts:**
   - Real GDP changes
   - Consumer welfare (compensating variation)
   - Terms of trade effects

### Strategic Trade-Offs

1. **Price vs Quantity:**
   - Higher production → lower equilibrium price (supply effect)
   - Strategic withholding → higher price but lower volume

2. **Subsidy Pass-Through:**
   - Production subsidy → lower MC → lower equilibrium P
   - Benefits consumers (lower prices) but costs treasury

3. **Tariff Incidence:**
   - Import tariff → higher delivered price P[i,j,p]
   - But equilibrium domestic price P[j,p] may fall (substitution effect)

---

## Example Scenarios

### Example 1: Tariff Impact on Equilibrium Prices

**Setup:**
- Two countries: A (exporter), B (importer)
- One product: Steel
- Initial equilibrium: P[A,steel] = 100, P[B,steel] = 105
- Transport cost: 5%
- Initial tariff: 0%

**Baseline:**
```
P[A,B,steel] = P[A,steel] * (1 + 0.05) * (1 + 0.00) = 105
Market clears: Demand[B,steel](105, Y[B]) = Supply[A,steel](100)
```

**Scenario:** Country B imposes 25% tariff

**Step 1: Immediate Price Impact**
```
P[A,B,steel]_new = 100 * 1.05 * 1.25 = 131.25  (delivered price in B)
```

**Step 2: Demand Response**
```
Demand[B,steel] decreases (higher price)
Assume elasticity = -1.5:
ΔQ/Q = -1.5 * (ΔP/P) = -1.5 * (26.25/105) = -0.375  (37.5% decline in demand)
```

**Step 3: Supply Adjustment**
```
Lower demand for exports from A → excess supply in A
P[A,steel] falls to clear domestic market
New equilibrium: P[A,steel] = 85 (15% decline)
```

**Step 4: New Equilibrium**
```
P[A,B,steel] = 85 * 1.05 * 1.25 = 111.56
Demand[B,steel](111.56) = Supply[A,steel](85)  # Market clears
```

**Result:**
- Producer price in A falls from 100 to 85 (-15%)
- Consumer price in B rises from 105 to 111.56 (+6.25%)
- Tariff incidence: 60% borne by producer, 40% by consumer
- Tariff revenue: (111.56 - 85*1.05) * Q_traded

---

### Example 2: Subsidy Equilibrium Impact

**Setup:**
- Country C produces Steel
- Marginal cost: MC = 100
- Initial equilibrium price: P = 105 (5% markup)
- Market demand elasticity: -2.0

**Scenario:** Country C introduces 20% production subsidy

**Step 1: Effective Marginal Cost**
```
MC_effective = MC * (1 - 0.20) = 80
```

**Step 2: Supply Increase**
```
Lower cost → firms produce more
Supply elasticity = 1.5:
ΔS/S = 1.5 * (ΔMC/MC) = 1.5 * (-20/100) = -0.30  (30% supply increase)
```

**Step 3: Price Adjustment**
```
Excess supply → price falls
Market clears when: Supply(P_new) = Demand(P_new)

Solve:
S_0 * 1.30 = D_0 * (P_new/P_0)^(-2.0)
1.30 = (P_new/105)^(-2.0)
P_new = 105 / (1.30)^0.5 = 92.15
```

**Result:**
- Equilibrium price falls from 105 to 92.15 (-12.2%)
- Quantity increases by 30%
- Consumer surplus increases
- Producer revenue: 92.15 * 1.30 * S_0 = 119.8 * S_0 (but subsidy costs treasury)
- Pass-through rate: 12.2% / 20% = 61% (rest retained as producer surplus)

---

## Computational Considerations

1. **Jacobian Sparsity:**
   - Most ∂Z[j,p]/∂P[k,q] = 0 (no cross-product effects)
   - Exploit sparsity for faster linear algebra
   - Use sparse matrix libraries (scipy.sparse)

2. **Numerical Stability:**
   - Avoid prices near zero (set minimum price floor)
   - Use logarithmic prices for better numerical behavior: P_log = log(P)
   - Damp large price swings (max 50% change per iteration)

3. **Warm Starting:**
   - Use previous period's prices as initial guess
   - Dramatically reduces iterations (typically 3-10 vs 100-500 cold start)

4. **Convergence Failures:**
   - If oscillating: Reduce adjustment speed λ
   - If diverging: Check for infeasible constraints (e.g., contradictory quotas)
   - If stuck at corner: Use complementarity solver (PATH)

5. **Parallelization:**
   - Country-level subproblems can be solved in parallel (Gauss-Seidel iteration)
   - Trade-off: Synchronization overhead vs computation time

---

## Extensions and Future Enhancements

1. **Imperfect Competition:**
   - Introduce markups: P[j,p] = MC[j,p] * (1 + μ[j,p])
   - Firm-level differentiation (Dixit-Stiglitz)

2. **Dynamics:**
   - Intertemporal prices (interest rates, savings decisions)
   - Capital accumulation
   - Expectations and forward-looking behavior

3. **Increasing Returns to Scale:**
   - Non-convexities in production
   - Requires different solution methods (integer programming, heuristics)

4. **Uncertainty:**
   - Stochastic shocks to demand/supply
   - Risk premiums in prices
   - Hedging and insurance markets

5. **Financial Integration:**
   - Exchange rates
   - Capital flows and portfolio allocation
   - Sovereign debt and default risk

---

## References and Data Sources

**Theoretical Foundation:**
- Arrow, K. J., & Debreu, G. (1954). "Existence of an equilibrium for a competitive economy." Econometrica.
- Scarf, H. E. (1973). "The Computation of Economic Equilibria." Yale University Press.
- Shoven, J. B., & Whalley, J. (1992). "Applying General Equilibrium." Cambridge University Press.

**Computational Methods:**
- Rutherford, T. F. (1995). "Extension of GAMS for complementarity problems." Journal of Economic Dynamics and Control.
- Ferris, M. C., & Munson, T. S. (2000). "Complementarity problems in GAMS and the PATH solver." Journal of Economic Dynamics and Control.

**CGE Applications:**
- Hertel, T. W. (1997). "Global Trade Analysis: Modeling and Applications." GTAP Book.
- Balistreri, E. J., & Rutherford, T. F. (2013). "Computing general equilibrium theories of monopolistic competition and heterogeneous firms." Handbook of CGE Modeling.

**Data Sources:**
- GTAP Database: https://www.gtap.agecon.purdue.edu/
- OECD ICIO: https://www.oecd.org/sti/ind/inter-country-input-output-tables.htm
- WIOD: http://www.wiod.org/

---

**End of Pricing & Market Equilibrium Engine Specification**
