# Action Interaction Matrix

**Generated**: 2025-10-28
**Purpose**: Map how player actions interact across modules, identify feedback loops, define processing order, and design missing route mechanics

---

## Executive Summary

When players choose MULTIPLE strategies in a single turn, understanding which systems interact—and in what order—is critical for realistic outcomes. This document:

1. **Maps cross-module interactions** (which actions affect which modules)
2. **Defines feedback loops** (where effects cascade and amplify)
3. **Specifies processing order** (which modules resolve first)
4. **Designs missing route mechanics** (gameplay-ready solutions for critical gaps)

**Key Finding**: Most "compound strategies" create 2-4 module interactions. The simulation needs **iterative CGE solving** to handle feedback loops correctly.

---

## Part 1: Single-Module Actions

These actions affect only ONE module. They're rare because most policies have economic ripple effects.

### Pure Trade Policy Actions

**Action**: Adjust tariff on single product from single country
**Module**: Trade Flow Module only
**Why Isolated**: If tariff is small (<5%) and product is non-critical, effects stay contained
**Example**: "Impose 3% tariff on Moroccan oranges"
**Outcome**: Orange imports from Morocco decrease slightly, minimal broader impact

**Action**: Issue origin certificate
**Module**: Compliance Module only
**Why Isolated**: Administrative action with no economic content
**Example**: "Grant certificate of origin to domestic wine producer"

### Pure Informational Actions

**Action**: Request trade data from partner
**Module**: Information system only
**Why Isolated**: No policy change, just intelligence gathering
**Example**: "Request detailed import statistics from EU"

**Action**: File UTA dispute (initial filing)
**Module**: UTA Dispute Resolution only
**Why Isolated**: Legal process, no immediate economic effect until ruling
**Example**: "File complaint against Chinese steel subsidies"

### Note on Rarity

In practice, even "small" actions often trigger secondary effects:
- Small tariff → domestic prices change → demand shifts → production adjusts
- Information request → reveals violation → triggers enforcement → sanctions

**Conclusion**: Single-module actions are <5% of gameplay. Most strategies are inherently multi-module.

---

## Part 2: Two-Module Interactions

Common pairs where actions require coordination between two modules.

### Trade + Pricing

**Example**: "Impose 25% steel tariff"
**Interaction**:
1. **Trade Flow Module**: Imports from target decrease (elasticity -2.5 → -25% tariff → -62.5% imports)
2. **Pricing Module**: Domestic steel price rises (pass-through rate 80% → +20% domestic price)
3. **Feedback**: Higher domestic price → increased domestic production → more supply → price moderates to +18%

**Processing Order**: Trade Flow calculates import reduction → Pricing calculates new equilibrium price → Trade Flow recalculates demand at new price → iterate until convergence

**Modules Involved**: 2 (Trade Flow, Pricing)
**Iterations Required**: 2-5 to converge

---

### Subsidy + Trade

**Example**: "Subsidize domestic semiconductor production by 15%"
**Interaction**:
1. **Subsidy Module**: Production costs drop 15% → domestic firms produce more
2. **Trade Flow Module**: Lower costs → exports increase, imports decrease
3. **Feedback**: Increased exports → foreign competitors lose share → foreign governments detect subsidy → countervailing duties

**Processing Order**: Subsidy → production cost adjustment → Trade Flow equilibrium → Compliance detection

**Modules Involved**: 2-3 (Subsidy, Trade Flow, possibly Compliance)
**Iterations Required**: 2-3

---

### Sanctions + Compliance

**Example**: "Impose sectoral sanctions on Russian energy"
**Interaction**:
1. **Sanctions Module**: Block Russia → EU oil trade
2. **Trade Flow Module**: Reroute flows (Russia → India, India → EU via refining)
3. **Compliance Module**: Detect triangulation attempt (India re-export spike)
4. **Sanctions Module**: Secondary sanctions on India if facilitating

**Processing Order**: Sanctions impose restrictions → Trade Flow reroutes → Compliance detects violations → Sanctions expands to intermediaries

**Modules Involved**: 3 (Sanctions, Trade Flow, Compliance)
**Critical Gap**: Route switching dynamics need formalization (see Part 4)

---

### Currency + Trade

**Example**: "Devalue currency by 10%"
**Interaction**:
1. **Currency Module**: FX intervention weakens exchange rate 10%
2. **Trade Flow Module**: Exports become 10% cheaper, imports 10% more expensive
3. **Pricing Module**: Import prices rise → domestic inflation +2-3%
4. **Trade Flow Module**: Export volume increases, import volume decreases

**Processing Order**: Currency intervention → exchange rate change → Trade Flow recalculates volumes and prices → Pricing adjusts for inflation

**Modules Involved**: 3 (Currency, Trade Flow, Pricing)
**Iterations Required**: 3-4

---

### Energy + Trade

**Example**: "Release strategic oil reserves (50M barrels)"
**Interaction**:
1. **Energy Module**: Additional supply → oil price drops -10%
2. **Trade Flow Module**: Lower prices → increased demand, decreased production (supply-demand elasticity)
3. **Pricing Module**: Downstream products (petrochemicals, transportation) costs fall
4. **Energy Module**: Reserve depletion (must refill later)

**Processing Order**: Energy supply shock → Pricing calculates new oil price → Trade Flow adjusts to new equilibrium → cascades to oil-dependent sectors

**Modules Involved**: 3 (Energy, Pricing, Trade Flow)
**Duration**: Temporary effect (60-90 days until reserves depleted)

---

### Military + Trade

**Example**: "Naval blockade of Taiwan"
**Interaction**:
1. **Military Module**: Throughput -80% through Taiwan Strait
2. **Trade Flow Module**: Asia-Europe trade reroutes around Indonesia (+15% distance, +3 days)
3. **Pricing Module**: Transport costs increase 30% → consumer prices +5%
4. **Military Module**: Insurance rates spike 200bps

**Processing Order**: Military action → Trade Flow reroutes → Pricing calculates cost impact → Trade volumes decrease (marginal trades become unprofitable)

**Modules Involved**: 3 (Military, Trade Flow, Pricing)
**Escalation Risk**: 80% (near-war scenario)

---

## Part 3: Multi-Module Cascades

Complex strategies that create chains of effects across 4+ modules.

### Full Economic Warfare: Comprehensive Sanctions

**Example**: "Impose comprehensive sanctions on Iran"

**Phase 1 - Immediate (Turn T)**:
1. **Sanctions Module**: Block all Iran trade
2. **Trade Flow Module**: Iran exports/imports → 0
3. **Pricing Module**: Oil prices spike +$10/barrel (Iran supplies 3% global)
4. **Compliance Module**: Flag triangulation attempts

**Phase 2 - Secondary Effects (Turn T+1)**:
5. **Currency Module**: Iranian rial collapses -50% (no trade, no forex)
6. **Energy Module**: Iran's oil revenue drops to $0
7. **Trade Flow Module**: Regional powers (India, China, Turkey) increase imports from Iran covertly

**Phase 3 - Detection & Enforcement (Turn T+2)**:
8. **Compliance Module**: Detects India oil re-exports (volume spike)
9. **Sanctions Module**: Secondary sanctions threaten India
10. **Geopolitical Module**: India faces choice: comply or defy

**Phase 4 - Equilibrium (Turn T+3+)**:
11. **Trade Flow Module**: Iran trade stabilizes at ~40% pre-sanction (via triangulation)
12. **Pricing Module**: Oil prices moderate to +$5/barrel
13. **Energy Module**: Alternative suppliers (Saudi, US shale) increase production

**Modules Involved**: 7 (Sanctions, Trade Flow, Pricing, Compliance, Currency, Energy, Geopolitical)
**Iterations Required**: 8-12 for full equilibrium
**Duration**: 3-4 turns to stabilize

**Key Insight**: Sanctions don't work instantly. Multi-turn dynamics with circumvention attempts create realistic complexity.

---

### Industrial Dominance Strategy: Subsidy + Dumping + Market Capture

**Example**: China's semiconductor strategy

**Phase 1 - Build Capacity (Turns 1-3)**:
1. **Subsidy Module**: 15% production subsidy + $50B R&D
2. **Firm-State Module**: SOEs invest in fabs (3-turn construction lag)
3. **Trade Flow Module**: No immediate effect (capacity not online yet)

**Phase 2 - Market Entry (Turns 4-6)**:
4. **Firm-State Module**: New capacity online, SOEs undercut foreign competitors -20%
5. **Trade Flow Module**: Chinese semiconductor exports surge +200%
6. **Pricing Module**: Global chip prices fall -15%
7. **Compliance Module**: Detect below-cost pricing (dumping signals)

**Phase 3 - Foreign Response (Turns 7-9)**:
8. **Subsidy Module** (US/EU): Countervailing duties +15%
9. **Sanctions Module** (US): Technology export controls on advanced chipmaking equipment
10. **Geopolitical Module**: Tech alliance forms (US-Taiwan-South Korea-Japan)

**Phase 4 - Escalation (Turns 10-15)**:
11. **Firm-State Module**: Chinese SOEs sustain losses (state absorbs -$5B/year)
12. **Trade Flow Module**: Market share shifts (China 25% → 40%, others decline)
13. **Subsidy Module** (Competitors): Match subsidies or exit market
14. **Geopolitical Module**: Technology decoupling (separate supply chains)

**Modules Involved**: 6 (Subsidy, Firm-State, Trade Flow, Pricing, Compliance, Geopolitical)
**Iterations Required**: 20-30 (long-term strategy)
**Outcome**: Market restructuring, bloc fragmentation

**Key Insight**: Industrial policy creates decade-long feedback loops. State capacity to sustain losses is critical variable.

---

### Energy Leverage + Economic Coercion

**Example**: Russia weaponizes gas supplies to Europe

**Phase 1 - Threat (Turn T)**:
1. **Geopolitical Module**: Russia signals gas cutoff if sanctions not lifted
2. **Energy Module**: Europe assesses vulnerability (40% gas from Russia)
3. **Trade Flow Module**: No immediate change (threat only)

**Phase 2 - Execution (Turn T+1)**:
4. **Energy Module**: Russia reduces gas flows -60% (Nord Stream "maintenance")
5. **Pricing Module**: European gas prices spike +300%
6. **Trade Flow Module**: European industry curtails production (energy-intensive sectors)
7. **Pricing Module**: European GDP falls -1.5%

**Phase 3 - European Response (Turn T+2)**:
8. **Energy Module**: Emergency measures (release reserves, coal restart, rationing)
9. **Trade Flow Module**: Emergency LNG imports from US, Qatar (+150%)
10. **Currency Module**: Euro weakens -8% (economic crisis)
11. **Geopolitical Module**: Maintain sanctions despite economic pain (political will test)

**Phase 4 - Structural Adjustment (Turns T+3 to T+10)**:
12. **Energy Module**: Build LNG terminals (3-turn construction)
13. **Trade Flow Module**: Permanent shift from pipeline to LNG
14. **Geopolitical Module**: Russia loses leverage permanently
15. **Energy Module**: European energy security improves (diversified suppliers)

**Modules Involved**: 5 (Geopolitical, Energy, Pricing, Trade Flow, Currency)
**Iterations Required**: 15-20 (structural break)
**Outcome**: Permanent decoupling (Russia-Europe energy relationship ends)

**Key Insight**: Resource leverage is use-it-or-lose-it. Weaponizing supply drives permanent substitution.

---

### Currency War + Trade War + Alliance Formation

**Example**: US-China strategic rivalry escalates

**Phase 1 - Trade Skirmish (Turns 1-3)**:
1. **Sanctions Module** (US): 25% tariffs on $250B Chinese goods
2. **Trade Flow Module**: US-China trade falls -30%
3. **Geopolitical Module** (China): Retaliate with tariffs on US soybeans, aircraft
4. **Pricing Module**: US consumer prices +1.5%, Chinese export prices fall -10%

**Phase 2 - Currency Escalation (Turns 4-6)**:
5. **Currency Module** (China): Allow yuan to weaken -8%
6. **Trade Flow Module**: Chinese exports recover competitiveness
7. **Currency Module** (US): Label China "currency manipulator"
8. **Compliance Module**: UTA investigation into currency manipulation

**Phase 3 - Technology Decoupling (Turns 7-10)**:
9. **Sanctions Module** (US): Ban Huawei, semiconductor export controls
10. **Subsidy Module** (China): Crash program for chip self-sufficiency ($150B)
11. **Firm-State Module**: Chinese SOEs invest in domestic semiconductor capacity
12. **Trade Flow Module**: Tech supply chains fragment (two separate ecosystems)

**Phase 4 - Alliance Competition (Turns 11-15)**:
13. **Geopolitical Module** (US): Form Tech Democracy Alliance (US-EU-Japan-Taiwan-S. Korea)
14. **Geopolitical Module** (China): Counter with BRICS+ expansion, Belt & Road acceleration
15. **Trade Flow Module**: Global trade splinters into US-led and China-led blocs
16. **Pricing Module**: Efficiency losses from fragmentation (-2% global GDP)

**Phase 5 - Cold War Equilibrium (Turns 16+)**:
17. **Geopolitical Module**: Bipolar system stabilizes (managed competition)
18. **Trade Flow Module**: Within-bloc trade intensifies, cross-bloc trade minimal
19. **Energy Module**: Separate energy markets (China secures Russia, US controls Middle East)
20. **Military Module**: Deterrence without direct conflict (gray zone competition)

**Modules Involved**: 8 (ALL major modules engaged)
**Iterations Required**: 40-60 (decade-long transformation)
**Outcome**: Systemic restructuring (multipolar or bipolar world order)

**Key Insight**: Great power competition engages entire simulation. No module is isolated.

---

## Part 4: Critical Missing Interactions

### Gap #1: Route Switching Dynamics (CRITICAL)

**Scenario**: EU sanctions Russian oil → flows must reallocate

**Current State**: Trade Flow Module describes scenario but lacks dynamic adjustment mechanics

**Missing Mechanics**:

#### Phase 1: Immediate Disruption (Turn T)

**What Happens**:
```
1. Sanctions impose: Russia → EU oil routes blocked
2. Immediate effects:
   - Russia oil exports: Sudden -3 million bbl/day capacity (blocked EU route)
   - EU oil imports: Sudden -3 million bbl/day deficit
   - Global oil price: SPIKE

Price Spike Calculation:
  Supply_Shock = -3M bbl/day / 100M bbl/day global = -3% supply
  Price_Elasticity = -0.3 (short-run inelastic)
  Price_Change = Supply_Shock / Elasticity = -3% / -0.3 = +10% price increase

  If oil was $80/bbl → immediate spike to $88/bbl
```

**Player Options (Russia)**:
- Accept revenue loss and wait for alternative buyers
- Offer deep discounts to Asian buyers (-20% to -30% to incentivize immediate purchases)
- Threaten further supply cuts to spike prices higher

**Player Options (EU)**:
- Tap strategic reserves (buys 60-90 days)
- Emergency LNG imports (expensive, limited capacity)
- Ease sanctions to allow some Russian imports (political cost)

#### Phase 2: Short-Term Reallocation (Turns T+1 to T+4)

**What Happens**:
```
Constraint: Alternative routes have CAPACITY LIMITS

Russia Seeks New Buyers:
  - China current capacity: Takes 2M bbl/day via pipeline (85% utilized)
  - India capacity: Takes 0.5M bbl/day via tanker (60% utilized)
  - Turkey capacity: Takes 0.3M bbl/day via Black Sea (70% utilized)

  Total Available Capacity: ~1M bbl/day additional (within existing infrastructure)
  Shortfall: 3M blocked - 1M rerouted = 2M bbl/day still stranded

Russia Options:
  1. Deep Storage: Store 2M bbl/day temporarily (expensive, fills in ~3 months)
  2. Shut-In Production: Turn off wells (costly to restart, reservoir damage)
  3. Discounted Sales: Sell at -$30/bbl to incentivize capacity expansion

EU Finds Alternatives:
  - Middle East supplies: +0.8M bbl/day (Saudi spare capacity)
  - US shale: +0.5M bbl/day (can ramp quickly)
  - Strategic reserves: Release 0.5M bbl/day (temporary)
  - Demand destruction: High prices reduce consumption -1.2M bbl/day

  Total: +0.8 + 0.5 + 0.5 + 1.2 = 3M bbl/day (BALANCED)

Price Dynamics:
  Turn T+1: $88/bbl (still elevated, adjustment beginning)
  Turn T+2: $85/bbl (partial rebalancing)
  Turn T+3: $83/bbl (approaching new equilibrium)
  Turn T+4: $82/bbl (new equilibrium, +$2 vs pre-sanction due to higher transport costs)
```

**Gameplay Mechanics**:

**Capacity Utilization Rules**:
```
For each alternative route:
  - If Utilization < 70%: Can absorb additional flows immediately at current price
  - If Utilization 70-85%: Can absorb flows but congestion adds +$5/bbl cost
  - If Utilization 85-95%: Severe congestion adds +$10/bbl, delays 5-10 days
  - If Utilization > 95%: Physical capacity limit, cannot absorb more
```

**Rerouting Cost Premium**:
```
Direct route (Russia → EU): $2/bbl transport cost
Alternative routes:
  - Russia → China via pipeline: $3/bbl (longer distance)
  - Russia → India via tanker: $8/bbl (long sea route)
  - Russia → Turkey via Black Sea: $4/bbl (Bosphorus transit fees)

Premium paid by buyer or seller depending on bargaining power
```

**Player Strategic Choices**:

**Russia Turn T+1**:
- Option A: Discount $30/bbl to China/India to incentivize immediate purchases
- Option B: Reduce production 2M bbl/day, maintain price
- Option C: Build emergency storage capacity (1-turn construction, $500M)

**EU Turn T+1**:
- Option A: Bid up Middle East oil (+$5/bbl premium to secure supply)
- Option B: Continue reserve releases (depletes buffer)
- Option C: Negotiate partial sanctions exemption for critical industries

#### Phase 3: Long-Term Adjustment (Turns T+5+)

**What Happens**:
```
Infrastructure Investment:
  - Russia builds: Arctic oil terminal to China (3-turn construction, $5B)
                   Expanded India tanker capacity (2-turn, $2B)
  - China builds: Pipeline capacity expansion (4-turn, $8B)
  - EU builds: LNG import terminals (3-turn, $2B each)
             Hydrogen infrastructure (10-turn, $50B)

Capacity Expands:
  Turn T+5: Additional +0.5M bbl/day capacity online
  Turn T+7: Additional +1.0M bbl/day capacity online
  Turn T+10: Additional +1.5M bbl/day capacity online (full structural adjustment)

Price Dynamics:
  Turn T+5 to T+10: Price gradually falls $82 → $78/bbl (new long-run equilibrium)
  New Equilibrium: Slightly higher than pre-sanction due to:
    - Longer transport distances (+$2/bbl)
    - Less efficient routing (+$1/bbl)
    - Risk premium (+$1/bbl)
  Total: $4/bbl permanent premium
```

**Long-Term Strategic Implications**:

**Russia**:
- Permanently loses EU market (trust destroyed, infrastructure diverted)
- Becomes more dependent on Asia (China leverage increases)
- Accepts structural discount (-$5/bbl vs pre-sanction long-term)

**EU**:
- Achieves energy independence from Russia (strategic goal)
- Pays premium (+$4/bbl permanent) for diversification
- Accelerates green transition (high prices incentivize alternatives)

**China**:
- Gains leverage over Russia (sole major buyer)
- Negotiates structural discounts ($10/bbl below market)
- Locks in long-term supply contracts at favorable terms

**Gameplay Implementation**:

```python
# Pseudocode for Route Switching Dynamics

def handle_route_blockage(blocked_route, volume_blocked):
    """
    blocked_route: (origin, destination, product)
    volume_blocked: float (millions of units/day)
    """

    # Phase 1: Immediate Disruption (Turn T)
    price_spike = calculate_supply_shock_price_impact(volume_blocked)
    origin_country.stranded_volume = volume_blocked
    destination_country.supply_deficit = volume_blocked

    # Phase 2: Short-Term Reallocation (Turns T+1 to T+4)
    for turn in range(1, 5):
        # Origin seeks alternative buyers
        rerouted_volume = 0
        for alt_buyer in get_alternative_buyers(origin_country, product):
            available_capacity = alt_buyer.import_capacity - alt_buyer.current_imports
            capacity_utilization = alt_buyer.current_imports / alt_buyer.import_capacity

            # Apply congestion costs
            if capacity_utilization > 0.95:
                congestion_cost = float('inf')  # Cannot absorb more
            elif capacity_utilization > 0.85:
                congestion_cost = 10  # $/unit
            elif capacity_utilization > 0.70:
                congestion_cost = 5
            else:
                congestion_cost = 0

            # Calculate rerouting cost
            reroute_cost = transport_cost(origin_country, alt_buyer) + congestion_cost

            # Buyer accepts if price + reroute_cost < market_price
            if base_price + reroute_cost < market_price + discount_threshold:
                absorbed = min(volume_blocked - rerouted_volume, available_capacity)
                trade_flows.add(origin_country, alt_buyer, product, absorbed)
                rerouted_volume += absorbed

        # Remaining volume: storage or shut-in
        stranded_volume = volume_blocked - rerouted_volume
        if stranded_volume > 0:
            if origin_country.storage_capacity > stranded_volume:
                origin_country.storage_inventory += stranded_volume
            else:
                origin_country.production_shutin += stranded_volume

        # Destination seeks alternative suppliers
        deficit_filled = 0
        for alt_supplier in get_alternative_suppliers(destination_country, product):
            spare_capacity = alt_supplier.production_capacity - alt_supplier.current_production
            if spare_capacity > 0:
                supplied = min(volume_blocked - deficit_filled, spare_capacity)
                trade_flows.add(alt_supplier, destination_country, product, supplied)
                deficit_filled += supplied

        # Remaining deficit: demand destruction or reserve release
        remaining_deficit = volume_blocked - deficit_filled
        if remaining_deficit > 0:
            # Price rises until demand falls
            demand_reduction = remaining_deficit  # Assumes demand elasticity
            market_price = calculate_new_equilibrium_price(demand_reduction)

            # Or release strategic reserves (temporary)
            if destination_country.strategic_reserves > 0:
                release = min(remaining_deficit, destination_country.reserve_release_capacity)
                destination_country.strategic_reserves -= release
                remaining_deficit -= release

    # Phase 3: Long-Term Adjustment (Turns T+5+)
    # Players can invest in infrastructure (see infrastructure investment actions)
    # Capacity expands gradually, prices normalize

    return new_equilibrium_price, rerouted_trade_flows
```

**Player-Facing Summary**:

When a trade route is blocked by sanctions:
1. **Immediate (Turn 1)**: Prices spike, stranded volumes
2. **Short-term (Turns 2-4)**: Rerouting within existing capacity (congestion costs apply)
3. **Long-term (Turns 5+)**: Infrastructure investment enables full structural adjustment

**Strategic Choices**:
- **Origin**: Discount to incentivize rerouting, build storage, or shut-in production
- **Destination**: Bid for alternatives, release reserves, or accept demand destruction
- **Third Parties**: Expand capacity to capture rerouted flows (profit opportunity)

---

### Gap #2: Multi-Hop Route Optimization (CRITICAL)

**Scenario**: US sanctions Iranian oil → Iran ships to China → China refines → China exports refined products to EU

**Current State**: Compliance Module has detection rates, but Trade Flow Module lacks route optimization logic

**Missing Mechanics**:

#### When Do Multi-Hop Routes Make Sense?

**Decision Tree for Firms/Countries**:

```
Is direct route (A → B) blocked by sanctions?
├─ NO: Use direct route (lowest cost)
└─ YES: Evaluate multi-hop alternatives

For each potential intermediary C:
  ├─ Is route A → C → B physically feasible?
  │  ├─ NO: Skip this intermediary
  │  └─ YES: Continue evaluation
  │
  ├─ Calculate Total Cost:
  │  ├─ Transport Leg 1 (A → C): $X₁ per unit
  │  ├─ Handling at C: $H per unit (transshipment fee)
  │  ├─ Transport Leg 2 (C → B): $X₂ per unit
  │  ├─ Detection Risk Cost: (Detection_Probability × UTA_Penalty)
  │  └─ Total: $X₁ + $H + $X₂ + (P_detect × Penalty)
  │
  ├─ Compare to Direct Route Benefit:
  │  └─ Direct Route Value: $V (what you'd earn selling to B)
  │
  └─ Decision: Use multi-hop if Total_Cost < V
```

**Key Variables**:

**Transport Costs**:
```
Mode Costs ($/unit per 1000 km):
  - Sea freight: $50 (bulk commodities)
  - Pipeline: $20 (oil, gas)
  - Rail: $80
  - Air: $1800 (high-value only)

Distance Premiums:
  - Direct route (A → B): Distance_AB
  - Multi-hop (A → C → B): Distance_AC + Distance_CB (typically 20-50% longer)
```

**Handling Costs**:
```
Transshipment Fees by Intermediary:
  - Complicit Intermediary (actively facilitating): $50-100/unit
  - Neutral Hub (Singapore, Dubai): $150-200/unit (higher but legitimate cover)
  - Token Processing (minimal value-add): $20-50/unit (cheap but raises suspicion)
```

**Detection Risk**:
```
P(detection) = Base_Rate × Volume_Factor × Anomaly_Score × (1 - Opacity)

Where:
  Base_Rate = 0.60 (60% base for triangulation)
  Volume_Factor = 1 + (Volume_Spike / Historical_Average) × 0.5
    - If intermediary's re-exports spike 100% → Factor = 1.5
  Anomaly_Score = Production_Export_Ratio
    - If C exports more than it produces → Score = 2.0
  Opacity = Sector_Opacity × Country_Financial_Secrecy
    - Chemicals (0.7) in tax haven (0.8) → Opacity = 0.56
    - Oil (0.3) in transparent country (0.2) → Opacity = 0.06

Example:
  Iranian oil via Turkey to EU:
    Base = 0.60
    Volume surge 200% → Factor = 2.0
    Turkey exports exceed production → Anomaly = 1.5
    Oil sector → Opacity = 0.3 → (1 - 0.3) = 0.7

    P(detection) = 0.60 × 2.0 × 1.5 × 0.7 = 1.26 (capped at 1.0 = 100%)
```

**UTA Penalty**:
```
If detected and attributed:
  - Origin (Iran): -400 UTA credits (sanctions evasion)
  - Intermediary (Turkey): -200 UTA credits (facilitation)
  - Destination (EU firms): -100 UTA credits (complicity)

Monetary Penalties:
  - Shipment seized (lose goods value)
  - Fines (2x value of transaction)
  - Banned from market (EU) for 10 turns
```

#### Gameplay Mechanics: Route Selection Algorithm

**Player-Facing Interface**:

When a player wants to export to a sanctioned destination, system presents options:

**Option 1: Direct Route (Blocked)**
- Route: Iran → EU
- Status: BLOCKED (US sanctions)
- Cost: N/A
- Risk: 100% seizure if attempted

**Option 2: Single Intermediary (Turkey)**
- Route: Iran → Turkey → EU
- Transport: $250/bbl (Iran-Turkey) + $150/bbl (Turkey-EU) = $400/bbl
- Handling: $75/bbl (Turkey transshipment fee)
- Detection Risk: 80% (high volume, obvious pattern)
- Expected Penalty: 0.80 × $500 (UTA + fines) = $400/bbl
- **Total Expected Cost**: $400 + $75 + $400 = $875/bbl

**Option 3: Multi-Hop Chain (Turkey → India → EU)**
- Route: Iran → Turkey → India → EU (refined products)
- Transport: $250 + $200 + $300 = $750/bbl
- Handling: $75 (Turkey) + $100 (India refining) = $175/bbl
- Detection Risk: 40% (more complex, genuine refining value-add)
- Expected Penalty: 0.40 × $500 = $200/bbl
- **Total Expected Cost**: $750 + $175 + $200 = $1125/bbl

**Option 4: Complex Network (Multiple Routes)**
- Route: Iran → China (80%), Iran → Turkey (20%), blend → various destinations
- Transport: (Varied, $300-600/bbl average)
- Handling: $200/bbl (complex coordination)
- Detection Risk: 25% (diversified, harder to trace)
- Expected Penalty: 0.25 × $500 = $125/bbl
- **Total Expected Cost**: ~$700/bbl

**Player Decision**:
Compare Expected Cost to Market Price:
- EU oil market price: $800/bbl
- Option 1: Blocked
- Option 2: -$75/bbl loss (Expected Cost $875 > Price $800) → NOT VIABLE
- Option 3: -$325/bbl loss → NOT VIABLE
- Option 4: +$100/bbl profit (Price $800 - Cost $700) → VIABLE

**Strategic Choice**: Use complex network (Option 4) despite higher complexity because it's the only profitable option.

#### Implementation Pseudocode

```python
def optimize_sanctioned_route(origin, destination, product, volume, market_price):
    """
    Find optimal route when direct path is blocked.
    Returns best route and expected profit/loss.
    """

    if not is_sanctioned(origin, destination, product):
        # Direct route available - always use it
        transport_cost = calculate_transport_cost(origin, destination, volume, product)
        return {
            'route': ['direct', origin, destination],
            'cost': transport_cost,
            'profit': market_price - transport_cost,
            'detection_risk': 0.0
        }

    # Direct route blocked - evaluate alternatives
    best_option = None
    best_profit = float('-inf')

    # Evaluate single intermediaries
    for intermediary in get_potential_intermediaries(origin, destination):
        # Check feasibility
        if is_sanctioned(origin, intermediary) or is_sanctioned(intermediary, destination):
            continue  # This intermediary is also sanctioned

        # Calculate costs
        leg1_transport = calculate_transport_cost(origin, intermediary, volume, product)
        leg2_transport = calculate_transport_cost(intermediary, destination, volume, product)
        handling = get_transshipment_cost(intermediary, product)

        # Calculate detection risk
        detection_prob = calculate_detection_probability(
            origin, intermediary, destination, product, volume
        )
        expected_penalty = detection_prob * get_uta_penalty('triangulation')

        # Total cost
        total_cost = leg1_transport + leg2_transport + handling + expected_penalty
        profit = market_price - total_cost

        if profit > best_profit:
            best_profit = profit
            best_option = {
                'route': ['single_hop', origin, intermediary, destination],
                'transport_cost': leg1_transport + leg2_transport,
                'handling_cost': handling,
                'detection_risk': detection_prob,
                'expected_penalty': expected_penalty,
                'total_cost': total_cost,
                'profit': profit
            }

    # Evaluate multi-hop chains (2+ intermediaries)
    for intermediary_chain in get_intermediary_chains(origin, destination, max_hops=3):
        # Similar calculation but with multiple legs
        total_transport = sum(calculate_transport_cost(leg[0], leg[1], volume, product)
                             for leg in intermediary_chain)
        total_handling = sum(get_transshipment_cost(node, product)
                            for node in intermediary_chain[1:-1])

        # Detection risk decreases with complexity
        detection_prob = calculate_complex_chain_detection(intermediary_chain, product, volume)
        expected_penalty = detection_prob * get_uta_penalty('complex_triangulation')

        total_cost = total_transport + total_handling + expected_penalty
        profit = market_price - total_cost

        if profit > best_profit:
            best_profit = profit
            best_option = {
                'route': ['multi_hop'] + intermediary_chain,
                'transport_cost': total_transport,
                'handling_cost': total_handling,
                'detection_risk': detection_prob,
                'expected_penalty': expected_penalty,
                'total_cost': total_cost,
                'profit': profit
            }

    # Evaluate complex networks (split volume across multiple routes)
    # ... (more advanced strategy, can defer to later implementation)

    return best_option


def calculate_detection_probability(origin, intermediary, destination, product, volume):
    """
    Calculate probability of triangulation detection.
    """
    base_rate = 0.60  # 60% base for triangulation

    # Volume factor: spike in intermediary's re-exports
    historical_reexports = get_historical_exports(intermediary, destination, product)
    current_reexports = get_current_exports(intermediary, destination, product) + volume
    volume_spike = (current_reexports / historical_reexports) - 1.0
    volume_factor = 1.0 + (volume_spike * 0.5)

    # Anomaly score: production-export ratio
    production = get_production(intermediary, product)
    exports = current_reexports
    if production > 0:
        anomaly_score = min(exports / production, 3.0)  # Cap at 3x
    else:
        anomaly_score = 3.0  # No production but exports = highly suspicious

    # Opacity: sector and country characteristics
    sector_opacity = get_sector_opacity(product)  # 0.1 (transparent) to 0.8 (opaque)
    country_opacity = get_country_financial_secrecy(intermediary)  # 0.0 to 1.0
    opacity = sector_opacity * country_opacity

    # Combined detection probability
    detection_prob = base_rate * volume_factor * anomaly_score * (1.0 - opacity)

    # Cap at 100%
    return min(detection_prob, 1.0)


def calculate_complex_chain_detection(intermediary_chain, product, volume):
    """
    Detection probability for multi-hop chains (lower than single intermediary).
    """
    # Base detection rate lower for complex chains (harder to trace)
    base_rate = 0.40

    # Each additional hop reduces detection by 15%
    complexity_discount = 0.85 ** (len(intermediary_chain) - 2)

    # But each node still has detection risk
    node_detection_risks = []
    for i in range(len(intermediary_chain) - 1):
        node_risk = calculate_detection_probability(
            intermediary_chain[i],
            intermediary_chain[i+1],
            intermediary_chain[-1],
            product,
            volume
        )
        node_detection_risks.append(node_risk)

    # Overall detection is max of node risks, discounted by complexity
    max_node_risk = max(node_detection_risks)
    overall_risk = max_node_risk * complexity_discount * base_rate

    return min(overall_risk, 1.0)
```

**Player-Facing Summary**:

**When to Use Multi-Hop Routes**:
- Direct route is blocked by sanctions
- Multi-hop cost (transport + handling + detection risk) < market price
- You can find intermediaries willing to facilitate (complicit or neutral hubs)

**Cost-Benefit Tradeoff**:
- **Simple Triangulation**: Cheaper transport, but higher detection (60-80%)
- **Complex Networks**: More expensive, but lower detection (25-40%)
- **Expected Penalty**: Must include in cost calculation (detection % × UTA penalty)

**Strategic Considerations**:
- **Volume**: Small volumes easier to hide (lower detection)
- **Intermediary Choice**: Complicit partners charge less but may defect; neutral hubs are expensive but provide cover
- **Product Type**: Opaque sectors (chemicals, services) easier to triangulate than transparent (oil, agriculture)
- **Reputation**: Prior violations increase scrutiny (detection probability +30%)

---

### Gap #3: Infrastructure Capacity as Strategic Resource

**Scenario**: Port capacity, pipeline throughput, LNG terminal capacity become strategic chokepoints

**Current State**: Energy Module specifies capacities, but Trade Flow Module doesn't enforce constraints

**Missing Mechanics**:

#### Hard Constraints (Pipeline, Rail)

**Mechanics**:
```
Physical Limit: Cannot exceed maximum throughput

Example: Nord Stream Pipeline
  - Maximum capacity: 55 billion cubic meters (bcm) per year
  - Monthly capacity: 4.58 bcm/month

If Russia attempts to ship 5 bcm in a month:
  - Feasible volume: 4.58 bcm (capacity limit)
  - Excess demand: 0.42 bcm → MUST find alternative route

Alternative Options:
  1. Reroute via Ukraine pipeline (if open)
  2. Switch to LNG tankers (slower, more expensive)
  3. Delay shipment to next month (storage cost)
  4. Reduce sales to EU (foregone revenue)
```

**Hard Constraint Enforcement**:
```python
def enforce_pipeline_capacity(pipeline, scheduled_flow):
    """
    Cap flow at physical maximum.
    """
    max_capacity = get_pipeline_capacity(pipeline)  # bcm/month

    if scheduled_flow <= max_capacity:
        return scheduled_flow, 0  # No excess
    else:
        excess = scheduled_flow - max_capacity
        return max_capacity, excess  # Capped flow, excess must reroute
```

**Gameplay Implication**:
- Players cannot simply "send more gas" through pipeline
- Must invest in alternative infrastructure (LNG terminals, new pipelines)
- Strategic: Control over pipelines is REAL leverage (can't be bypassed instantly)

#### Soft Constraints (Ports, Airports)

**Mechanics**:
```
Port Capacity: Can exceed nominal capacity but with congestion costs

Example: Rotterdam Port
  - Nominal capacity: 14 million TEU (twenty-foot containers) per year
  - Current throughput: 13.2 million TEU (94% utilization)

Congestion Cost Function:
  Delay_Cost = Base_Cost × (Utilization_Rate - 0.85)²

  If utilization = 0.94 (94%):
    Congestion = (0.94 - 0.85)² = 0.0081
    Delay per container = $50 × 0.0081 = $0.40 (minimal)

  If utilization = 1.05 (105% overcapacity):
    Congestion = (1.05 - 0.85)² = 0.04
    Delay per container = $50 × 0.04 = $2.00 (significant)

  If utilization = 1.20 (120% severe congestion):
    Congestion = (1.20 - 0.85)² = 0.1225
    Delay per container = $50 × 0.1225 = $6.13 (severe, ships reroute)
```

**Soft Constraint Enforcement**:
```python
def calculate_port_congestion_cost(port, throughput):
    """
    Congestion cost increases quadratically above 85% capacity.
    """
    capacity = get_port_capacity(port)
    utilization = throughput / capacity

    if utilization < 0.85:
        return 0  # No congestion
    else:
        congestion_factor = (utilization - 0.85) ** 2
        delay_cost_per_unit = 50  # Base delay cost ($/TEU per day)
        avg_delay_days = congestion_factor * 5  # Delays scale with congestion
        return delay_cost_per_unit * avg_delay_days
```

**Gameplay Implication**:
- Ports CAN handle excess volume, but costs rise sharply
- At ~105% utilization, costs become prohibitive → ships reroute to alternative ports
- Strategic: Invest in port expansion to attract trade, or bottleneck rivals

#### Investment Dynamics

**Capacity Expansion Options**:

**Pipeline Expansion**:
- Cost: $5M to $15M per kilometer
- Duration: 4-8 turns (permitting, construction)
- Benefit: Permanent capacity increase (+50% to +100% original)
- Example: "Expand Nord Stream capacity from 55 bcm/year to 80 bcm/year"
  - Cost: $8B
  - Duration: 6 turns
  - Benefit: +25 bcm/year capacity (permanent)

**Port Expansion**:
- Cost: $500M to $5B (new cranes, dredging, terminal)
- Duration: 2-4 turns
- Benefit: +20% to +50% throughput
- Example: "Expand Rotterdam from 14M TEU to 18M TEU"
  - Cost: $2B
  - Duration: 3 turns
  - Benefit: +4M TEU/year (28% increase)

**LNG Terminal**:
- Cost: $2B per import terminal
- Duration: 3 turns
- Benefit: Enables LNG imports (diversifies suppliers, no pipeline lock-in)
- Example: "Build German LNG terminal"
  - Cost: $2B
  - Duration: 3 turns
  - Benefit: +5 bcm/year LNG import capacity

**Strategic Implications**:
- **Pre-Crisis Investment**: Build capacity before you need it (Germany should have built LNG terminals before Russia crisis)
- **Crisis Response**: Emergency capacity (temporary LNG ships, trucking) expensive but available immediately
- **Long-Term**: Infrastructure is sticky (once built, lasts decades) → permanent shift in trade patterns

---

## Part 5: Module Processing Order

When multiple modules interact in a single turn, order of resolution matters.

### Sequential Resolution (Non-Negotiable Order)

**Phase 1: Policy Announcement (Simultaneous)**
- All players announce actions simultaneously (no advantage to moving first)
- Prevents gaming (front-running, strategic delays)

**Phase 2: Defensive Actions (First)**
- Capital controls, emergency reserve releases
- Rationale: Defensive measures counter offensive actions

**Phase 3: Alliance Formations (Second)**
- Coalition membership locks in before conflicts resolve
- Rationale: Alliances determine who sides with whom in subsequent actions

**Phase 4: Economic Policies (Third)**
- Tariffs, subsidies, quotas applied
- Rationale: Set the "rules" before flows adjust

**Phase 5: Sanctions & Restrictions (Fourth)**
- Embargos, export controls imposed
- Rationale: Block routes before trade flows calculate

**Phase 6: Trade Flow Equilibrium (Fifth - ITERATIVE)**
- Given policies and restrictions, calculate equilibrium flows
- **Critical**: This is NOT a single pass - requires iterative solving
- Feedback loop: Prices → Demand → Supply → Prices (iterate until convergence)
- Integration with Pricing Module (outer loop)

**Phase 7: Military Operations (Sixth)**
- Blockades, cyber attacks, infrastructure sabotage
- Rationale: Military actions occur AFTER economic equilibrium, create NEW disequilibrium for next turn

**Phase 8: Detection & Enforcement (Seventh)**
- Compliance Module scans for violations
- Audits triggered, penalties assessed
- Rationale: Enforcement happens AFTER actions are executed (can't preempt)

**Phase 9: Reaction Window (Eighth - Sequential by Influence)**
- Countries may respond to actions taken against them
- Order: Highest influence score acts first (dominant powers respond faster)
- Each country gets ONE reaction

**Phase 10: State Updates (Ninth - System)**
- Update reputation scores, UTA credits
- Check archetype transitions, victory conditions
- Generate intelligence for next turn

### CGE Integration Loop (Critical)

**Outer Loop: Full Equilibrium**
```
For each turn:
  1. Players announce policies (tariffs, subsidies, sanctions)
  2. Pricing Module proposes initial prices P₀
  3. Demand Module calculates quantities demanded Q_d at P₀
  4. Supply Module calculates quantities supplied Q_s at P₀
  5. Trade Flow Module:
     - Calculate bilateral flows given P₀
     - Apply transport costs and tariffs
     - Enforce capacity constraints
     - Balance flows (RAS algorithm)
     - Return effective supplies S_eff and demands D_eff
  6. Pricing Module checks excess demand: Z = D_eff - S_eff
  7. If |Z| < tolerance for all products: EQUILIBRIUM FOUND, exit
  8. Else: Update prices P₁ = P₀ × (1 + α × Z/S_eff), return to step 3
  9. Repeat until convergence (max 500 iterations)
```

**Inner Loop: Trade Flow Balancing**
```
Within Trade Flow Module (step 5 above):
  For each iteration:
    a. Calculate gravity-predicted flows T given prices P
    b. Apply sanctions (zero out blocked routes)
    c. Optimize routes (select cheapest feasible path including triangulation)
    d. Enforce capacity constraints (hard: cap, soft: add congestion cost)
    e. Balance flows using RAS:
       - Row adjustment: scale to match origin supplies
       - Column adjustment: scale to match destination demands
       - Check convergence: |Supply - Demand| < 0.1% world trade
    f. If converged: Return balanced flows
       Else: Iterate (max 100 inner iterations)
```

**Convergence Criteria**:
- **Outer Loop (CGE)**: |Z/Q| < 0.0001 (0.01% relative excess demand) for ALL markets
- **Inner Loop (Trade Flow)**: Σ|Supply - Demand| < 0.001 × World_Trade (0.1%)
- **Maximum Iterations**: Outer 500, Inner 100 (if not converged, flag as infeasible)

**Why This Matters**:
Without proper iteration, simulation produces WRONG results:
- Tariff increases → higher prices → lower demand → lower imports (feedback)
- Subsidies → lower costs → higher exports → higher world supply → lower prices (feedback)
- Sanctions → rerouted flows → congestion → higher costs → lower demand (feedback)

Single-pass calculations miss these feedback effects.

---

## Part 6: Critical Feedback Loops

### Positive Feedback Loops (Amplifying)

**Escalation Spiral**:
```
Country A sanctions Country B
  → B retaliates with counter-sanctions
    → A escalates with secondary sanctions
      → B weaponizes energy/resources
        → A forms coalition, comprehensive embargo
          → B forms counter-coalition
            → System fragments into hostile blocs
```

**Prevention**: De-escalation mechanics, reputation costs, third-party mediation

---

**Resource Cartel Breakdown**:
```
OPEC cuts production to raise prices
  → High prices → windfall profits for members
    → Temptation to cheat (sell more at high prices)
      → Members increase production covertly
        → Prices fall (oversupply)
          → Cartel discipline breaks down
            → Price collapse (everyone sells maximum)
```

**Stabilization**: Side payments to low-production members, Saudi swing producer role

---

**Debt-Crisis Spiral**:
```
Country borrows heavily (high debt/GDP)
  → Credit rating downgrade
    → Borrowing costs increase (risk premium)
      → Fiscal burden worsens (higher interest payments)
        → More borrowing needed
          → Further downgrades
            → Crisis: Unable to borrow, default imminent
```

**Escape**: IMF bailout, debt restructuring, austerity (painful)

---

### Negative Feedback Loops (Stabilizing)

**Price Self-Correction**:
```
Oil price spikes +50%
  → Demand falls (consumers cut usage, recession)
    → Supply rises (high prices incentivize production)
      → Inventory builds (more supply than demand)
        → Prices fall (back toward equilibrium)
```

**System Characteristic**: Commodity markets self-stabilize over 6-12 months

---

**Subsidy Detection & Countervailing**:
```
Country A subsidizes steel production
  → Exports surge, prices fall
    → Rivals detect below-cost pricing
      → UTA investigation, subsidy proven
        → Countervailing duties imposed (offset subsidy)
          → A's advantage neutralized
```

**System Characteristic**: Enforcement limits beggar-thy-neighbor policies

---

**Reputation Equilibrium**:
```
Country cheats repeatedly
  → Reputation falls
    → Higher scrutiny (more audits, lower trust)
      → Detection probability rises
        → Penalties accumulate
          → Cheating becomes unprofitable
            → Country shifts to compliance
              → Reputation gradually recovers
```

**System Characteristic**: Reputational capital constrains long-term cheating

---

### Tipping Points & Hysteresis

**Economic Decoupling**:
- **Before Tipping Point**: US-China trade high, strategic competition managed
- **After Tipping Point**: Comprehensive decoupling, separate supply chains, cold war dynamics
- **Threshold**: ~30% tariff level + technology restrictions + financial sanctions
- **Hysteresis**: Once decoupled, very hard to re-couple (infrastructure, trust destroyed)

**Energy Transition**:
- **Before Tipping Point**: Fossil fuels dominant, renewables niche
- **After Tipping Point**: Renewables cost-competitive, fossil fuel demand collapse
- **Threshold**: Renewables reach grid parity (~$0.04/kWh)
- **Hysteresis**: Fossil fuel assets stranded, transition irreversible

**Regime Stability**:
- **Before Tipping Point**: Economic hardship, protests, but regime stable
- **After Tipping Point**: Cascading elite defections, military coup, regime change
- **Threshold**: -25% GDP collapse + loss of military loyalty
- **Hysteresis**: New regime establishes, old regime cannot return

---

## Part 7: Recommendations

### For Immediate Implementation

**Priority 1: Complete TIER 1 Gap Specifications** (10-12 hours)
- Route Switching Dynamics (Part 4, Gap #1)
- Multi-Hop Route Optimization (Part 4, Gap #2)
- Capacity Constraints Enforcement (Part 4, Gap #3)

**Priority 2: Define CGE Integration Loop** (3-4 hours)
- Outer loop convergence criteria
- Inner loop (Trade Flow) balancing
- Maximum iteration limits
- Infeasibility handling

**Priority 3: Implement Module Processing Order** (2-3 hours)
- Sequential phase definitions
- Reaction window mechanics
- System state update procedures

### For Development Phase

**Iterative Solver Implementation**:
- Start with simple tâtonnement (price adjustment proportional to excess demand)
- Upgrade to Newton-Raphson if convergence issues
- Consider damping factor (0.3-0.5) to prevent oscillation

**Modular Architecture**:
- Each module should have clear input/output contracts
- Trade Flow Module receives: prices, policies, restrictions
- Trade Flow Module returns: flows, excess demands, anomalies
- Pricing Module orchestrates iteration

**Performance Optimization**:
- Sparse matrices (most country-pairs don't trade most products)
- Parallel processing (product-level equilibria can solve independently)
- Caching (transport costs, gravity predictions)
- Warm starts (use previous turn's solution as initial guess)

### For Testing & Validation

**Historical Scenario Replication**:
1. 2022 Russia-Ukraine energy crisis → Test route switching, price spikes
2. 2018 US-China tariff war → Test retaliation dynamics, coalition formation
3. 2020 Suez blockage → Test capacity constraints, rerouting

**Stress Testing**:
- Simultaneous shocks (pandemic + energy crisis + financial crisis)
- Extreme policies (100% tariffs, comprehensive sanctions on major economy)
- Coalition breakdown (fragmentation cascade)

**Convergence Analysis**:
- Track iterations to equilibrium (should converge <100 outer iterations typical)
- Identify infeasible scenarios (no equilibrium exists - rare but possible)
- Validate convergence criteria (R² > 0.90 vs historical data)

---

## Conclusion

The UTA Simulation is an **integrated system** where player actions cascade across modules in complex, realistic ways. The key insights:

1. **Most strategies engage 3-5 modules** - isolation is rare
2. **Feedback loops require iterative solving** - single-pass calculations are WRONG
3. **Processing order matters** - sanctions before trade flows, detection after execution
4. **Critical gaps are narrow but blocking** - 3 TIER 1 gaps in Trade Flow Module
5. **Route mechanics are gameplay-ready** - specifications in Part 4 can be implemented

**Next Steps**:
1. Architect completes TIER 1 specifications (Part 4, Gaps 1-3)
2. Developers implement CGE integration loop (Part 5)
3. Validate against historical scenarios
4. Release MVP (85% complete)
5. Iterate based on gameplay testing

The simulation is **closer to ready than it appears**. Focus on the critical gaps, implement proper iteration, and you'll have a credible, policy-relevant geo-economic model.
