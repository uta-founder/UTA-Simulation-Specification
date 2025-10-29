# Country Turn - Complete Player Action Space (V2)

## Document Purpose

This is the **comprehensive reference** for everything a player can do each turn in the UTA Simulation. If an action isn't listed here, it's either not implemented or requires new game mechanics.

This document consolidates ALL player-facing options from:
- Trade Flow Module
- Sanctions & Geopolitics Module
- Subsidy & Industrial Policy Module
- Currency Strategy Module
- Energy & Logistics Module
- Compliance & Cheating Detection Module
- Military Module
- Agent Intelligence Module
- Firm-vs-State Module
- Geopolitical Module

---

## Quick Reference: Action Categories

**Economic Tools**
- [Trade Policy](#trade-policy-actions) (tariffs, quotas, agreements)
- [Industrial Policy](#industrial-policy-actions) (subsidies, procurement, R&D)
- [Currency & Finance](#currency--financial-actions) (exchange rates, reserves, capital controls)

**Strategic Tools**
- [Sanctions & Embargos](#sanctions--embargo-actions) (unilateral, coalition, secondary)
- [Alliances & Coalitions](#alliance--coalition-actions) (formation, coordination, burden-sharing)
- [Military & Coercive](#military--coercive-actions) (blockades, cyber, deterrence)

**Infrastructure & Resources**
- [Energy & Logistics](#energy--logistics-actions) (reserves, capacity, chokepoints)
- [Resource Strategy](#resource-strategy-actions) (stockpiling, cartels, monopolization)

**Institutional & Normative**
- [UTA System](#uta-system-actions) (credits, disputes, membership)
- [Standards & Regulations](#standards--regulation-actions) (rule-setting, certification)

**Gray Zone & Cheating**
- [Compliance Strategies](#compliance--cheating-actions) (detection avoidance, triangulation)
- [Information Warfare](#information-warfare-actions) (deception, propaganda, intelligence)

**Firm-Level Control**
- [State-Owned Enterprises](#state-enterprise-control-actions) (SOE mandates, pricing directives)
- [Enforcement Calibration](#enforcement--monitoring-actions) (audit intensity, penalties)

---

## Trade Policy Actions

### Tariff Management

**Adjust Tariff Rates**
- **What**: Change ad valorem, specific, or compound tariffs on imports from specific countries/sectors
- **Range**: 0% to 100% (above 50% triggers retaliation risk)
- **Effect**: Domestic prices increase, imports decrease, potential retaliation
- **Example**: "Impose 25% tariff on Chinese steel"

**Preferential Tariff Schedules**
- **What**: Offer reduced tariffs to trade agreement partners
- **Effect**: Trade creation (more imports from partners), trade diversion (less from non-partners)
- **Integration**: Requires trade agreement (see Alliance Actions)

**Retaliatory Tariffs**
- **What**: Automatic or manual counter-tariffs when partner raises barriers
- **Options**: Tit-for-tat (match rate), escalatory (2x partner rate), targeted (high-value sectors)
- **Strategic**: Signals credibility, deters further escalation

### Quotas & Volume Controls

**Import Quotas**
- **What**: Limit total volume of specific products from specific origins
- **Effect**: Price increases, scarcity, domestic producer protection
- **Example**: "Limit Japanese auto imports to 500,000 units/year"

**Export Quotas**
- **What**: Limit your own exports to maintain domestic supply or leverage
- **Use Case**: Resource exporters during shortages, industrial policy (keep inputs domestic)
- **Example**: "Limit rare earth exports to force downstream processing domestically"

**Tariff-Rate Quotas (TRQs)**
- **What**: Low tariff up to quota volume, high tariff above
- **Effect**: Balances market access with protection
- **Example**: "First 100,000 tons sugar at 5%, then 50% tariff"

### Trade Agreements & Market Access

**Negotiate Bilateral Trade Agreement**
- **Duration**: 2-4 turns to negotiate
- **Content**: Tariff reductions, quotas, standards harmonization, dispute resolution
- **Effect**: Trade volume increases 15-40% with partner

**Form Preferential Trade Bloc**
- **Requirements**: 3+ countries, shared interests
- **Effect**: Internal tariffs drop to 0-5%, external tariffs coordinate
- **Examples**: Form "Pacific Trade Alliance", "Eurasian Economic Union"

**Withdraw from Trade Agreement**
- **Effect**: Tariffs revert to MFN rates, reputation damage
- **Timing**: Takes 1-2 turns (exit clauses)

### Non-Tariff Barriers

**Technical Standards & Certification**
- **What**: Impose domestic standards that imports must meet
- **Effect**: Raises compliance costs, delays market entry
- **Detection**: Low (legitimate if based on safety/quality)
- **Example**: "Electronics must meet domestic EMF standards" (blocks imports)

**Inspection & Licensing Requirements**
- **What**: Require import licenses, inspection protocols
- **Effect**: Creates delays, administrative burden
- **Example**: "Agricultural imports require 30-day phytosanitary inspection"

**Rules of Origin Enforcement**
- **What**: Strict verification of product origin to prevent transshipment
- **Effect**: Blocks triangulation attempts, administrative burden
- **Intensity**: Low (10% inspection) to High (100% verification)

---

## Industrial Policy Actions

### Production Subsidies

**Direct Production Subsidies**
- **Types**: Per-unit ($/ton) or percentage (% of costs)
- **Range**: 5% (subtle) to 50% (massive intervention)
- **Effect**: Production increases, prices fall, global competitiveness rises
- **Detection**: 40-70% probability depending on size and concealment
- **Penalty**: -150 UTA credits if challenged, countervailing duties

**Subsidy by Sector**
- **Target**: Choose sector (steel, semiconductors, agriculture, etc.)
- **Pass-Through**: 60-90% flows to consumers as lower prices, rest to producer profits
- **Duration**: Specify temporary (3-5 turns) or permanent

**Hidden Subsidies**
- **Methods**: Below-market loans, cheap land, free inputs, SOE purchases at premium prices
- **Detection**: 20-40% probability (harder to prove)
- **Risk**: Higher UTA penalty (-250 credits) if discovered due to deception

### Export Promotion

**Export Subsidies**
- **What**: Pay exporters per unit sold abroad
- **Effect**: Boosts competitiveness, but internationally banned (WTO rules)
- **Detection**: 70% probability (trade data makes it obvious)
- **Penalty**: -250 credits, mandatory removal

**Export Credit Programs**
- **What**: Subsidized financing for foreign buyers of your exports
- **Effect**: Makes your products more attractive (affordable financing)
- **Legality**: Allowed within OECD limits
- **Example**: "2% interest loans for buyers of domestic aircraft"

**Export Processing Zones**
- **What**: Special zones with tax exemptions, no duties on imported inputs
- **Effect**: Attracts export-oriented investment
- **Abuse Risk**: Can be used for triangulation (import → minimal processing → export)

### R&D and Innovation Support

**R&D Subsidies**
- **What**: Fund research programs for specific technologies
- **Cost**: 0.5% to 3% of GDP
- **Effect**: Productivity gains arrive after 3-5 turn lag
- **Example**: "Invest $500M in AI research" → +10% productivity in tech sector in 5 turns

**Technology Acquisition Programs**
- **Legitimate**: License foreign technology, joint ventures, attract foreign R&D
- **Gray Zone**: Mandate technology transfer as condition for market access
- **Illegal**: Industrial espionage, IP theft (25% detection risk, -500 credits)

**Patent & IP Protection Adjustment**
- **Strong Protection**: Attracts foreign investment, higher technology costs
- **Weak Protection**: Enables domestic copying, deters foreign firms
- **Strategic**: Can shift between strong/weak depending on development stage

### Capital Support

**Investment Tax Credits**
- **What**: Tax deductions for firms that invest in new capacity
- **Effect**: Capacity expansion accelerates, production increases with lag
- **Example**: "25% tax credit for new semiconductor fabs" → capacity +30% in 3-4 turns

**Accelerated Depreciation**
- **What**: Allow firms to deduct capital costs faster
- **Effect**: Reduces effective capital costs by 10-20%
- **Detection**: Low (legitimate tax policy)

**State Development Banks**
- **What**: Provide below-market loans for strategic sectors
- **Effect**: Reduces financing costs, enables expansion
- **Detection**: 30% (hard to prove subsidy vs commercial lending)

### Strategic Procurement

**Government Procurement Mandates**
- **What**: Government purchases domestic at premium prices (5-20% above market)
- **Effect**: Guaranteed demand supports domestic industry
- **Example**: "Military purchases 100% domestic steel even if 15% more expensive"

**Buy National Policies**
- **What**: Formal preference for domestic suppliers in government contracts
- **Effect**: Creates protected market segment
- **Legality**: Allowed within limits (WTO Government Procurement Agreement)

**Technology Procurement**
- **What**: Government advance-purchases emerging technology products
- **Effect**: De-risks private R&D, accelerates commercialization
- **Example**: "Purchase $1B in domestic electric vehicles for government fleet"

---

## Currency & Financial Actions

### Exchange Rate Policy

**Policy Interest Rate Adjustment**
- **What**: Raise/lower central bank rates
- **Effect**: Higher rates → stronger currency, lower inflation, slower growth
- **Range**: -0.5% to +2% per turn (large moves risk instability)

**FX Intervention (Spot Market)**
- **What**: Buy/sell your currency using reserves
- **Effect**: Can move exchange rate 2-10% depending on size and market conditions
- **Cost**: Depletes reserves (need adequate stock)
- **Example**: "Sell $50B in reserves to weaken currency and boost exports"

**Competitive Devaluation**
- **What**: Engineer deliberate currency weakness for export advantage
- **Effect**: Exports +20% competitive, imports more expensive, inflation risk
- **Detection**: 70% if sustained, triggers "currency manipulator" label
- **Penalty**: -100 UTA credits, potential counter-devaluation by partners

### Reserve Management

**Reserve Accumulation/Decumulation**
- **What**: Build or draw down foreign exchange reserves
- **Effect**: Insurance against shocks, but opportunity cost
- **Target**: 90 days of imports (IEA standard)
- **Strategic**: Massive reserves enable currency intervention

**Forward Contract Offerings**
- **What**: Central bank offers FX forwards to exporters/importers
- **Effect**: Reduces currency risk for businesses, stabilizes trade flows
- **Commitment**: Must fulfill contracts (can't renege without reputation damage)

**Reserve Diversification**
- **What**: Shift reserves from USD to EUR, gold, SDR, or rival currencies
- **Effect**: Reduces dependence on hegemon currency
- **Strategic**: Coordinated reserve shifts can threaten reserve currency status
- **Example**: "Shift 20% of reserves from USD to EUR and gold"

### Capital Controls

**Capital Flow Restrictions**
- **What**: Limit inflows/outflows of financial capital
- **Types**: Taxation (Tobin tax), volume limits, approval requirements
- **Effect**: Reduces volatility but deters investment
- **Use Case**: Prevent capital flight during crisis or hot money surges

**Foreign Investment Screening**
- **What**: Require approval for foreign direct investment (FDI)
- **Intensity**: Light (national security only) to Heavy (all sectors)
- **Effect**: Can block strategic acquisitions
- **Example**: "Block Chinese purchase of domestic semiconductor firm"

### Currency Warfare

**Trade Invoicing Currency Mandates**
- **What**: Require trade with you be settled in your currency or alternative to USD
- **Effect**: Builds demand for your currency, undermines hegemon
- **Success**: Requires large economy or resource leverage
- **Example**: "Demand all oil purchases be settled in rubles or yuan"

**Currency Swap Agreements**
- **What**: Bilateral agreements to provide currency liquidity
- **Effect**: Enables trade without USD intermediation
- **Strategic**: Building alternative financial architecture
- **Example**: "Establish $50B currency swap line with partner"

**Reserve Weaponization**
- **What**: Dump holdings of rival's currency/bonds
- **Effect**: -30% target currency value, but depletes your reserves
- **Use Case**: Financial warfare during major conflict
- **Consequence**: Irreversible relationship break, -150 UTA credits

### Financial Market Tools

**Reserve Ratio Requirements**
- **What**: Mandate banks hold % of deposits as reserves
- **Effect**: Higher ratios reduce lending capacity, tighten credit
- **Range**: 5% (loose) to 25% (tight)

**Directed Credit Allocation**
- **What**: Mandate banks lend to priority sectors
- **Effect**: Channels capital to strategic industries
- **Efficiency Loss**: 10-20% due to market distortion

**Sovereign Bond Issuance**
- **Domestic Currency**: Safe, can monetize if needed
- **Foreign Currency**: Cheaper rates but exchange rate risk
- **Strategic**: Foreign issuance signals confidence or desperation depending on context

**Sterilization Operations**
- **What**: Offset FX intervention via domestic bond sales
- **Effect**: Prevents money supply expansion from intervention
- **Technical**: Maintains domestic monetary policy independence

---

## Sanctions & Embargo Actions

### Unilateral Sanctions

**Comprehensive Sanctions**
- **What**: Total embargo on trade with target country
- **Effect**: -15% to -30% target GDP, -3% own GDP
- **Success Rate**: 35% achieve policy change
- **Duration**: Often years (rarely work quickly)
- **Penalty**: -500 UTA credits (major system disruption)

**Sectoral Sanctions**
- **What**: Block specific industries (energy, finance, technology, military)
- **Effect**: -5% to -10% target sector, -1% own GDP
- **Success Rate**: 30%
- **Example**: "Sanction Russia's energy sector"
- **Penalty**: -200 UTA credits

**Targeted/Smart Sanctions**
- **What**: Freeze assets and restrict individuals/entities
- **Effect**: -1% to -3% target GDP, minimal own cost
- **Success Rate**: 25% (surgical pressure)
- **Penalty**: -100 UTA credits

**Financial Sanctions**
- **What**: Block access to banking systems (SWIFT cutoff), freeze assets
- **Effect**: -20% target liquidity, payment crisis
- **Use Case**: Pre-war escalation, major conflict
- **Penalty**: -400 UTA credits

### Secondary Sanctions

**Third-Party Enforcement**
- **What**: Force neutral countries to choose: trade with you OR trade with target
- **Effect**: Extends sanction reach, multiplies pressure
- **Risk**: Damages relations with third parties
- **Example**: "Countries trading with sanctioned state lose access to our market"
- **Penalty**: -300 UTA credits

**Sanctions Evasion Enforcement**
- **What**: Investigate and punish triangulation attempts
- **Intensity**: Light (monitoring) to Heavy (asset freezes, prosecutions)
- **Investment**: $50M to $500M per turn
- **Effect**: Detection probability +10% to +40%

### Coalition Sanctions

**Form Sanctions Coalition**
- **Requirements**: 2+ countries, shared threat perception
- **Effect**: Effectiveness +50%, costs shared
- **Stability**: 70% initial cohesion, decays without maintenance
- **Example**: "Coordinate comprehensive Iran sanctions with EU and allies"

**Coalition Burden Sharing**
- **What**: Negotiate cost distribution among coalition members
- **Equity**: Equal per capita vs proportional to GDP vs ability to pay
- **Free-Rider Problem**: Monitor and punish defectors

**Coalition Exit/Defection**
- **Trigger**: Economic pain exceeds benefits
- **Consequence**: Coalition weakens, defector faces reputation loss (-0.3)
- **Strategic**: Survive to last defector for maximum gain

---

## Alliance & Coalition Actions

### Trade Bloc Formation

**Create Preferential Trade Area**
- **Requirements**: 3+ members, combined GDP >15% world
- **Terms**: Internal tariff reductions, external tariff coordination
- **Effect**: +2-5% GDP for members, trade diversion from non-members
- **Example**: "Form Pacific Trade Partnership with 8 member countries"

**Join Existing Trade Bloc**
- **Process**: Application → negotiation (2-3 turns) → ratification
- **Conditions**: May require regulatory harmonization, policy commitments
- **Benefits**: Immediate market access, lower tariffs

**Exit Trade Bloc**
- **Duration**: 1-2 turns notice period
- **Consequence**: Tariffs revert, reputation damage (-0.3), potential retaliation
- **Example**: Historical analogue is Brexit

### Security Alliances

**Mutual Defense Pact**
- **What**: Military support if member attacked
- **Effect**: Deters aggression, binds members
- **Cost**: Defense spending obligation (1-2% GDP)
- **Example**: "Form defensive alliance with neighboring states"

**Security Guarantee**
- **What**: Unilateral promise to defend another country
- **Effect**: Binds client, deters third parties
- **Credibility**: Requires military capability and reputation
- **Example**: "Guarantee Taiwan security against invasion"

### Policy Coordination

**Joint Sanctions Regime**
- **What**: Coordinate sanctions targeting with allies
- **Effect**: +50% effectiveness, shared enforcement
- **Mechanism**: Joint monitoring, intelligence sharing

**Technology Alliance**
- **What**: Pool R&D resources, share standards
- **Effect**: +20% innovation rate, locks out rivals
- **Example**: "Form semiconductor alliance with Taiwan, South Korea, Japan"

**Energy/Resource Security Pact**
- **What**: Coordinate strategic reserves, emergency sharing
- **Effect**: Reduced vulnerability, collective bargaining
- **Example**: "Form Asian energy buyers coalition to negotiate with OPEC"

### Coalition Maintenance

**Burden Sharing Adjustments**
- **What**: Renegotiate contribution levels
- **Trigger**: Free-riding detected, economic conditions change
- **Mechanism**: Larger members pay disproportionately (Olson-Zeckhauser effect)

**Side Payments**
- **What**: Compensate members who bear higher costs
- **Effect**: Maintains coalition cohesion
- **Example**: "Pay Eastern European members to compensate for Russia sanctions costs"

**Coalition Discipline**
- **What**: Monitor compliance, punish defectors
- **Mechanism**: Reduce benefits, threaten expulsion
- **Example**: "Reduce market access for member violating sanctions"

---

## Military & Coercive Actions

### Naval Operations

**Naval Blockade**
- **What**: Block sea trade routes to/from target port(s)
- **Effect**: -80% throughput, massive supply chain disruption
- **Detection**: 100% (AIS, satellites)
- **Penalty**: -1000 UTA credits, potential war
- **Example**: "Blockade Taiwan Strait"

**Naval Interception/Inspection**
- **What**: Board and search vessels for contraband
- **Effect**: Enforces sanctions, deters smuggling
- **Detection**: 100% visible
- **Legality**: Depends on international law, flag state
- **Example**: "Intercept North Korean vessels for coal inspection"

**Convoy Escort**
- **What**: Armed protection of own commercial shipping
- **Effect**: Defensive posture, insurance costs decrease
- **Penalty**: -50 UTA credits (militarization of trade)
- **Example**: "Escort oil tankers through contested waters"

**Maritime Exclusion Zone**
- **What**: Declare no-go area in international waters
- **Effect**: Forces trade rerouting, intimidation
- **Detection**: 100%
- **Penalty**: -300 UTA credits, escalation risk 40%

### Chokepoint Control

**Chokepoint Seizure/Control**
- **What**: Military control of strait, canal, or critical passage
- **Effect**: Levy tolls, deny access to adversaries, intelligence advantage
- **Targets**: Hormuz, Suez, Malacca, Panama, Bab el-Mandeb
- **Consequence**: Global trade disruption, military confrontation risk
- **Penalty**: -1500 UTA credits if coercive

**Chokepoint Denial**
- **What**: Mine, block, or threaten chokepoint closure
- **Effect**: Forces rerouting (adds 15-30% transport costs), price spikes
- **Escalation**: 80% probability of military retaliation
- **Example**: "Mine Strait of Hormuz in retaliation for sanctions"

### Infrastructure Sabotage

**Pipeline Attack**
- **What**: Physical or cyber sabotage of energy infrastructure
- **Effect**: -30% to -100% supply depending on alternative routes
- **Detection**: 60% attribution probability
- **Penalty**: -600 UTA credits if attributed
- **Example**: "Sabotage Nord Stream pipeline"

**Undersea Cable Disruption**
- **What**: Sever or tap fiber-optic cables
- **Effect**: Internet/financial communication disruption
- **Detection**: 50% attribution
- **Use Case**: Information warfare, financial disruption

**Port/Logistics Attack**
- **What**: Damage port facilities, cranes, storage
- **Effect**: -30% to -50% throughput for 6-12 months
- **Recovery**: Slow (infrastructure takes time to rebuild)

### Cyber Operations

**Port/Logistics Cyberattack**
- **What**: Hack port systems, logistics software
- **Effect**: -10% to -30% throughput disruption
- **Detection**: 60% probability
- **Attribution**: 40% probability (plausible deniability)
- **Penalty**: -500 UTA credits if attributed

**Supply Chain Data Manipulation**
- **What**: Falsify shipping records, customs data
- **Effect**: Enables smuggling, sanctions evasion, intelligence
- **Detection**: 50%
- **Use Case**: Support triangulation efforts

**Financial Network Disruption**
- **What**: Attack SWIFT, payment systems, stock exchanges
- **Effect**: Liquidity crisis, trading halts
- **Severity**: Systemic risk if sustained
- **Penalty**: -800 UTA credits (attacks critical infrastructure)

**Electronic Warfare**
- **What**: GPS jamming, AIS spoofing, communication disruption
- **Effect**: Navigation uncertainty, shipping delays
- **Use Case**: Gray zone harassment, deniable coercion

### Deterrence & Signaling

**Military Exercises**
- **What**: Conduct drills near rival territory/trade routes
- **Effect**: -5% throughput (ships reroute cautiously), insurance +50bps
- **Detection**: 100% visible
- **Penalty**: -50 UTA credits (low)
- **Escalation Risk**: 15%

**Naval Deployments**
- **What**: Position warships near rival ports/chokepoints
- **Effect**: Show of force, intimidation
- **Cost**: $100M to $500M per turn
- **Escalation Risk**: 25%

**Weapons Sales/Transfers**
- **What**: Arm proxies, shift regional balance
- **Effect**: Empowers allies, threatens rivals
- **Example**: "Sell advanced missiles to partner nation"

**Base Access Agreements**
- **What**: Establish military bases in strategic locations
- **Effect**: Forward positioning, power projection
- **Cost**: Rent + maintenance (~$1B/year major base)

### Economic Warfare

**Asset Seizures**
- **What**: Freeze foreign holdings, nationalize assets
- **Effect**: -30% target foreign assets, relationship breakdown
- **Use Case**: Pre-war or major sanctions escalation
- **Penalty**: -400 UTA credits

**Strategic Resource Denial**
- **What**: Embargo critical exports (rare earths, technology, energy)
- **Effect**: Target supply chain disruption
- **Effectiveness**: High if monopoly supply position
- **Example**: "Embargo rare earth exports to defense contractors"

---

## Energy & Logistics Actions

### Strategic Reserves

**Build/Expand Strategic Reserves**
- **What**: Stockpile oil, gas, critical minerals, food
- **Cost**: $50-200/barrel for oil (infrastructure + commodity)
- **Effect**: Insurance against supply shocks
- **Target**: 90 days oil, 30 days gas (IEA standards)
- **Timing**: 1-3 turns to build infrastructure

**Release Strategic Reserves**
- **What**: Sell reserves to market
- **Effect**: Prices drop temporarily (-10% to -20%), stabilizes domestic supply
- **Duration**: Effective for 60-90 days
- **Cost**: Depletes buffer (must refill later at potentially higher prices)

**Coordinate Reserve Release**
- **What**: Allied nations release simultaneously
- **Effect**: Multiplies price impact (2-3x individual release)
- **Example**: "IEA coordinated release" (historical 2022)

### Infrastructure Investment

**Port Capacity Expansion**
- **Cost**: $500M to $5B depending on scale
- **Duration**: 2-4 turns construction
- **Effect**: +20% to +50% throughput, reduces congestion costs
- **Strategic**: Attracts transshipment, hub status

**Pipeline Construction**
- **Cost**: $5M to $15M per kilometer
- **Duration**: 4-8 turns (permitting + construction)
- **Effect**: Enables new trade routes, reduces transport costs 40%
- **Example**: "Build gas pipeline from Norway to Germany"

**Rail Network Development**
- **Cost**: $2B to $20B depending on scale
- **Duration**: 5-10 turns
- **Effect**: Enables continental trade, alternative to sea/air
- **Example**: "Develop Trans-Caspian rail corridor"

**LNG Terminal Construction**
- **Cost**: $2B per import terminal
- **Duration**: 3 turns
- **Effect**: Enables LNG imports, supplier diversification
- **Strategic**: Reduces pipeline dependency

### Energy Policy

**Fuel Subsidy Programs**
- **What**: Subsidize domestic energy consumption
- **Cost**: 1-3% GDP
- **Effect**: Reduces industrial costs, consumer protection
- **Drawback**: Fiscal burden, demand distortion

**Green Energy Transition**
- **What**: Accelerate renewable energy deployment
- **Cost**: 2-5% GDP over 5-10 turns
- **Effect**: Reduces import dependency long-term
- **Lag**: 5+ turns before significant impact

**Energy Efficiency Mandates**
- **What**: Require efficiency standards for buildings, vehicles, industry
- **Effect**: Reduces demand 10-20% over time
- **Cost**: Compliance burden on businesses

**Fuel Mix Mandate**
- **What**: Specify % of electricity from coal/gas/nuclear/renewable
- **Effect**: Energy security, environmental, cost tradeoffs
- **Example**: "Phase out coal by turn 20"

### Logistics Optimization

**Trade Route Diversification**
- **What**: Invest in alternative shipping/rail/air routes
- **Effect**: Reduces chokepoint vulnerability
- **Example**: "Develop Arctic shipping route as Suez alternative"

**Bonded Warehouse Networks**
- **What**: Create special zones for re-export, logistics hubs
- **Effect**: Attracts transshipment business, logistics revenue
- **Abuse Risk**: Can enable triangulation

**Emergency Sharing Agreements**
- **What**: Mutual assistance pacts for energy/logistics crises
- **Effect**: Collective resilience
- **Example**: "EU emergency gas sharing mechanism"

---

## Resource Strategy Actions

### Resource Cartels

**Form Commodity Cartel**
- **Requirements**: Control >60% global supply
- **Members**: 2+ major producers
- **Mechanism**: Coordinate production cuts
- **Effect**: Prices +40% to +200%
- **Stability**: Fragile (cheating incentive), 20% fragmentation risk/turn
- **Example**: "Form OPEC+ alliance for oil production cuts"

**Enforce Cartel Discipline**
- **What**: Monitor member compliance, punish cheaters
- **Mechanism**: Side payments to compensate low-production members
- **Example**: "Saudi Arabia acts as swing producer to stabilize prices"

**Break Rival Cartel**
- **What**: Offer incentives to defectors
- **Effect**: Cartel collapses, prices crash
- **Example**: "Offer technology transfer to OPEC member to increase production"

### Resource Monopolization

**Strategic Acquisition**
- **What**: Purchase foreign mining rights, energy reserves
- **Cost**: Varies (billions to tens of billions)
- **Effect**: Locks up supply, denies to rivals
- **Example**: "Acquire lithium mines in South America"

**Processing Dominance**
- **What**: Build monopoly in refining/processing even if don't control raw materials
- **Effect**: Capture value-add, bottleneck access
- **Example**: "China's rare earth refining dominance"

**Export Restrictions**
- **What**: Limit raw material exports to force domestic processing
- **Effect**: Forces downstream industries to relocate to your country
- **Example**: "Ban bauxite exports, only allow aluminum exports"

### Resource Substitution

**Alternative Source Development**
- **What**: Invest in substitutes for rival-controlled resources
- **Cost**: 1-3% GDP R&D over 5-10 turns
- **Success**: 40-70% depending on technical difficulty
- **Example**: "Develop synthetic substitutes for rare earths"

**Recycling Programs**
- **What**: Recover critical materials from waste streams
- **Effect**: Reduces import dependency 10-30%
- **Lag**: 2-3 turns to establish infrastructure

---

## UTA System Actions

### Credit Management

**Earn UTA Credits**
- **Clean Audits**: +10 credits per compliant period
- **Enforcement Contribution**: +1 credit per $10M invested in UTA
- **Voluntary Disclosure**: +20 credits for reporting own violations
- **Dispute Victory**: +50 credits if your complaint upheld

**Spend UTA Credits**
- **Tariff-Credit Redemption**: Convert credits to tariff waivers
- **Priority Customs Processing**: 100 credits for fast-track treatment
- **Dispute Filing**: 50 credits to file formal complaint
- **Rule Change Vote**: Credits determine voting weight

**Build Credit Reserve**
- **Strategic**: Bank credits during peaceful periods for future violations
- **Decay**: -2% annually (use it or lose it)

### Membership Actions

**Apply for UTA Membership**
- **Requirements**: Transparency standards, compliance record
- **Process**: 3-5 turns (application → review → vote)
- **Benefits**: Full market access, credit system, institutional voice

**Threaten Withdrawal**
- **What**: Signal potential UTA exit to extract concessions
- **Credibility**: Requires alternative markets or self-sufficiency
- **Risk**: Called bluff loses reputation

**Bloc Shift**
- **What**: Move between UTA tripartite blocs (US-led, EU-led, China-led)
- **Effect**: Changes alliance structure, market access, enforcement intensity
- **Example**: "Turkey pivots from Western to Eurasian bloc"

### Dispute Resolution

**File Dispute Against Rival**
- **Cost**: 50 UTA credits
- **Process**: 2-4 turns (evidence → hearing → ruling)
- **Grounds**: Subsidy violations, dumping, origin fraud, triangulation
- **Outcome**: If successful, rival penalized; if unsuccessful, you lose reputation

**Defend Against Dispute**
- **Response**: Provide evidence, argue legitimacy
- **Settlement Option**: Negotiate with complainant to withdraw
- **Risk**: Guilty verdict = credit penalty + mandatory policy change

**Challenge UTA Rule**
- **What**: Propose rule change through institutional process
- **Requirements**: Support from 30% of members or 3+ major economies
- **Example**: "Challenge export subsidy ban as outdated"

### Enforcement Contribution

**Invest in UTA Enforcement**
- **Amount**: $10M to $500M per turn
- **Effect**: Global detection rates increase, earn credits, gain institutional influence
- **Strategic**: High contributors shape enforcement priorities

**Share Intelligence**
- **What**: Provide violation evidence to UTA
- **Effect**: Builds cases against rivals, earns credits
- **Risk**: Exposes your own intelligence capabilities

---

## Standards & Regulation Actions

### Standard Setting

**Propose Global Standards**
- **What**: Push domestic technical standards internationally
- **Success**: Requires regulatory capacity, market size
- **Effect**: Global firms comply with your rules (Brussels Effect)
- **Example**: "GDPR forces global data privacy standards"

**Lead International Standards Body**
- **What**: Chair ISO committee, technical working groups
- **Effect**: Shape standards development to favor domestic industries
- **Example**: "Lead 5G standards committee"

**Technology Certification Regime**
- **What**: Require products pass your certification to enter any market
- **Effect**: Non-tariff barrier, locks out rivals
- **Example**: "Require cybersecurity certification for all telecom equipment"

### Regulatory Export

**Environmental Standards**
- **What**: Impose carbon border adjustments, emissions requirements
- **Effect**: Forces foreign producers to adopt your environmental regulations
- **Example**: "EU carbon border tax" → global firms reduce emissions

**Labor Standards**
- **What**: Ban imports from countries violating labor rights
- **Effect**: Pressures rivals to improve standards or lose market access
- **Enforcement**: Supply chain due diligence requirements

**ESG Requirements**
- **What**: Mandate Environmental/Social/Governance compliance for market access
- **Effect**: Regulatory leverage, values-based screening
- **Example**: "Require human rights due diligence for all imports"

### Regulatory Arbitrage

**Create Special Economic Zones**
- **What**: Designate zones with relaxed regulations
- **Effect**: Attracts investment, may enable gray zone activities
- **Example**: "Freezone allows re-export without full regulatory compliance"

**Regulatory Divergence**
- **What**: Intentionally maintain different standards than major markets
- **Effect**: Protects domestic producers, but limits export potential
- **Strategic**: Developing countries resist "standards imperialism"

---

## Compliance & Cheating Actions

### Triangulation & Origin Laundering

**Simple Triangulation**
- **Method**: Ship sanctioned goods through neutral third country
- **Cost**: +10% markup (transit fees, risk premium)
- **Detection**: 60% probability (trade asymmetries, sudden spikes)
- **Penalty**: -400 UTA credits, trade suspension
- **Example**: "Ship Russian oil via Turkey to evade EU sanctions"

**Multi-Hop Triangulation**
- **Method**: Use 2+ intermediaries to obscure trail
- **Cost**: +20% markup
- **Detection**: 25% probability (harder to trace)
- **Penalty**: -600 UTA credits if detected
- **Effectiveness**: Best when intermediaries are complicit and add genuine value

**Minimal Processing**
- **Method**: Add token value (repackaging, blending, minor assembly) to claim origin change
- **Cost**: +5% processing
- **Detection**: 45% (rules of origin verification)
- **Penalty**: -400 UTA credits
- **Example**: "Import Chinese steel, cut to length, export as 'domestic'"

### Transfer Pricing Manipulation

**Intercompany Pricing Games**
- **Method**: Manipulate prices between subsidiaries to shift profits to low-tax jurisdictions
- **Effect**: Reduce tariff base, avoid taxes
- **Detection**: 25-40% depending on sophistication
- **Penalty**: -300 UTA credits + back-taxes at 2x avoided amount
- **Example**: "Sell to own subsidiary at $50 (low), they resell at market $100"

**Stay Within Safe Harbor**
- **Method**: Keep transfer prices within 20% of arm's length benchmarks
- **Detection**: <10% (hard to prove intent)
- **Benefit**: Legitimate tax optimization

### Subsidy Concealment

**Hidden State Support**
- **Methods**: Below-market loans, free land, SOE purchases at premium, energy subsidies
- **Detection**: 20-30% (very hard to prove)
- **Penalty**: -350 UTA credits + countervailing duties
- **Example**: "State bank provides loans at 2% when market rate is 8%"

**Subsidy Laundering**
- **Method**: Channel subsidies through SOEs, development banks, or regional governments
- **Effect**: Obscures paper trail
- **Detection**: Reduces detection probability by 30%

### Shadow Fleet Operations

**Dark Ship Networks**
- **Method**: Register ships under flags of convenience, turn off transponders
- **Cost**: +30% (uninsured shipping, higher risk)
- **Detection**: 55% (satellite monitoring improving)
- **Penalty**: -600 UTA credits, asset seizure
- **Use Case**: Sanctions evasion for high-value commodities
- **Example**: "Russian oil exports via 'ghost tankers'"

**Ship-to-Ship Transfers**
- **Method**: Transfer cargo in international waters to evade port monitoring
- **Detection**: 40% (satellite imagery catches most)
- **Effect**: Obscures origin and destination

### Document Fraud

**Origin Certificate Falsification**
- **Method**: Forge certificates of origin
- **Detection**: 70% (physical inspection catches most)
- **Penalty**: -300 UTA credits, shipment seizure
- **Low Success**: Not recommended unless inspection rates are low

**Invoice Manipulation**
- **Method**: Misreport value, quantity, or product classification
- **Detection**: 50% (customs verification)
- **Effect**: Reduce tariff liability
- **Example**: "Declare $50/unit when actual value $100/unit"

### Detection Avoidance

**Reduce Opacity Through Compliance**
- **Method**: Maintain high transparency in non-critical areas
- **Effect**: Reduces audit risk for covert operations
- **Strategic**: Build clean reputation, then violate strategically once

**Diversify Cheating Methods**
- **Method**: Rotate tactics to avoid pattern detection
- **Effect**: Each method has independent detection probability
- **Example**: "Triangulate oil, transfer price steel, hide subsidies in tech"

**Small-Scale Testing**
- **Method**: Trial run violations at low volume to assess detection
- **Effect**: Learn enforcement weaknesses before large commitment
- **Example**: "Test triangulation with $10M before scaling to $1B"

**Limit to Opaque Sectors**
- **Method**: Focus violations in sectors with low transparency (chemicals, finance, services)
- **Effect**: Reduces detection probability by 30%
- **Avoid**: Agriculture, mining, manufacturing (easy to monitor)

---

## Information Warfare Actions

### Deception & Disinformation

**Data Fabrication**
- **What**: Report false economic statistics
- **Effect**: Mislead rivals about your strength/weakness
- **Detection**: 30% (cross-validation catches inconsistencies)
- **Penalty**: -400 UTA credits, credibility collapse
- **Use Case**: Desperate survival states or strategic misdirection

**Trade Data Manipulation**
- **What**: Misreport export/import volumes
- **Effect**: Conceal violations, avoid scrutiny
- **Detection**: 50% (partner reports don't match)
- **Penalty**: -200 UTA credits

**Economic Propaganda**
- **What**: Exaggerate own success, rival failures
- **Effect**: Shapes perceptions, affects investor/partner confidence
- **Legality**: Allowed (political speech)

### Intelligence Operations

**Corporate Espionage**
- **What**: Steal trade secrets, technology, business strategies
- **Effect**: Accelerate catch-up, competitive advantage
- **Detection**: 25% (hard to prove state involvement)
- **Penalty**: -500 UTA credits if proven state-sponsored
- **Example**: "Hack rival semiconductor firms for chip designs"

**Signal Intelligence**
- **What**: Monitor rival communications, trade flows
- **Effect**: Advance warning of policy changes, commercial intelligence
- **Legality**: Gray zone

### Counter-Intelligence

**Anonymous Tips Against Rivals**
- **What**: Provide UTA with evidence of rival violations
- **Effect**: Triggers investigations, damages rival reputation
- **Risk**: If traced back, reputation damage

**False Flag Operations**
- **What**: Attribute your own violations to third party
- **Detection**: Difficult but devastating if uncovered
- **Penalty**: -800 UTA credits

---

## State-Enterprise Control Actions

### State-Owned Enterprise (SOE) Mandates

**Production Targets**
- **What**: Order SOEs to produce X volume regardless of profitability
- **Effect**: Can force capacity expansion, market flooding
- **Cost**: SOEs may run losses (requires state support)
- **Example**: "Order state steel mills to produce 200M tons despite -20% margins"

**Pricing Directives**
- **What**: Command SOEs to sell at specific prices (below cost for dumping)
- **Effect**: Undercut competitors, gain market share
- **Detection**: 60% (sustained below-cost pricing is obvious)
- **Penalty**: -250 UTA credits (anti-dumping)

**Market Allocation Orders**
- **What**: Direct SOEs to prioritize specific customers or markets
- **Effect**: Strategic favoritism, withhold supply from rivals
- **Example**: "SOE energy companies prioritize domestic buyers during shortage"

**Technology Sharing Mandates**
- **What**: Require SOEs to transfer knowledge to domestic private firms
- **Effect**: Accelerates sectoral competitiveness
- **Legality**: Domestic policy, hard to challenge

**Loss Tolerance**
- **What**: Accept negative margins for strategic purposes
- **Duration**: Can sustain 3-5 turns before fiscal stress
- **Effect**: Competitors exit, then SOE can raise prices
- **Example**: "Accept $5B annual losses in semiconductor sector to achieve dominance"

### Private Firm Incentives

**Government Procurement Guarantees**
- **What**: Promise to purchase firm output at premium
- **Effect**: De-risks investment, encourages capacity expansion
- **Example**: "Guarantee purchase of all domestic EV production"

**Export Performance Requirements**
- **What**: Grant subsidies conditional on export volume
- **Effect**: Incentivizes export focus
- **Legality**: Prohibited export subsidies (high detection risk)

**Local Content Requirements**
- **What**: Mandate use of domestic inputs
- **Effect**: Forces supply chain localization
- **Example**: "Solar panels must use 50% domestic components"

### Strategic Partnership Contracts

**Long-Term Supply Agreements**
- **What**: Government-backed contracts with foreign buyers
- **Effect**: Secures market access, stable demand
- **Example**: "20-year LNG supply contract with Japan"

**Technology Transfer Conditions**
- **What**: Market access requires joint ventures, IP sharing
- **Effect**: Acquires foreign technology
- **Legality**: Gray zone, may violate WTO
- **Example**: "Foreign carmakers must form JVs and share EV technology"

---

## Enforcement & Monitoring Actions

### Domestic Enforcement Intensity

**Customs Inspection Rate**
- **Low (10%)**: Fast clearance, high smuggling risk
- **Medium (30%)**: Balanced
- **High (70%)**: Slow but secure
- **Cost**: $50M to $200M per year depending on intensity

**Audit Frequency**
- **What**: How often to audit firms for subsidy compliance, transfer pricing
- **Range**: 5% (light touch) to 40% (heavy scrutiny)
- **Effect**: Detection rates scale linearly
- **Cost**: $1M per audit

**Penalty Severity**
- **What**: Set fines and sanctions for violations
- **Light**: Warnings, small fines (limited deterrence)
- **Heavy**: Asset seizures, criminal prosecution (strong deterrence but drives activity underground)
- **Optimal**: 2x benefit of violation (break-even)

### Transparency Requirements

**Corporate Disclosure Mandates**
- **What**: Require firms report subsidies, ownership, transfer pricing
- **Effect**: Reduces opacity, eases detection
- **Resistance**: Firms lobby against (competitive disadvantage)

**Trade Data Sharing Agreements**
- **What**: Real-time customs data exchange with partners
- **Effect**: Catches trade asymmetries immediately
- **Privacy Tradeoff**: Reveals commercial intelligence

**Whistleblower Rewards**
- **What**: Pay informants for reporting violations
- **Amount**: 10-30% of recovered penalties
- **Effect**: +20% detection rate
- **Risk**: False accusations, social instability

### International Enforcement

**Support UTA Enforcement Budget**
- **Contribution**: $50M to $500M annually
- **Benefit**: +1 credit per $10M, shapes enforcement priorities
- **Strategic**: High contributors influence which violations are pursued

**Joint Investigation Teams**
- **What**: Coordinate with partners on complex cases
- **Effect**: Shares costs, combines expertise
- **Example**: "EU-US joint investigation of Chinese steel subsidies"

**Intelligence Sharing Networks**
- **What**: Exchange violation evidence with allies
- **Effect**: Coalition enforcement more effective
- **Risk**: Exposes intelligence methods

---

## Strategic Meta-Actions

### Diplomatic Signaling

**Red Line Declarations**
- **What**: Announce non-negotiable positions
- **Effect**: Deters rival actions, commits you publicly
- **Credibility**: Must follow through or lose reputation
- **Example**: "Any sanctions on our energy sector will trigger complete cutoff"

**Offer Concessions**
- **What**: Propose policy changes in exchange for rival concessions
- **Effectiveness**: Requires credible commitment
- **Example**: "We'll reduce steel tariffs if you remove tech export controls"

**Threaten Escalation**
- **What**: Signal willingness to escalate if demands not met
- **Credibility**: Requires capability + reputation
- **Risk**: Called bluff damages reputation

**De-Escalation Proposals**
- **What**: Offer mutual step-back from confrontation
- **Use Case**: When conflict costs exceed benefits
- **Example**: "Propose simultaneous 50% tariff reduction"

### Strategic Ambiguity

**Deliberate Opacity**
- **What**: Don't clarify intentions, keep rivals guessing
- **Effect**: Deters without commitment, preserves flexibility
- **Risk**: Miscalculation, alliance uncertainty

**Multiple Signaling**
- **What**: Send contradictory signals to different audiences
- **Effect**: Hedges bets, confuses rivals
- **Example**: "Publicly condemn sanctions, privately facilitate them"

### Reputation Management

**Consistency Building**
- **What**: Follow through on threats and promises
- **Duration**: 10-15 turns to establish credibility
- **Effect**: Reputation → 0.8-1.0
- **Benefit**: Threats more credible, lower monitoring costs

**Strategic Violation**
- **What**: Burn reputation for one major gain
- **Calculation**: Gain must exceed long-term reputation value
- **Example**: "Violate treaty to avoid economic collapse"

**Reputation Repair**
- **What**: Consistent compliance after violation
- **Duration**: 15-20 turns to rebuild
- **Methods**: Voluntary disclosures, over-compliance, institutional contributions

---

## Turn Planning Tools

### Action Point Budget

**Base Points**: 10 per turn
**Modifiers**:
- Hegemon: +5 points
- Rising Power: +3 points
- Resource Emperor: +0 points
- Normative Leader: +2 points
- Survival State: -2 points

**Costs**:
- Minor policy: 1-2 points
- Major policy: 3-5 points
- Military operation: 5-8 points
- Coalition leadership: 4 + 1 per member
- Crisis response: 0 points (emergency override)

### Priority Sequencing

**Phase 1**: Defensive Actions (protect yourself)
**Phase 2**: Alliance Formation (lock in partnerships)
**Phase 3**: Economic Policies (tariffs, subsidies)
**Phase 4**: Sanctions/Enforcement
**Phase 5**: Military Operations
**Phase 6**: Offensive Financial Attacks

### Reaction Options

After all players reveal actions, you get ONE reaction:
- Retaliate against action targeting you
- Emergency counter-sanctions
- Military escalation or de-escalation
- Coalition coordination

---

## Quick Start: Archetype-Specific Strategies

### If You're a HEGEMON
**Priorities**: Maintain system control, contain rivals, preserve currency dominance
**Turn 1 Actions**: Monitor rising power (intel), strengthen alliances, invest in enforcement
**Avoid**: Overextension, unilateral sanctions (build coalitions instead)

### If You're a RISING POWER
**Priorities**: Build alternative institutions, achieve tech parity, expand influence
**Turn 1 Actions**: Industrial subsidies, R&D programs, secure resource supplies
**Avoid**: Premature confrontation with hegemon (wait until 60% GDP parity)

### If You're a RESOURCE EMPEROR
**Priorities**: Maximize resource rents, leverage supply for political goals, diversify economy
**Turn 1 Actions**: Form/join cartel, long-term supply contracts, strategic reserve builds
**Avoid**: Overplaying resource leverage (drives substitution)

### If You're a NORMATIVE LEADER
**Priorities**: Set global standards, lead institutions, build soft power
**Turn 1 Actions**: Propose regulations, lead international bodies, form high-standards club
**Avoid**: Military confrontation (not your strength)

### If You're a SURVIVAL STATE
**Priorities**: Extract maximum aid, avoid taking sides, survive crises
**Turn 1 Actions**: Bid for aid from competing powers, maintain strategic ambiguity
**Avoid**: Firm commitments to any bloc (need flexibility)

---

## End Notes

**This document is EXHAUSTIVE but NOT EXCLUSIVE**:
- If you can justify a strategy economically and it doesn't break game mechanics, propose it via Agent Intelligence Module
- New strategies will be evaluated, formalized, and added to this list
- The game evolves with player creativity

**Remember**:
- Every action has costs (monetary, reputation, UTA credits, escalation risk)
- Coordination with allies multiplies effectiveness
- Detection probabilities are REAL - you WILL get caught eventually if you cheat repeatedly
- Long-term reputation often exceeds short-term gains
- Strategic timing matters as much as action selection

**Victory comes from**:
- Matching actions to your archetype strengths
- Building coalitions to share costs
- Timing interventions for maximum impact
- Managing escalation without losing control
- Balancing aggressive expansion with systemic stability

Good luck navigating the complex world of geo-economic strategy!
