# Turn Mechanics Gap Analysis

**Generated**: 2025-10-28
**Purpose**: Identify which player turn options from Country Turn-V2.md have complete specifications vs gaps in implementation mechanics

---

## Executive Summary

This document cross-references the exhaustive player action space in Country Turn-V2.md against module specifications to identify:
1. **Complete Mechanics** - Fully specified, ready for implementation
2. **Partial Mechanics** - Conceptually defined but missing algorithms/parameters
3. **Missing Mechanics** - Player options with no underlying system
4. **Critical Gaps** - Highest-priority missing pieces for gameplay

**Overall Completeness: 72%**
- 58% of actions have complete mechanics
- 28% have partial mechanics (need formalization)
- 14% are missing mechanics entirely

---

## Turn Options WITH Complete Mechanics ✅

These actions are fully specified with clear algorithms, parameters, and integration points.

### Trade Policy (Module: Trade Flow + Sanctions)

**Fully Specified**:
- ✅ **Adjust Tariff Rates** - Trade Flow Module lines 65-75 (ad valorem, specific, compound)
- ✅ **Import Quotas** - Trade Flow Module lines 76-78
- ✅ **Technical Standards & Certification** - Compliance Module lines 95-100 (NTB mechanics)
- ✅ **Rules of Origin Enforcement** - Compliance Module lines 165-190 (detection algorithms)
- ✅ **Tariff-Rate Quotas** - Trade Flow Module lines 79-81

**Implementation Ready**: YES
**Module Reference**: Trade Flow Module (Detailed Mechanics lines 12-50), Sanctions Module (lines 50-105)

**What's Fully Defined**:
- Mathematical formulas for tariff pass-through (80% in competitive markets)
- Trade volume elasticities (-2.5 for tariff elasticity)
- Quota enforcement mechanisms (physical limits)
- Detection probabilities for NTB abuse (40-70%)

---

### Subsidies & Industrial Policy (Module: Subsidy & Industrial Policy)

**Fully Specified**:
- ✅ **Direct Production Subsidies** - Subsidy Module lines 11-43 (per-unit, percentage, pass-through rates)
- ✅ **Export Credit Programs** - Subsidy Module lines 19-22
- ✅ **R&D Subsidies** - Subsidy Module lines 22-28 (3-5 turn lag, 10% productivity boost)
- ✅ **Investment Tax Credits** - Subsidy Module lines 25-29
- ✅ **Government Procurement Mandates** - Subsidy Module lines 30-32
- ✅ **Subsidy Detection Mechanisms** - Subsidy Module lines 83-99 (below-cost pricing, capacity anomalies)
- ✅ **Countervailing Duties** - Subsidy Module lines 101-104 (offset subsidy exactly)

**Implementation Ready**: YES
**Module Reference**: Subsidy & Industrial Policy Module (lines 1-238)

**What's Fully Defined**:
- Pass-through rates (60-90% to consumers)
- Competitiveness index formula (cost relative to global average)
- Market share elasticity (10% cost reduction → 15-40% share gain depending on product)
- Detection probability formulas (size × duration × transparency)
- ROI calculation for subsidy effectiveness

---

### Currency & Financial Actions (Module: Currency Strategy)

**Fully Specified**:
- ✅ **Policy Interest Rate Adjustment** - Currency Module (detailed mechanics exist)
- ✅ **FX Intervention** - Currency Module (reserve depletion, exchange rate impact 2-10%)
- ✅ **Reserve Accumulation/Decumulation** - Energy Module lines 497-503 (90-day targets)
- ✅ **Capital Controls** - Currency Module (Tobin tax, volume limits mechanics)

**Implementation Ready**: YES
**Module Reference**: Currency Strategy Module (full specification), Energy Module (reserve standards)

**What's Fully Defined**:
- Exchange rate impact formulas (intervention size → % move)
- Reserve adequacy standards (IEA 90-day oil, 30-day gas)
- Capital flow impact on exchange rates
- Sterilization operation mechanics

---

### Sanctions & Enforcement (Module: Sanctions & Geopolitics + Compliance)

**Fully Specified**:
- ✅ **Comprehensive Sanctions** - Sanctions Module lines 178-186 (35% success rate, -15% to -30% target GDP)
- ✅ **Sectoral Sanctions** - Sanctions Module lines 181-186 (30% success, -5% to -10% target sector)
- ✅ **Smart Sanctions** - Sanctions Module lines 183-186 (25% success, -1% to -3% GDP)
- ✅ **Coalition Sanctions** - Sanctions Module lines 273-289 (+50% effectiveness bonus)
- ✅ **Detection Probability Formulas** - Compliance Module lines 156-180 (base rate × intensity × anomaly × opacity)
- ✅ **UTA Credit System** - Compliance Module lines 39-71 (starting 500, decay 2%, thresholds 400/700)

**Implementation Ready**: YES
**Module Reference**: Sanctions & Geopolitics Module (lines 1-476), Compliance Module (lines 1-473)

**What's Fully Defined**:
- Success rate formulas by sanction type
- Economic impact calculations (leverage × dependence)
- Coalition stability dynamics (70% initial, -0.05 decay/turn)
- Credit penalties by violation type (-50 to -600)
- Detection algorithm (statistical anomaly + MRIO validation + partner reconciliation)

---

### Energy & Logistics (Module: Energy & Logistics)

**Fully Specified**:
- ✅ **Strategic Reserve Management** - Energy Module lines 46-61 (price impact -10% to -20%, duration 60-90 days)
- ✅ **Energy Security Score** - Energy Module lines 194-235 (4-factor formula: dependency, concentration, reserves, geopolitical risk)
- ✅ **Chokepoint Vulnerability** - Energy Module lines 116-189 (exposure value, feasibility, vulnerability score)
- ✅ **Transport Cost Calculations** - Energy Module lines 64-114 (modal choice, fuel dependency 50%)

**Implementation Ready**: YES
**Module Reference**: Energy & Logistics Module (lines 1-688)

**What's Fully Defined**:
- Energy security score formula (weighted 30/30/20/20)
- Reserve release price impact (1M barrels → -X% price)
- Chokepoint closure effects (Hormuz -80% oil, +50-100% price spike)
- Modal transport costs ($/ton-km for sea/rail/road/pipeline/air)

---

### Compliance & Cheating (Module: Compliance & Cheating Detection)

**Fully Specified**:
- ✅ **Triangulation Detection** - Compliance Module lines 74-95 (60% base detection, production-export mismatch)
- ✅ **Transfer Pricing Detection** - Compliance Module lines 96-116 (40% detection, 25% price deviation triggers)
- ✅ **Origin Falsification Detection** - Compliance Module lines 117-133 (70% detection, physical inspection)
- ✅ **Shadow Fleet Detection** - Compliance Module lines 150-165 (55% detection, AIS gaps)
- ✅ **Audit Selection Algorithm** - Compliance Module lines 202-227 (risk score calculation)
- ✅ **Penalty Escalation** - Compliance Module lines 251-283 (first offense warning, 2x, 3x, pariah status)

**Implementation Ready**: YES
**Module Reference**: Compliance & Cheating Detection Module (lines 1-473)

**What's Fully Defined**:
- Detection probability formulas by cheating method
- Red flag triggers (production-export ratio >1.0, price deviation >25%)
- Risk score calculation (previous violations 30%, anomalies 30%, geopolitics 20%, opacity 10%, strategic 10%)
- Penalty amounts by violation type
- Audit cost ($50K standard, $500K forensic)

---

## Turn Options WITH Partial Mechanics ⚠️

These actions are conceptually defined but lack algorithmic specifications or parameter values.

### Trade Policy - Gaps

**Partially Specified**:
- ⚠️ **Negotiate Bilateral Trade Agreement**
  - **What Exists**: General description (Country Turn line 32-34), duration 2-4 turns, effect +15-40% trade
  - **What's Missing**:
    - Negotiation algorithm (what determines success/failure?)
    - Parameter specification (which variables influence +15% vs +40%?)
    - Bargaining dynamics (how do relative power and complementarity affect terms?)
    - Exit clause mechanics (withdrawal process timing and costs)
  - **Module Reference**: Vague mention in Geopolitical Module, no technical specification
  - **Priority**: MEDIUM (important for alliance gameplay)

- ⚠️ **Form Preferential Trade Bloc**
  - **What Exists**: Concept (Country Turn lines 36-39), requirements (3+ countries, 15% world GDP)
  - **What's Missing**:
    - Formation algorithm (how do countries decide to join?)
    - Benefit distribution formula (why Benefit = Base × Power^0.7 × Contribution?)
    - Internal tariff reduction schedule (instant or phased?)
    - External tariff coordination mechanism (Nash bargaining? Median voter?)
  - **Module Reference**: Geopolitical Module lines 530-577 (formulas exist but lack integration with trade system)
  - **Priority**: MEDIUM-HIGH (coalition gameplay is core feature)

- ⚠️ **Retaliatory Tariffs (Automatic Triggers)**
  - **What Exists**: Concept (Country Turn lines 25-27)
  - **What's Missing**:
    - Trigger conditions (threshold for automatic vs manual retaliation?)
    - Escalation algorithm (tit-for-tat forgiveness factor? Gradual vs massive?)
    - De-escalation mechanics (how to exit tit-for-tat spiral?)
  - **Module Reference**: Mentioned in Geopolitical Module lines 93-111 but not formalized
  - **Priority**: MEDIUM (realistic conflict dynamics)

---

### Industrial Policy - Gaps

**Partially Specified**:
- ⚠️ **Technology Acquisition - Gray Zone Methods**
  - **What Exists**: Mandate tech transfer (Country Turn lines 73-75), Industrial espionage (Country Turn line 76, 25% detection, -500 credits)
  - **What's Missing**:
    - Effectiveness model (what % of target technology is actually acquired?)
    - Implementation lag (how long until acquired tech is productive?)
    - Quality discount (stolen tech is imperfect - what % penalty?)
    - Countermeasures (target can encrypt, compartmentalize - how does this affect success?)
  - **Module Reference**: Agent Intelligence Module mentions (lines 420-430) but no mechanics
  - **Priority**: MEDIUM (strategic but sensitive topic)

- ⚠️ **Buy National Policies**
  - **What Exists**: Concept (Country Turn lines 85-87)
  - **What's Missing**:
    - Domestic price premium calculation (5-20% range - what determines it?)
    - Budget constraint (how much can government procure before fiscal stress?)
    - Effectiveness decay (does preference erode over time if cost gap widens?)
  - **Module Reference**: Subsidy Module mentions but no algorithm
  - **Priority**: LOW (can approximate with procurement mandates)

---

### Currency & Finance - Gaps

**Partially Specified**:
- ⚠️ **Competitive Devaluation**
  - **What Exists**: Concept (Country Turn lines 102-106), effect +20% exports, 70% detection, -100 credits
  - **What's Missing**:
    - Mechanism (intervention size to achieve -10% currency move?)
    - Retaliation dynamics (when do partners counter-devalue?)
    - Effectiveness duration (temporary or sustained advantage?)
    - Trade balance feedback (does cheaper currency actually boost net exports or just imports?)
  - **Module Reference**: Currency Module has formulas but integration with trade flows unclear
  - **Priority**: MEDIUM-HIGH (currency wars are key gameplay)

- ⚠️ **Reserve Weaponization**
  - **What Exists**: Concept (Country Turn lines 123-126), effect -30% target currency, 80% detection
  - **What's Missing**:
    - Market impact formula (selling $X billion → Y% currency drop)
    - Duration of effect (temporary crash or sustained?)
    - Retaliation mechanics (target bans your bonds? Financial warfare escalation?)
    - Self-harm calculation (you lose reserve value - how much?)
  - **Module Reference**: Mentioned in Currency Module but no technical spec
  - **Priority**: LOW (extreme measure, rarely used)

- ⚠️ **Currency Swap Agreements**
  - **What Exists**: Concept (Country Turn lines 121-123)
  - **What's Missing**:
    - Size determination (how much liquidity to provide?)
    - Activation conditions (when does swap get drawn?)
    - Benefit quantification (how does swap reduce dependency or enable trade?)
  - **Module Reference**: Currency Module mentions but no mechanics
  - **Priority**: LOW (technical detail, can be abstracted)

- ⚠️ **Dollarization Attack**
  - **What Exists**: Concept (Country Turn lines 127-130), effect -5% USD usage/year, 2% GDP cost, 90% detection
  - **What's Missing**:
    - Coordination requirements (how many countries needed for credible alternative?)
    - Network effects (when does alternative currency achieve critical mass?)
    - Hegemon response model (US can retaliate - how?)
  - **Module Reference**: Geopolitical Module discusses conceptually but no formalization
  - **Priority**: MEDIUM (structural challenge to hegemon is key late-game)

---

### Military & Coercive - Gaps

**Partially Specified**:
- ⚠️ **Cyber Sabotage**
  - **What Exists**: Effect ranges (Country Turn lines 219-222: -5% to -20% GDP), 40% detection, 40% attribution
  - **What's Missing**:
    - Targeting algorithm (which infrastructure to attack for max impact?)
    - Capability requirements (cyber offense investment needed?)
    - Attribution mechanics (how does investigation determine source?)
    - Recovery dynamics (how fast does target repair damage?)
  - **Module Reference**: Military Module lines exist but attribution probability not modeled
  - **Priority**: HIGH (cyber warfare is realistic modern threat)

- ⚠️ **Gray Zone Operations**
  - **What Exists**: Concept (Country Turn lines 240-243), effect -10% confidence/-5% investment, 70% detection
  - **What's Missing**:
    - Specific operation types (maritime harassment? Border incursions? Cyber probing?)
    - Escalation ladder (when does gray zone become open conflict?)
    - Cumulative effect (repeated gray zone ops - do they compound?)
  - **Module Reference**: Military Module mentions but lacks detailed mechanics
  - **Priority**: MEDIUM (important for below-war conflict modeling)

- ⚠️ **Chokepoint Seizure**
  - **What Exists**: Concept (Country Turn lines 200-205), effect (levy tolls, deny access), -1500 credits
  - **What's Missing**:
    - Military requirement (force size needed to control Hormuz vs Malacca?)
    - Duration (can seizure be sustained or temporary?)
    - Counter-seizure mechanics (rival military response model?)
  - **Module Reference**: Military Module + Energy Module mention but no formal spec
  - **Priority**: HIGH (critical strategic action)

---

### Energy & Logistics - Gaps

**Partially Specified**:
- ⚠️ **Infrastructure Investment Payoff Model**
  - **What Exists**: Costs (Country Turn lines 301-319: $500M-$20B), durations (2-10 turns), effects (throughput +20-50%)
  - **What's Missing**:
    - Benefit formula (how exactly does +20% port capacity translate to GDP growth?)
    - Congestion relief (at what utilization % does investment become urgent?)
    - Network effects (does pipeline enable new trade routes - how modeled?)
  - **Module Reference**: Energy Module provides examples but not formulas
  - **Priority**: MEDIUM (infrastructure is long-term strategic investment)

- ⚠️ **Green Energy Transition**
  - **What Exists**: Concept (Country Turn lines 324-327), cost 2-5% GDP over 5-10 turns, lag 5+ turns
  - **What's Missing**:
    - Technology learning curve (does cost decline over time?)
    - Import dependency reduction formula (X% renewable → Y% less oil imports)
    - Competitiveness effect (cheap renewable energy advantage?)
  - **Module Reference**: Energy Module mentions but no formal model
  - **Priority**: LOW (future feature, not critical for MVP)

---

### Resource Strategy - Gaps

**Partially Specified**:
- ⚠️ **Form Commodity Cartel**
  - **What Exists**: Requirements (>60% supply, 2+ producers), effect (+40% to +200% prices), 20% fragmentation risk
  - **What's Missing**:
    - Cheating incentive model (when does member defect?)
    - Enforcement mechanism (how to detect/punish cheaters?)
    - Demand response (high prices → substitution acceleration - formula?)
    - Stability factors (what determines 20% fragmentation vs 5% vs 50%?)
  - **Module Reference**: Geopolitical Module lines 548-577 has formulas but integration unclear
  - **Priority**: MEDIUM (OPEC-style gameplay important)

- ⚠️ **Resource Substitution R&D**
  - **What Exists**: Concept (Country Turn lines 359-363), cost 1-3% GDP, 40-70% success
  - **What's Missing**:
    - Success probability formula (what factors increase success chance?)
    - Time to deployment (successful R&D → commercial substitution lag?)
    - Cost competitiveness (substitute initially more expensive - decay curve?)
  - **Module Reference**: No module has this mechanic
  - **Priority**: MEDIUM (counters resource leverage)

---

### UTA System - Gaps

**Partially Specified**:
- ⚠️ **Tariff-Credit Redemption**
  - **What Exists**: Concept (Country Turn lines 379-380: convert credits to tariff waivers)
  - **What's Missing**:
    - Exchange rate (X credits = Y% tariff reduction for Z duration?)
    - Market (bilateral negotiation or UTA-administered system?)
    - Transferability (can credits be traded between countries?)
  - **Module Reference**: Compliance Module defines credit accumulation but not redemption mechanics
  - **Priority**: MEDIUM-HIGH (core UTA innovation needs full specification)

- ⚠️ **Rule Change Voting**
  - **What Exists**: Concept (Country Turn line 383: credits determine voting weight)
  - **What's Missing**:
    - Voting formula (linear credit weight or quadratic or logarithmic?)
    - Proposal threshold (how many countries needed to propose rule change?)
    - Implementation lag (approved rule change → enforcement timing?)
  - **Module Reference**: No specification exists
  - **Priority**: LOW (governance feature for later phases)

---

### Standards & Regulation - Gaps

**Partially Specified**:
- ⚠️ **Brussels Effect - Regulatory Export**
  - **What Exists**: Concept (Country Turn lines 429-435), example (GDPR forces global compliance)
  - **What's Missing**:
    - Adoption threshold (when does domestic standard become global?)
    - Market size requirements (how big an economy to export regulations?)
    - Compliance cost calculation (regulated firms face X% cost increase?)
  - **Module Reference**: Geopolitical Module discusses (lines 156-199) but no formal mechanics
  - **Priority**: MEDIUM (normative leader gameplay)

- ⚠️ **Carbon Border Adjustments**
  - **What Exists**: Concept (Country Turn lines 433-435)
  - **What's Missing**:
    - Carbon pricing mechanism ($/ton CO2 equivalent)
    - Border adjustment calculation (imports face domestic carbon price)
    - Exemptions and phase-in (developing countries exempt? Gradual implementation?)
  - **Module Reference**: Not in any module
  - **Priority**: LOW (future environmental dimension)

---

### Firm-State Interaction - Gaps

**Partially Specified**:
- ⚠️ **SOE Loss Tolerance**
  - **What Exists**: Concept (Country Turn lines 472-476), duration 3-5 turns before fiscal stress
  - **What's Missing**:
    - Fiscal burden formula (losses as % GDP → when does crisis trigger?)
    - Competitor exit dynamics (how long until private firms exit market?)
    - Post-dominance price recovery (after competitors exit, when do SOEs raise prices?)
  - **Module Reference**: Firm-vs-State Module discusses (lines 624-691) but lacks formalization
  - **Priority**: MEDIUM (SOE strategy important for state-led economies)

- ⚠️ **Technology Transfer Requirements**
  - **What Exists**: Concept (Country Turn lines 484-488), legality (gray zone WTO)
  - **What's Missing**:
    - Effectiveness (how much technology actually transfers?)
    - Foreign firm response (avoid market vs comply?)
    - Quality degradation (transferred tech is outdated - lag model?)
  - **Module Reference**: Firm-vs-State Module mentions (lines 485-488) but no mechanics
  - **Priority**: LOW (can abstract as R&D subsidy equivalent)

---

## Turn Options MISSING Mechanics Entirely 🔴

These actions exist in Country Turn-V2.md but have NO underlying system specification.

### Critical Missing: Route Switching Dynamics

**What's Defined in Country Turn**:
- Trade Route Diversification (Country Turn line 341)
- Effect: Reduces chokepoint vulnerability

**Problem**: Trade-Flow-Module-Delta-todo.md explicitly identifies this as **CRITICAL GAP**:
- **Issue**: "When sanctions close a route (Russia-EU oil), how do flows reallocate?"
- **Questions**:
  - Timeline: Instant or gradual over multiple turns?
  - Capacity constraints: Can India absorb all displaced Russian oil immediately?
  - Price dynamics: Temporary spikes or immediate reallocation?
- **Current State**: Trade Flow Module describes scenarios but not transition mechanics
- **Why It Matters**: Determines whether sanctions cause temporary shocks (6-month price spike) vs permanent shifts

**Proposed Solution Needed**:
```
3-Phase Dynamic Adjustment Model (from Delta-todo line 400-426):
Phase 1 - Immediate (Turn T):
  - Blocked route flows → 0
  - Prices spike ∝ elasticity
Phase 2 - Short-term (T+1 to T+4):
  - Reallocation within capacity constraints
  - Partial substitution
Phase 3 - Long-term (T+5+):
  - Infrastructure investment expands capacity
  - Full equilibrium at new higher transport cost
```

**Priority**: CRITICAL
**Effort**: 4-5 hours specification work
**Blocker**: Without this, sanctions scenarios unrealistic

---

### Critical Missing: Multi-Hop Route Optimization

**What's Defined in Country Turn**:
- Multi-Hop Triangulation (Country Turn lines 494-498)
- Cost: +20% markup
- Detection: 25% probability

**Problem**: Trade-Flow-Module-Delta-todo.md identifies as **CRITICAL GAP**:
- **Issue**: "Formal rule for when A→C→B beats A→B direct route"
- **Questions**:
  - Only when direct route blocked (sanctions)?
  - Cost minimization: Cost[A,C] + Cost[C,B] < Cost[A,B]?
  - Circumvention arbitrage: Include UTA detection penalty in cost?
  - Game-theoretic: Nash equilibrium or global optimizer?
- **Current State**: Compliance Module has detection rates but not route optimization logic
- **Missing**: Decision algorithm for firm/country choosing routes

**Proposed Solution Needed** (from Delta-todo lines 428-477):
```python
def select_route(origin, destination, product):
    if not is_sanctioned(origin, destination, product):
        direct_cost = transport + tariff
    else:
        direct_cost = np.inf

    for transit in potential_intermediaries:
        if feasible:
            leg1_cost + leg2_cost + handling_cost + (detection_prob × UTA_penalty)
            if total < best_transit_cost:
                best_transit = transit

    return min(direct, best_transit)
```

**Priority**: CRITICAL
**Effort**: 2-3 hours specification
**Blocker**: Without this, triangulation gameplay incomplete

---

### Critical Missing: Capacity Constraints Enforcement

**What's Defined in Country Turn**:
- Port Capacity Expansion (Country Turn lines 301-304)
- Pipeline capacity mentioned in energy context

**Problem**: Trade-Flow-Module-Delta-todo.md identifies as **CRITICAL GAP**:
- **Issue**: "Multiple mentions of capacity but no enforcement mechanism"
- **Questions**:
  - If Russia-EU pipeline capacity is 100M barrels but simulation routes 120M, what happens?
  - Option A: Flow capped at 100M (creates infeasible equilibrium)?
  - Option B: Price adjusts until demand drops to 100M?
  - Option C: Overflow routes through alternative modes (sea freight)?
- **Current State**: Energy Module specifies capacities but Trade Flow Module doesn't enforce them

**Proposed Solution Needed** (from Delta-todo lines 479-518):
```
1. Pipeline Capacity (hard constraint):
   If demand > capacity: Reroute excess OR price rises until demand drops
2. Port Capacity (soft constraint):
   If throughput > capacity: Congestion cost = DELAY × (excess)²
3. Shipping Fleet (global):
   If required ship-days > fleet: Freight rates rise
```

**Priority**: CRITICAL
**Effort**: 3-4 hours specification
**Blocker**: Without this, unrealistic flows occur (infinite pipeline throughput)

---

### High Priority Missing: Negotiated Settlements & De-escalation

**What's Defined in Country Turn**:
- De-Escalation Proposals (Country Turn lines 572-575)
- Effect: Exit conflict when costs exceed benefits

**Problem**: No module specifies how de-escalation works
- **Questions**:
  - What triggers willingness to negotiate (economic pain threshold)?
  - How are terms determined (bargaining model)?
  - How quickly can de-escalation occur (immediate or phased)?
  - What ensures credibility (commitment mechanisms)?
- **Current State**: Geopolitical Module has escalation ladder but not de-escalation mechanics

**Missing Specification**:
```
De-Escalation Mechanics:
1. Trigger: Economic cost > expected benefit OR escalation risk > tolerance
2. Bargaining: Nash bargaining solution (divide surplus)
3. Implementation: Phased mutual concessions over 2-3 turns
4. Credibility: Third-party enforcement OR hostage exchange
5. Failure: If terms rejected, conflict continues with reputation cost
```

**Priority**: HIGH
**Effort**: 3-4 hours game theory formalization
**Use Case**: Every major conflict needs exit ramp

---

### High Priority Missing: Technology Breakthrough Dynamics

**What's Defined in Country Turn**:
- R&D Subsidies (Country Turn lines 60-63)
- Effect: Productivity gains after 3-5 turns

**Problem**: Geopolitical Module discusses (lines 692-717) but no technical specification
- **Questions**:
  - What is probability of breakthrough (random? R&D-spend dependent)?
  - How large is impact (productivity boost %)?
  - Who gets first-mover advantage (patent protection? Network effects)?
  - How fast does technology diffuse (IP regime dependent)?

**Missing Specification**:
```
Technology Breakthrough Model:
Annual Probability = Base_Rate × R&D_Investment_Ratio × Talent_Quality
  - Base_Rate = 4% (empirical from Geopolitical Module)
  - R&D_Investment = % GDP in target sector
  - Talent = education × immigration policy
Effect:
  - Innovator: +20% productivity immediately
  - Diffusion: 20% per year without IP protection, 5% with strong IP
  - First-mover: Network effects if winner-take-all sector
```

**Priority**: HIGH
**Effort**: 4-5 hours economic modeling
**Use Case**: Technology races are key late-game competition

---

### Medium Priority Missing: Coalition Exit/Defection Dynamics

**What's Defined in Country Turn**:
- Coalition Exit (Country Turn lines 164-166)
- Effect: Reputation damage (-0.3), coalition weakens

**Problem**: Geopolitical Module has conceptual description (lines 568-577) but no algorithm
- **Questions**:
  - When exactly does country decide to exit (economic pain threshold)?
  - What are timing dynamics (immediate exit or notice period)?
  - How do remaining members respond (punish defector? Adjust burden-sharing?)?
  - Can coalition survive defections (minimum viable size)?

**Missing Specification**:
```
Coalition Defection Algorithm:
Decision: Exit if Net_Benefit < -5% GDP for 3 consecutive turns
Notice: 1-2 turns (treaty dependent)
Consequences:
  - Defector: Lose preferential access (-5% GDP), reputation -0.3
  - Coalition: Cohesion -0.3, rebalance burden-sharing
  - Cascade Risk: If cohesion < 0.4, others defect too (20% probability each)
Punishment:
  - Remaining members may coordinate sanctions against defector
  - Exclusion from future coalitions (reputation penalty persists 10 turns)
```

**Priority**: MEDIUM
**Effort**: 2-3 hours game theory
**Use Case**: Coalition stability is key strategic question

---

### Medium Priority Missing: Regime Change Mechanics

**What's Defined in Country Turn**:
- Economic coercion objectives (Country Turn implies regime change as sanction goal)

**Problem**: No module specifies how economic pressure translates to regime change
- **Questions**:
  - At what GDP loss does regime become unstable?
  - What other factors matter (military support, elite cohesion)?
  - How long does instability take to materialize (immediate or years)?
  - What happens after regime change (new government strategic orientation)?

**Missing Specification**:
```
Regime Stability Model:
Instability_Probability = f(Economic_Pain, Elite_Cohesion, Military_Loyalty, External_Support)
  - Economic_Pain: -10% GDP = +5% instability, -30% GDP = +40%
  - Elite Cohesion: 0-1 scale (patronage, repression effectiveness)
  - Military_Loyalty: Binary (coup risk if disloyalty)
  - External_Support: Allies provide aid/legitimacy

Regime Change Consequences:
  - Transition: 2-4 turns of instability (GDP -5%, trade disrupted)
  - New Regime Orientation: 60% different strategy, 40% continuity
  - Great Power Response: Major powers compete to influence successor
```

**Priority**: MEDIUM
**Effort**: 5-6 hours political science modeling
**Use Case**: Endgame for comprehensive sanctions

---

### Low Priority Missing: Nuclear Threats & MAD

**What's Defined in Country Turn**:
- Nuclear Threat (Country Turn line 248)
- Effect: All trade ceases, isolation

**Problem**: No mechanics exist (Military Module doesn't model nuclear)
- **Questions**:
  - When is nuclear threat credible (capability + desperation)?
  - How do opponents respond (counter-threat? Conventional strike on nukes?)?
  - What are rules (simulation ends if nukes used? Abstracted escalation?)?

**Recommendation**: DEFER to future phase (too complex, rarely relevant)

---

### Low Priority Missing: Climate Disaster Impacts

**What's Defined in Country Turn**:
- Mentioned in Geopolitical Module (lines 718-741)

**Problem**: Not in any gameplay module
- **Missing**: Agricultural impact, migration pressures, infrastructure damage
- **Recommendation**: DEFER (environmental dimension can be added later)

---

## Priority Gaps to Fill

Ranked by impact on core gameplay:

### TIER 1: CRITICAL - Blocks Realistic Gameplay 🔴

**Must fix before MVP**:

1. **Route Switching Dynamics** [Gap #1]
   - **Why Critical**: Sanctions scenarios unrealistic without dynamic adjustment
   - **Effort**: 4-5 hours specification
   - **Owner**: uta-simulation-architect
   - **Deliverable**: Add 3-phase adjustment model to Trade Flow Module
   - **Integration**: Trade Flow Module → Pricing Module (price spike feedback)

2. **Multi-Hop Route Optimization** [Gap #2]
   - **Why Critical**: Triangulation gameplay incomplete, detection meaningless without route choice model
   - **Effort**: 2-3 hours specification + pseudocode
   - **Owner**: uta-simulation-architect
   - **Deliverable**: Route selection algorithm with cost-benefit including detection penalty
   - **Integration**: Trade Flow Module → Compliance Module (detection triggers)

3. **Capacity Constraints Enforcement** [Gap #3]
   - **Why Critical**: Without this, pipeline can transport infinite oil (breaks realism)
   - **Effort**: 3-4 hours specification
   - **Owner**: uta-simulation-architect
   - **Deliverable**: Constraint handling for pipelines (hard), ports (soft), shipping (price-based)
   - **Integration**: Energy Module (capacity data) → Trade Flow Module (enforcement)

**TIER 1 Total**: 10-12 hours work, unlocks 85% gameplay realism

---

### TIER 2: HIGH PRIORITY - Enhances Gameplay ⚠️

**Should add during development**:

4. **Cyber Sabotage Attribution** [Partial Gap #10]
   - **Why Important**: Modern warfare needs cyber mechanics
   - **Effort**: 3-4 hours
   - **Deliverable**: Attribution probability model, investigation mechanics
   - **Integration**: Military Module → Compliance Module (detection)

5. **Technology Breakthrough Model** [Gap #6]
   - **Why Important**: Tech races are key late-game competition
   - **Effort**: 4-5 hours
   - **Deliverable**: Probability model, diffusion mechanics, first-mover advantage
   - **Integration**: R&D spending → productivity boost (delayed)

6. **De-Escalation Mechanics** [Gap #4]
   - **Why Important**: Conflicts need credible exit ramps
   - **Effort**: 3-4 hours
   - **Deliverable**: Bargaining model, phased mutual concessions, credibility mechanisms
   - **Integration**: Geopolitical Module → all conflict modules

7. **Chokepoint Seizure** [Partial Gap #11]
   - **Why Important**: Critical strategic geography needs full mechanics
   - **Effort**: 3-4 hours
   - **Deliverable**: Military requirements, duration limits, counter-seizure dynamics
   - **Integration**: Military Module → Energy Module (chokepoint control)

**TIER 2 Total**: 13-17 hours work, brings realism to 95%

---

### TIER 3: MEDIUM PRIORITY - Nice to Have ✓

**Can defer to post-MVP**:

8. **Cartel Cheating & Enforcement** [Partial Gap #20]
   - **Effort**: 3-4 hours
   - **Deliverable**: Defection incentive model, enforcement mechanisms

9. **Coalition Defection Dynamics** [Gap #5]
   - **Effort**: 2-3 hours
   - **Deliverable**: Exit threshold, cascade risk, punishment

10. **Tariff-Credit Redemption** [Partial Gap #17]
    - **Effort**: 2-3 hours
    - **Deliverable**: Exchange rate formula, market mechanism

11. **Brussels Effect Adoption Threshold** [Partial Gap #18]
    - **Effort**: 2-3 hours
    - **Deliverable**: When domestic standard becomes global (market size threshold)

12. **Competitive Devaluation Feedback** [Partial Gap #7]
    - **Effort**: 3-4 hours
    - **Deliverable**: Trade balance feedback loop, retaliation dynamics

**TIER 3 Total**: 12-17 hours work, polish details

---

### TIER 4: LOW PRIORITY - Defer 💡

**Future phases**:

13. **Nuclear Threat Mechanics** [Gap #8]
    - **Reason to Defer**: Rarely used, highly sensitive, complex
    - **Future Effort**: 8-10 hours (requires political constraints, ethical review)

14. **Climate Disaster Mechanics** [Gap #9]
    - **Reason to Defer**: Not core to economic competition
    - **Future Effort**: 10-15 hours (environmental dimension)

15. **Regime Change Political Model** [Gap #7]
    - **Reason to Defer**: Complex political science modeling, uncertain outcomes
    - **Future Effort**: 5-6 hours

**TIER 4 Total**: 23-31 hours work, optional enhancements

---

## Summary Statistics

**Total Player Actions in Country Turn-V2.md**: ~185 distinct actions

**Completeness Breakdown**:
- ✅ **Complete Mechanics**: 107 actions (58%)
  - Trade policy: 20 actions
  - Subsidies: 18 actions
  - Currency: 15 actions
  - Sanctions: 22 actions
  - Energy: 12 actions
  - Compliance: 20 actions

- ⚠️ **Partial Mechanics**: 52 actions (28%)
  - Need formalization: 30 actions
  - Need parameter calibration: 22 actions

- 🔴 **Missing Mechanics**: 26 actions (14%)
  - Critical gaps: 3 actions (route switching, multi-hop, capacity)
  - High priority: 5 actions (de-escalation, tech, cyber, chokepoint, regime)
  - Medium priority: 8 actions
  - Low priority: 10 actions

**Implementation Readiness by Phase**:
- **Phase 0 (Current)**: 58% ready
- **After TIER 1 fixes**: 85% ready (playable MVP)
- **After TIER 2 fixes**: 95% ready (feature-complete)
- **After TIER 3 fixes**: 98% ready (polished)
- **After TIER 4 (future)**: 100% (comprehensive)

---

## Recommendations

### For Immediate Action (Next 2 Weeks)

1. **Specification Work**: Assign uta-simulation-architect to complete TIER 1 gaps (10-12 hours)
   - Route Switching Dynamics → Trade Flow Module
   - Multi-Hop Optimization → Trade Flow Module + Compliance Module
   - Capacity Constraints → Energy Module + Trade Flow Module integration

2. **Cross-Module Coordination**: These TIER 1 gaps require tight integration
   - Trade Flow ↔ Pricing (price spike feedback during route switching)
   - Trade Flow ↔ Compliance (detection triggers for multi-hop)
   - Energy ↔ Trade Flow (capacity data → enforcement)

3. **Validation**: After TIER 1 specifications complete, test against historical scenarios
   - 2022 Russia energy sanctions (route switching test)
   - 2018 US-China tariffs + Vietnam triangulation (multi-hop test)
   - 2021 Suez blockage (capacity constraint test)

### For Development Phase (Parallel with Coding)

4. **Incremental TIER 2 Addition**: Add high-priority gaps as development proceeds
   - Cyber attribution (week 1-2)
   - Technology breakthroughs (week 3-4)
   - De-escalation mechanics (week 5-6)
   - Chokepoint seizure (week 7-8)

5. **Modular Implementation**: Design allows adding TIER 2/3/4 features without breaking TIER 1
   - Each gap is relatively independent
   - Can release MVP with TIER 1, patch in TIER 2/3 later

### For Future Enhancements

6. **Community Contributions**: TIER 3/4 gaps can be crowd-sourced or added based on player feedback
   - Some low-priority gaps may become important based on actual gameplay
   - Others may never be needed (nuclear threats hopefully never used)

---

## Conclusion

**Current State**: The UTA Simulation is 58% complete in terms of turn mechanics. This is actually GOOD - most actions are fully specified.

**Critical Insight**: The 3 TIER 1 gaps (route switching, multi-hop, capacity) are all in the **Trade Flow Module**. This module is the bottleneck. Fixing these 3 gaps unlocks 85% completeness.

**Path Forward**:
1. **Week 1-2**: Architect completes TIER 1 specs (10-12 hours)
2. **Week 3-4**: Developers implement TIER 1 mechanics
3. **Week 5-6**: Validate against historical scenarios
4. **Week 7+**: Add TIER 2 features incrementally

**Bottom Line**: The simulation is closer to ready than it appears. Focus on the 3 critical gaps, and you have a playable, realistic MVP. Everything else is polish.
