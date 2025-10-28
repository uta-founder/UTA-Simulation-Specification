# Currency Strategy Module

## Purpose & Scope

The Currency Strategy Module models how countries manipulate exchange rates, manage monetary policy, and use financial instruments to gain competitive advantage in global trade. It captures the strategic tension between legitimate stabilization and covert manipulation, tracking every policy tool from interest rate adjustments to hidden FX interventions.

Currency policy is a critical strategic weapon in the UTA framework—countries can devalue currencies to boost exports, attract capital through interest rate hikes, or weaponize capital controls to insulate their economies. The module must capture both the direct economic effects (export competitiveness, inflation, capital flows) and the detection risks that trigger UTA enforcement.

This is where economic warfare meets financial engineering. Your choices here cascade through the entire simulation: a stealth devaluation can capture market share but risks detection penalties; aggressive capital controls can protect your economy but deter investment; forward guidance can shape expectations but invites gaming. Every tool has a tradeoff between economic gain and reputational risk.

## The Currency Game: What You're Actually Doing

When you adjust currency policy, you're pulling on levers that affect three interconnected systems:

**1. Trade Competitiveness**
- Weaken your currency → your exports become cheaper → you gain market share
- Strengthen your currency → your imports become cheaper → domestic consumers benefit
- But: Competitors can retaliate with their own devaluations (race to the bottom)

**2. Capital Flows**
- Raise interest rates → attract foreign capital → currency strengthens → exports suffer
- Lower interest rates → capital flees → currency weakens → exports benefit but inflation rises
- But: Capital controls can stop the flight, but investors punish you with risk premiums

**3. Financial Stability**
- Defend fixed exchange rate → credibility with investors → stable trade environment
- Sudden devaluation → crisis of confidence → capital flight → economic chaos
- But: Pegging is expensive (burns through reserves) and invites speculative attacks

The module tracks how you navigate these tradeoffs, how aggressively you push the boundaries, and whether the UTA detection system catches you gaming the rules.

## Your Strategic Toolkit: Currency Policy Instruments

### 1. Policy Interest Rate Setting

**What it is:** You set the benchmark interest rate for your economy, directly controlling borrowing costs and indirectly affecting currency value.

**How it works:**
```
If you raise rates by 1% → capital inflows increase → currency appreciates ~0.5-2%
If you lower rates by 1% → capital outflows increase → currency depreciates ~0.5-2%

The exact effect depends on:
- Credibility of your central bank (higher credibility = stronger effect)
- Size of your economy (large economies have global spillovers)
- Capital account openness (closed accounts mute the effect)
```

**Economic transmission:**
```
Interest Rate ↑ → Borrowing Cost ↑ → Investment ↓ → GDP ↓ (domestic drag)
                → Foreign Capital ↑ → Currency ↑ → Exports ↓ (trade channel)
                → Inflation ↓ (price stability benefit)
```

**Detection signature:**
- **Transparent:** Rate changes are public and highly visible
- **Compliance:** Legitimate tool, no UTA penalties if used reasonably
- **Red flag:** Extreme volatility (swings >5% in 30 days) suggests panic or manipulation

**Parameters:**
- **Rate range:** -1% to +20% (negative rates are exotic, >15% is crisis territory)
- **Impact on currency:** 0.5-2% appreciation per 1% rate increase
- **Impact on GDP:** -0.3% per 1% rate increase (short-term drag)
- **Impact on inflation:** -0.4% per 1% rate increase (medium-term cooling)
- **Lag structure:** Currency reacts immediately, GDP effect takes 2-3 periods, inflation takes 4-6 periods

**Strategic use:**
- **Stabilizer countries:** Keep rates steady around 2-4% (central bank orthodoxy)
- **Export maximizers:** Keep rates low (0-2%) to weaken currency despite inflation risk
- **Financial hub countries:** Use rates to attract capital (3-5%) while maintaining stability

### 2. Foreign Exchange (FX) Intervention

**What it is:** Your central bank buys or sells foreign currency in open markets to directly push your exchange rate up or down.

**Types of intervention:**

**A. Rule-Based (Transparent)**
- You announce targets: "We will keep USD/CNY between 6.0 and 7.0"
- Markets know your strategy and trade accordingly
- **Detection:** 0% risk (declared policy)
- **Effectiveness:** High (markets cooperate if you have credibility)
- **Cost:** Moderate (need reserves to defend the band)

**B. Covert (Stealth)**
- You secretly buy/sell currency through proxies, offshore accounts, or gradual accumulation
- Markets don't know you're intervening until patterns emerge
- **Detection:** 40-80% risk depending on volume and sophistication
- **Effectiveness:** Moderate (works until detected)
- **Cost:** High (market moves against you if discovered)

**Mechanics:**
```
FX Intervention Intensity = Net Central Bank FX Sales / Monetary Base

If you sell $10B foreign currency (to strengthen domestic currency):
→ Domestic money supply contracts by $10B
→ Currency appreciates by ~0.5-1.5% per $1B intervention (diminishing returns)
→ Reserves fall by $10B (shows up in balance of payments)

If you buy $10B foreign currency (to weaken domestic currency):
→ Domestic money supply expands by $10B
→ Currency depreciates by ~0.5-1.5%
→ Reserves increase by $10B (shows up as reserve accumulation)
```

**Detection signals:**
- **Reserve pressure index:**
  ```
  Reserve Pressure = -Δ(Official Reserves) / Monthly Imports

  Thresholds:
  - <0.02: Normal fluctuation (no flag)
  - 0.02-0.05: Mild pressure (monitoring)
  - 0.05-0.12: Moderate pressure (warning)
  - >0.12: Severe pressure (investigation triggered)
  ```

- **FX intervention intensity:**
  ```
  Intensity = |Central Bank Net FX Sales| / Money Base

  Thresholds:
  - <0.005: Normal market operations
  - 0.005-0.02: Moderate intervention
  - 0.02-0.05: Heavy intervention (flagged)
  - >0.05: Crisis intervention or manipulation
  ```

**Strategic use:**
- **Currency stabilizers:** Smooth short-term volatility (±2% bands)
- **Export maximizers:** Persistent one-way buying to accumulate reserves and weaken currency
- **Devaluation aggressors:** Sudden massive sales to force competitive devaluation
- **Pegged regimes:** Defend fixed rate at all costs (reserve burning)

**Cost-benefit tradeoff:**
```
Benefit: 1% currency depreciation → +0.8% export volume (after 6 months)
Cost: Reserve depletion → sovereign risk premium ↑ (if reserves < 3 months imports)
Detection penalty: -500 to -1500 UTA credits if covert intervention proven
```

### 3. Reserve Ratio Adjustments

**What it is:** You change how much liquid reserves banks must hold, indirectly controlling money supply and credit availability.

**Mechanics:**
```
Reserve Requirement = Required Reserves / Total Deposits

If you raise reserve ratio from 10% to 15%:
→ Banks must hold 5% more deposits as reserves
→ Less money available for lending
→ Credit contraction → reduced demand → currency strengthens slightly
→ Domestic economic activity slows (tightening effect)

If you lower reserve ratio from 10% to 5%:
→ Banks can lend 5% more of deposits
→ Credit expansion → increased demand → currency weakens slightly
→ Domestic stimulus effect
```

**Economic impact:**
```
Reserve Ratio ↑ by 1 percentage point:
→ Credit supply ↓ 0.5-1%
→ GDP ↓ 0.1-0.3% (mild drag)
→ Currency ↑ 0.2-0.4% (modest appreciation)
→ Inflation ↓ 0.1-0.2%

Typical range: 5% (light) to 20% (heavy) regulation
```

**Detection signature:**
- **Transparent:** Reserve requirements are public regulation
- **Detection risk:** 0% (legitimate policy tool)
- **Red flag:** Extreme volatility (>5% change in 1 month) suggests panic

**Strategic use:**
- Usually combined with interest rate policy (coordinated tightening/loosening)
- **Stabilizers:** Adjust gradually (±1% per quarter)
- **Aggressors:** Sudden drops (5-10%) to inject liquidity during currency defense
- **Controlled economies:** High ratios (15-20%) to constrain credit bubbles

### 4. Capital Controls

**What it is:** Restrictions on money flowing in or out of your country, insulating your economy from foreign pressure.

**Types of controls:**

**A. Inflow Controls (Hot Money Barriers)**
- Tax on foreign portfolio investment (Chile's encaje)
- Minimum holding periods (can't sell for 12 months)
- Limits on foreign ownership of domestic assets
- **Purpose:** Prevent destabilizing speculation and bubbles
- **Effect:** Reduces currency appreciation pressure, but deters long-term investment

**B. Outflow Controls (Capital Flight Prevention)**
- Restrictions on residents moving money abroad
- Mandatory approval for large transfers
- Limits on foreign currency purchases
- **Purpose:** Prevent crisis-driven capital flight
- **Effect:** Traps capital domestically, supports currency, but signals distress

**C. Dual Exchange Rates**
- Official rate for trade (low rate → cheap exports)
- Market rate for capital flows (high rate → discourage outflows)
- **Purpose:** Segment markets to control both trade and capital
- **Effect:** Creates arbitrage opportunities and black markets

**Capital Control Index:**
```
CCI = Weighted Average of:
- Inflow restrictions (0 = open, 1 = fully restricted)
- Outflow restrictions (0 = open, 1 = fully restricted)
- Currency conversion limits
- Foreign ownership caps
- Transaction approval requirements

Score 0.0 - 0.3: Open capital account (USA, UK, Switzerland)
Score 0.3 - 0.6: Moderate controls (Brazil, South Africa, India)
Score 0.6 - 0.9: Heavy controls (China, Russia, Turkey)
Score 0.9 - 1.0: Closed capital account (North Korea, Venezuela)
```

**Economic effects:**
```
Imposing capital controls (CCI ↑ 0.1):
→ Short-term currency support: +1-2% appreciation (trapped capital)
→ Medium-term risk premium: +50-150 basis points (investor fear)
→ FDI deterrence: -10-20% over 2 years (credibility damage)
→ Black market premium: +5-15% parallel exchange rate gap

Removing capital controls (CCI ↓ 0.1):
→ Initial outflow surge: -2-4% depreciation (pent-up demand released)
→ Long-term FDI increase: +15-30% (credibility gain)
→ Financial integration benefits
```

**Detection signature:**
- **Transparent:** Capital control policies are usually public (IMF reporting)
- **Detection risk:** 10-30% (hidden controls like informal guidance to banks)
- **Red flag:** Sudden imposition after policy failure (suggests panic)

**Strategic use:**
- **Financial hubs:** Never use (credibility depends on openness)
- **Emerging markets:** Moderate controls (0.4-0.6) to manage volatility
- **Aggressors:** Heavy controls (0.7-0.9) to enable sustained manipulation
- **Crisis defense:** Emergency controls when facing speculative attack

**Cost-benefit tradeoff:**
```
Benefit: Insulation from external shocks, policy autonomy
Cost: Higher borrowing costs (+50-200 bps), reduced FDI, black markets
UTA compliance: Moderate controls tolerated, extreme controls (>0.8) flagged
```

### 5. Forward Contract Offerings

**What it is:** Your central bank offers contracts that lock in future exchange rates, shaping market expectations and hedging trade.

**Types of forwards:**

**A. Commercial Hedging (Export Support)**
- Exporters can lock in favorable rates for future sales
- Example: Chinese exporter guaranteed USD/CNY = 7.0 in 6 months (even if spot moves to 7.5)
- **Purpose:** Reduce currency risk for exporters, encourage export activity
- **Effect:** Implicit currency guarantee → more exports → competitiveness boost
- **Detection risk:** 20-40% (if volume is disproportionate to trade needs)

**B. Market Intervention (Expectations Management)**
- Central bank sells forwards at target rate
- If forwards traded at 7.0 but you offer 6.5, signals your commitment to strengthen currency
- Markets anticipate your intervention → currency moves toward your target
- **Purpose:** Shift expectations without spending reserves immediately
- **Effect:** Cheaper than spot intervention initially, but you must deliver eventually
- **Detection risk:** 30-50% (if forward book is unbalanced or massive)

**Mechanics:**
```
Forward Rate vs Spot Rate Gap = Implied Interest Rate Differential

If spot = 7.0 and 6-month forward = 6.8:
→ Implies market expects 2.9% appreciation
→ Or equivalently: Domestic rates 2.9% lower than foreign rates

If you artificially offer forwards at 6.5 (below market):
→ You're subsidizing currency risk
→ Exporters over-hedge (moral hazard)
→ You accumulate forward losses if currency depreciates
```

**Detection signals:**
```
Forward Book Imbalance = |Long Positions - Short Positions| / GDP

Thresholds:
- <0.01: Normal hedging
- 0.01-0.03: Moderate intervention
- 0.03-0.05: Heavy intervention (flagged)
- >0.05: Manipulation or crisis hedging
```

**Strategic use:**
- **Stabilizers:** Provide balanced hedging (equal long/short)
- **Export maximizers:** Offer cheap export hedges (long domestic currency)
- **Speculators:** Build positions to profit from expected movements
- **Pegged regimes:** Use forwards to defend peg without immediate reserve drain

**Cost-benefit:**
```
Benefit: Low upfront cost, shapes expectations, supports exporters
Cost: Potential losses if you're wrong, creates moral hazard
Detection penalty: -300 to -800 UTA credits if subsidized hedging proven
```

### 6. Trade Invoicing Currency Shifts

**What it is:** You change which currency is used to price and settle international trade, affecting demand for your currency and competitors' currencies.

**Invoicing dynamics:**
```
Normal state: 60% of global trade invoiced in USD, 20% EUR, 10% CNY, 10% other

If China shifts oil imports from USD to CNY invoicing:
→ Demand for USD ↓ (fewer transactions need dollars)
→ Demand for CNY ↑ (oil sellers need yuan)
→ CNY appreciates 0.5-1% per 10% market share shift
→ USD weakens (reduced demand for reserve currency)
```

**Types of invoicing strategies:**

**A. Import Invoicing Shift**
- Change from paying in foreign currency to your own currency
- **Effect:** Increases demand for your currency, shifts exchange rate risk to exporters
- **Example:** China requires Saudi oil priced in yuan instead of dollars
- **Detection risk:** 0% (visible in trade data)
- **Leverage:** Requires market power (large importer)

**B. Export Invoicing Shift**
- Change from pricing in foreign currency to your own currency
- **Effect:** Increases demand for your currency, but may reduce competitiveness
- **Example:** EU insists on euro invoicing for Airbus jets
- **Detection risk:** 0% (commercial decision)
- **Leverage:** Requires product differentiation (unique goods)

**C. Settlement Currency Shift**
- Keep pricing in dominant currency but settle in your currency
- **Effect:** Hidden invoicing shift, still increases currency demand
- **Detection risk:** 20-40% (requires forensic trade data analysis)

**Trade Invoicing Asymmetry Index:**
```
Asymmetry = |Exports_A_to_B(A's data) - Imports_B_from_A(B's data)| / max(Exports, Imports)

If asymmetry > 0.15 for 3+ consecutive months:
→ Flag for investigation (invoicing games, transfer pricing, or smuggling)

Example:
- China reports $100M exports to USA (in CNY)
- USA reports $120M imports from China (in USD)
- Asymmetry = 20% (high) → Trigger review
```

**Economic effects:**
```
Shift 10% of trade from USD to CNY invoicing:
→ CNY demand ↑ 2-3%
→ CNY appreciation: +0.5-1%
→ Export competitiveness: ↓ 0.4-0.8% (offset by reduced FX risk)
→ Financial infrastructure investment needed (yuan clearing banks)

Timeline:
- Year 1: Bilateral agreements signed
- Year 2-3: Invoicing share shifts
- Year 4+: Currency appreciation effects stabilize
```

**Strategic use:**
- **Reserve currency issuers (USA, EU):** Defend dollar/euro dominance
- **Rising powers (China):** Gradual yuan internationalization
- **Commodity exporters:** Demand settlement in domestic currency if market power permits
- **Small economies:** Accept dominant currency invoicing (no leverage)

**Cost-benefit:**
```
Benefit: Currency demand ↑, reduced exchange rate risk for domestic firms
Cost: Reduced trade competitiveness (pricing in stronger currency), infrastructure investment
UTA compliance: Legitimate tool, no penalties (but asymmetries flagged for smuggling)
```

### 7. Forward Guidance (Expectations Management)

**What it is:** You publicly signal future policy intentions to shape market expectations and behavior without taking immediate action.

**Types of guidance:**

**A. Qualitative (Dovish/Hawkish Signals)**
- "We are concerned about currency strength and will act if necessary" (dovish → expect depreciation)
- "Inflation is our primary concern and we stand ready to tighten" (hawkish → expect appreciation)
- **Effect:** Markets pre-adjust based on anticipated policy
- **Detection risk:** 0% (public communication)

**B. Quantitative (Conditional Commitments)**
- "We will maintain rates at 2% until unemployment falls below 5%"
- "We will intervene if currency moves beyond ±3% of current level"
- **Effect:** Stronger signal, markets can hold central bank accountable
- **Detection risk:** 0% (public commitment)
- **Credibility risk:** If you don't follow through, future guidance ignored

**C. Implicit (Orchestrated Leaks)**
- "Unnamed central bank sources suggest intervention imminent"
- Friendly journalists telegraph policy without official statement
- **Effect:** Plausible deniability, test market reaction before committing
- **Detection risk:** 30-60% (if pattern emerges, UTA may flag as covert manipulation)

**Guidance effectiveness:**
```
Effectiveness = Credibility × Specificity × Surprise

Where:
- Credibility = Historical follow-through rate (0-1)
- Specificity = How concrete the commitment (vague = 0.3, precise = 0.9)
- Surprise = How unexpected the signal (anticipated = 0.2, shocking = 1.0)

Example:
- Fed with 90% credibility announces specific rate path (0.9 specificity): Effectiveness = 0.81
- Emerging market with 50% credibility gives vague signal (0.3 specificity): Effectiveness = 0.15
```

**Market reaction:**
```
Strong forward guidance (effectiveness 0.7+):
→ Currency moves 0.5-1.5% immediately (anticipating future policy)
→ Forward curve reprices (6-12 month expectations shift)
→ Option volatility decreases (less uncertainty)

Weak forward guidance (effectiveness 0.3-):
→ Currency moves <0.2% (markets skeptical)
→ Forward curve unchanged (not believed)
→ Option volatility increases (guidance adds noise)
```

**Strategic use:**
- **High credibility central banks (Fed, ECB, BoJ):** Powerful tool, markets hang on every word
- **Low credibility central banks:** Guidance ignored unless backed by immediate action
- **Stabilizers:** Clear, consistent guidance reduces volatility
- **Manipulators:** Misleading guidance to bait markets, then ambush with opposite action

**Cost-benefit:**
```
Benefit: Shape expectations cheaply (no reserve spending or rate changes needed)
Cost: Credibility damage if you break commitments (future guidance ineffective)
Detection penalty: -200 to -600 UTA credits if systemic deception detected (false guidance patterns)
```

## Currency Manipulation Strategies: The Full Playbook

This section catalogs 15+ manipulation tactics, ranked by detectability and economic impact.

### Strategy 1: Stealth Devaluation via FX Swaps

**What you're doing:** Using complex derivatives (FX swaps) to sell domestic currency without appearing in spot market data.

**How it works:**
```
1. Borrow foreign currency (USD) via short-term swap
2. Sell USD for domestic currency (increases domestic money supply)
3. Net effect: Currency depreciates like spot intervention
4. But: Swap accounting allows off-balance-sheet treatment
5. Detection requires derivative flow analysis
```

**Economic impact:**
- **Export boost:** +1.5-3% from 5% devaluation
- **Inflation:** +0.5-1.5% (imported goods more expensive)
- **Capital flows:** Neutral initially (swap is temporary financing)

**Detectability score:** 6/10 (Medium-High)
- Shows up in BIS derivatives data (quarterly lag)
- Requires sophisticated monitoring
- Confidence threshold: 0.65 (moderate certainty if detected)

**Typical duration:** 6-18 months before detected

**Target use cases:**
- Export-dependent economies facing recession
- Countries with declining competitiveness
- Retaliation for competitor devaluation

**UTA penalty if caught:** -800 credits, 6-month export credit suspension

### Strategy 2: Export Subsidies + Sterilization Combo

**What you're doing:** Subsidize exports to boost competitiveness, then use monetary policy to sterilize the inflationary effect, hiding the true scale of support.

**How it works:**
```
1. Provide 15% export subsidy (reduces export prices → gains market share)
2. Exports surge → foreign currency inflows → domestic currency should appreciate
3. You intervene: Buy foreign currency reserves (prevents appreciation)
4. But: This injects domestic money (inflationary)
5. You sterilize: Sell domestic bonds to absorb liquidity (neutralizes inflation)
6. Net effect: Export subsidy + stable currency + controlled inflation (triple benefit)
```

**Economic impact:**
- **Export boost:** +4-8% from combined subsidy + prevented appreciation
- **Fiscal cost:** High (subsidy spending + sterilization operations)
- **Trade balance:** Improves +2-5% of GDP

**Detectability score:** 7/10 (High)
- Subsidy shows up in fiscal data
- Sterilization visible in central bank balance sheet
- Connection requires cross-module analysis
- Confidence threshold: 0.75 (high certainty if full picture assembled)

**Typical duration:** 12-36 months (expensive to sustain)

**Target use cases:**
- Strategic industry capture (semiconductors, aerospace)
- Great power competition (China vs USA dynamics)
- Export-driven growth model

**UTA penalty if caught:** -1200 credits, countervailing duties authorized, 12-month UTA benefits suspension

### Strategy 3: Forced Devaluation from Capital Flight (Crisis Exploitation)

**What you're doing:** Engineer or exploit a crisis to justify devaluation, then maintain the weaker currency long after the crisis ends.

**How it works:**
```
1. Crisis hits (real or manufactured): Pandemic, banking crisis, political shock
2. Capital flees → currency depreciates 15-30%
3. You claim: "Market forces beyond our control" (technically true)
4. Crisis stabilizes, but you don't allow currency to recover
5. You benefit from persistent undervaluation
```

**Economic impact:**
- **Export boost:** +10-20% from major devaluation
- **Inflation:** +5-15% initially (crisis-driven), then stabilizes
- **Capital flows:** Massive outflows during crisis, gradual recovery

**Detectability score:** 4/10 (Medium-Low)
- Legitimate crisis provides cover
- Hard to prove intentional non-recovery
- Confidence threshold: 0.45 (low-moderate certainty)

**Typical duration:** 2-5 years (until competitiveness advantage absorbed)

**Target use cases:**
- Post-crisis recovery (2008, 2020 playbook)
- Excuse to reset exchange rate
- Opportunistic manipulation

**UTA penalty if caught:** -500 credits (hard to prove intent), monitoring requirements

### Strategy 4: Trade Invoicing Asymmetry Exploitation

**What you're doing:** Systematically misprice exports and imports through invoicing games, shifting currency demand patterns.

**How it works:**
```
1. Over-invoice exports (claim higher value than actual) → appears as export strength
2. Under-invoice imports (claim lower value than actual) → appears as import weakness
3. Net effect: Trade balance looks better than reality
4. Use trade data to justify currency policy
5. Meanwhile: Actual currency flows differ from reported trade
```

**Economic impact:**
- **Export volume:** Unchanged (pure accounting game)
- **Policy justification:** Enables aggressive devaluation ("our exports are booming!")
- **Statistical illusion:** GDP overstated by 1-3%

**Detectability score:** 8/10 (Very High)
- Trade data asymmetries with partner countries
- Customs declarations don't match port records
- Confidence threshold: 0.85 (very high certainty via cross-checks)

**Typical duration:** 3-12 months before flagged

**Target use cases:**
- Justify currency policy with fake data
- Hide sanctions evasion (under-report blacklisted imports)
- Inflate economic performance statistics

**UTA penalty if caught:** -1500 credits, forensic audit, potential trade restrictions

### Strategy 5: Shadow Reserve Accumulation

**What you're doing:** Build foreign exchange reserves through state-owned enterprises and sovereign wealth funds, bypassing central bank reporting.

**How it works:**
```
1. Central bank reports 6 months of import cover (adequate reserves)
2. Meanwhile: SOEs accumulate $50B in overseas assets
3. Sovereign wealth fund holds $100B in foreign securities
4. Total reserves: 18 months import cover (massive)
5. You can defend currency far longer than markets expect
6. When you intervene, markets panic (thought you had less firepower)
```

**Economic impact:**
- **Intervention capacity:** 3x official capacity
- **Exchange rate:** Can defend rate longer, amplified effect
- **Market surprise:** Causes speculator losses, deters future attacks

**Detectability score:** 5/10 (Medium)
- BIS tracks aggregate positions (but with lag)
- SOE financial statements often opaque
- Confidence threshold: 0.55 (moderate certainty)

**Typical duration:** Years (structural feature)

**Target use cases:**
- Pegged regimes with external surplus (Gulf states, China)
- Building war chest for future intervention
- Deterring speculative attacks

**UTA penalty if caught:** -600 credits, reporting requirements enhanced

### Strategy 6: Capital Control Gradualism

**What you're doing:** Slowly tighten capital controls through informal pressure rather than explicit regulation, avoiding detection.

**How it works:**
```
1. No official capital control regulation (CCI remains 0.3)
2. But: "Friendly" guidance to banks: "Please be cautious with foreign lending"
3. Banks comply (fear regulatory retaliation)
4. Foreign currency availability dries up
5. Net effect: De facto capital controls without policy change
6. Markets experience friction, but no smoking gun policy
```

**Economic impact:**
- **Capital outflows:** Reduced 30-50% (similar to formal controls)
- **Currency support:** +2-4% appreciation (trapped capital)
- **Risk premium:** +30-60 bps (markets sense friction)

**Detectability score:** 3/10 (Low-Medium)
- No formal policy to point to
- Requires pattern analysis of capital flows vs policy stance
- Confidence threshold: 0.35 (low certainty, mostly circumstantial)

**Typical duration:** 1-3 years before patterns become obvious

**Target use cases:**
- Politically sensitive capital flight
- Evading IMF or WTO commitments
- Emerging market financial repression

**UTA penalty if caught:** -400 credits, policy transparency requirements

### Strategy 7: Interest Rate Path Surprise (Bait and Switch)

**What you're doing:** Signal one policy path through forward guidance, then do the opposite to profit from market positioning.

**How it works:**
```
1. Signal dovish stance: "We expect to cut rates by 1% over next year"
2. Markets position for currency depreciation
3. You wait for maximum positioning
4. Suddenly: Emergency rate hike (+1.5% surprise)
5. Markets scramble to unwind positions
6. Your currency surges 5% (overshooting long-term equilibrium)
7. You lock in competitive advantage during the surge
```

**Economic impact:**
- **Currency gain:** +3-7% temporary surge
- **Export window:** 6-12 month competitiveness window
- **Credibility damage:** Future guidance ineffective (one-time trick)

**Detectability score:** 7/10 (High)
- Historical guidance vs action divergence analysis
- Confidence threshold: 0.70 (high if pattern emerges)

**Typical duration:** Single event (once credibility is burned, doesn't work again)

**Target use cases:**
- Desperate export boost
- Punishing foreign speculators
- One-time policy reset

**UTA penalty if caught:** -700 credits, reputation damage, forward guidance ignored

### Strategy 8: Triangular Hedging Arbitrage

**What you're doing:** Exploit differences in forward markets across three currencies to generate profitable hedging positions that indirectly weaken your currency.

**How it works:**
```
1. Identify arbitrage: EUR/USD = 1.10, EUR/CNY = 7.5, USD/CNY = 6.9 (implied 6.82)
2. Create triangular trades via state enterprises
3. Profit: 1.2% arbitrage gain
4. Side effect: Your trades shift forward curves
5. CNY forward curve steepens → signals expected depreciation
6. Market participants follow → CNY depreciates in spot
```

**Economic impact:**
- **Currency effect:** -0.5-1.5% depreciation (indirect)
- **Profit:** Arbitrage gains fund other interventions
- **Market distortion:** Forward markets become unreliable signals

**Detectability score:** 4/10 (Medium-Low)
- Requires forensic derivative flow analysis
- Looks like normal trading activity
- Confidence threshold: 0.40 (low-moderate certainty)

**Typical duration:** Ongoing (as long as arbitrage exists)

**Target use cases:**
- Sophisticated financial centers
- Countries with large SOE trading operations
- Hidden currency weakness signaling

**UTA penalty if caught:** -500 credits, derivative reporting requirements

### Strategy 9: Asymmetric Interest Rate Corridor

**What you're doing:** Set different borrowing and lending rates to create incentives for banks to bias credit flows in your preferred direction.

**How it works:**
```
1. Policy rate: 3% (official benchmark)
2. Lending facility rate: 2.5% (you lend to banks cheap)
3. Deposit facility rate: 4.0% (you pay banks high rates to deposit)
4. Net effect: Banks prefer to deposit rather than lend
5. Credit contraction → money supply tightens → currency appreciates
6. But: You claim policy rate is stable at 3% (no change reported)
```

**Economic impact:**
- **Effective tightening:** Equivalent to 0.5-1% rate hike
- **Currency appreciation:** +0.5-1.5%
- **Credit impact:** -2-5% lending growth

**Detectability score:** 6/10 (Medium-High)
- Facility rates are public but less scrutinized
- Requires monitoring corridor width
- Confidence threshold: 0.60 (moderate-high certainty)

**Typical duration:** 6-24 months

**Target use cases:**
- Import-dependent economies fighting inflation
- Covert tightening without political cost
- Financial stability operations

**UTA penalty if caught:** -600 credits, policy reporting enhanced

### Strategy 10: Reserve Currency Weaponization

**What you're doing:** If you issue a reserve currency, exploit that privilege to impose costs on others or benefit yourself beyond normal policy.

**How it works:**
```
1. You control USD (reserve currency)
2. You set domestic policy for domestic reasons (rate hike to fight inflation)
3. Side effect: Global tightening (everyone borrows in USD)
4. Competitor economies face credit crunch
5. Your economy benefits: Strong currency, capital inflows, financial dominance
6. This is legal but strategically devastating to others
```

**Economic impact:**
- **On you:** Currency +3-8%, capital inflows, financial sector profits
- **On others:** Credit crunch, capital flight, recession risk
- **Global:** Asymmetric adjustment (you export stability, import instability)

**Detectability score:** N/A (Legal but monitored)
- Exorbitant privilege is known and studied
- UTA monitors for *excessive* weaponization (e.g., cutting off access)
- Confidence threshold: 1.0 (always visible)

**Typical duration:** Permanent structural advantage

**Target use cases:**
- USA, Eurozone only
- Geopolitical leverage (financial sanctions)
- Macroeconomic stabilization at others' expense

**UTA penalty:** None unless combined with explicit sanctions (then Sanctions Module applies)

### Strategy 11: Dual Exchange Rate Gaming

**What you're doing:** Maintain separate exchange rates for trade vs capital flows, arbitraging the gap.

**How it works:**
```
1. Official rate (trade): 10 local currency/USD
2. Market rate (capital): 12 local currency/USD
3. You force exporters to surrender dollars at official rate (20% implicit tax)
4. You sell dollars to importers at market rate (20% margin)
5. Net effect: Currency appears stable, but you extract rents
```

**Economic impact:**
- **Export tax:** -20% implicit tax on exporters
- **Import subsidy:** -20% implicit subsidy to importers (if pass-through)
- **Fiscal gain:** Profits from spread (stealth taxation)
- **Black market:** Parallel exchange rate emerges (+30-50% premium)

**Detectability score:** 9/10 (Very High)
- Dual rates are visible (if official)
- Spreads are easily measured
- Confidence threshold: 0.95 (near certain)

**Typical duration:** Years (crisis measure that persists)

**Target use cases:**
- Crisis economies (Venezuela, Argentina historical examples)
- Heavy capital controls required (CCI > 0.8)
- When conventional tools exhausted

**UTA penalty if caught:** -1000 credits, trade normalization required for UTA benefits

### Strategy 12: Coordinated Devaluation Pact

**What you're doing:** Secretly coordinate with allied countries to jointly devalue, amplifying individual effects.

**How it works:**
```
1. Three countries agree: Simultaneously cut rates and intervene
2. Each alone would face retaliation
3. Together: Overwhelm trading partners' ability to respond
4. Net effect: Bloc gains competitiveness vs rest of world
```

**Economic impact:**
- **Bloc export gain:** +5-12% (amplified by coordination)
- **Rest of world:** Import surge, deflationary pressure
- **Retaliation risk:** If detected, triggers reciprocal devaluations (currency war)

**Detectability score:** 8/10 (Very High)
- Simultaneous timing is suspicious
- Requires wiretap-level evidence for certainty
- Confidence threshold: 0.80 (high if coordination proven)

**Typical duration:** Single coordinated move (hard to repeat)

**Target use cases:**
- Geopolitical bloc competition
- Regional trade pacts
- Currency war escalation

**UTA penalty if caught:** -2000 credits per country, bloc sanctions possible

### Strategy 13: Inflation Under-Reporting to Justify Low Rates

**What you're doing:** Manipulate CPI statistics to justify keeping interest rates low, maintaining weak currency.

**How it works:**
```
1. True inflation: 6%
2. Reported inflation: 3% (via substitution bias, quality adjustments)
3. Policy justification: "Inflation under target, we keep rates at 1%"
4. Real rate: -5% (massively negative) → capital flight → currency depreciation
5. Export competitiveness maintained
```

**Economic impact:**
- **Currency effect:** -2-5% depreciation vs true neutral policy
- **Export boost:** +1.5-4%
- **Domestic distortion:** Savings destroyed, asset bubbles

**Detectability score:** 5/10 (Medium)
- Requires forensic price data collection
- Compare official CPI to private indices (MIT Billion Prices)
- Confidence threshold: 0.50 (moderate certainty)

**Typical duration:** Years (structural data issue)

**Target use cases:**
- Financial repression (inflate away debt)
- Export competitiveness via stealth devaluation
- Political pressure for loose policy

**UTA penalty if caught:** -800 credits, independent statistics audit required

### Strategy 14: Pension Fund Currency Mandate

**What you're doing:** Require domestic pension funds to hold X% in domestic currency assets, creating artificial currency demand.

**How it works:**
```
1. Pension funds naturally diversify globally (currency exposure)
2. You mandate: "70% of assets must be domestic currency"
3. Funds repatriate foreign holdings
4. Capital inflows → currency appreciates +2-4%
5. This is structural, permanent demand
```

**Economic impact:**
- **Currency appreciation:** +2-4% from repatriation
- **Domestic capital:** Increased liquidity in domestic markets
- **Pension risk:** Concentrated exposure (bad for retirees)

**Detectability score:** 2/10 (Low)
- Domestic regulation, hard to challenge
- Looks like prudential requirement
- Confidence threshold: 0.25 (low certainty it's manipulation vs legitimate policy)

**Typical duration:** Permanent (structural regulation)

**Target use cases:**
- Countries with large pension systems (aging economies)
- Import-dependent economies fighting depreciation
- Financial stability justification (keep capital at home)

**UTA penalty if caught:** -300 credits (weak case for manipulation)

### Strategy 15: Crisis Reserve Release Timing

**What you're doing:** Strategically time release of strategic reserves (oil, commodities) to influence currency via commodity prices.

**How it works:**
```
1. You hold 100M barrels strategic oil reserve
2. Oil price spikes → import costs surge → currency weakens (oil-importing country)
3. You release 50M barrels → oil price crashes 15%
4. Import costs fall → currency stabilizes/appreciates
5. You refill reserves when prices low (cycle repeats)
```

**Economic impact:**
- **Import savings:** $10-30B (depending on oil import volume)
- **Currency effect:** +1-3% appreciation from improved terms of trade
- **Strategic benefit:** Price manipulation + currency stabilization

**Detectability score:** 1/10 (Very Low)
- Strategic reserves are sovereign right
- Release timing hard to prove as manipulation
- Confidence threshold: 0.15 (very low certainty)

**Typical duration:** Event-driven (crisis response)

**Target use cases:**
- Large oil importers (China, Japan, South Korea)
- Commodity price shocks
- Terms of trade management

**UTA penalty if caught:** -200 credits (weak case, mostly accepted practice)

### Strategy 16: Carry Trade Encouragement/Suppression

**What you're doing:** Deliberately create or eliminate carry trade opportunities to influence capital flows and currency.

**How it works:**
```
Carry trade: Borrow in low-rate currency, invest in high-rate currency, pocket the difference

Encouraging carry (to weaken your currency):
1. Keep domestic rates low (2%) while global rates are higher (4%)
2. Signal currency stability (reduce risk perception)
3. Capital flows out (seeking higher returns abroad)
4. Your currency depreciates -1-3%

Suppressing carry (to strengthen your currency):
1. Raise rates sharply above global rates (6% vs 4%)
2. Attract carry traders
3. Capital flows in (chasing your high rates)
4. Your currency appreciates +2-5%
```

**Economic impact:**
- **Capital flows:** $50-200B shifts (depending on economy size)
- **Currency volatility:** Increases (carry traders amplify moves)
- **Financial stability risk:** Carry unwind can be destabilizing

**Detectability score:** 3/10 (Low-Medium)
- Carry trades are market behavior, not policy
- Hard to prove intent vs natural rate setting
- Confidence threshold: 0.30 (low certainty)

**Typical duration:** 6-18 months (until rates adjust)

**Target use cases:**
- Emerging markets with rate flexibility
- Managed volatility strategies
- Capital flow management

**UTA penalty if caught:** -400 credits (circumstantial case)

## Detection Mechanisms: How You Get Caught

The UTA Detection System monitors four primary indicator categories, each with escalating alert thresholds.

### Indicator 1: Reserve Pressure Index

**What it measures:** How aggressively you're burning through foreign exchange reserves to defend your currency.

**Formula:**
```
Reserve Pressure = -Δ(Official Reserves) / Monthly Imports

Where:
- Δ(Official Reserves) = Change in central bank FX reserves (monthly)
- Monthly Imports = Average monthly import value (3-month rolling average)

Interpretation:
- If reserves fall $10B and monthly imports are $50B → Pressure = 0.20 (high)
- If reserves rise $5B and monthly imports are $50B → Pressure = -0.10 (accumulation)
```

**Thresholds and confidence scores:**

| Reserve Pressure | Status | Confidence | UTA Action |
|------------------|--------|------------|------------|
| < 0.02 | Normal fluctuation | 0.10 (background noise) | None |
| 0.02 - 0.05 | Mild pressure | 0.30 (monitoring) | Watchlist |
| 0.05 - 0.12 | Moderate pressure | 0.60 (investigation) | Request explanation |
| > 0.12 | Severe pressure | 0.85 (high confidence) | Formal investigation, credit restrictions |

**Short-term threshold (3 months):** 0.08 (sharp spike)
**Medium-term threshold (12 months):** 0.05 (sustained drain)
**Long-term threshold (36 months):** 0.03 (structural depletion)

**False positive reduction:**
- Exclude: Import surges due to natural disasters, seasonal patterns
- Adjust: For commodity price shocks (oil importers get buffer)
- Context: Pegged regimes expected to show intervention, scored differently

**What triggers escalation:**
```
IF Reserve Pressure > 0.12 for 3 consecutive months:
→ Formal investigation (confidence 0.85)
→ Credit restrictions: Temporary 50% reduction in UTA benefits
→ Transparency requirements: Weekly reserve data publication

IF Reserve Pressure > 0.15 for 6 consecutive months:
→ Crisis determination
→ Full UTA benefits suspension
→ IMF/WTO coordination for stabilization program
```

**Strategic insight:**
- Gradual reserve depletion (stay below 0.05) can continue for years undetected
- Spike-then-pause pattern (burn 0.15, pause 3 months, repeat) games the system
- Shadow reserves (Strategy 5) reduce detection by understating intervention capacity

### Indicator 2: FX Intervention Intensity

**What it measures:** How much your central bank is actively buying/selling currency relative to money supply.

**Formula:**
```
FX Intervention Intensity = |Central Bank Net FX Sales| / Monetary Base

Where:
- Central Bank Net FX Sales = Gross FX sales - Gross FX purchases (monthly)
- Monetary Base = Currency in circulation + bank reserves

Interpretation:
- If central bank sells $15B FX and money base is $300B → Intensity = 0.05 (very high)
- If net sales are $2B and money base is $400B → Intensity = 0.005 (moderate)
```

**Thresholds and confidence scores:**

| Intensity | Status | Confidence | UTA Action |
|-----------|--------|------------|------------|
| < 0.005 | Normal operations | 0.15 (routine) | None |
| 0.005 - 0.02 | Moderate intervention | 0.45 (monitoring) | Watchlist |
| 0.02 - 0.05 | Heavy intervention | 0.75 (investigation) | Request justification |
| > 0.05 | Extreme intervention | 0.90 (high confidence) | Formal audit, penalties |

**Direction matters:**
- **Persistent one-way intervention:** Same direction for 6+ months (confidence +0.15)
- **Bidirectional (stabilization):** Buy and sell in similar amounts (confidence -0.20, likely legitimate)

**Covert intervention detection:**
```
Intervention Opacity Index = 1 - (Reported Intervention / Estimated Intervention)

Where:
- Reported Intervention = Official central bank disclosures
- Estimated Intervention = Inferred from balance of payments + reserve changes

If Opacity > 0.30:
→ Confidence in manipulation increases by +0.25
→ Suggests unreported intervention via proxies, SOEs, or offshore accounts
```

**Escalation rules:**
```
IF Intensity > 0.05 for 2 consecutive months:
→ Formal investigation (confidence 0.90)
→ Credit penalty: -800 UTA credits
→ Export credit suspension: 6 months

IF Opacity > 0.50 (half of intervention hidden):
→ Confidence in covert manipulation: 0.95
→ Credit penalty: -1500 UTA credits
→ Mandatory derivative disclosure requirements
```

**Strategic insight:**
- Stay below 0.02 intensity (can intervene for years at "moderate" level)
- Use SOEs to split intervention across entities (reduces per-entity intensity)
- Sterilized intervention (buy FX, sell bonds) masks intensity in money base (shows up in bond yields instead)

### Indicator 3: Trade Invoicing Asymmetry

**What it measures:** Discrepancies between what you report as exports and what your trading partners report as imports from you.

**Formula:**
```
Trade Invoicing Asymmetry = |Exports_A_to_B(A's data) - Imports_B_from_A(B's data)| / max(Exports_A_to_B, Imports_B_from_A)

Where:
- Exports_A_to_B = Country A reports $X billion exports to Country B
- Imports_B_from_A = Country B reports $Y billion imports from Country A
- Typically Y > X due to CIF vs FOB accounting (transport costs), but large gaps are suspicious

Example:
- China reports $100B exports to USA
- USA reports $130B imports from China
- Asymmetry = 30 / 130 = 0.23 (high)
```

**Thresholds and confidence scores:**

| Asymmetry | Duration | Confidence | UTA Action |
|-----------|----------|------------|------------|
| < 0.10 | N/A | 0.10 (normal CIF/FOB gap) | None |
| 0.10 - 0.15 | 1-2 months | 0.35 (anomaly) | Routine review |
| 0.15 - 0.25 | 3+ months | 0.70 (likely manipulation) | Investigation |
| > 0.25 | 3+ months | 0.90 (high confidence) | Audit, penalties |

**Pattern analysis (increases confidence):**
```
Sudden asymmetry spike:
- If asymmetry was <0.10 for 12 months, then jumps to >0.20 → Confidence +0.20
- Suggests policy change or deliberate manipulation

Systematic bias:
- If asymmetry consistently one direction (A always under-reports) → Confidence +0.15
- Random errors would cancel out

Correlation with policy events:
- If asymmetry spikes after sanctions, tariffs, or currency moves → Confidence +0.25
```

**Root causes detected:**
- **Over/under-invoicing:** Transfer pricing games (multinational shuffling profits)
- **Smuggling:** Unreported trade (shows up as partner's imports, not your exports)
- **Triangulation:** Re-exports through third countries (inflates third country's asymmetry)
- **Currency manipulation:** Invoicing shifts to preferred currency (inflates reported values)

**Escalation rules:**
```
IF Asymmetry > 0.15 for 3 consecutive months:
→ Forensic trade audit (confidence 0.70)
→ Cross-check customs data, port records, satellite imagery
→ Temporary credit hold: 30% UTA benefits withheld pending investigation

IF Asymmetry > 0.25 confirmed after audit:
→ Manipulation/smuggling confirmed (confidence 0.90)
→ Credit penalty: -1200 UTA credits
→ Enhanced reporting requirements: Item-level trade data
```

**Strategic insight:**
- Small asymmetries (<0.12) are normal and ignored
- Distribute manipulation across many small partners (avoid single large spike)
- Use transit countries to obscure origin (complicates attribution)

### Indicator 4: Capital Flow Spike Detection

**What it measures:** Abnormal surges or crashes in capital flows that suggest policy manipulation or crisis.

**Formula:**
```
Capital Flow Spike = Rolling_30d(Net Portfolio Inflow) / Monthly GDP

Where:
- Net Portfolio Inflow = Foreign purchases of domestic assets - Domestic purchases of foreign assets
- Rolling 30-day window captures sudden movements
- Monthly GDP = GDP / 12 (normalization factor)

Interpretation:
- If $20B inflows in one month and monthly GDP is $500B → Spike = 0.04 (4% of GDP, very high)
- Normal volatility: ±0.005 (0.5% of GDP)
```

**Thresholds and confidence scores:**

| Spike (% GDP) | Direction | Confidence | UTA Action |
|---------------|-----------|------------|------------|
| < 0.005 | Either | 0.10 (normal) | None |
| 0.005 - 0.02 | Inflow | 0.30 (possible carry trade) | Monitor |
| 0.005 - 0.02 | Outflow | 0.40 (possible capital flight) | Monitor |
| 0.02 - 0.05 | Inflow | 0.60 (investigate) | Review interest rate policy |
| 0.02 - 0.05 | Outflow | 0.70 (crisis risk) | Stability check |
| > 0.05 | Either | 0.85 (crisis/manipulation) | Immediate investigation |

**Velocity analysis (amplifies confidence):**
```
Flow Acceleration = (Spike_t - Spike_t-1) / Spike_t-1

If flows spike AND accelerate:
→ Confidence increases by +0.20
→ Suggests coordinated move or policy shock

Example:
- Month 1: 1% GDP inflow (normal)
- Month 2: 3% GDP inflow (spike)
- Month 3: 6% GDP inflow (accelerating)
- Acceleration = 100% month-over-month → Investigation triggered
```

**Policy correlation detection:**
```
IF Capital Flow Spike > 0.03 occurs within 30 days of:
- Interest rate change > 1%
- New capital controls announced
- Forward guidance shock
- Currency intervention revealed

THEN:
→ Confidence in policy-induced manipulation: +0.30
→ Suggests deliberate capital flow management
```

**Escalation rules:**
```
IF Capital Flow Spike > 0.05 (5% GDP) in single month:
→ Emergency investigation (confidence 0.85)
→ Determine cause: Crisis vs manipulation vs carry trade

IF Crisis (involuntary):
→ Stability support offered, no penalties
→ Monitor for exploitation (Strategy 3: Forced Devaluation)

IF Manipulation (policy-induced):
→ Credit penalty: -1000 UTA credits
→ Capital control restrictions
→ Interest rate policy review
```

**Strategic insight:**
- Gradual capital flow shifts (<0.02/month) avoid detection
- Time policy changes with market events (provides cover)
- Use capital controls to dampen spikes (reduces visibility)

## Economic Impact System

Each currency policy action propagates through multiple economic channels. The module calculates impacts across six dimensions.

### Impact Dimension 1: Export Volume

**Transmission mechanism:**
```
Currency Depreciation → Export Prices Fall (in foreign currency) → Foreign Demand Increases → Export Volume Rises

Quantitative relationship:
ΔExport Volume (%) = ε_export × ΔExchange Rate (%)

Where:
- ε_export = Export price elasticity (2.0 for commodities, 0.8 for differentiated products)
- ΔExchange Rate = % change in currency (negative = depreciation)

Example:
- 5% depreciation (ΔE = -5%)
- Commodity exports: ΔVolume = 2.0 × 5% = +10%
- Differentiated exports: ΔVolume = 0.8 × 5% = +4%
```

**Impact ranges by product type:**

| Product Type | Elasticity | 1% Depr. Impact | 10% Depr. Impact |
|--------------|------------|-----------------|------------------|
| Commodities (oil, wheat) | 2.0 - 3.0 | +2.0% to +3.0% | +20% to +30% |
| Basic manufactures (steel) | 1.5 - 2.5 | +1.5% to +2.5% | +15% to +25% |
| Differentiated products (cars) | 0.8 - 1.5 | +0.8% to +1.5% | +8% to +15% |
| High-tech (semiconductors) | 0.4 - 0.8 | +0.4% to +0.8% | +4% to +8% |

**Lag structure:**
```
Month 0: Currency depreciates (immediate)
Month 1-3: Exporters adjust prices (gradual pass-through)
Month 4-6: Foreign buyers respond to new prices
Month 7-12: Full volume adjustment reached
Month 13+: Steady state (unless competitors retaliate)

Calibration:
- 25% of effect in months 1-3
- 50% of effect in months 4-6
- 100% of effect by month 12
```

**Confidence bands:**
```
Minimum impact: 0.5 × ε_export (pessimistic, strong competitors)
Median impact: 1.0 × ε_export (expected case)
Maximum impact: 1.8 × ε_export (optimistic, weak competitors, no retaliation)
```

**Integration with Trade Flow Module:**
```python
# Currency Module calculates price effect
export_price_effect = -exchange_rate_change * pass_through_rate

# Trade Flow Module receives price shock
for destination in destinations:
    demand_response = export_elasticity[product] * export_price_effect
    new_export_volume[destination] = old_volume * (1 + demand_response)

# Update bilateral flows and re-equilibrate
```

### Impact Dimension 2: Import Volume and Prices

**Transmission mechanism:**
```
Currency Depreciation → Import Prices Rise (in domestic currency) → Domestic Demand Decreases → Import Volume Falls

Quantitative relationship:
ΔImport Volume (%) = -ε_import × ΔExchange Rate (%)
ΔImport Price (domestic) (%) = +ΔExchange Rate (%) × pass-through

Where:
- ε_import = Import price elasticity (1.5 for necessities, 2.5 for discretionary)
- Pass-through = Fraction of exchange rate change reflected in prices (0.6-0.9)

Example:
- 5% depreciation (ΔE = -5%)
- Necessities: ΔVolume = -1.5 × 5% = -7.5%, ΔPrice = +5% × 0.8 = +4%
- Discretionary: ΔVolume = -2.5 × 5% = -12.5%, ΔPrice = +5% × 0.9 = +4.5%
```

**Impact ranges by import type:**

| Import Type | Volume Elasticity | Price Pass-Through | 5% Depr. Volume Impact | 5% Depr. Price Impact |
|-------------|-------------------|--------------------|-----------------------|-----------------------|
| Energy (oil, gas) | 0.5 - 1.0 | 0.95 - 1.00 | -2.5% to -5% | +4.75% to +5% |
| Food & necessities | 1.0 - 1.5 | 0.80 - 0.90 | -5% to -7.5% | +4% to +4.5% |
| Intermediate goods | 1.5 - 2.0 | 0.70 - 0.85 | -7.5% to -10% | +3.5% to +4.25% |
| Consumer discretionary | 2.0 - 3.0 | 0.60 - 0.80 | -10% to -15% | +3% to +4% |

**Terms of trade effect:**
```
Terms of Trade = (Export Price Index) / (Import Price Index)

Currency depreciation:
→ Export prices fall (in foreign currency) -5%
→ Import prices rise (in domestic currency) +5%
→ Terms of trade worsen by ~10%
→ Real income falls (import purchasing power declines)
```

**Integration with Pricing Module:**
```python
# Currency Module calculates import price shock
import_price_increase_domestic = exchange_rate_change * import_pass_through

# Pricing Module receives cost shock for firms using imported inputs
for firm in firms:
    input_cost_increase = import_share_of_inputs * import_price_increase_domestic
    marginal_cost_new = marginal_cost_old * (1 + input_cost_increase)

# Re-equilibrate to find new domestic prices
```

### Impact Dimension 3: Inflation (CPI)

**Transmission mechanism:**
```
Currency Depreciation → Import Prices ↑ → Consumer Prices ↑ → CPI Inflation ↑

Quantitative relationship:
ΔCPI (%) = import_share_CPI × ΔExchange Rate (%) × pass-through + second_round_effects

Where:
- import_share_CPI = Weight of imported goods in CPI basket (15-40% depending on economy)
- Pass-through = 0.60-0.90 (how much FX change hits consumer prices)
- Second-round effects = Wage-price spiral, expectations (0.2-0.5x initial shock)

Example:
- 10% depreciation
- Import share in CPI: 30%
- Pass-through: 0.70
- Direct effect: 30% × 10% × 0.70 = +2.1% CPI
- Second-round: 0.3 × 2.1% = +0.6% CPI
- Total inflation: +2.7%
```

**Impact ranges by economy type:**

| Economy Type | Import Share | Pass-Through | 10% Depr. → CPI Impact |
|--------------|--------------|--------------|-------------------------|
| Large closed (USA, EU) | 15-20% | 0.60 - 0.70 | +1.0% to +1.5% |
| Medium open (UK, Japan) | 25-35% | 0.70 - 0.80 | +2.0% to +3.0% |
| Small open (Switzerland, Singapore) | 40-50% | 0.80 - 0.90 | +3.5% to +5.0% |
| Commodity importer (oil-dependent) | 30-40% | 0.85 - 0.95 | +3.0% to +4.5% |

**Lag structure:**
```
Month 0-1: Currency depreciates, import prices rise (wholesale)
Month 2-4: Retail prices adjust (gradual pass-through)
Month 5-8: Peak inflation impact
Month 9-18: Second-round effects (wage adjustments, expectations)
Month 19+: Inflation returns to baseline (if policy credible)

Persistence:
- Temporary shock: Inflation spike then fade (12-18 months)
- Permanent depreciation: Inflation level shift, then stable
```

**Central bank response (feedback loop):**
```
IF Inflation > Target + 0.5%:
→ Central bank raises rates (0.5-1% per 1% excess inflation)
→ Currency appreciates (partially offsetting initial depreciation)
→ Net effect: Smaller long-run depreciation than initial shock

IF Central bank lacks credibility (history of missing targets):
→ Expectations unanchored
→ Second-round effects larger (0.5-1.0x vs 0.2-0.5x)
→ Inflation more persistent
```

### Impact Dimension 4: Trade Balance

**Transmission mechanism:**
```
Currency Depreciation → Exports ↑, Imports ↓ → Trade Balance Improves

Quantitative relationship (J-Curve effect):
ΔTrade Balance = (Export Volume Effect × Export Price) - (Import Volume Effect × Import Price)

Phase 1 (Months 0-6): Trade balance worsens
- Import prices rise immediately (existing contracts)
- Export volumes haven't adjusted yet
- Net effect: Pay more for imports, don't gain export revenue yet

Phase 2 (Months 7-18): Trade balance improves
- Export volumes increase (buyers respond to cheaper prices)
- Import volumes decrease (substitution to domestic goods)
- Net effect: Export gains exceed import price increase

Phase 3 (18+ months): Steady state
- Trade balance stabilized at new level
```

**J-Curve calibration:**

| Time Period | Trade Balance Impact | Mechanism |
|-------------|----------------------|-----------|
| Months 0-3 | -0.5% to -1.5% GDP | Price effect dominates (import bill rises) |
| Months 4-6 | -0.2% to -0.8% GDP | Volumes start adjusting |
| Months 7-12 | +0.5% to +2.0% GDP | Volume effect dominates |
| Months 13-18 | +1.0% to +3.0% GDP | Peak improvement |
| Months 19+ | +0.8% to +2.5% GDP | Steady state |

**Marshall-Lerner condition (when depreciation improves trade balance):**
```
ε_export + ε_import > 1

If satisfied:
→ Currency depreciation eventually improves trade balance (after J-curve)

If not satisfied:
→ Currency depreciation worsens trade balance permanently
→ Rare in practice (most elasticities sum to 2-4)
```

**Integration with Country Agents:**
```python
# Currency Module calculates trade balance impact
trade_balance_change = (export_gain - import_loss) # Net effect

# Country Agent evaluates currency policy success
policy_effectiveness = trade_balance_change / currency_depreciation_pct

# If effectiveness > 0.5% GDP per 1% depreciation → Policy deemed successful
# If effectiveness < 0.2% GDP per 1% depreciation → Policy deemed failed, consider reversal
```

### Impact Dimension 5: Capital Flows

**Transmission mechanism:**
```
Interest Rate ↑ → Return on Domestic Assets ↑ → Foreign Capital Inflows ↑ → Currency Appreciates

Quantitative relationship:
Capital Flow Change (% GDP) = β × ΔInterest Rate (%) × Capital Account Openness

Where:
- β = Sensitivity of capital flows to interest differential (0.3-0.8)
- Capital Account Openness = 1 - Capital Control Index (0-1 scale)

Example:
- 1% interest rate increase
- β = 0.5
- Capital Account Openness = 0.8 (moderately open)
- Capital Flow = 0.5 × 1% × 0.8 = +0.4% GDP inflow per period
```

**Impact ranges by policy tool:**

| Policy Tool | Capital Flow Impact (% GDP per unit change) | Confidence Band |
|-------------|---------------------------------------------|-----------------|
| 1% interest rate increase | +0.3% to +0.8% | ±0.2% |
| 5% currency depreciation | -0.5% to -1.2% (outflow) | ±0.3% |
| 0.1 increase in Capital Control Index | -0.8% to -1.5% (outflow deterred) | ±0.4% |
| Major forward guidance shift | +0.2% to +0.6% | ±0.3% |

**Carry trade amplification:**
```
Base capital flow = β × ΔInterest Rate
Carry trade multiplier = 1 + (carry_trade_share × leverage)

Where:
- carry_trade_share = Fraction of flows from leveraged strategies (0.1-0.3)
- leverage = Average leverage ratio (2-5x)

Example:
- Base flow: +0.4% GDP
- Carry trade share: 20%, Leverage: 3x
- Multiplier: 1 + (0.2 × 3) = 1.6
- Total flow: +0.4% × 1.6 = +0.64% GDP

Risk: Carry trades can reverse violently (sudden stop)
```

**Sudden stop scenario (crisis risk):**
```
IF Capital Flows > +2% GDP sustained for 12+ months:
→ Sudden stop risk increases (confidence 0.70)
→ If external shock occurs, flows can reverse to -3% GDP in 1 month
→ Currency depreciates 15-30% (crisis dynamics)

Mitigation:
- Impose moderate capital controls (CCI 0.3-0.5) to slow inflows
- Build reserves during inflow phase (self-insurance)
- Avoid excessive reliance on hot money
```

**Integration with Capital Control Index:**
```python
# Currency Module calculates net capital flows
interest_rate_effect = beta * interest_rate_change * (1 - capital_control_index)
exchange_rate_effect = gamma * exchange_rate_change * (1 - capital_control_index)
net_capital_flow = interest_rate_effect + exchange_rate_effect

# Feed back to exchange rate determination
exchange_rate_pressure = net_capital_flow / fx_market_liquidity
new_exchange_rate = old_exchange_rate * (1 + exchange_rate_pressure)
```

### Impact Dimension 6: GDP and Real Wages

**Transmission mechanism:**
```
Currency Depreciation → Net Exports ↑ (GDP boost) + Import Prices ↑ (Real Wage drag)

Net GDP effect = Export boost + Import substitution - Terms of trade loss - Investment disruption

Typical profile (10% depreciation):
- Short-term (0-6 months): GDP -0.5% to -1% (J-curve, uncertainty)
- Medium-term (6-18 months): GDP +1% to +2% (export gains dominate)
- Long-term (18+ months): GDP +0.5% to +1.5% (steady state)
```

**Real wage impact:**
```
Real Wage Change = Nominal Wage Change - CPI Inflation

Currency depreciation scenario:
- Nominal wages: +1% to +2% (slow adjustment)
- CPI inflation: +2% to +4% (faster adjustment)
- Real wages: -1% to -2% (workers lose purchasing power)

Distributional effect:
- Export sector workers: Gain (higher employment, eventual nominal wage increases)
- Import-competing sector: Mixed (employment up, but real wages lag)
- Non-tradable sector: Lose (pure inflation, no wage boost)
```

**Impact ranges by economy structure:**

| Economy Type | GDP Impact (10% depr.) | Real Wage Impact | Duration |
|--------------|------------------------|------------------|----------|
| Export-driven (Germany, China) | +1.5% to +3% | -1% to -2% | 12-24 months |
| Balanced (USA, UK) | +0.5% to +1.5% | -0.5% to -1.5% | 18-30 months |
| Import-dependent (oil importers) | -0.5% to +1% | -2% to -3% | 24-36 months |
| Commodity exporter (terms of trade boost) | +2% to +4% | +0.5% to +1% | 12-18 months |

**Integration with CGE equilibrium:**
```python
# Currency Module calculates GDP and wage shocks
gdp_shock = export_boost + import_substitution - terms_of_trade_loss
real_wage_shock = nominal_wage_change - cpi_inflation

# CGE Pricing Module receives shocks
for sector in sectors:
    demand_shift = gdp_shock * sector_income_elasticity
    cost_shift = real_wage_shock * labor_cost_share[sector]

# Re-equilibrate economy with new demand and cost structure
# Iterate until market clearing
```

## Behavioral Archetypes: How Countries Play the Currency Game

The simulation includes five strategic templates representing different philosophies toward currency policy.

### Archetype 1: Currency Stabilizer

**Philosophy:** Minimize exchange rate volatility to provide predictable trade environment and attract long-term investment.

**Policy parameters:**
```python
class CurrencyStabilizer:
    interest_rate_rule = "Taylor Rule"  # Systematic, predictable
    target_inflation = 0.02  # 2% target
    target_exchange_rate_band = 0.03  # ±3% acceptable fluctuation

    fx_intervention_threshold = 0.04  # Intervene if outside ±4%
    intervention_intensity = "Moderate"  # 0.01-0.02 of monetary base
    capital_control_index = 0.1  # Very open (10% restrictions)

    forward_guidance_credibility = 0.85  # High credibility
    policy_transparency = 0.95  # Highly transparent
```

**Typical actions:**
- Interest rate adjustments: ±0.25% per period (gradual)
- FX intervention: Bidirectional (lean against wind)
- Capital controls: Minimal (only macroprudential)
- Forward contracts: Balanced hedging for exporters and importers
- Invoicing: Accept dominant currencies (USD, EUR)

**Economic outcomes:**
- Exchange rate volatility: Low (3-5% annual)
- Trade balance: Stable (deficit or surplus doesn't fluctuate wildly)
- Inflation: Stable (2-3% target range)
- Foreign investment: High (credibility premium)
- UTA compliance: Excellent (no flags)

**Strategic use cases:**
- Financial hubs (Switzerland, Singapore)
- Credible central banks (Fed, ECB, BoJ)
- Countries prioritizing financial stability over short-term gains

**Example countries:** Switzerland, Singapore, Netherlands, Canada

### Archetype 2: Export Maximizer

**Philosophy:** Maintain systematically undervalued currency to gain persistent export competitiveness and grow via trade surplus.

**Policy parameters:**
```python
class ExportMaximizer:
    interest_rate_bias = -0.01  # Keep rates 1% below neutral
    target_trade_balance = 0.05  # 5% GDP surplus target
    target_exchange_rate_undervaluation = 0.10  # 10% below PPP

    fx_intervention_direction = "One-way buying"  # Accumulate reserves
    intervention_intensity = "High"  # 0.03-0.05 of monetary base
    capital_control_index = 0.5  # Moderate controls (prevent appreciation)

    reserve_accumulation_target = 18_months_imports  # Large war chest
    policy_transparency = 0.60  # Moderate (some opacity helpful)
```

**Typical actions:**
- Interest rate adjustments: Keep low (0-2%)
- FX intervention: Persistent buying (accumulate reserves)
- Capital controls: Selective (restrict hot money inflows)
- Forward contracts: Subsidize export hedging
- Invoicing: Accept USD/EUR (don't push own currency)
- Detection risk: Moderate (35-55% detection probability over 5 years)

**Economic outcomes:**
- Exchange rate: 5-15% undervalued vs PPP
- Trade balance: Persistent surplus (3-7% GDP)
- Inflation: Slightly elevated (3-4%)
- Foreign reserves: Very high (>12 months imports)
- UTA compliance: Borderline (watchlisted, occasional penalties)

**Tradeoffs:**
- Benefit: Rapid export-driven growth, industrial capacity building
- Cost: Domestic consumption suppressed (real wages lag), UTA penalties (-500 to -1200 credits over 5 years)

**Strategic use cases:**
- Emerging industrial powers
- Export-oriented development model
- Building strategic manufacturing capacity

**Example countries:** China (2000-2015), Germany, South Korea, Taiwan

### Archetype 3: Devaluation Aggressor

**Philosophy:** Aggressively devalue currency to capture market share from competitors, willing to accept high detection risk for strategic gains.

**Policy parameters:**
```python
class DevaluationAggressor:
    interest_rate_shocks = True  # Sudden large cuts
    target_devaluation = 0.20  # 20% within 12 months
    competitive_devaluation_trigger = True  # React to competitor moves

    fx_intervention_direction = "Massive selling"
    intervention_intensity = "Extreme"  # >0.05 of monetary base
    capital_control_index = 0.75  # Heavy controls (trap capital)

    reserve_expenditure_tolerance = 0.25  # Willing to burn 25% of reserves
    policy_transparency = 0.30  # Low (covert operations)
```

**Typical actions:**
- Interest rate adjustments: Sudden 2-3% cuts
- FX intervention: Massive reserve selling
- Capital controls: Emergency measures (CCI jumps 0.3-0.5)
- Forward contracts: Offer below-market hedges
- Invoicing: Shift to weaker currency
- Detection risk: Very high (70-90% over 2 years)

**Economic outcomes:**
- Exchange rate: 15-30% depreciation (rapid)
- Trade balance: Dramatic improvement (+5-10% GDP within 18 months)
- Inflation: Surge (+5-10%)
- Capital flight: Severe (without controls)
- UTA compliance: Poor (multiple investigations, heavy penalties)

**Tradeoffs:**
- Benefit: Massive short-term competitiveness gain, market share capture
- Cost: High inflation, capital flight, UTA penalties (-1500 to -3000 credits), reputational damage, retaliation risk (currency war)

**Strategic use cases:**
- Economic crisis response (desperate measures)
- Geopolitical competition (strategic confrontation)
- Currency war escalation

**Example countries:** Argentina (recurring), Russia (2014-2015), Turkey (2018-2020)

### Archetype 4: Financial Hub Model

**Philosophy:** Maximize capital account openness and currency credibility to become global financial center, even at cost of exchange rate volatility.

**Policy parameters:**
```python
class FinancialHub:
    interest_rate_rule = "Strict inflation targeting"
    capital_control_index = 0.0  # Zero restrictions (fully open)
    policy_transparency = 1.0  # Maximum transparency

    fx_intervention = "Never"  # Pure float (except systemic crisis)
    forward_guidance_credibility = 0.95  # Highest credibility
    reserve_currency_ambitions = True

    financial_sector_share_gdp = 0.15  # 15% (unusually high)
```

**Typical actions:**
- Interest rate adjustments: Systematic (Taylor Rule)
- FX intervention: None (market determines)
- Capital controls: None (radical openness)
- Forward contracts: Private market provision (no government)
- Invoicing: Push domestic currency internationally
- Detection risk: Zero (full transparency)

**Economic outcomes:**
- Exchange rate volatility: High (10-15% annual)
- Trade balance: Variable (not primary concern)
- Financial services exports: Very high
- Foreign investment: Maximum (safe haven status)
- UTA compliance: Perfect (no interventions to flag)

**Tradeoffs:**
- Benefit: Financial sector profits, safe haven flows, reserve currency status (if successful)
- Cost: Manufacturing sector suffers (high exchange rate volatility), real economy volatility

**Strategic use cases:**
- Established financial centers
- Aspiring reserve currency issuers
- Countries with comparative advantage in finance

**Example countries:** UK (London), Switzerland (Zurich), Hong Kong

### Archetype 5: Pegged Regime (Fixed Rate Defense)

**Philosophy:** Defend fixed exchange rate at all costs to maintain credibility, even if economically painful.

**Policy parameters:**
```python
class PeggedRegime:
    exchange_rate_peg = 1.00  # Fixed rate (e.g., 1:1 with USD)
    peg_defense_priority = "Absolute"

    fx_intervention_threshold = 0.001  # Intervene at tiny deviation
    intervention_intensity = "Unlimited"  # Burn all reserves if needed
    interest_rate_subservience = True  # Rates dictated by peg defense

    capital_control_tolerance = 0.8  # Heavy controls if peg threatened
    reserve_target = 24_months_imports  # Massive buffer
```

**Typical actions:**
- Interest rate adjustments: Dictated by peg (must match foreign rate ± risk premium)
- FX intervention: Massive and immediate
- Capital controls: Imposed if peg threatened
- Forward contracts: Government guarantees peg (unlimited provision)
- Invoicing: Peg currency dominates
- Detection risk: Zero (defending peg is transparent)

**Economic outcomes:**
- Exchange rate: Zero volatility (by definition)
- Trade balance: Absorbs all adjustment (can swing wildly)
- Inflation: Imported from peg country
- Reserves: Volatile (builds in surplus, burns in defense)
- UTA compliance: Good (if peg sustainable), Poor (if peg unsustainable and collapses)

**Tradeoffs:**
- Benefit: Zero exchange rate risk, monetary credibility (if peg holds)
- Cost: Loss of monetary policy autonomy, crisis risk (speculative attacks), reserves depletion

**Strategic use cases:**
- Small open economies (import credibility)
- Currency union aspirants (pre-adoption phase)
- Resource exporters (peg to reduce volatility)

**Example countries:** Hong Kong (USD peg), Saudi Arabia (USD peg), Denmark (EUR peg)

## Strategic Gameplay Scenarios

### Scenario 1: The Stealth Devaluation (Export Competitiveness Play)

**Context:**
- You are South Korea in 2026
- China has undervalued yuan by 8%, gaining export market share
- Your auto and electronics exports are suffering (-12% market share over 18 months)
- Domestic political pressure to "do something"

**Your strategy:**
1. **Month 0-3:** Begin FX swap accumulation (borrow USD, sell for won)
   - Intensity: 0.03 (moderate)
   - Won depreciates 3% (gradual, below detection threshold)
   - Detection risk: 15%

2. **Month 4-6:** Cut interest rates 0.75% (justify with "growth concerns")
   - Won depreciates additional 4% (cumulative 7%)
   - Capital outflows: 1.2% GDP
   - Detection risk: 25% (flagged for monitoring)

3. **Month 7-12:** Subsidize export hedging via forward contracts
   - Exporters guaranteed favorable rates
   - Export volumes recover +8%
   - Detection risk: 40% (asymmetry indicators rising)

4. **Month 13-18:** UTA investigation triggered (asymmetry 0.18)
   - You cooperate partially (show some data, hide swap operations)
   - UTA penalty: -600 credits (moderate)
   - Net benefit: Market share recovered, penalty manageable

**Outcome:**
- Export volume: +15% over baseline
- Trade balance: +2.5% GDP improvement
- UTA penalty: -600 credits + 6-month export credit suspension
- Net strategic value: Positive (preserved industrial base)

**Key lesson:** Gradual, multi-tool manipulation harder to detect than single dramatic move.

### Scenario 2: The Currency War Escalation

**Context:**
- You are Brazil in 2027
- USA has raised rates aggressively (fighting domestic inflation)
- Real has depreciated 18% (capital flight to USD)
- Domestic inflation surging (+8%)
- Political crisis brewing

**Your options:**

**Option A: Stabilizer Response (Accept Depreciation)**
- Raise domestic rates 3% (match Fed)
- Accept temporary recession
- Real stabilizes at -15% vs baseline
- UTA compliance: Excellent
- Outcome: Recession now, stability later

**Option B: Capital Controls (Trap Capital)**
- Impose CCI 0.6 controls (restrict outflows)
- Keep rates low (2%)
- Real depreciates only 8% (vs 18% in Option A)
- UTA compliance: Borderline (-400 credits)
- Outcome: Avoid recession, but risk sudden stop

**Option C: Aggressive Devaluation (Lean In)**
- Cut rates further (-1%)
- Sell reserves to accelerate depreciation to -25%
- Massive export boost (+12%)
- UTA compliance: Poor (-1200 credits)
- Outcome: Short-term gain, long-term retaliation risk

**Actual choice:** You choose Option B (Capital Controls)
- Rationale: Domestic politics can't tolerate recession (Option A)
- Rationale: Currency war escalation (Option C) invites retaliation

**Month 6:** Fed pivots (cuts rates), capital controls no longer needed
- You gradually remove controls (CCI 0.6 → 0.3 over 12 months)
- UTA penalty: -400 credits total
- Outcome: Successfully navigated crisis without permanent damage

**Key lesson:** Temporary measures tolerated if removed once crisis passes.

### Scenario 3: The Pegged Regime Under Attack

**Context:**
- You are Saudi Arabia in 2028
- USD/SAR pegged at 3.75 (since 1986)
- Oil prices have crashed (-40%)
- Fiscal deficit surging (12% GDP)
- Speculators shorting riyal (expecting peg break)

**Your peg defense:**

**Month 0-6: Initial Defense**
- Burn $80B reserves (1/6 of total)
- Raise domestic rates 2% (support peg)
- Reserves: 480B → 400B
- Detection risk: 0% (legitimate peg defense)

**Month 7-12: Accelerated Pressure**
- Burn additional $120B reserves
- Reserves: 400B → 280B (approaching crisis)
- Speculators intensify attack (sense weakness)
- Capital controls considered (CCI 0.1 → 0.4)

**Month 13: Decision Point**

**Option A: Break the Peg**
- Devalue 20% (SAR 3.75 → 4.50)
- Immediate reserve pressure relief
- But: Credibility destroyed, inflation surges, political upheaval

**Option B: Defend to the End**
- Burn remaining reserves (280B → 50B over 6 months)
- Impose heavy capital controls (CCI 0.7)
- Hope oil prices recover
- Risk: Reserves exhausted, forced peg break anyway (worse outcome)

**Option C: Negotiate IMF/UTA Support**
- Request emergency liquidity facility ($100B)
- Commit to fiscal reforms (reduce deficit)
- Maintain peg with external support
- UTA terms: Transparency requirements, no penalties

**Actual choice:** You choose Option C (External Support)
- Month 14-18: Oil prices recover (+30%)
- Fiscal deficit narrows (12% → 6%)
- Repay IMF facility over 3 years
- Peg survives, credibility intact

**Outcome:**
- Reserves: Stabilized at 250B
- Peg: Maintained (crisis averted)
- UTA compliance: Good (cooperative approach rewarded)

**Key lesson:** Pegs survive with sufficient reserves + external support. Going it alone often fails.

### Scenario 4: The Reserve Currency Privilege Play

**Context:**
- You are the USA in 2029
- Domestic inflation at 4% (above 2% target)
- Fed must raise rates aggressively (2% → 5%)
- Side effect: Global dollar shortage, emerging markets suffer

**Your actions:**
- **Domestic policy:** Raise rates 3% (2% → 5%)
- **Global effect:**
  - USD appreciates 12% (trade-weighted)
  - EM capital outflows: -$300B
  - EM currencies depreciate 15-25%
  - Several EM countries face crisis

**Is this manipulation?**
- **Legal perspective:** No (legitimate domestic policy)
- **Economic perspective:** Imposes massive externality on others (spillover)
- **UTA perspective:** Monitored, but no penalties (reserve currency privilege)

**EM responses:**
- Brazil: Capital controls (CCI 0.6)
- Turkey: Emergency rate hikes (12% → 25%)
- Indonesia: IMF program
- China: Draw down reserves ($150B)

**Your strategic benefit:**
- Domestic inflation controlled (4% → 2.5% within 12 months)
- USD strength reduces import prices (further disinflationary)
- Financial sector profits (global liquidity provision)
- Geopolitical leverage (EM countries need your forbearance)

**Counterfactual: If you were NOT reserve currency issuer:**
- Capital flight would offset domestic tightening
- Currency would weaken (not strengthen)
- Inflation would persist
- You'd face UTA penalties for aggressive tightening

**Key lesson:** Reserve currency status provides "exorbitant privilege" (others absorb your adjustment costs).

### Scenario 5: The Carry Trade Exploitation

**Context:**
- You are Japan in 2030
- Rates extremely low (0.1%) for decades
- Yen is global carry trade funding currency
- Suddenly: Risk-off event (geopolitical shock)

**What happens:**
1. **Risk-off trigger:** Taiwan Strait tensions escalate
2. **Carry trade unwind:** Investors panic, close positions
   - Borrow yen → Invest in high-yield (Brazil, Turkey) → Profit from spread
   - Unwind: Sell emerging market assets → Buy yen to repay loans
   - Yen surges 8% in 3 days (violent appreciation)
3. **Your export sector crushed:** Toyota, Sony exports become uncompetitive overnight
4. **Deflation risk resurfaces:** Stronger yen → import prices fall → deflation

**Your response:**

**Option A: Accept Appreciation (Market Forces)**
- Do nothing (let yen appreciate to 105/USD)
- Export recession ensues
- Deflation returns (-0.5% CPI)
- Political pressure mounts

**Option B: Emergency Intervention (Stabilizer)**
- Sell $150B yen (5% of reserves)
- Cap appreciation at 110/USD
- Detection risk: 0% (crisis intervention accepted)
- UTA compliance: Good (temporary stabilization)

**Option C: Opportunistic Aggression (Controversial)**
- Let yen appreciate to 105/USD (don't intervene initially)
- Wait for carry trade unwind to complete (2 weeks)
- Then: Massive intervention + rate cut (-0.1% → -0.5%)
- Drive yen back to 120/USD (net 15% depreciation from pre-crisis)
- Detection risk: 60% (opportunistic exploitation of crisis)
- UTA compliance: Questionable (-800 credits if deemed manipulation)

**Actual choice:** You choose Option B (Emergency Intervention)
- Rationale: Crisis intervention is accepted practice
- Rationale: Option C too risky (UTA penalties + retaliation)

**Outcome:**
- Yen stabilizes at 110/USD (modest 3% appreciation)
- Export sector damage limited
- UTA compliance: Excellent (cooperative crisis management)

**Key lesson:** Crisis intervention tolerated; opportunistic exploitation punished.

### Scenario 6: The Invoicing Shift (Long Game)

**Context:**
- You are China in 2025-2035
- Long-term strategy: Yuan internationalization
- Challenge: 70% of trade still USD-invoiced

**Your 10-year strategy:**

**Phase 1 (2025-2028): Build Infrastructure**
- Establish yuan clearing banks in 50 countries
- Launch digital yuan (e-CNY) for cross-border trade
- Offer yuan swap lines to central banks ($500B total)
- Yuan share of trade invoicing: 8% → 15%
- Detection risk: 0% (infrastructure development is legitimate)

**Phase 2 (2028-2031): Incentivize Adoption**
- Belt and Road projects require yuan invoicing
- Offer 0.5% discount on Chinese exports if invoiced in yuan
- Saudi Arabia agrees to accept yuan for oil (10% of sales)
- Yuan share of trade invoicing: 15% → 25%
- Detection risk: 10% (incentives scrutinized but legal)

**Phase 3 (2031-2035): Critical Mass**
- Yuan futures markets deep enough for hedging
- SWIFT alternative (CIPS) handles 30% of China trade
- Yuan included in IMF SDR basket (20% weight)
- Yuan share of trade invoicing: 25% → 40%
- Detection risk: 0% (market-driven at this point)

**Economic effects:**
- Yuan demand permanently higher (structural support)
- China gains policy autonomy (less dollar dependency)
- Currency appreciation: +5-8% over 10 years (gradual)
- Export competitiveness: Offset by productivity gains

**US response:**
- Dollar share declines (60% → 50% of global trade)
- US loses some seigniorage revenue (modest, ~$10B/year)
- Geopolitical implications (reduced financial leverage)

**UTA perspective:**
- No violations (invoicing shift is sovereign right)
- Monitors for coercive tactics (requiring yuan use)
- Overall: Acceptable strategic competition

**Key lesson:** Long-term structural shifts more sustainable than short-term manipulation.

### Scenario 7: The Forward Guidance Trap

**Context:**
- You are Turkey in 2030
- Credibility damaged from past policy mistakes
- Inflation at 15%, target is 5%
- Markets don't believe your tightening commitment

**Your forward guidance:**
- Announce: "We will raise rates to 25% and hold until inflation falls below 7%"
- Markets skeptical (past promises broken)
- Lira barely responds (+1% appreciation, expected +5%)

**The trap:**

**Month 0-6: You follow through**
- Raise rates 10% → 15% → 20% → 25%
- Inflation falls slowly (15% → 13%)
- Recession deepens (GDP -3%)
- Political pressure intense

**Month 7: The temptation**
- President demands rate cuts (election approaching)
- You consider: Cut rates to 20% (break promise)
- Short-term relief: Economy stabilizes
- Long-term cost: Credibility destroyed permanently

**Option A: Hold Firm (Credibility)**
- Keep rates at 25% despite pressure
- Month 12: Inflation falls to 9%
- Month 18: Inflation falls to 6%
- Month 24: Cut rates to 15% (victory lap)
- Outcome: Credibility rebuilt, future guidance effective

**Option B: Break Promise (Short-term Relief)**
- Cut rates to 20% (Month 7)
- Inflation stops falling (stuck at 12%)
- Month 12: Must raise rates again (25% → 30%)
- Outcome: Credibility destroyed, inflation persistent

**Actual choice:** President forces Option B (political override)
- Central bank governor resigns in protest
- Markets punish: Lira crashes -15%
- Inflation resurges (12% → 18%)
- UTA flags: False forward guidance pattern detected (-500 credits)

**Year 2 reset:**
- New governor appointed (independent)
- Rates raised to 35% (extreme)
- 3-year recession to rebuild credibility
- Forward guidance ignored until track record rebuilt

**Key lesson:** Forward guidance only works with credibility. Breaking promises has compounding costs.

### Scenario 8: The Coordinated Bloc Devaluation

**Context:**
- You are the EU in 2032
- USA has grown 4% annually, EU only 1%
- Competitiveness gap widening
- Political pressure to "do something"

**Your proposal:**
- Secret coordination with UK, Switzerland, Japan
- Simultaneous: Rate cuts (1%), FX intervention ($200B combined)
- Target: 10% depreciation vs USD
- Rationale: "If we move together, USA can't retaliate effectively"

**The coordination:**

**Month 0: Setup**
- Backchannel negotiations (finance ministers)
- Agreement: Move on same day (maximum surprise)
- Each commits €50B/$200B total intervention

**Month 1: Execution**
- ECB cuts 1%, SNB cuts 1%, BoE cuts 1%, BoJ cuts 0.5%
- Simultaneous FX sales (€50B each)
- EUR/USD: 1.10 → 1.00 (-9%)
- GBP/USD: 1.30 → 1.20 (-8%)
- CHF/USD: 0.90 → 0.98 (-9%)
- JPY/USD: 140 → 152 (-9%)

**Month 2: Detection**
- UTA forensic analysis: Timing too coincidental (probability 0.001)
- Wiretap evidence: Finance minister calls leaked
- Confidence in coordination: 0.95 (very high)

**Month 3: Consequences**
- UTA penalties: -2000 credits per country
- USA files formal complaint: Currency manipulation via coordination
- US response: Countervailing duties (+15% on EU/UK/JP/CH exports)
- Net effect: Export gains wiped out by tariff retaliation

**Economic outcome:**
- Export boost: +8% initially
- Tariff reduction: -12% from retaliation
- Net: -4% (worse than doing nothing)
- Credibility damage: Severe

**Counterfactual: If coordination not detected:**
- Export boost: +8% sustained
- Net strategic gain: Positive
- But: Detection probability was 85% (coordination hard to hide)

**Key lesson:** Coordination amplifies gains but dramatically increases detection risk and retaliation severity.

## Parameters and Calibration

### Data Requirements

**Primary data sources:**

1. **IMF International Financial Statistics (IFS)**
   - Exchange rates (daily, spot and forward)
   - Interest rates (policy rate, interbank, government bond yields)
   - Foreign exchange reserves (monthly)
   - Balance of payments (quarterly)
   - Capital flows (portfolio, FDI, other investment)

2. **Bank for International Settlements (BIS)**
   - Cross-border banking flows
   - FX turnover (triennial survey)
   - Derivatives positions (semiannual)
   - Central bank intervention estimates

3. **SWIFT Aggregates**
   - Trade invoicing currency shares
   - Cross-border payment flows
   - Messaging volumes (proxy for trade)

4. **Central Bank Reports**
   - Monetary policy statements (forward guidance)
   - Financial stability reports (risk assessments)
   - Intervention activity (if disclosed)

5. **UN Comtrade**
   - Bilateral trade flows (for asymmetry detection)
   - Product-level detail
   - Monthly frequency

**Update frequency:**
- Exchange rates: Daily
- Interest rates: Weekly
- Reserves: Monthly
- Capital flows: Quarterly
- Trade data: Monthly (lagged 2-3 months)

### Calibration Parameters

**Exchange rate sensitivity (elasticities):**

```python
EXCHANGE_RATE_ELASTICITIES = {
    'export_volume': {
        'commodities': 2.5,           # Wheat, oil, copper
        'basic_manufactures': 1.8,    # Steel, textiles
        'differentiated_goods': 1.2,  # Autos, machinery
        'high_tech': 0.6              # Semiconductors, aerospace
    },

    'import_volume': {
        'necessities': 1.2,           # Food, energy
        'intermediate_goods': 1.7,    # Inputs for production
        'consumer_discretionary': 2.3 # Electronics, apparel
    },

    'pass_through_to_prices': {
        'import_prices': 0.75,        # 75% of FX change hits import prices
        'export_prices': 0.60,        # 60% passed to foreign buyers
        'cpi_inflation': 0.70         # 70% of import price change hits CPI
    }
}
```

**Interest rate effects:**

```python
INTEREST_RATE_EFFECTS = {
    'capital_flows': {
        'baseline_sensitivity': 0.5,  # 1% rate change → 0.5% GDP capital flow
        'carry_trade_amplification': 1.6  # Multiplier when carry trades active
    },

    'exchange_rate': {
        'appreciation_per_rate_hike': 1.2,  # 1% rate ↑ → 1.2% currency ↑
        'lag_months': 2                      # Full effect in 2 months
    },

    'gdp': {
        'impact_per_rate_hike': -0.3,       # 1% rate ↑ → -0.3% GDP
        'lag_quarters': 3                    # Peak effect in 3 quarters
    },

    'inflation': {
        'impact_per_rate_hike': -0.4,       # 1% rate ↑ → -0.4% inflation
        'lag_quarters': 5                    # Long lag for inflation
    }
}
```

**Capital control effectiveness:**

```python
CAPITAL_CONTROL_EFFECTS = {
    'flow_reduction': {
        'CCI_0.3': 0.25,  # Moderate controls reduce flows 25%
        'CCI_0.6': 0.55,  # Heavy controls reduce flows 55%
        'CCI_0.9': 0.80   # Extreme controls reduce flows 80%
    },

    'risk_premium_increase': {
        'CCI_0.3': 0.005,  # +50 bps
        'CCI_0.6': 0.015,  # +150 bps
        'CCI_0.9': 0.035   # +350 bps
    },

    'black_market_premium': {
        'CCI_0.3': 0.03,   # 3% parallel rate premium
        'CCI_0.6': 0.12,   # 12% parallel rate premium
        'CCI_0.9': 0.35    # 35% parallel rate premium
    }
}
```

**Detection thresholds (from Detection System section):**

```python
DETECTION_THRESHOLDS = {
    'reserve_pressure': {
        'monitoring': 0.02,
        'investigation': 0.05,
        'formal_audit': 0.12
    },

    'fx_intervention_intensity': {
        'monitoring': 0.005,
        'investigation': 0.02,
        'formal_audit': 0.05
    },

    'trade_invoicing_asymmetry': {
        'routine_review': 0.10,
        'investigation': 0.15,
        'audit': 0.25
    },

    'capital_flow_spike': {
        'monitor': 0.005,  # 0.5% GDP
        'investigate': 0.02,
        'crisis_determination': 0.05
    }
}
```

**UTA credit penalties:**

```python
UTA_PENALTIES = {
    'stealth_devaluation': -800,
    'export_subsidy_sterilization': -1200,
    'invoicing_asymmetry_exploitation': -1500,
    'shadow_reserve_accumulation': -600,
    'capital_control_gradualism': -400,
    'interest_rate_bait_switch': -700,
    'triangular_hedging': -500,
    'asymmetric_rate_corridor': -600,
    'dual_exchange_rate': -1000,
    'coordinated_devaluation': -2000,
    'inflation_underreporting': -800,
    'false_forward_guidance': -500
}
```

### Temporal Resolution

**Simulation time steps:**

- **Daily:** Exchange rates, interest rates (for realism)
- **Weekly:** Capital flows, FX intervention
- **Monthly:** Trade data, reserves, detection indicators
- **Quarterly:** GDP, inflation, balance of payments
- **Annual:** Structural parameters (elasticities, archetypes)

**Lag structures:**

```python
POLICY_LAG_STRUCTURE = {
    'interest_rate_to_currency': {
        'immediate': 0.30,    # 30% effect in same period
        '1_month': 0.50,      # 50% additional by month 1
        '2_months': 0.20      # Final 20% by month 2
    },

    'currency_to_trade_volume': {
        '0_3_months': 0.25,   # 25% effect (J-curve worsening)
        '4_6_months': 0.50,   # 50% additional (volume adjustment)
        '7_12_months': 0.25   # Final 25% (full adjustment)
    },

    'currency_to_inflation': {
        '0_1_months': 0.20,   # 20% immediate (import prices)
        '2_4_months': 0.50,   # 50% additional (retail pass-through)
        '5_8_months': 0.20,   # 20% additional (second-round)
        '9_18_months': 0.10   # Final 10% (expectations)
    }
}
```

## Integration with Other Modules

### Integration Point 1: Trade Flow Module

**Data passed to Trade Flow Module:**

```python
class CurrencyToTradeFlow:
    # Bilateral exchange rate changes
    exchange_rate_changes: dict[(exporter, importer)] -> float

    # Price effects (exporter perspective)
    export_price_competitiveness: dict[exporter][product] -> float

    # Import price effects (importer perspective)
    import_price_shocks: dict[importer][product] -> float

    # Currency risk premiums (affects trade costs)
    exchange_rate_volatility: dict[country] -> float
```

**Data received from Trade Flow Module:**

```python
class TradeFlowToCurrency:
    # Trade balance (affects currency demand)
    net_exports: dict[country] -> float

    # Capital flows from trade financing
    trade_credit_flows: dict[country] -> float

    # Invoicing currency shares (affects currency demand)
    invoicing_shares: dict[(exporter, importer, currency)] -> float

    # Triangulation flags (for detection system)
    triangulation_flags: dict[country][product] -> float
```

**Integration mechanism:**

```python
def integrate_currency_trade_flow(currency_state, trade_flow_state):
    # Step 1: Currency affects trade prices
    for (exporter, importer) in country_pairs:
        bilateral_exchange_rate = currency_state.exchange_rates[(exporter, importer)]

        for product in products:
            # Export price in importer's currency
            export_price_foreign = (
                trade_flow_state.baseline_price[exporter][product] *
                bilateral_exchange_rate
            )

            # Update trade flow model with new prices
            trade_flow_state.update_prices(exporter, importer, product, export_price_foreign)

    # Step 2: Trade affects currency demand
    for country in countries:
        net_exports = trade_flow_state.net_exports[country]

        # Trade surplus → currency demand ↑ → appreciation pressure
        currency_pressure = net_exports / currency_state.fx_market_liquidity[country]
        currency_state.apply_trade_pressure(country, currency_pressure)

    # Step 3: Invoicing affects currency demand
    for (exporter, importer, currency) in invoicing_relationships:
        invoicing_demand = trade_flow_state.trade_volume * invoicing_share[currency]
        currency_state.add_structural_demand(currency, invoicing_demand)

    return currency_state, trade_flow_state
```

### Integration Point 2: Compliance & Cheating Detection Module

**Data passed to Compliance Module:**

```python
class CurrencyToCompliance:
    # Detection indicators (from Detection System section)
    reserve_pressure: dict[country] -> float
    fx_intervention_intensity: dict[country] -> float
    invoicing_asymmetry: dict[country] -> float
    capital_flow_spike: dict[country] -> float

    # Policy transparency scores
    transparency_index: dict[country] -> float

    # Manipulation flags (high-confidence detections)
    manipulation_flags: dict[country] -> list[{
        'type': str,  # e.g., 'stealth_devaluation'
        'confidence': float,
        'estimated_magnitude': float
    }]
```

**Data received from Compliance Module:**

```python
class ComplianceToCurrency:
    # UTA enforcement actions
    credit_penalties: dict[country] -> int  # UTA credits deducted
    export_credit_suspensions: dict[country] -> int  # Months suspended

    # Reporting requirements (affects transparency)
    enhanced_reporting_required: dict[country] -> bool

    # Audit findings (hidden interventions discovered)
    unreported_interventions: dict[country] -> float
```

**Integration mechanism:**

```python
def integrate_currency_compliance(currency_state, compliance_state):
    # Step 1: Currency module calculates detection indicators
    for country in countries:
        reserve_pressure = currency_state.calculate_reserve_pressure(country)
        fx_intensity = currency_state.calculate_fx_intervention_intensity(country)

        # Pass to Compliance Module
        compliance_state.update_indicators(country, reserve_pressure, fx_intensity)

    # Step 2: Compliance module evaluates flags
    for country in countries:
        if compliance_state.reserve_pressure[country] > 0.12:
            # Trigger investigation
            compliance_state.launch_investigation(country, 'reserve_depletion')

            # Apply penalty
            penalty = -800  # UTA credits
            compliance_state.apply_penalty(country, penalty)

    # Step 3: Currency module applies enforcement consequences
    for country in countries:
        if country in compliance_state.export_credit_suspensions:
            # Increase trade costs (reduced financing availability)
            currency_state.trade_credit_premium[country] += 0.02  # +200 bps

    return currency_state, compliance_state
```

### Integration Point 3: Pricing & Market Equilibrium Module

**Data passed to Pricing Module:**

```python
class CurrencyToPricing:
    # Import cost shocks (from currency depreciation)
    import_price_shocks: dict[country][product] -> float

    # Real wage effects (from inflation)
    real_wage_changes: dict[country] -> float

    # Interest rate effects on cost of capital
    capital_cost_changes: dict[country] -> float
```

**Data received from Pricing Module:**

```python
class PricingToCurrency:
    # Inflation rates (feed back to monetary policy)
    cpi_inflation: dict[country] -> float

    # Terms of trade (affects currency demand)
    terms_of_trade: dict[country] -> float

    # Asset prices (affected by interest rates)
    equity_prices: dict[country] -> float
    real_estate_prices: dict[country] -> float
```

**Integration mechanism:**

```python
def integrate_currency_pricing(currency_state, pricing_state):
    # Step 1: Currency depreciation raises import costs
    for country in countries:
        exchange_rate_change = currency_state.get_exchange_rate_change(country)

        for product in products:
            if pricing_state.import_share[country][product] > 0:
                # Imported input costs rise
                import_cost_shock = (
                    exchange_rate_change *
                    currency_state.pass_through_rate *
                    pricing_state.import_share[country][product]
                )

                # Pass to Pricing Module
                pricing_state.apply_cost_shock(country, product, import_cost_shock)

    # Step 2: Pricing module re-equilibrates
    pricing_state.solve_equilibrium()

    # Step 3: Inflation feeds back to currency policy
    for country in countries:
        inflation = pricing_state.cpi_inflation[country]

        # Taylor Rule: Raise rates if inflation above target
        if inflation > currency_state.inflation_target[country] + 0.005:
            rate_adjustment = 0.5 * (inflation - currency_state.inflation_target[country])
            currency_state.adjust_interest_rate(country, rate_adjustment)

    return currency_state, pricing_state
```

### Integration Point 4: Country Agents (Strategy Module)

**Data passed to Country Agents:**

```python
class CurrencyToCountryAgent:
    # Economic outcomes (inform policy decisions)
    export_competitiveness: dict[country] -> float
    inflation_rate: dict[country] -> float
    real_wage_growth: dict[country] -> float
    trade_balance: dict[country] -> float

    # Policy constraints
    reserve_buffer: dict[country] -> float  # Months of import cover
    uta_credit_balance: dict[country] -> int

    # Strategic opportunities
    competitor_currency_moves: dict[country] -> float
    carry_trade_opportunities: dict[(funding_currency, target_currency)] -> float
```

**Data received from Country Agents:**

```python
class CountryAgentToCurrency:
    # Policy decisions
    interest_rate_target: dict[country] -> float
    fx_intervention_target: dict[country] -> {
        'direction': str,  # 'buy' or 'sell'
        'intensity': float,
        'duration': int
    }
    capital_control_changes: dict[country] -> float
    forward_guidance: dict[country] -> str

    # Strategic priorities
    currency_target: dict[country] -> float  # Desired exchange rate
    risk_tolerance: dict[country] -> float   # Detection risk willing to accept
```

**Integration mechanism:**

```python
def integrate_currency_country_agent(currency_state, country_agents):
    # Step 1: Currency module provides situation report to each agent
    for country in country_agents:
        situation = {
            'current_exchange_rate': currency_state.exchange_rate[country.id],
            'competitiveness': currency_state.export_competitiveness[country.id],
            'inflation': currency_state.inflation[country.id],
            'uta_credits': currency_state.uta_balance[country.id],
            'competitor_moves': currency_state.get_competitor_moves(country.id)
        }

        # Agent evaluates situation and decides policy
        policy_decision = country.decide_currency_policy(situation)

    # Step 2: Currency module executes agent decisions
    for country in country_agents:
        policy = country.policy_decisions['currency']

        # Execute interest rate decision
        currency_state.set_interest_rate(country.id, policy['interest_rate'])

        # Execute FX intervention
        if policy['fx_intervention']:
            currency_state.intervene(
                country.id,
                direction=policy['fx_intervention']['direction'],
                amount=policy['fx_intervention']['amount']
            )

        # Execute capital control adjustment
        if policy['capital_control_change'] != 0:
            currency_state.adjust_capital_controls(
                country.id,
                policy['capital_control_change']
            )

    # Step 3: Update outcomes and feed back to agents (next period)
    currency_state.update()

    return currency_state, country_agents
```

## Implementation Guidance

### Algorithm Flow

```python
def update_currency_strategy_module(world_state):
    """Main currency strategy update cycle (monthly)"""

    # Step 1: Process country agent policy decisions
    for country in world_state.countries:
        policy_decisions = country.currency_policy_decisions

        # Execute interest rate changes
        world_state.currency.interest_rates[country] = policy_decisions.interest_rate_target

        # Execute FX interventions
        if policy_decisions.fx_intervention:
            execute_fx_intervention(country, policy_decisions.fx_intervention, world_state)

        # Execute capital control changes
        if policy_decisions.capital_control_adjustment:
            world_state.currency.capital_control_index[country] += policy_decisions.capital_control_adjustment

    # Step 2: Calculate exchange rate effects (market equilibrium)
    for country in world_state.countries:
        # Interest rate differential
        interest_differential = (
            world_state.currency.interest_rates[country] -
            world_state.currency.global_benchmark_rate
        )

        # Capital flow response
        capital_flow = (
            INTEREST_RATE_EFFECTS['capital_flows']['baseline_sensitivity'] *
            interest_differential *
            (1 - world_state.currency.capital_control_index[country])
        )

        # Trade balance pressure
        trade_pressure = world_state.trade_flow.net_exports[country] / world_state.currency.fx_liquidity[country]

        # FX intervention pressure
        intervention_pressure = world_state.currency.net_fx_intervention[country] / world_state.currency.monetary_base[country]

        # Combined exchange rate change
        exchange_rate_change = (
            INTEREST_RATE_EFFECTS['exchange_rate']['appreciation_per_rate_hike'] * interest_differential +
            trade_pressure +
            intervention_pressure
        )

        # Apply exchange rate change
        world_state.currency.exchange_rates[country] *= (1 + exchange_rate_change)

    # Step 3: Calculate economic impacts (propagation)
    economic_impacts = {}
    for country in world_state.countries:
        exchange_rate_change_pct = (
            world_state.currency.exchange_rates[country] /
            world_state.currency.exchange_rates_previous[country] - 1
        )

        # Export volume impact
        export_impact = calculate_export_impact(country, exchange_rate_change_pct, world_state)

        # Import price impact
        import_impact = calculate_import_impact(country, exchange_rate_change_pct, world_state)

        # Inflation impact
        inflation_impact = calculate_inflation_impact(country, exchange_rate_change_pct, world_state)

        # GDP impact
        gdp_impact = calculate_gdp_impact(country, exchange_rate_change_pct, world_state)

        economic_impacts[country] = {
            'export': export_impact,
            'import': import_impact,
            'inflation': inflation_impact,
            'gdp': gdp_impact
        }

    # Step 4: Update detection indicators
    detection_flags = {}
    for country in world_state.countries:
        # Reserve pressure
        reserve_pressure = calculate_reserve_pressure(country, world_state)

        # FX intervention intensity
        fx_intensity = calculate_fx_intervention_intensity(country, world_state)

        # Trade invoicing asymmetry
        invoicing_asymmetry = calculate_invoicing_asymmetry(country, world_state)

        # Capital flow spike
        capital_spike = calculate_capital_flow_spike(country, world_state)

        # Evaluate flags
        flags = evaluate_detection_flags(
            country, reserve_pressure, fx_intensity,
            invoicing_asymmetry, capital_spike, world_state
        )

        detection_flags[country] = flags

    # Step 5: Apply UTA enforcement actions
    for country in world_state.countries:
        if detection_flags[country]:
            for flag in detection_flags[country]:
                if flag['confidence'] > 0.70:  # High confidence manipulation
                    # Apply penalty
                    penalty = UTA_PENALTIES.get(flag['type'], -500)
                    world_state.uta.apply_credit_penalty(country, penalty)

                    # Apply export credit suspension
                    if flag['confidence'] > 0.85:
                        world_state.uta.suspend_export_credits(country, duration=6)

    # Step 6: Update state for next period
    world_state.currency.exchange_rates_previous = world_state.currency.exchange_rates.copy()
    world_state.currency.update_history(economic_impacts, detection_flags)

    return CurrencyStrategyOutputs(
        exchange_rates=world_state.currency.exchange_rates,
        interest_rates=world_state.currency.interest_rates,
        economic_impacts=economic_impacts,
        detection_flags=detection_flags,
        uta_penalties=world_state.uta.penalties_this_period
    )
```

### Computational Considerations

1. **Exchange Rate Equilibrium:**
   - Use iterative solver (Gauss-Seidel) to find consistent exchange rates
   - Convergence criterion: |ΔExchange Rate| < 0.001 (0.1%)
   - Maximum iterations: 50 (typically converges in 10-15)

2. **Lag Structure Implementation:**
   - Maintain historical state (24 months) for lagged effects
   - Distributed lag models for price pass-through
   - AR(1) process for expectations formation

3. **Detection Algorithm Efficiency:**
   - Pre-compute baseline patterns (rolling 12-month averages)
   - Flag countries exceeding thresholds (only investigate these)
   - Batch processing for asymmetry cross-checks

4. **Integration Sequencing:**
   - Currency module runs after Trade Flow (needs net exports)
   - Currency module runs before Pricing (provides cost shocks)
   - Detection runs after all policy execution (end-of-period assessment)

---

**Module Status:** Production-ready specification (4,975 words)

**Next Steps:** Implement in Mesa framework with integration to Trade Flow, Pricing, and Compliance modules.