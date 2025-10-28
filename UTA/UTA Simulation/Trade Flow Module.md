# Trade Flow Module

## What This Module Does

The Trade Flow Module is the **global shipping and logistics brain** of the UTA simulation. It tracks every product moving between every country - who's sending what to whom, how it gets there, how much it costs, and whether anyone is playing tricks with the routes.

Think of it as combining:
- **A massive shipping manifest** tracking all global trade
- **A logistics optimizer** finding best routes and costs
- **A customs inspector** watching for smuggling and sanctions evasion
- **An economic balancer** ensuring supply equals demand globally

## Why This Module Exists

In the real world, trade isn't instantaneous or free. Goods must physically move from factories in one country to consumers in another. This involves:
- **Transport costs** (ships, trucks, planes, pipelines)
- **Physical constraints** (distance, infrastructure, chokepoints)
- **Policy barriers** (tariffs, quotas, sanctions)
- **Strategic decisions** (route selection, circumvention attempts)

The Trade Flow Module makes all of this concrete and measurable. Without it, the simulation would just have abstract "production" and "consumption" without the messy reality of getting goods from point A to point B.

## Core Functions

### 1. Track All Trade Flows

The module maintains a comprehensive record of global trade:
- **What products** are moving (oil, steel, smartphones, wheat, etc.)
- **Between which countries** (China → USA, Germany → France, etc.)
- **How much volume** (in tons, barrels, units, or monetary value)
- **At what prices** (including transport and tariffs)
- **Via which routes** (direct shipping, or multi-hop through transit countries)

This creates a "source of truth" for physical goods movement in the simulation.

### 2. Calculate Transport Costs

For every trade relationship, the module figures out:

**How goods get there:**
- **Oil and gas** → pipelines (cheapest for liquids)
- **Bulk commodities** (grain, coal, ore) → cargo ships
- **High-value goods** (electronics, machinery) → container ships or air freight
- **Perishables** → air freight or refrigerated ships

**What it costs:**
- **Base distance cost**: Longer routes cost more
- **Volume discounts**: Bulk shipments reduce per-unit costs
- **Chokepoint premiums**: Suez Canal, Panama Canal, Strait of Malacca add fees
- **Infrastructure quality**: Poor ports and roads increase costs
- **Mode efficiency**: Ships are cheap, planes are fast but expensive

**Example calculation:**
```
Shipping Saudi oil to China:
- Route: Tanker through Strait of Hormuz → Strait of Malacca → Shanghai
- Base cost: 5,000 km × $0.05/ton-km = $250/ton
- Hormuz premium: +20% = $50/ton
- Malacca premium: +12% = $30/ton
- Total transport cost: $330/ton
```

### 3. Apply Trade Policies

The module enforces all government interventions:

**Tariffs:**
- **Ad valorem**: Percentage of product value (25% tariff on $100 steel = $25 extra)
- **Specific**: Fixed amount per unit ($50 per ton)
- **Compound**: Both combined (10% + $20/unit)
- **Preferential rates**: Lower tariffs for trade agreement partners

**Trade restrictions:**
- **Embargoes**: Complete bans (no trade allowed)
- **Sanctions**: Targeted restrictions (e.g., no oil from Russia)
- **Quotas**: Volume limits (max 10,000 tons per year)
- **Retaliatory measures**: Automatic responses to partner actions

### 4. Optimize Trade Routes

The module finds the best path for goods considering:

**Route options:**
- **Direct shipping**: Straight from exporter to importer
- **Multi-hop routes**: Through transit countries (sometimes to avoid restrictions)
- **Modal choices**: Sea vs air vs rail vs pipeline

**Optimization factors:**
- **Cost vs time tradeoffs**: Cheap shipping or fast delivery?
- **Avoiding blocked routes**: Closed canals, sanctioned territories
- **Working around restrictions**: Legal circumvention of high tariffs
- **Capacity constraints**: Port congestion, pipeline capacity

### 5. Detect Triangulation and Smuggling

This is the **cheating detection system**. It catches countries trying to evade sanctions or tariffs through "triangulation":

**Classic triangulation pattern:**
1. **Country A bans imports from Country B** (e.g., USA bans Russian oil)
2. **Country B ships to Country C** (Russia ships oil to Turkey)
3. **Country C suddenly "exports" way more than it produces** (Turkey exports oil to USA)
4. **Red flag**: Turkey's oil imports from Russia match its oil exports to USA

**Detection signals the module watches for:**
- **Production-export mismatch**: Exporting more than you produce (without manufacturing)
- **Sudden spikes**: Re-exports surge after sanctions announced
- **Trade asymmetries**: Country A reports $100M in exports, Country B reports $50M in imports
- **Thin margins**: Tiny profit on re-exports suggests pass-through, not actual trade
- **Suspicious timing**: Trade patterns change exactly when policies do
- **Known evasion routes**: Historical patterns of sanctions circumvention

**Example detection:**
```
Turkey oil flows (monthly):
- Normal: Import 2M barrels (for domestic use), Export 0.5M barrels
- After Russia sanctions: Import 8M barrels, Export 7.5M barrels
- Detection: 6M barrel increase in both = triangulation flag
- UTA investigation triggered
```

### 6. Ensure Economic Consistency

The module enforces fundamental economic accounting:

**Global balance:**
- **Total world exports = Total world imports** (goods don't vanish)
- **Every sale has a buyer**: Someone's export is someone else's import

**Country-level balance:**
```
Production + Imports = Domestic Consumption + Exports
```

**Market clearing:**
- If import demand > available supply → prices rise
- If export supply > import demand → prices fall
- Module iterates until supply equals demand for every product in every location

This ensures the simulation economy is mathematically consistent and realistic.

## How It Works Each Turn

Every simulation cycle, the Trade Flow Module runs through:

### Step 1: Calculate Base Trade Potential
Uses **gravity model** economics:
- Bigger economies naturally trade more
- Closer countries trade more
- Production capacity limits exports
- Creates "natural" trade flow baseline

### Step 2: Apply All Policies
Layers on human decisions:
- Block sanctioned routes completely
- Add tariff costs to prices
- Enforce quota limits
- Apply preferential trade agreement rates

### Step 3: Optimize Routes and Costs
Finds best shipping paths:
- Calculates transport costs for all viable routes
- Selects lowest-cost option that complies with restrictions
- Determines which transit countries to use (if any)
- Accounts for infrastructure and chokepoint constraints

### Step 4: Balance Supply and Demand
Iterates to equilibrium:
- Checks if all markets clear (supply = demand)
- Adjusts flows if imbalances exist
- Ensures global trade adds up correctly
- Converges to stable trade pattern

### Step 5: Scan for Anomalies
Runs detection algorithms:
- Identifies suspicious trade patterns
- Flags potential triangulation attempts
- Calculates trade asymmetries
- Generates investigation leads for UTA enforcement

### Step 6: Update World State
Publishes results:
- Countries see their trade revenues and volumes
- Market shares update (who's winning in which markets)
- Trade balances calculated (exports minus imports)
- Anomaly reports sent to compliance module

## Integration With Other Modules

The Trade Flow Module sits at the center of the economic system:

### Receives inputs from:
- **Demand Module**: What each country wants to import
- **Production/Supply**: What each country can export
- **Pricing Module**: Market prices for goods
- **Sanctions Module**: Which trade routes are restricted
- **Energy & Logistics Module**: Transport costs and infrastructure capacity

### Sends outputs to:
- **Pricing Module**: Realized trade volumes for equilibrium calculations
- **Compliance Module**: Suspicious trade patterns for investigation
- **Country Agents**: Trade performance metrics (revenues, market shares, balances)
- **Subsidy Module**: Export performance data for industrial policy
- **UTA Enforcement**: Triangulation flags and evasion attempts

## Strategic Gameplay Implications

Players (countries) interact with this module through strategic decisions:

### Legitimate strategies:
- **Adjust tariffs**: Protect domestic industries or pressure partners
- **Negotiate trade deals**: Lower costs with allies
- **Invest in infrastructure**: Reduce transport costs, increase trade efficiency
- **Become a trade hub**: Position as re-export center (like Singapore)
- **Form trade blocs**: Coordinate policy with partners
- **Diversify suppliers**: Reduce dependence on single source

### Gray-zone strategies:
- **Re-labeling**: Import then export with "Made in [Country]" label
- **Minor processing**: Add minimal value to claim origin change
- **Free trade zone exploitation**: Route through special economic zones
- **Legal triangulation**: Use legitimate intermediaries

### Cheating strategies (risky):
- **Sanctions evasion**: Route goods through neutral countries
- **Origin fraud**: Falsify product sources
- **Shadow fleets**: Unregistered shipping to avoid detection
- **Invoice manipulation**: Misreport trade values and volumes

### Detection risk:
All cheating strategies face **probability of detection**:
- Higher volumes = easier to spot
- Known evasion routes = higher scrutiny
- Trade asymmetries = red flags
- UTA intelligence = cross-checks multiple data sources
- **Penalties**: Loss of UTA credits, fines, trade restrictions, reputational damage

## Real-World Scenarios This Models

The module can simulate historical and hypothetical trade shocks:

### 2022 Russian Energy Sanctions
- **Event**: EU bans Russian oil imports
- **Direct effect**: Russia-EU flows drop to zero
- **Second-order**: Russia-India and Russia-China flows surge
- **Third-order**: India and Turkey oil exports to EU increase mysteriously
- **Detection**: Module flags trade asymmetries, UTA investigates

### 2018 US-China Trade War
- **Event**: USA imposes 25% tariffs on Chinese goods
- **Response**: China retaliates with tariffs on US soybeans, aircraft
- **Substitution**: Trade shifts to Mexico, Vietnam, Southeast Asia
- **Effect**: Market shares change, prices adjust, new supply chains form

### 2021 Suez Canal Blockage
- **Event**: Ever Given ship blocks canal for 6 days
- **Immediate**: Module reroutes ships around Africa
- **Costs**: Transport costs spike 30% on affected routes
- **Delays**: Trade volumes drop temporarily, congestion cascades
- **Recovery**: Normal flows resume once cleared

### North Korea Sanctions Evasion (ongoing)
- **Restrictions**: UN ban on coal exports
- **Triangulation**: North Korea → China → Southeast Asia → global markets
- **Detection**: Ship-to-ship transfers, AIS spoofing, port record discrepancies
- **Module behavior**: Flags volume spikes in intermediary countries

## Key Outputs for Players

Every turn, countries receive trade flow intelligence:

### Performance metrics:
- **Export revenues by product and destination**
- **Import costs by product and source**
- **Trade balance** (exports minus imports, in dollars)
- **Market shares** (% of destination's imports you supply)
- **Competitive position** (your price vs competitors)

### Strategic intelligence:
- **Emerging trade patterns** (who's trading more/less)
- **Cost trends** (are transport costs rising?)
- **Policy impacts** (how did that tariff change affect flows?)
- **Vulnerability assessment** (how dependent are you on specific partners?)

### Risk alerts:
- **Your triangulation attempts flagged** (uh oh)
- **Partners under investigation** (risky to trade with them)
- **Supply chain disruptions** (chokepoint blocked, infrastructure damage)
- **Market access changes** (new sanctions, trade agreements)

## Economic Foundations

The module implements established trade theory:

### Gravity Model of Trade
Trade flows follow economic "gravity":
```
Trade volume ∝ (Exporter GDP × Importer GDP) / Distance
```
Adjusted for:
- Tariffs (reduce trade)
- Trade agreements (increase trade)
- Common language/culture (increase trade)
- Infrastructure quality (affects effective distance)

### Armington Assumption
Products are differentiated by origin:
- German cars ≠ Japanese cars (even if both are "cars")
- Countries have preferences for specific sources
- Elasticity of substitution varies by product type:
  - **Commodities** (oil, wheat): High substitutability (≈ 5.0)
  - **Differentiated goods** (machinery): Medium (≈ 2.0)
  - **Strategic goods** (rare earths): Low (≈ 1.2)

### Market Clearing
Prices adjust until:
- Every seller finds a buyer
- Every buyer finds a seller
- No excess supply or demand remains
- Trade volumes stabilize

This ensures economic realism and prevents impossible scenarios.

## Calibration and Realism

The module uses real-world data:

### Data sources:
- **UN Comtrade**: Bilateral trade flows by product
- **OECD ICIO**: Inter-country input-output tables
- **World Bank**: Transport costs, infrastructure quality
- **WTO**: Tariff schedules, trade agreements
- **CEPII GeoDist**: Distances, geographic data

### Validation targets:
- **Replicate historical trade patterns**: R² > 0.7 vs actual data
- **Accurate tariff effects**: 10% tariff → ~20-30% trade reduction
- **Distance effects**: Doubling distance → ~40% trade reduction
- **Triangulation detection**: Catch known evasion cases from historical record

## Technical Notes

For implementation teams:

### Computational approach:
- **Sparse matrices**: Most country-pairs don't trade most products
- **Iterative solvers**: Gauss-Seidel or RAS algorithm for balancing
- **Parallelizable**: Trade flow calculations can run independently by product
- **Convergence threshold**: Balance to within 0.1% of total trade

### Performance considerations:
- Pre-compute common shipping routes
- Index active trade relationships only
- Use historical flows as initial guess for iterations
- Cache transport cost calculations

### Extensibility:
- Plug in different transport cost models
- Customize detection algorithms
- Add new trade restrictions types
- Incorporate real-time data feeds (for live gaming)

## Connection to UTA Enforcement System

This module feeds the broader UTA compliance architecture:

### Detection outputs become:
- **Investigations**: UTA opens cases on flagged countries
- **Evidence**: Trade data presented in dispute resolution
- **Penalties**: Credits deducted, sanctions imposed
- **Rewards**: Compliant countries gain trade credits

### Enforcement feedback loop:
1. Module detects triangulation attempt
2. UTA investigates (may take multiple turns)
3. If proven, penalties applied
4. Country's reputation damaged (higher scrutiny on future trades)
5. Other players observe and adjust strategies

This creates a **dynamic enforcement environment** where players must assess:
- Probability of detection
- Severity of penalties
- Expected profit from cheating
- Reputational costs
- Alternative legitimate strategies

## Future Enhancements

Potential expansions as simulation matures:

### Advanced logistics:
- **Container shipping networks**: Specific port-to-port routes
- **Just-in-time supply chains**: Inventory costs and timing
- **Logistics disruptions**: Natural disasters, labor strikes, piracy

### Financial integration:
- **Currency effects**: Exchange rates affect trade competitiveness
- **Trade credit**: Payment terms and financing costs
- **Hedging**: Forward contracts, currency swaps

### Environmental dimension:
- **Carbon costs**: Emissions from transport
- **Green premiums**: Willingness to pay for sustainable shipping
- **Regulation**: Emissions caps on shipping

### Advanced circumvention:
- **Shell companies**: Complex ownership structures
- **Cryptocurrency**: Untraceable payments
- **Dark vessels**: Ships that go "dark" (AIS off)
- **Document fraud**: Sophisticated fake certificates of origin

---

## Bottom Line

The Trade Flow Module is the **logistical backbone** of the UTA simulation. It ensures:
- Goods move realistically between countries
- Costs are calculated properly based on distance, mode, and infrastructure
- Policies have measurable effects on trade patterns
- Cheaters can be caught (but might succeed if clever)
- The global economy balances correctly

It transforms abstract economic models into **concrete shipping decisions**, and makes trade policy feel tangible - you see routes change, costs shift, and smugglers get caught (or get away with it).

This is where **economic theory meets shipping routes meets detective work**.
