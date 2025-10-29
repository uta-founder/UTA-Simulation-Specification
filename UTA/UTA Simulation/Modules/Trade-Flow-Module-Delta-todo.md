# Trade Flow Module - Gap Analysis & Implementation TODO

**Generated**: 2025-10-28
**Analyzer**: uta-simulation-architect agent
**Assessment**: 67/100 → **Production-Ready After Tier 1 Fixes**

---

## Executive Summary

The Trade Flow Module specification is **conceptually excellent and pedagogically strong**, achieving its plain-English accessibility goals while grounding mechanics in established economic theory (gravity models, Armington aggregation, structural trade theory). The White Paper demonstrates academic rigor and awareness of state-of-the-art algorithms (PPML, Benders decomposition, network flow optimization).

### Overall Scores

| Evaluation Criterion | Status | Score | Notes |
|---------------------|--------|-------|-------|
| **Plain English Explanations** | ✅ Complete | 10/10 | All components explained accessibly |
| **Economic Foundations** | ✅ Strong | 8.5/10 | Gravity, Armington, transport costs well-covered; multilateral resistance missing |
| **Algorithm Flow** | ⚠️ Partial | 6/10 | High-level clear; iteration mechanics undefined |
| **Integration - Inputs** | ✅ Good | 8/10 | Well-documented; minor formula gaps |
| **Integration - Outputs** | ⚠️ Incomplete | 5.5/10 | Concepts defined; data structures ambiguous |
| **Integration - Feedback Loops** | 🔴 Missing | 3/10 | CGE iteration not specified |
| **Validation Metrics** | ⚠️ Partial | 5/10 | Thresholds given; procedures missing |
| **Missing Mechanics** | ⚠️ Moderate | 6/10 | Route dynamics, capacity, multi-hop need formalization |
| **Implementability** | ⚠️ 65% | 6.5/10 | Conceptually sound; procedural gaps block coding |

### Critical Finding

**The critical gap is not in what economics it models, but in how it integrates with the broader CGE system.** The specification treats the module as **quasi-standalone** when it's actually a **tightly-coupled component** of an iterative equilibrium solver. The missing **CGE integration loop specification** is the difference between a well-designed subsystem and an implementable module.

---

## Goals Achievement Status

### ✅ Goal 1: Plain English Key Components - FULLY MET

All required components have clear explanations:
- ✅ Bilateral Trade Tensor T[i,j,p] - Defined in Detailed Mechanics line 12
- ✅ Price Matrix P[i,j,p] - Defined line 13 with CIF + tariff decomposition
- ✅ Route Registry - Graph structure for tracking routes (line 14-15)
- ✅ Transit Trade Tracker - Tracks re-export flows (line 15)
- ✅ Transport Cost Calculator - Comprehensive (Main Module lines 38-61, Detailed lines 129-153)
- ✅ Tariff Engine - Fully explained with ad valorem, specific, compound types
- ✅ Trade Flow Optimizer - Gravity model + route selection described

### ✅ Goal 2: Economic Foundations - WELL-COVERED

#### Gravity Model Foundation ✅ COMPLETE
- **Location**: Main Module lines 294-304, Detailed Mechanics lines 104-115, White Paper lines 7-16
- ✅ Formula provided: T[i,j,p] = A × (Y[i]^α × Y[j]^β × P[i,p]^γ) / (D[i,j]^δ × (1 + τ[i,j,p])^ε)
- ✅ Plain English: "Bigger economies trade more, closer countries trade more"
- ✅ Parameter ranges: Distance elasticity δ ≈ -1.2, tariff elasticity ε ≈ -2.5
- ✅ Empirical grounding: CEPII Gravity Database, UN Comtrade
- ⚠️ **Gap**: Multilateral resistance terms (OMR, IMR) from Anderson & van Wincoop (2003) not incorporated

#### Armington Assumption ✅ COMPLETE
- **Location**: Main Module lines 305-320, Detailed Mechanics lines 118-127
- ✅ CES formula: Q[j,p] = (Σ[i] a[i,j,p] × T[i,j,p]^((σ-1)/σ))^(σ/(σ-1))
- ✅ Plain English: "German cars ≠ Japanese cars even if both are 'cars'"
- ✅ Elasticity ranges: Commodities σ ≈ 5.0, differentiated goods σ ≈ 2.0, strategic goods σ ≈ 1.2
- ✅ Consistent with Demand Module specification

#### Transport Cost Function ✅ COMPREHENSIVE
- **Location**: Main Module lines 38-61, Detailed Mechanics lines 129-153
- ✅ Modal choice logic: Pipeline vs sea vs air decision tree
- ✅ Cost components: Base distance + volume discounts + chokepoint premiums
- ✅ Numerical example: Saudi oil to China calculation ($330/ton total)
- ⚠️ **Gap**: Infrastructure quality to cost multiplier mapping undefined (mentioned line 112 but not formalized)

### ⚠️ Goal 3: Algorithm Flow - PARTIALLY SPECIFIED

**What's Well-Defined**:
- ✅ 6-step high-level process clearly documented
- ✅ Pseudocode skeleton provided (Detailed Mechanics lines 240-285)

**Critical Gaps**:

#### Gap 3A: Step 4 "Balance Supply and Demand" - HOW?
**Current**: "balanced_flows = balance_supply_demand(..., convergence_threshold=0.001)"
**Missing**:
- What algorithm? RAS? Iterative proportional fitting? Newton-Raphson?
- What variables adjust? Prices, quantities, or trade shares?
- Convergence criteria formula not specified (threshold given but test undefined)
- Maximum iterations not specified
- Failure handling if no equilibrium exists

#### Gap 3B: Step 3 "Optimize Routes" - Objective Function Unclear
**Current**: "Selects lowest-cost option that complies with restrictions"
**Missing**:
- Objective function: Minimize total transport cost? Per unit? Maximize profit?
- Constraints: Capacity on routes? Port throughput? Pipeline capacity?
- Multi-hop routing criteria: Cost advantage or only when sanctioned?
- Game-theoretic approach: Nash equilibrium or global optimizer?

#### Gap 3C: Iteration Sequence With Other Modules - UNDEFINED
**Critical Issue**: Module describes **internal** iteration but not **external** iteration with Pricing & Market Equilibrium Module.
**Missing**:
- Outer loop convergence criteria for full CGE system
- Price update responsibility (Trade Flow or Pricing Module?)
- Maximum outer iterations before declaring non-convergence
- Feedback mechanism: quantities → prices → updated transport costs → new quantities

### ⚠️ Goal 4: Integration Points - INCOMPLETE

#### Inputs From Other Modules ✅ WELL-DOCUMENTED
**Location**: Detailed Mechanics lines 187-213
- ✅ From Demand Module: Domestic consumption, import demand, substitution elasticities
- ✅ From Supply Module: Production volumes, minimum prices, capacity constraints
- ✅ From Pricing & Equilibrium Module: Market-clearing prices, excess demand signals
- ✅ From Sanctions Module: Trade restrictions, embargoes, tariff schedules
- ✅ From Energy & Logistics Module: Transport cost matrices, infrastructure capacity
- ⚠️ **Minor Gap**: Energy price to transport cost functional form not specified

#### Outputs To Other Modules ⚠️ PARTIALLY SPECIFIED
**Location**: Detailed Mechanics lines 215-235, Main Module lines 187-204
- ✅ To Pricing Module: Realized trade volumes, effective supply/demand by location
- ✅ To Compliance Module: Trade asymmetries, triangulation flags
- ✅ To Country Agents: Market shares, revenues, trade balance
- 🔴 **Critical Gap**: Output data structures not formalized
  - Bilateral flows T[i,j,p] vs aggregates Σ[i] T[i,j,p]?
  - Physical units (tons) or value terms (dollars)?
  - Includes intermediate use or only final demand?

### ⚠️ Goal 5: Validation Metrics - THRESHOLDS WITHOUT PROCEDURES

**What's Defined**:
- ✅ Bilateral Trade Accuracy: R² > 0.7 vs actual data
- ✅ Gravity Model Fit: Standard gravity coefficients
- ✅ Trade Balance Consistency: Σ exports = Σ imports globally
- ✅ Price Pass-through: Tariff changes affect prices correctly
- ✅ Triangulation Detection Rate: Catch known circumvention cases

**Critical Gaps**:

#### Gap 5A: R² Calculation - HOW?
**Missing**:
- What is predicted vs observed? Bilateral flows for base year?
- Aggregation level? Product-level R² or aggregate?
- Sample: All country-pairs or only active trade relationships?
- Acceptance by product vs aggregate?

#### Gap 5B: Price Pass-Through - UNDEFINED TEST
**Missing**:
- What is "correctly"? Full, partial, or zero pass-through expected?
- Test scenario specification
- Expected range based on elasticities
- Tolerance for acceptance

#### Gap 5C: Triangulation Detection Rate - NO BENCHMARK DATASET
**Missing**:
- What cases? Russian oil? North Korea coal? Chinese transshipment?
- Ground truth labels for validation
- Metrics: Precision, recall, F1-score, false positive rate?

---

## Critical Missing Mechanics

### 🔴 Missing Mechanic 1: Route Switching Dynamics
**Strategic Importance**: HIGH

**What's Missing**: When sanctions close a route (e.g., Russia-EU oil), how do flows reallocate?
- Timeline: Instant or gradual over multiple turns?
- Capacity constraints: Can India absorb all displaced Russian oil immediately?
- Price dynamics: Temporary spikes during transition or immediate reallocation?

**Current State**: Main Module line 242-247 describes Russia energy sanctions scenario but doesn't specify **transition mechanics**.

**Why This Matters**: Determines whether sanctions cause **temporary shocks** (high prices for 6 months while routes adjust) vs **permanent shifts** (immediate reallocation at slightly higher costs).

**Recommendation**: Add 3-phase dynamic adjustment model:
1. **Immediate (Turn T)**: Direct trade drops to zero, prices spike
2. **Short-term (T+1 to T+4)**: Reallocation within existing capacity constraints
3. **Long-term (T+5+)**: Infrastructure investment expands alternative routes

### 🔴 Missing Mechanic 2: Multi-Hop Route Optimization
**Strategic Importance**: HIGH (Core of Triangulation)

**What's Missing**: Formal rule for when A→C→B beats A→B direct route.

**Current State**:
- Line 82-87: "Multi-hop routes through transit countries"
- Line 96: "Route through neutral countries" (sanctions evasion)
- No formal selection criteria

**Options**:
1. Only when direct route blocked (sanctions)?
2. Cost minimization: Cost[A,C] + Cost[C,B] < Cost[A,B]?
3. Circumvention arbitrage: Tariff[A,C] + Tariff[C,B] < Tariff[A,B]?
4. Detection risk included in cost calculation?

**Recommendation**: Add decision rule with cost-benefit analysis including UTA detection penalty.

### 🔴 Missing Mechanic 3: Capacity Constraints Enforcement
**Realism Impact**: CRITICAL

**What's Missing**: Multiple mentions of capacity (port, pipeline, shipping) but **no enforcement mechanism**.

**Current State**:
- Line 92: "Capacity constraints: Port congestion, pipeline capacity"
- Energy & Logistics Module: Infrastructure capacity mentioned but not formalized
- White Paper line 169: `add_arc_with_capacity_and_unit_cost(i, j, capacities[i,j], cost)`

**Problem**: If Russia-EU pipeline capacity is 100M barrels/year but simulation routes 120M barrels, what happens?
- Option A: Flow capped at 100M (infeasible equilibrium)?
- Option B: Price adjusts until demand drops to 100M?
- Option C: Overflow routes through alternative modes (sea freight)?

**Recommendation**: Specify constraint handling for:
1. Pipeline capacity (hard constraint)
2. Port capacity (soft constraint with congestion costs)
3. Shipping fleet capacity (affects freight rates)

### ⚠️ Missing Mechanic 4: Policy Feedback to Country Agents
**Integration Impact**: MAJOR

**What's Missing**: Country agents receive trade performance data (line 269-289), but **how do they respond?**

**Example**: If Country A's export market share drops in Country B due to tariffs:
- Response option 1: Negotiate trade deal
- Response option 2: Subsidize exporters
- Response option 3: Retaliate with own tariffs
- Response option 4: Seek alternative markets

**Which one? What determines choice?**

**Recommendation**: Specify strategic decision metrics provided to agents:
1. Market competitiveness index
2. Market access score
3. Dependency vulnerability indices

---

## Cross-Module Consistency Issues

### ⚠️ Conflict 1: Price Authority (UNRESOLVED)
**Issue**: Both Pricing & Market Equilibrium Module and Trade Flow Module seem to adjust prices.

**Resolution Needed**: Clarify division of labor:
- **Recommended**: Pricing Module sets producer prices P[i,p]; Trade Flow Module computes delivered prices P[i,j,p] = P[i,p] × (1 + τ) × (1 + t)
- Trade Flow Module reports excess demand to Pricing Module but does NOT adjust producer prices

### ✅ Conflict 2: Transport Cost Treatment (RESOLVED)
**Observation**: Energy & Logistics Module specifies USD per ton-km, while Trade Flow White Paper mentions iceberg costs.

**Resolution**: Detailed Mechanics uses USD per ton-km consistently. No actual conflict - iceberg costs are alternative formulation, not chosen implementation.

### ⚠️ Conflict 3: Bilateral Trade Data Structure (MINOR)
**Issue**: Demand Module outputs "import demand by preferred sources" but Trade Flow receives "aggregate demand dict[country][product]".

**Resolution**: Armington assumption means demand is aggregate with source choice determined by relative prices. Clarify that "preferred sources" means share parameters α[i,j,p], not predetermined bilateral demands.

---

## Prioritized Implementation TODO

### TIER 1: MUST-HAVE FOR IMPLEMENTATION 🔴
**Blocks Development - Complete Before Coding**

**Estimated Total**: 7 hours specification work
**Outcome**: Moves from 65% to 85% implementation-ready

#### T1.1: Specify Supply-Demand Balancing Algorithm [Gap 3A]
**Priority**: CRITICAL
**Effort**: 2-3 hours
**Assignee**: uta-simulation-architect or cge-game-logic-implementer
**Location**: New section in Detailed Mechanics after line 186

**Deliverable**: Add "Supply-Demand Balancing Algorithm" section with:
```
Algorithm: RAS (Biproportional Adjustment)
Input: Initial flows T[i,j,p], target supplies S[i,p], target demands D[j,p]
Output: Adjusted flows T'[i,j,p] satisfying material balance

Pseudocode:
1. Initialize: T'[i,j,p] = T[i,j,p] (gravity-predicted)
2. For iter = 1 to MAX_ITER:
   a. Row adjustment: r[i,p] = S[i,p] / Σ[j] T'[i,j,p]
   b. Update: T'[i,j,p] = r[i,p] × T'[i,j,p]
   c. Column adjustment: c[j,p] = D[j,p] / Σ[i] T'[i,j,p]
   d. Update: T'[i,j,p] = c[j,p] × T'[i,j,p]
   e. Convergence check: If |Σ[i] T'[i,j,p] - D[j,p]| < tolerance: BREAK
3. If not converged: raise InfeasibleProblem
4. Return T'[i,j,p]

Parameters:
- MAX_ITER = 1000
- tolerance = 0.001 × Σ[i,j,p] T[i,j,p] (0.1% of world trade)

Economic Interpretation: RAS preserves relative trade shares while
adjusting absolute magnitudes to satisfy material balance.
```

#### T1.2: Define CGE Integration Loop [Gap 3C]
**Priority**: CRITICAL
**Effort**: 3-4 hours
**Assignee**: uta-simulation-architect (coordinate with Pricing Module spec)
**Location**: New section in Detailed Mechanics after line 235

**Deliverable**: Add "Integration With CGE Equilibrium Loop" showing:
```
Outer Loop (CGE Equilibrium):
1. Pricing Module: Proposes prices P[j,p]
2. Demand Module: Computes Q_d[j,p] at prices P[j,p]
3. Supply Module: Computes Q_s[i,p] at prices P[i,p]
4. Trade Flow Module (this module):
   a. Calculate bilateral flows T[i,j,p] using gravity
   b. Apply transport costs and tariffs
   c. Balance flows (RAS algorithm)
   d. Return effective supplies/demands to Pricing Module
5. Pricing Module: Check Z[j,p] = D[j,p] - S[j,p] ≈ 0
   - If YES: equilibrium found, STOP
   - If NO: Update prices P_new = P_old × (1 + α × Z/S)
6. Repeat until convergence

Convergence Criteria (global):
- |Z[j,p]| / Q[j,p] < 0.0001 for all j,p
- |ΔP[j,p]| / P[j,p] < 0.001 for all j,p
- OR maximum 500 outer iterations

Trade Flow Internal Convergence:
- Faster threshold: 0.1% of world trade
- Maximum 100 inner iterations
```

#### T1.3: Formalize Output Data Structures [Gap 4B]
**Priority**: CRITICAL
**Effort**: 1-2 hours
**Assignee**: uta-simulation-architect
**Location**: Detailed Mechanics lines 81-99 (expand with explicit schemas)

**Deliverable**: Add explicit Python-like schemas:
```python
class TradeFlowOutputs:
    # For Pricing & Equilibrium Module
    bilateral_flows: np.ndarray[n_countries, n_countries, n_products]
        # Physical units (tons, barrels, units)
    bilateral_values: np.ndarray[n_countries, n_countries, n_products]
        # Monetary values (USD)
    effective_supply_by_dest: dict[country][product] -> float
        # Production[i,p] + Σ[i≠j] Imports[i,j,p]
    effective_demand_by_source: dict[country][product] -> float
        # Consumption[i,p] + Σ[j≠i] Exports[i,j,p]

    # Price-relevant outputs
    delivered_prices: np.ndarray[n_countries, n_countries, n_products]
        # P[i,j,p] = P[i,p] × (1+τ) × (1+t)
    armington_price_indices: dict[country][product] -> float
        # P[j,p] from CES aggregation

    # For Compliance Module
    triangulation_flags: list[dict]
        # Structure: [{'transit': ISO3, 'source': ISO3,
        #              'dest': ISO3, 'product': str,
        #              'volume': float, 'confidence': float}]
    trade_asymmetries: pd.DataFrame
        # Columns: [reporter, partner, product,
        #           reported_export, partner_import, discrepancy_pct]

    # For Country Agents
    market_shares: dict[exporter][importer][product] -> float
        # Share of importer's market (0-1)
    export_revenues: dict[exporter][importer][product] -> float
        # USD value
    trade_balance_by_partner: dict[country][partner] -> float
        # Exports - Imports in USD
```

#### T1.4: Clarify Price Authority [Conflict 2B]
**Priority**: CRITICAL
**Effort**: 30 min clarify + 1 hour propagate to related specs
**Assignee**: uta-simulation-architect
**Location**: Integration section in both Trade Flow and Pricing modules

**Deliverable**: Add explicit statement:
```
Price Authority Division:
- Pricing & Market Equilibrium Module: Sets producer prices P[i,p]
- Trade Flow Module: Computes delivered prices P[i,j,p] = P[i,p] × (1+τ) × (1+t)
- Trade Flow Module: Calculates Armington price indices P[j,p] via CES
- Trade Flow Module does NOT adjust producer prices
- Trade Flow Module reports excess demand Z[j,p] to Pricing Module
- Pricing Module performs price updates in outer loop
```

---

### TIER 2: IMPORTANT FOR REALISM ⚠️
**Affects Simulation Quality - Add During MVP Development**

**Estimated Total**: 10 hours
**Outcome**: Brings realism to 92%

#### T2.1: Add Route Switching Dynamics [Missing Mechanic 1]
**Priority**: HIGH
**Effort**: 4-5 hours
**Assignee**: uta-simulation-architect
**Location**: After line 260 in Main Module (after "Real-World Scenarios")

**Deliverable**: 3-phase dynamic adjustment model:
```
When trade route becomes unavailable (sanctions, chokepoint closure):

Phase 1: Immediate (Turn T):
- Direct trade on blocked route → 0
- Excess supply at origin A: ES[A,p]
- Excess demand at destination B: ED[B,p]
- Prices spike: P[B,p] increases ∝ ED[B,p] / Q[B,p]

Phase 2: Short-term reallocation (Turns T+1 to T+4):
- A seeks alternative buyers (gravity-weighted)
- B seeks alternative suppliers (Armington substitution)
- Constraint: Capacity limits on alternative routes
- Rerouting_capacity = min(Port_cap, Pipeline_cap, Shipping_avail)

Phase 3: Long-term adjustment (Turns T+5+):
- Infrastructure investments expand capacity
- Substitution elasticities increase (supply chain redesign)
- Prices converge to new equilibrium (higher transport costs)

Parameters:
- Immediate_capacity_utilization = 0.70
- Capacity_expansion_rate = 0.05 per turn
- Short_term_elasticity = -0.3 (inelastic)
- Long_term_elasticity = -1.2 (elastic)
```

#### T2.2: Specify Multi-Hop Route Selection Rule [Missing Mechanic 2]
**Priority**: HIGH
**Effort**: 2-3 hours (including detection risk calculation)
**Assignee**: uta-simulation-architect
**Location**: Detailed Mechanics line 31-35 (expand "Trade Flow Optimizer")

**Deliverable**: Decision rule for triangulation:
```python
def select_route(origin, destination, product):
    # Direct route
    if not is_sanctioned(origin, destination, product):
        direct_cost = transport_cost(origin, destination) +
                      tariff(origin, destination, product)
    else:
        direct_cost = np.inf

    # Single-transit routes
    best_transit_cost = np.inf
    best_transit = None
    for transit in potential_intermediaries:
        if is_sanctioned(origin, transit, product) or
           is_sanctioned(transit, destination, product):
            continue

        leg1_cost = transport_cost(origin, transit) +
                    tariff(origin, transit, product)
        leg2_cost = transport_cost(transit, destination) +
                    tariff(transit, destination, product)
        handling_cost = TRANSSHIPMENT_COST[transit]
        detection_risk_cost = UTA_PENALTY ×
            detection_probability(origin, transit, destination, product)

        total = leg1_cost + leg2_cost + handling_cost + detection_risk_cost

        if total < best_transit_cost:
            best_transit_cost = total
            best_transit = transit

    # Select minimum cost route
    if direct_cost <= best_transit_cost:
        return ['direct', origin, destination], direct_cost
    else:
        return ['transit', origin, best_transit, destination],
               best_transit_cost

Parameters:
TRANSSHIPMENT_COST[country] = $50-200/ton
UTA_PENALTY = -500 to -2000 credits
detection_probability = f(volume spike, country reputation)
```

#### T2.3: Define Capacity Constraint Enforcement [Missing Mechanic 3]
**Priority**: HIGH
**Effort**: 3-4 hours
**Assignee**: uta-simulation-architect
**Location**: New subsection in Detailed Mechanics

**Deliverable**: Constraint handling for all capacity types:
```
Capacity Constraints:

1. Pipeline Capacity (hard constraint):
   T[i,j,p] ≤ Capacity[i,j,p] for pipeline_goods

   If Σ[p] T[i,j,p] > Capacity[i,j]:
     - Priority allocation: Strategic goods first
     - Excess demand ED = Σ T_desired - Capacity
     - Reroute excess to sea/rail (higher cost)
     - If no alternative: Price rises until demand drops

2. Port Capacity (soft constraint):
   Throughput[port] = Σ[i,j,p: uses port] T[i,j,p]

   If Throughput > Capacity:
     - Congestion_cost = DELAY_COST × (Throughput/Capacity - 1)²
     - Added to transport cost
     - Equilibrium: Flows shift to less-congested ports

3. Shipping Fleet Capacity (global):
   Required_ship_days = Σ T[i,j,p] × distance / ship_speed

   If Required > Fleet_capacity:
     - Freight rates increase (supply/demand)
     - Low-value goods stop trading
     - Marginal trades become unprofitable

Parameters:
DELAY_COST = $10-30/ton per day
Port_capacity = 10-50M TEU/year (major ports)
Fleet_capacity = 2 billion DWT globally (2023)
```

#### T2.4: Link Energy Prices to Transport Costs [Gap 4A]
**Priority**: MEDIUM
**Effort**: 1-2 hours
**Assignee**: uta-simulation-architect
**Location**: Detailed Mechanics line 17-22 (Transport Cost Calculator)

**Deliverable**: Energy price pass-through formula:
```
Transport_Cost[mode] = Base_Cost[mode] ×
    (1 + β[mode] × (Energy_Price / Energy_Price_base - 1))

Where:
- β['sea'] = 0.50 (50% of shipping cost is fuel)
- β['air'] = 0.35 (35% of air freight is fuel)
- β['road'] = 0.30 (30% of trucking is fuel)
- β['rail'] = 0.20 (20% of rail is energy)
- β['pipeline'] = 0.10 (10% of pipeline ops is energy)

Energy_Price refers to:
- Oil price for sea, air, road
- Electricity price for rail
- Natural gas price for pipeline compression

Source: Energy & Logistics Module outputs energy_price_index[mode]
```

---

### TIER 3: DESIRABLE FOR VALIDATION ✅
**Improves Confidence - Add Post-MVP**

**Estimated Total**: 12 hours
**Outcome**: Production-quality validation framework

#### T3.1: Operationalize R² Calculation [Gap 5A]
**Priority**: MEDIUM
**Effort**: 2 hours
**Assignee**: uta-simulation-architect
**Location**: New section "Validation Procedures" at end of Detailed Mechanics

**Deliverable**: Step-by-step R² validation:
```
Bilateral Trade Accuracy Validation:

Step 1: Load historical data
- UN Comtrade bilateral flows for validation year (2019)
- Match to simulation country/product aggregation

Step 2: Run simulation to replicate historical scenario
- Set policies, tariffs, GDP to historical values
- Run equilibrium solver
- Extract bilateral flows T_sim[i,j,p]

Step 3: Calculate R² by product
For each product p:
  R²[p] = 1 - Σ[i,j] (T_sim - T_actual)² /
              Σ[i,j] (T_actual - mean(T_actual))²

Step 4: Calculate aggregate R²
R²_agg = 1 - Σ[i,j,p] (T_sim - T_actual)² /
             Σ[i,j,p] (T_actual - mean)²

Acceptance Criteria:
- R²_aggregate > 0.70
- ≥80% of products have R²[p] > 0.60
- No products with R²[p] < 0.40
```

#### T3.2: Define Price Pass-Through Test [Gap 5B]
**Priority**: MEDIUM
**Effort**: 1-2 hours (including theoretical derivation)
**Assignee**: uta-simulation-architect
**Location**: Same "Validation Procedures" section

**Deliverable**: Expected pass-through test:
```
Price Pass-Through Validation:

Scenario: Impose 10% tariff on imports from Country A
          to Country B for product P

Theoretical Prediction (Armington CES):
Pass-through = σ / (σ + market_share_A × (σ - 1))

Where:
- σ = substitution elasticity
- market_share_A = T[A,B,p] / Σ[i] T[i,B,p]

Example:
If σ = 3 (differentiated goods), market_share = 0.30:
  Pass-through = 3 / (3 + 0.30×2) = 3/3.6 = 83%
  Expected ΔP[A,B,p] = 0.83 × 10% = 8.3%

Acceptance Criteria:
- Simulated ΔP within 20% of theoretical prediction
- If theory predicts 8.3%, accept [6.6%, 10.0%]
```

#### T3.3: Create Triangulation Test Dataset [Gap 5C]
**Priority**: MEDIUM
**Effort**: 4-6 hours (compile cases from literature)
**Assignee**: deep-research-orchestrator + uta-simulation-architect
**Location**: Separate file "Triangulation_Validation_Dataset.md"

**Deliverable**: Labeled historical evasion cases:
```
Triangulation Detection Validation Dataset:

1. Russian Oil Circumvention (2022-2024):
   True Positives:
   - Russia → India → EU refined products
     Volume: ~3.7M tonnes/year
     Source: Silverado Policy Accelerator
   - Russia → Turkey → Mediterranean buyers
     Volume: ~2M tonnes/year
     Source: Ship-tracking data

2. Chinese Transshipment Through Vietnam (2018-2024):
   True Positives:
   - China → Vietnam → USA (furniture, electronics, textiles)
     Volume: $40B+ annually
     Source: Harvard study

3. False Positives to Avoid:
   - Singapore legitimate re-exports (value-added processing)
   - Netherlands Rotterdam hub (genuine intermediation)

Metrics:
- Precision = TP / (TP + FP) > 0.70
- Recall = TP / (TP + FN) > 0.80
- F1 Score > 0.75

Test Procedure:
1. Run detection algorithm on 2022-2023 period
2. Flag potential triangulation
3. Compare against documented cases
4. Calculate precision/recall
```

#### T3.4: Add Walras' Law Check [Validation 3A]
**Priority**: LOW
**Effort**: 30 minutes
**Assignee**: uta-simulation-architect
**Location**: End of equilibrium solver section

**Deliverable**: Post-convergence verification:
```
Walras' Law Verification:

After equilibrium convergence, compute:
  Value_imbalance = Σ[j,p] P[j,p] × (Demand[j,p] - Supply[j,p])

Acceptance Criterion:
  |Value_imbalance| < 0.001 × World_GDP

Rationale: In general equilibrium with budget constraints,
the value of excess demands must sum to zero.
```

---

### TIER 4: POLISH & EXTENSIONS 💡
**Can Defer to Later Phases**

**Estimated Total**: 8 hours
**Outcome**: Academic-quality refinements

#### T4.1: Add Arbitrage Constraint [Validation 3B]
**Priority**: LOW
**Effort**: 1-2 hours
**Assignee**: uta-simulation-architect
**Location**: Route optimization section

**Deliverable**: Profit margin requirement:
```
Re-Export Arbitrage Constraint:

If Country C re-exports product P from A to B:
  P[B,p] × (1 - margin_C) ≥
    P[A,p] × (1 + t[A,C]) × (1 + τ[A,C]) +
    P[C,p] × (1 + t[C,B]) × (1 + τ[C,B])

Where margin_C = minimum profit margin (e.g., 5%)

If inequality violated: C cannot profitably intermediate
```

#### T4.2: Calibrate Transport Cost Elasticity [Validation 3C]
**Priority**: LOW
**Effort**: 30 min literature review + 15 min update
**Assignee**: uta-simulation-architect
**Location**: Detailed Mechanics line 131

**Deliverable**: Citation-backed distance scaling:
```python
# Current: Linear scaling
base_cost = unit_cost * distance

# Recommended: Sublinear (economies of scale)
base_cost = unit_cost * (distance ** 0.8)

# Source: Hummels (2007), "Transportation Costs and
# International Trade in the Second Era of Globalization"
# Estimated elasticity ~0.8 for ocean freight
```

#### T4.3: Specify Decision Metrics for Country Agents [Missing Mechanic 4]
**Priority**: LOW
**Effort**: 2-3 hours
**Assignee**: uta-simulation-architect
**Location**: Output section

**Deliverable**: Strategic metrics formulas:
```
Strategic Decision Metrics for Country Agents:

1. Market Competitiveness Index:
   Competitiveness[i,j,p] =
     (P[i,j,p] - min_k P[k,j,p]) / P[i,j,p]

   Interpretation:
   - 0.0 = lowest-cost supplier (most competitive)
   - 0.2 = 20% more expensive than cheapest
   - 0.5 = 50% more expensive (losing share)

2. Market Access Score:
   Access[i,j] = Σ[p] (T[i,j,p] / T_potential[i,j,p])

   Where T_potential = gravity-predicted absent barriers
   - 1.0 = no barriers (free trade)
   - 0.5 = trade at 50% of potential
   - 0.0 = complete blockage

3. Dependency Vulnerability:
   Import_dependency[j,p,i] = T[i,j,p] / Consumption[j,p]
   Export_dependency[i,p,j] = T[i,j,p] / Production[i,p]

   Higher values = strategic vulnerability

These metrics inform Agent Intelligence Module decisions.
```

#### T4.4: Add Multilateral Resistance to Gravity [Economic Foundation Gap]
**Priority**: LOW (advanced feature)
**Effort**: 2-3 hours (ensure consistency with structural gravity)
**Assignee**: uta-simulation-architect
**Location**: Economic Logic section (Detailed Mechanics line 104-115)

**Deliverable**: Anderson-van Wincoop formulation:
```
Enhanced Gravity Model with Multilateral Resistance:

T[i,j,p] = (Y[i,p] × Y[j,p]) / Y[world,p] ×
           (t[i,j,p] / (OMR[i,p] × IMR[j,p]))^(1-σ)

Where:
- OMR[i,p] = Outward Multilateral Resistance (seller's)
  = (Σ[j] (t[i,j,p] / IMR[j,p])^(1-σ) × (Y[j,p]/Y[world,p]))^(1/(1-σ))

- IMR[j,p] = Inward Multilateral Resistance (buyer's)
  = (Σ[i] (t[i,j,p] / OMR[i,p])^(1-σ) × (Y[i,p]/Y[world,p]))^(1/(1-σ))

- t[i,j,p] = bilateral trade cost (distance, tariffs)
- σ = substitution elasticity

Interpretation: Trade depends not just on bilateral barriers,
but on average trade costs to/from all partners.

Computation: Iterative fixed-point algorithm
- Initialize OMR = IMR = 1
- Iterate until convergence (typically 10-20 iterations)

Source: Anderson & van Wincoop (2003), "Gravity with
Gravitas: A Solution to the Border Puzzle"
```

---

## Implementation Pathway

### Phase 1: Pre-Development (TIER 1) - 7 Hours
**Objective**: Make module 85% implementation-ready

**Week 1 Sprint**:
- [ ] Day 1: T1.1 - RAS balancing algorithm (3 hours)
- [ ] Day 2: T1.2 - CGE integration loop (4 hours)
- [ ] Day 3: T1.3 - Output data structures (1.5 hours)
- [ ] Day 3: T1.4 - Price authority clarification (0.5 hours)

**Deliverable**: Updated Trade Flow Module specification with all TIER 1 additions

**Review Gate**: uta-simulation-architect validation that specification is implementation-ready

---

### Phase 2: During MVP Development (TIER 2) - 10 Hours
**Objective**: Bring realism to 92%

**Week 2-3 Sprint**:
- [ ] T2.1 - Route switching dynamics (5 hours)
- [ ] T2.2 - Multi-hop route selection (3 hours)
- [ ] T2.3 - Capacity constraints (4 hours)
- [ ] T2.4 - Energy-transport linkage (2 hours)

**Integration Points**:
- Coordinate T2.1 with Sanctions Module (route closure events)
- Coordinate T2.3 with Energy & Logistics Module (capacity data)
- Coordinate T2.4 with Energy & Logistics Module (energy prices)

**Deliverable**: Realistic dynamic trade adjustment mechanics

---

### Phase 3: Post-MVP Validation (TIER 3) - 12 Hours
**Objective**: Production-quality validation framework

**Week 4-5 Sprint**:
- [ ] T3.1 - R² validation procedure (2 hours)
- [ ] T3.2 - Price pass-through test (2 hours)
- [ ] T3.3 - Triangulation test dataset (6 hours)
  - Research documented evasion cases
  - Create labeled test data
  - Define precision/recall metrics
- [ ] T3.4 - Walras' Law check (0.5 hours)

**Deliverable**: Comprehensive validation test suite

---

### Phase 4: Polish (TIER 4) - 8 Hours
**Optional - Academic Quality Refinements**

**Future Enhancements**:
- [ ] T4.1 - Arbitrage constraints (1.5 hours)
- [ ] T4.2 - Transport cost elasticity calibration (1 hour)
- [ ] T4.3 - Country agent decision metrics (3 hours)
- [ ] T4.4 - Multilateral resistance terms (2.5 hours)

---

## Success Metrics

### After TIER 1 Completion:
- ✅ Specification score: 85/100
- ✅ Developer can write code without making algorithmic assumptions
- ✅ Integration with Pricing Module is procedurally defined
- ✅ Output data contracts are formalized

### After TIER 2 Completion:
- ✅ Specification score: 92/100
- ✅ Dynamic adjustment to policy shocks is realistic
- ✅ Capacity constraints prevent unrealistic flows
- ✅ Multi-hop routing includes detection risk

### After TIER 3 Completion:
- ✅ Specification score: 95/100
- ✅ Validation procedures are executable
- ✅ Historical replication tests are defined
- ✅ Triangulation detection can be benchmarked

### After TIER 4 Completion:
- ✅ Specification score: 98/100
- ✅ Publication-quality economic rigor
- ✅ Structural gravity model consistency
- ✅ Agent decision-making is well-grounded

---

## Risk Assessment

### High Risk (Address Immediately):
🔴 **CGE Integration Loop**: Without this, module cannot participate in equilibrium iteration. **CRITICAL PATH**.

🔴 **Output Data Structures**: Ambiguity will cause integration failures between modules. **BLOCKS DEVELOPMENT**.

### Medium Risk (Address in TIER 2):
⚠️ **Capacity Constraints**: Without enforcement, unrealistic flows undermine credibility.

⚠️ **Route Switching Dynamics**: Without temporal adjustment, sanctions scenarios lack realism.

### Low Risk (Acceptable to Defer):
💡 **Validation Procedures**: Can be developed in parallel with implementation.

💡 **Multilateral Resistance**: Advanced feature, not required for MVP.

---

## Coordination Requirements

### With Other Modules:
1. **Pricing & Market Equilibrium Module** (T1.2, T1.4)
   - Must agree on price update authority
   - Must define outer loop convergence criteria
   - Coordinate variable naming conventions

2. **Energy & Logistics Module** (T2.3, T2.4)
   - Receive capacity constraint data
   - Receive energy price indices
   - Define infrastructure quality mapping

3. **Compliance & Cheating Detection Module** (T2.2, T3.3)
   - Provide detection probability function
   - Receive triangulation flags
   - Share validation test dataset

4. **Agent Intelligence Module** (T4.3)
   - Define strategic decision metrics
   - Specify how agents use trade performance data

### With External Resources:
- **Data Sources** (T3.1, T3.3): UN Comtrade, CEPII Gravity Database, ship-tracking datasets
- **Literature** (T4.2, T4.4): Hummels (2007), Anderson & van Wincoop (2003), PPML estimation papers

---

## Appendix: Quick Reference

### Current Specification Files:
- Main Module: `UTA/UTA Simulation/Trade Flow Module.md` (425 lines)
- Detailed Mechanics: `UTA/UTA Simulation/Trade Flow Module details draft.md` (375 lines)
- White Paper: `UTA/UTA Simulation/WhitePapers/Trade Flow Module White Paper.md` (220 lines)

### Related Module Specs:
- Demand Module: `UTA/UTA Simulation/Demand Module.md` (780 lines) ✅
- Pricing & Market Equilibrium Module: `UTA/UTA Simulation/Pricing & Market Equilibrium Module.md` (908 lines) ✅
- Energy & Logistics Module: `UTA/UTA Simulation/Energy & Logistics Module.md` ✅
- Compliance & Cheating Detection Module: `UTA/UTA Simulation/Compliance & Cheating Detection Module.md` ✅

### Key Contacts (Agents):
- **uta-simulation-architect**: Module design, gap analysis, economic consistency
- **cge-game-logic-implementer**: Algorithm specification, equilibrium mechanics
- **uta-maya-patel**: Business translation, MBA-friendly explanations

---

## Changelog

**2025-10-28**: Initial gap analysis by uta-simulation-architect agent
- Identified 4 TIER 1 critical gaps (7 hours to fix)
- Identified 4 TIER 2 realism gaps (10 hours)
- Identified 4 TIER 3 validation gaps (12 hours)
- Identified 4 TIER 4 polish items (8 hours)
- Total pathway: 37 hours to 98/100 specification quality

---

**END OF REPORT**
