# Energy & Logistics: The Physical Foundation of Global Trade

## What This System Does

Think of Energy & Logistics as the "physics engine" of the UTA simulation. While other modules track what countries want to buy and sell, this system determines **whether they actually can** - and at what cost.

Every ship needs fuel. Every pipeline has a maximum capacity. Every trade route passes through chokepoints that can be blocked. This module tracks all of it, turning abstract trade flows into real-world logistics challenges that shape your strategic options.

**Bottom line**: Geography isn't just background scenery in UTA - it's a strategic asset and a potential vulnerability.

---

## Why This Matters to Your Strategy

### The Three Strategic Levers

1. **Energy Prices Control Your Costs**: When oil spikes 50%, your shipping costs jump by 25%. Energy-intensive industries see production costs surge. Countries dependent on imported energy face inflation shocks.

2. **Chokepoints Are Strategic Weapons**: The Strait of Hormuz carries 21% of global oil trade. Block it, and you've just weaponized geography. Own it, and you have leverage over every country whose energy imports pass through.

3. **Infrastructure Determines Who Wins Trade Wars**: Countries with diversified shipping routes, strategic energy reserves, and efficient ports can weather disruptions. Those dependent on a single supplier or route are vulnerable to economic coercion.

---

## The Energy System: How Fuel Prices Shape Global Trade

### Energy as a Dual Asset

Energy functions in two critical ways:

**As a Tradable Commodity**: Oil, natural gas, and coal are products you buy and sell like any other - but with outsized geopolitical importance.

**As a Production Input**: Energy powers factories, ships goods, and heats homes. Changes in energy prices cascade through your entire economy.

### How Energy Pricing Works in the Game

The system tracks three major energy markets:

**Oil (Global Market)**:
- One global price with regional variations (Brent crude in Europe, WTI in North America, Dubai in Asia)
- Price responds to supply/demand imbalances: every 1% gap between supply and demand moves prices by roughly 3%
- Strategic reserves act as shock absorbers - countries with 90+ days of reserves can ride out short-term disruptions

**Natural Gas (Regional Markets)**:
- Three distinct markets: North America, Europe, and Asia
- Limited arbitrage opportunities because gas is hard to move without pipelines or LNG infrastructure
- LNG capacity determines how much prices can converge - without it, a gas shortage in Europe doesn't automatically raise prices in Texas

**Electricity (National Grids)**:
- Priced at the national or regional level
- Cross-border interconnections allow limited trade
- Renewable capacity affects long-term price stability

### Strategic Implications for Players

**If you're an energy exporter**: You have geopolitical leverage. Threaten to cut supplies, and importing countries face potential economic crisis.

**If you're an energy importer**: Diversify your suppliers. A country that sources 80% of its gas from one supplier is strategically vulnerable - one diplomatic breakdown could leave factories idle.

**For everyone**: Watch inventory levels. When global oil inventories drop below 30 days of demand, prices become volatile. Building strategic reserves costs money upfront but provides insurance against supply shocks.

---

## The Transportation System: How Goods Actually Move

### Five Transport Modes, Each with Trade-offs

The game automatically selects the optimal shipping method based on cost, time, and cargo characteristics. Understanding these trade-offs helps you anticipate how disruptions will affect your economy.

**Maritime Shipping (Sea Freight)**:
- **Best for**: Bulk goods, manufactured products, anything heavy and non-perishable
- **Cost**: $30-50 per ton for commodities, $1,000-2,000 per container
- **Speed**: 20-40 days for intercontinental routes
- **Key risk**: Vulnerable to chokepoint blockades, piracy, fuel price spikes
- **Fuel dependency**: 50% of shipping cost is fuel - when oil doubles, shipping costs jump 50%

**Rail Networks**:
- **Best for**: Continental trade, bulk commodities (coal, grain, minerals)
- **Cost**: ~$0.03 per ton-kilometer (cheaper than road for long distances)
- **Speed**: 3-7 days for cross-continental routes
- **Key risk**: Limited to countries with rail connections - mostly Eurasia and North America

**Road Transport**:
- **Best for**: Regional distribution, last-mile delivery, border trade
- **Cost**: ~$0.12 per ton-kilometer (4x more expensive than rail)
- **Speed**: Flexible and fast for short distances
- **Key risk**: Fuel-intensive, border delays add costs

**Pipelines**:
- **Best for**: Oil, natural gas, chemicals
- **Cost**: ~$0.01 per ton-kilometer (cheapest for bulk liquids/gases)
- **Speed**: Continuous flow
- **Key risk**: Fixed routes, vulnerable to sabotage, massive upfront investment

**Air Cargo**:
- **Best for**: High-value electronics, perishables, time-sensitive goods
- **Cost**: ~$1.80 per ton-kilometer (60x more expensive than rail)
- **Speed**: 1-3 days globally
- **Key risk**: Fuel-intensive, only economic for valuable cargo

### How the System Chooses Routes

For every trade flow, the system calculates:
- **Direct transport cost** (fuel, labor, tolls)
- **Time value of goods in transit** (capital tied up = opportunity cost)
- **Risk premium** (insurance for piracy, conflict zones, sanction exposure)

**Example**: Shipping $1 million of electronics from China to Germany
- **Sea route via Suez**: $2,000 transport + $800 time cost (30 days × $1M × 0.01% daily) = $2,800 total
- **Rail route via Kazakhstan**: $5,000 transport + $200 time cost (7 days) = $5,200 total
- **Air freight**: $45,000 transport + $30 time cost (1 day) = $45,030 total

→ The system picks sea freight (lowest total cost). But if the Suez Canal closes, rail suddenly becomes optimal.

---

## Critical Chokepoints: The Strategic Battlegrounds

### What Makes a Chokepoint Strategic

A chokepoint is any narrow passage that concentrates trade flows. Control one, and you can:
- Levy tolls (economic leverage)
- Threaten closure (geopolitical leverage)
- Monitor flows (intelligence advantage)
- Deny access to adversaries (strategic weapon)

### The Big Five Maritime Chokepoints

**Strait of Hormuz** (Persian Gulf):
- **Throughput**: 21 million barrels/day of oil (21% of global supply)
- **Alternative routes**: Very limited - rerouting requires pipelines that don't exist
- **Controlled by**: Iran (north shore), Oman/UAE (south shore)
- **If blocked**: Oil prices spike 50-100% within days, Asia and Europe face energy crisis

**Suez Canal** (Egypt):
- **Throughput**: 12% of global trade, 10% of seaborne oil
- **Alternative route**: Around Africa's Cape of Good Hope (adds 3,500 miles, +15 days, costs 1.8x more)
- **Controlled by**: Egypt (levies $700,000 per transit)
- **If blocked**: Europe-Asia trade costs surge, delivery times double

**Strait of Malacca** (between Malaysia and Indonesia):
- **Throughput**: 25% of traded goods, 40% of Asian oil imports
- **Alternative route**: Sunda Strait (adds 3 days, limited capacity)
- **If blocked**: Japan, Korea, China face immediate supply disruptions

**Panama Canal** (Central America):
- **Throughput**: 6% of global trade, crucial for US East-West coast trade
- **Alternative route**: Around South America's Cape Horn (adds 8,000 miles)
- **Controlled by**: Panama (levies $450,000 per transit)

**Bab el-Mandeb Strait** (Red Sea entrance):
- **Throughput**: Connects Suez Canal to Indian Ocean (4.8 million barrels/day of oil)
- **Alternative route**: Around Africa
- **Recent relevance**: Houthi attacks demonstrated vulnerability

### How the Game Calculates Chokepoint Risk

For each country, the system tracks:

**Exposure Value**: Total annual trade value passing through the chokepoint
**Exposure Share**: What percentage of your trade depends on this route
**Alternative Feasibility**: Can your trade flows reroute if the chokepoint closes?

**Example - Germany's Suez Exposure**:
- €120 billion/year in trade passes through Suez
- 18% of Germany's total trade (high exposure)
- Alternative via Cape of Good Hope adds €15 billion in annual costs (feasible but expensive)
- **Vulnerability score**: High exposure × expensive alternatives = 0.72 (scale 0-1)

**Example - Japan's Malacca Exposure**:
- ¥40 trillion/year in trade passes through Malacca
- 35% of Japan's total trade (very high exposure)
- Alternative via Sunda Strait has limited capacity (not all flows can reroute)
- **Vulnerability score**: 0.89 (Japan is highly vulnerable)

### Strategic Implications

**If you control a chokepoint**:
- You can levy tolls (Egypt earns $6 billion/year from Suez)
- You can threaten closure to extract concessions
- You can deny access to sanctioned countries
- You become a high-value target

**If you're vulnerable to a chokepoint**:
- Diversify trade routes (develop alternative suppliers/markets)
- Build strategic reserves (stockpile 90+ days of critical inputs)
- Invest in alternative infrastructure (new pipelines, rail networks)
- Secure military or diplomatic protection for critical passages

---

## Energy Security: Measuring Your Vulnerability

### The Four Dimensions of Energy Security

The system calculates an Energy Security Score (0-100) for each country based on:

**1. Import Dependency** (30% weight):
- What percentage of your energy comes from imports?
- **Example**: Germany imports 70% of oil, 95% of gas → high vulnerability

**2. Supplier Concentration** (30% weight):
- Are your imports diversified or concentrated?
- Measured using the Herfindahl-Hirschman Index (HHI)
- **Example**: Pre-2022, Germany sourced 55% of gas from Russia → HHI of 0.40 (highly concentrated)

**3. Reserve Adequacy** (20% weight):
- How many days of consumption can your strategic reserves cover?
- **Target**: IEA standard is 90 days for oil, 30 days for gas
- **Example**: Japan maintains 180+ days of oil reserves (world-leading)

**4. Supplier Geopolitical Risk** (20% weight):
- Are your suppliers stable and friendly?
- **Example**: Importing from Norway (stable) vs Venezuela (unstable) vs Iran (hostile)

### Real-World Examples

**Strong Energy Security (Score: 85/100)**:
- Country: Norway or Canada
- 100% energy self-sufficient (exporters)
- Diversified export markets
- Low geopolitical risk

**Moderate Energy Security (Score: 55/100)**:
- Country: Japan
- 90% import-dependent BUT diversified suppliers (Australia, Middle East, SE Asia)
- Massive strategic reserves (180 days)
- Pays premium for diversification

**Weak Energy Security (Score: 25/100)**:
- Country: Germany (pre-2022)
- 70% import-dependent
- 55% of gas from single supplier (Russia)
- Inadequate reserves (30 days gas storage)
- **Consequence**: Russia threatened cutoffs → Germany faced deindustrialization risk

### How to Improve Your Energy Security

**Short-term actions** (effective within 1-2 turns):
- Fill strategic reserves (expensive but immediate protection)
- Sign long-term supply contracts with new suppliers
- Reduce consumption via rationing or industrial slowdowns

**Medium-term actions** (3-5 turns):
- Build LNG import terminals (enables supplier diversification)
- Develop alternative transport routes (pipelines from new suppliers)
- Accelerate renewable energy deployment

**Long-term actions** (5+ turns):
- Develop domestic energy production
- Build interconnected regional grids
- Invest in energy efficiency across all sectors

---

## Infrastructure Capacity: When Systems Max Out

### Bottlenecks Create Strategic Opportunities

Every port, pipeline, and rail line has a maximum throughput capacity. When demand exceeds capacity, two things happen:

1. **Congestion costs rise**: Ships wait in harbor queues, pipelines run at maximum pressure, rail yards back up
2. **Strategic value spikes**: Control over bottleneck infrastructure becomes a negotiating chip

### How the System Tracks Capacity Stress

**Infrastructure Utilization Score** (0-100%):
- **Below 70%**: Normal operations, minimal delays
- **70-85%**: Mild congestion, costs rise 10-20%
- **85-95%**: Severe congestion, costs rise 30-50%, delays frequent
- **Above 95%**: Critical bottleneck, some flows can't be accommodated

**Example - Rotterdam Port**:
- Normal capacity: 14 million TEU (twenty-foot equivalent containers) per year
- Current throughput: 13.2 million TEU
- **Utilization**: 94% (approaching critical)
- **Impact**: Container ships queue 3-5 days to unload, adding €2,000 per container in costs

### Strategic Implications

**When you control congested infrastructure**:
- You can ration access (favor allies, penalize adversaries)
- You can levy premium fees (users have no alternative)
- You become a critical node in supply chains

**When your trade depends on congested infrastructure**:
- Costs rise unpredictably
- Supply reliability falls
- **Solution**: Invest in capacity expansion OR develop alternative routes

**Investment opportunities**:
- Ports, pipelines, and rail networks with utilization above 85% are strong investment targets
- Expansion projects reduce your vulnerability and can generate revenue from other users

---

## How This Affects Your Gameplay

### Energy Price Shocks: Ripple Effects Across Your Economy

**Scenario**: OPEC cuts production by 2 million barrels/day

**Immediate effects** (Turn 1):
- Global oil price rises from $80 to $105/barrel (+31%)
- Your shipping costs increase by 15% (fuel is 50% of sea freight cost)
- Energy-intensive industries (chemicals, steel, cement) see production costs rise 8-12%

**Secondary effects** (Turns 2-3):
- Higher transport costs push up consumer prices (inflation +1.5%)
- Airlines and logistics companies raise rates
- Demand for your exports falls as they become more expensive

**Strategic responses**:
- **If you're an oil exporter**: You benefit from higher prices - boost production to maximize revenue
- **If you're an oil importer**:
  - Draw down strategic reserves to stabilize domestic prices (short-term relief)
  - Negotiate new supply deals (long-term diversification)
  - Consider fuel subsidies to protect politically sensitive sectors (expensive but avoids unrest)

### Chokepoint Blockades: When Trade Routes Vanish

**Scenario**: Strait of Hormuz closed due to military conflict

**Immediate impact**:
- 21% of global oil supply instantly offline
- Oil prices spike from $80 to $140/barrel within 48 hours
- Asian economies (Japan, Korea, China, India) face immediate shortages

**Countries most affected**:
- **Japan**: 80% of oil imports pass through Hormuz → immediate energy crisis
- **China**: 40% of oil imports affected → rationing required
- **India**: 60% affected → economic slowdown

**Alternative routes**:
- Middle East oil must reroute via pipelines to Red Sea ports (limited capacity)
- Some flows diverted to Mediterranean via Suez (costly, slow)
- Global LNG markets mobilize to partially offset (inadequate capacity)

**Your strategic options**:

**If you're a major oil importer**:
- Deploy naval forces to reopen Hormuz (expensive, risky, only works if you have power projection capability)
- Tap strategic reserves (buys 90 days if reserves are full)
- Negotiate emergency deals with alternative suppliers (Africa, Americas)
- Implement rationing to stretch supplies
- Consider diplomatic intervention to end conflict

**If you're an oil exporter outside Middle East**:
- Windfall opportunity - you can sell at $140/barrel vs normal $80
- Ramp up production to maximum capacity
- Sign premium contracts with desperate buyers

**If you control alternative routes**:
- Red Sea ports, East African pipelines, and trans-Arabian pipelines surge in value
- You can levy tolls or demand political concessions for access

### Infrastructure Investments: Building Strategic Resilience

**Scenario**: You're Germany, dependent on Russian gas via Nord Stream pipeline

**Vulnerability analysis**:
- 55% of gas imports from Russia (concentrated supplier risk)
- Only 30 days of gas storage (inadequate reserves)
- Limited alternative import infrastructure (no LNG terminals)
- **Energy Security Score**: 25/100 (critically vulnerable)

**Investment options**:

**Option 1: Build LNG Import Terminals**
- Cost: $2 billion per terminal, 3 turns to construct
- Benefit: Enables imports from global LNG markets (US, Qatar, Australia)
- **Impact on security score**: +20 points (diversification)

**Option 2: Expand Gas Storage**
- Cost: $500 million, 2 turns to construct
- Benefit: Increases reserves from 30 to 90 days
- **Impact on security score**: +10 points (buffer capacity)

**Option 3: Build Pipeline to Norway**
- Cost: $3 billion, 4 turns to construct
- Benefit: Secure supply from reliable ally
- **Impact on security score**: +15 points (friendly supplier)

**Optimal strategy**: Combination approach
- Turn 1: Begin LNG terminal construction (fast diversification)
- Turn 2: Expand storage (immediate shock absorption)
- Turn 3: Negotiate with Norway on pipeline (long-term security)
- **Total cost**: $6 billion over 4 turns
- **Final security score**: 70/100 (secure against most threats)

---

## Advanced Strategic Concepts

### Energy as Geopolitical Leverage

**How it works**: Countries with surplus energy production can weaponize exports by threatening cutoffs.

**Historical example**: Russia-Europe gas relationship
- Russia supplied 40% of Europe's gas pre-2022
- Periodically threatened cutoffs to influence European policy
- Europe ultimately paid premium prices to diversify away from Russian supply

**In-game mechanics**:
- If you supply >30% of another country's energy imports, you gain diplomatic leverage
- You can threaten supply cutoffs (forces target to concede or face economic crisis)
- Target can retaliate with sanctions, military action, or by developing alternatives
- **Warning**: Weaponizing energy damages long-term customer relationships (buyers will diversify away)

### Logistics Arbitrage: Exploiting Route Inefficiencies

**The opportunity**: When global events disrupt standard routes, savvy players can profit from alternative routing.

**Example scenario**: Suez Canal blockage (as happened in 2021 with Ever Given)

**Standard route** (China → Europe):
- Via Suez: 20 days, $2,000 per container

**During blockage**:
- Via Cape of Good Hope: 35 days, $3,600 per container
- Via Trans-Siberian Rail: 14 days, $5,000 per container
- Time-sensitive goods pay premium for rail route

**Arbitrage opportunity**:
- If you control Trans-Siberian rail capacity, you can charge premium rates
- If you operate shipping lines, you can reroute via Cape and charge surge pricing
- If you're a Middle Eastern transshipment hub, you become more valuable

**Strategic insight**: Disruptions create profit opportunities for countries with alternative infrastructure.

### Shadow Fleet Detection: When Unusual Routes Signal Cheating

The system tracks "expected" vs "actual" routing for every trade flow.

**Normal routing** (Saudi oil → China):
- Expected: Strait of Hormuz → Malacca Strait → Shanghai (7,500 miles, 18 days)

**Suspicious routing** (Iranian oil → China, evading sanctions):
- Actual: Oman coast → ship-to-ship transfer → indirect route via Indonesia → Shanghai (9,200 miles, 24 days)
- **Red flags**: 23% longer distance, 33% longer time, 18% higher cost, passes through unusual transshipment points

**How detection works**:
- System compares actual route cost vs optimal route cost
- Routes that are >15% more expensive than optimal trigger investigation
- Additional red flags: ship transponders turned off, ship-to-ship transfers, circuitous paths

**For sanctions enforcers**: This data feeds the Compliance Module to detect sanctions evasion
**For sanctions evaders**: You can attempt circuitous routing, but it's expensive and may be detected

---

## Integration with Other Game Systems

### How Energy & Logistics Connects to Your Other Decisions

**Pricing & Market Equilibrium**:
- Energy costs flow into production costs for all sectors
- Transport costs determine delivered prices (same product, different prices in different markets)
- When energy spikes, inflation cascades through your economy

**Trade Flows**:
- Transport costs determine which trade flows are profitable
- Chokepoint closures eliminate certain routes, potentially killing trade relationships
- Infrastructure capacity limits how much you can export/import

**Sanctions & Geopolitics**:
- Energy embargoes are enforced through this system
- Blocking chokepoints is a military action with economic consequences
- Infrastructure sabotage (pipeline explosions, port attacks) causes supply disruptions

**Subsidy & Industrial Policy**:
- Fuel subsidies reduce energy costs for domestic industries (competitive advantage)
- Infrastructure investment builds strategic resilience
- Strategic reserves are expensive but provide insurance

**Agent Intelligence (AI opponents)**:
- AI countries monitor their Energy Security Scores and invest to reduce vulnerability
- AI exporters will exploit energy leverage when they have it
- AI importers will diversify suppliers if dependency becomes too concentrated

---

## Quick Reference: Key Metrics to Monitor

### Energy Dashboard (check every turn)

**Your Energy Security Score** (0-100):
- Below 40: Critically vulnerable (priority investments needed)
- 40-60: Moderate risk (diversification recommended)
- 60-80: Good position (maintain current policies)
- Above 80: Secure (can focus elsewhere)

**Oil Price** ($/barrel):
- $60-80: Normal range
- $80-100: Elevated (moderate inflation pressure)
- $100-130: Crisis pricing (significant economic impact)
- Above $130: Severe crisis (recession risk for oil importers)

**Strategic Reserves** (days of consumption):
- Below 30 days: Insufficient (vulnerable to short-term shocks)
- 30-60 days: Adequate for minor disruptions
- 60-90 days: IEA standard (can weather most shocks)
- Above 90 days: Excellent buffer

### Logistics Dashboard

**Critical Chokepoint Status**:
- Green: Open and functioning normally
- Yellow: Tensions or congestion (monitor closely)
- Red: Closed or severely restricted (immediate crisis)

**Your Chokepoint Exposure** (% of trade through each):
- Below 15%: Low exposure
- 15-25%: Moderate exposure (have backup plans)
- 25-40%: High exposure (major vulnerability)
- Above 40%: Critical dependency (urgent diversification needed)

**Infrastructure Capacity Stress** (% utilization):
- Below 70%: Healthy capacity
- 70-85%: Monitor for congestion
- 85-95%: Investment opportunity or vulnerability
- Above 95%: Critical bottleneck (constrains trade)

### Strategic Alerts (the system will notify you when these occur)

**Energy Security**: Your security score drops below 50
**Chokepoint Risk**: A chokepoint you depend on shows elevated blockade probability
**Infrastructure Bottleneck**: A facility you use hits >90% utilization
**Price Shock**: Energy prices move >20% in a single turn
**Unusual Routing**: Your trade partners are using suspicious routes (potential sanctions evasion)

---

## Gameplay Tips: Making Energy & Logistics Work for You

### For Energy Exporters

**Maximize leverage without losing customers**:
- Use supply threats sparingly (buyers will diversify if you overplay your hand)
- Lock customers into long-term contracts before threatening cutoffs
- Invest in transport infrastructure to your key markets (makes them more dependent)

**When energy prices spike**:
- Ramp up production to maximize revenue
- Resist cartel pressure to cut supply (grab market share while prices are high)
- Use windfall revenues to invest in diversification (don't rely on energy forever)

### For Energy Importers

**Diversification is expensive but essential**:
- Don't wait for crisis - build LNG terminals and diversify suppliers before you need them
- Strategic reserves are insurance - expensive upfront, invaluable during disruptions
- Pay premium for friendly suppliers vs discount for risky ones (security > savings)

**When facing energy coercion**:
- Tap reserves immediately (buys negotiating time)
- Implement rationing for non-essential uses (extends supplies)
- Rally allies to provide emergency shipments
- Consider military or diplomatic action to secure supplies

### For Chokepoint Controllers

**You're sitting on strategic gold**:
- Levy reasonable tolls (generate revenue without triggering alternatives)
- Offer preferential access to allies (build coalitions)
- Threaten closure as diplomatic lever (but rarely execute - you lose revenue too)

**Expect to become a target**:
- High-value chokepoints attract military action
- Invest in defense or secure guarantees from powerful allies
- Diversify your economy (don't depend entirely on toll revenue)

### For Logistics-Dependent Traders

**Infrastructure quality matters**:
- Countries with efficient ports and low congestion have competitive advantage
- Invest in infrastructure to reduce costs (20% cost reduction = 5% boost to export competitiveness)

**When routes close**:
- Have alternative routes mapped out before crisis hits
- Build relationships with alternative transport providers
- Consider building redundant infrastructure (expensive but reduces single points of failure)

### Universal Principles

**Geography is destiny - but you can reshape it**:
- Natural chokepoints and resource locations are fixed
- Infrastructure investments change your strategic position over time
- Diversification costs money but reduces vulnerability

**Energy security is like insurance**:
- Costs money when you don't need it
- Priceless when crisis hits
- Cheaper to build before you need it than during crisis

**Watch the numbers, not the headlines**:
- Your Energy Security Score tells you if you're vulnerable (below 50 = high risk)
- Chokepoint exposure above 25% of trade = strategic vulnerability
- Infrastructure utilization above 85% = bottleneck forming

---

## Example: A Complete Turn Through the Energy & Logistics System

Let's walk through how all these systems interact in a realistic scenario.

**Starting Situation**: You're playing as Japan

**Your Energy Profile**:
- 90% energy import-dependent (oil, gas, coal)
- Major suppliers: Middle East (65%), Australia (20%), SE Asia (15%)
- 180 days of oil reserves (excellent), 45 days of gas reserves (adequate)
- Energy Security Score: 58/100 (moderate vulnerability due to high import dependency, but strong on diversification and reserves)

**Turn 1 Events**:
- OPEC announces 2 million barrel/day production cut
- Tensions rise in Persian Gulf (Hormuz blockade probability increases from 5% to 25%)

**System calculations**:

**Energy pricing**:
- Oil price rises from $75 to $92/barrel (+23%)
- Asian gas prices rise in parallel (oil-linked contracts) from $10 to $11.50/mmBtu (+15%)

**Your costs**:
- Shipping costs increase 11% (fuel is 50% of cost, fuel up 23%, so 0.5 × 23% = 11.5%)
- Electricity costs increase 8% (gas-fired plants raise costs)
- Industrial production costs rise 3-5% depending on sector

**Your chokepoint exposure analysis**:
- Hormuz exposure: ¥28 trillion/year trade (35% of total) passes through Hormuz
- If Hormuz closes: Alternative via Cape of Good Hope adds ¥4.5 trillion/year in costs
- Vulnerability score increases from 0.64 to 0.78 (high)

**Alerts you receive**:
- "Energy Security Warning: Hormuz blockade risk elevated to 25%"
- "Cost Impact: Shipping costs up 11%, electricity costs up 8%"
- "Strategic Recommendation: Consider drawing strategic reserves if situation escalates"

**Your decisions this turn**:

**Option A: Wait and See**
- Cost: $0
- Risk: If Hormuz closes next turn, you face immediate crisis
- Benefit: Save money if crisis doesn't materialize

**Option B: Activate Strategic Reserves**
- Cost: $2 billion (premium to release reserves)
- Benefit: Stabilize domestic fuel prices, signal to markets that you're prepared
- Drawback: Depletes buffer (reserves drop from 180 to 150 days)

**Option C: Emergency Diversification**
- Cost: $8 billion (accelerate LNG terminal construction, sign emergency supply contracts with US/Qatar)
- Benefit: Reduce Hormuz exposure from 35% to 25% within 2 turns
- Long-term: Improves Energy Security Score to 68/100

**Option D: Diplomatic/Military Action**
- Cost: $5 billion (deploy naval forces to protect Hormuz)
- Benefit: Reduce blockade probability from 25% back to 5%
- Risk: Escalates tensions with Iran, requires allied support

**Your choice**: Option C + Option D (invest $13 billion)
- Emergency diversification protects long-term
- Naval deployment protects short-term
- Total cost is 0.3% of GDP (manageable)

**Turn 2 outcome**:
- Hormuz tensions de-escalate (naval presence deterred Iran)
- Your diversification projects begin (2 turns to completion)
- Oil prices stabilize at $88/barrel (crisis premium fades)
- Your Energy Security Score improves to 62/100 (projected 68/100 when projects complete)

**Lesson**: Proactive investments in energy security paid off. Countries that waited faced crisis when Hormuz tensions spiked again in Turn 4.

---

## Closing Thought: Think Like a CFO, Act Like a Strategist

Energy and logistics aren't exciting - until they fail. Then they're the only thing that matters.

**The CFO mindset**: Track your vulnerabilities, quantify your risks, invest in resilience before crisis hits.

**The strategist mindset**: Geography creates opportunities and constraints. Infrastructure is power. Diversification is insurance.

Countries that master Energy & Logistics can weather any crisis. Countries that ignore it become hostages to geography.

**Your goal**: Keep your Energy Security Score above 60, your chokepoint exposure below 25%, and your strategic reserves above 60 days. Do that, and you'll have the freedom to focus on winning the game - not surviving the next supply shock.
