# Player (Country) Move - Complete Action Set

## Current Actions
- **Tariff schedule** (by partner and sector)
- **Enforcement spend and tooling**
- **Export controls/sanctions lists**
- **FX policy: No CDS or options, but rates, reserves and forwards allowed**
- **Industrial policy** (sector subsidies)

## Currency & Financial Actions

### Currency Policy Instruments
- **Policy interest rate adjustments** → affects capital flows, exchange rates
- **FX intervention** (spot market purchases/sales from reserves)
- **Forward contract offerings** (official FX forwards to exporters/importers)
- **Reserve accumulation/decumulation strategy**
- **Capital controls** (flow restrictions, taxation on inflows/outflows)
- **Trade invoicing currency mandates** (shift from USD to local currency)
- **Currency swap agreements** (with other central banks)
- **Sterilization operations** (offset FX intervention via domestic bonds)

### Financial Market Actions
- **Reserve ratio requirements** (bank lending capacity)
- **Directed credit allocation** (priority lending sectors)
- **Sovereign bond issuance** (domestic vs foreign currency)
- **Foreign investment screening intensity** (approve/block FDI)

## Additional Strategic Actions

### Trade Infrastructure
- **Port/logistics investment** (capacity expansion, efficiency upgrades)
- **Strategic commodity stockpiling** (build/release reserves)
- **Export credit programs** (subsidized financing for exporters)
- **Trade finance guarantees**

### Market Access & Standards
- **Non-tariff barriers** (technical standards, licensing, inspection protocols)
- **Quota systems** (import/export volume limits)
- **Preferential trade agreement negotiation** (bilateral/multilateral)
- **Rules of origin enforcement intensity**

### Compliance & Transparency
- **Data reporting quality** (transparency vs. obfuscation)
- **Customs enforcement intensity** (inspection rates, verification)
- **Origin laundering tolerance** (enforcement against transshipment)
- **Shadow fleet enablement** (registry/insurance leniency)

### Institutional
- **UTA membership actions** (application, withdrawal, bloc shift)
- **Tariff-credit redemption** (how/when to use accumulated credits)
- **Dispute resolution filing** (challenge other states)
- **Vote on UTA rule changes**

### State-Enterprise Control
- **SOE production mandates** (output targets, pricing directives)
- **Strategic partnership contracts** (long-term supply agreements)
- **Technology transfer requirements** (market access conditions)

### Diplomatic & Coercive
- **Coalition formation** (coordinate policies with allies)
- **Economic coercion signals** (threaten sanctions/tariffs)
- **Aid/development packages** (influence smaller states)
- **Intelligence sharing agreements**
- **Red line declarations** (non-negotiable positions)

### Sector-Specific
- **R&D investment priorities** (shift technological capabilities)
- **Labor standards enforcement** (intensity, wage floors)
- **Environmental regulation stringency** (affects production costs)
- **Energy policy** (fuel mix, efficiency mandates, strategic reserves)

### Reactive/Emergency
- **Retaliatory tariffs** (automatic or manual triggers)
- **Counter-subsidy measures**
- **Emergency safeguards** (surge protection)
- **Credit claim filing** (demand UTA compensation)


# Military Actions 

## Kinetic Operations
- **Naval interception/inspection** (flag vessels, board and search)
- **Port blockade** (single port, limited duration)
- **Convoy escort** (armed protection of own shipping)
- **Chokepoint control** (straits, canals - mining, passage denial)
- **Infrastructure sabotage** (pipelines, undersea cables, port facilities)
- **Maritime exclusion zones** (declare/enforce no-go areas)
- **Airspace restrictions** (no-fly zones over contested waters)

## Cyber & Electronic Operations
- **Port/logistics cyberattacks** (throughput disruption)
- **Supply chain data manipulation** (falsify shipping records)
- **Electronic warfare** (GPS jamming, AIS spoofing)
- **Financial network disruption** (SWIFT access, payment systems)

## Deterrence & Signaling
- **Military exercises** (near trade routes, rival ports)
- **Naval deployments** (show of force)
- **Weapons sales/transfers** (arm proxies, shift regional balance)
- **Base access agreements** (forward positioning)

## Economic Warfare
- **Asset seizures** (freeze foreign holdings, nationalize)
- **Strategic resource denial** (rare earths embargo, tech exports)
- **Secondary sanctions** (punish third parties trading with adversary)

## Proxy/Covert
- **Non-state actor support** (pirates, insurgents disrupting rival trade)
- **Plausibly deniable sabotage** (accidents, mysterious disruptions)


## Military Actions Consiqences

### Detection & Attribution
- **Naval deployment**: 100% visible (AIS, satellites), 100% attributable → UTA instantly detects
- **Cyber sabotage**: 60% detection probability, 40% attribution confidence → delayed/uncertain UTA response
- **Proxy support**: 20% detection, plausible deniability → might escape punishment

### Economic Impact Magnitude
- **Port blockade**: -80% throughput, massive supply chain disruption
- **Naval exercise**: -5% throughput (ships reroute cautiously), insurance +50bps
- **Pipeline sabotage**: Depends on alternative routes, could be 0% or 100% impact

###  UTA Penalty Severity
- **Overt blockade**: -1000 credits, immediate sanctions, expulsion risk
- **Convoy escort** (defensive): -50 credits, monitoring flag
- **Cyber attack** (if proven): -500 credits + tech sanctions

### Escalation Risk
- **Chokepoint mining**: 80% probability of military retaliation
- **Show of force**: 15% escalation probability
- **Asset seizure**: 30% but economic retaliation likely

### Strategic Purpose
Players choose based on:
- **High-risk/high-reward**: Blockade (massive leverage but huge costs)
- **Low-visibility**: Cyber/proxy (smaller impact but harder to punish)
- **Signaling**: Exercises (cheap deterrence, minimal UTA penalty)

**Implementation**: Each action has a parameter vector: `{economic_impact, detection_prob, attribution_prob, UTA_penalty, escalation_risk, duration}`. Players optimize their strategy accordingly.
**Key constraint**: All actions have economic impact parameters (% trade flow disruption, insurance cost spike, duration) and escalation probabilities that feed into game mechanics.
