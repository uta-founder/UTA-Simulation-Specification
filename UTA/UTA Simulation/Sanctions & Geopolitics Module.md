# Sanctions & Geopolitics Module

## What This Module Does

The Sanctions & Geopolitics Module transforms the UTA simulation from pure economic competition into a strategic game of power, influence, and economic warfare. Countries don't just trade—they wield economic tools as weapons, form alliances for protection and leverage, and navigate the dangerous waters between cooperation and conflict.

Think of this as the "diplomacy and conflict" layer of the game. While other modules handle production, trade, and market dynamics, this module governs how countries use those economic relationships strategically. Can you strangle an adversary's economy with sanctions? Will your allies back you up, or will they prioritize their own economic interests? How far can you push before triggering dangerous retaliation?

## Core Gameplay Mechanics

### The Strategic Toolkit

Countries in the UTA simulation have powerful geopolitical tools at their disposal:

**Economic Warfare Options**:
- **Sanctions**: Block specific products, sectors, or all trade with target countries
- **Secondary Sanctions**: Force third parties to choose between trading with you or your target
- **Financial Restrictions**: Freeze assets, block payments, restrict currency access
- **Technology Embargos**: Prevent access to critical technologies and know-how

**Alliance & Coalition Building**:
- **Trade Blocs**: Form preferential trading zones with reduced barriers
- **Sanctions Coalitions**: Coordinate economic pressure for greater impact
- **Security Alliances**: Mutual defense that affects economic decisions
- **Burden Sharing**: Distribute the costs of economic warfare among allies

**Strategic Responses**:
- **Retaliation**: Counter-sanctions and asymmetric responses
- **Circumvention**: Find alternative routes and suppliers
- **Escalation Control**: Carefully calibrated responses to avoid spiraling conflicts
- **De-escalation**: Face-saving exits and negotiated settlements

### How Sanctions Work in the Game

When you impose sanctions, you're essentially telling the trade system: "Block these specific flows." But it's not that simple. Every sanction creates ripples:

**The Sanction Decision Tree**:
1. **Choose Your Target**: Which country threatens your interests?
2. **Select Sanction Type**:
   - Comprehensive (35% success rate): Total trade embargo
   - Sectoral (30% success rate): Target specific industries
   - Targeted (25% success rate): "Smart" sanctions on entities
   - Symbolic (10% success rate): Political signaling with minimal impact

3. **Build a Coalition** (optional but powerful):
   - Coalition sanctions are 50% more effective
   - Costs are shared among participants
   - But maintaining unity is challenging (20% fragmentation risk)

4. **Calculate the Trade-offs**:
   - **Political Gain**: Will this achieve your objectives?
   - **Economic Cost**: How much will YOU suffer from lost trade?
   - **Reputation Impact**: Will others see you as reliable or aggressive?

**Example Scenario**:
The US sanctions China's semiconductor sector. US loses access to Chinese rare earths (economic cost), but potentially slows China's tech advancement (political gain). If the EU joins, effectiveness increases by 50%, but if Japan defects for economic reasons, the coalition weakens.

### Alliance Dynamics

Alliances aren't just political badges—they fundamentally alter your economic options and obligations.

**How Alliances Function**:

1. **Preferential Trading**:
   - Members reduce tariffs and barriers within the bloc
   - Shared standards and regulations reduce transaction costs
   - But you may need to discriminate against efficient non-members

2. **Collective Security Economics**:
   - An attack on one affects all members' trade policies
   - Larger members contribute disproportionally (Olson-Zeckhauser effect)
   - Free-riding temptation: Let others bear the costs while you benefit

3. **Policy Coordination**:
   - Synchronized sanctions for maximum impact
   - Shared intelligence on circumvention attempts
   - But requires compromising on national preferences

**Alliance Stability Mechanics**:

The game tracks "bloc cohesion" (0-1 scale). High cohesion means coordinated action and shared costs. Low cohesion leads to:
- Members pursuing side deals
- Unequal burden sharing
- Potential bloc dissolution

Your actions affect cohesion:
- Honoring commitments: +10% cohesion
- Violating agreements: -30% cohesion
- Free-riding detected: -20% cohesion

### The Retaliation Game

Retaliation is where game theory meets economic warfare. Every aggressive action invites a response, but how countries respond depends on their strategy:

**Retaliation Strategies**:

1. **Tit-for-Tat** (70% base probability):
   - Match opponent's action severity
   - Built-in 10% "forgiveness" to prevent endless spirals
   - Predictable but stable

2. **Massive Retaliation**:
   - Disproportionate response for deterrence
   - Escalation multiplier based on capability
   - High risk of triggering escalation ladder

3. **Graduated Response**:
   - Incremental escalation with clear steps
   - Allows for negotiation between rounds
   - Each step increases pressure by defined amount

**The Escalation Ladder** (5 steps to conflict):
1. Diplomatic protests and symbolic sanctions
2. Targeted economic measures
3. Broad sectoral sanctions
4. Comprehensive economic warfare
5. Military posturing or action threats

Each step up reduces de-escalation probability by 10%. At step 5, you're one miscalculation from kinetic conflict.

### Reputation & Credibility System

Your reputation isn't just a score—it's currency in the geopolitical game.

**How Reputation Works**:

Starting reputation: 0.5 (neutral)
- Decays 5% per turn (memory fades)
- Maximum reputation: 1.0 (completely trustworthy)
- Minimum reputation: 0.0 (pariah state)

**Actions That Build Reputation**:
- Successfully enforcing sanctions: +0.15 credibility
- Honoring alliance commitments: +0.10 reliability
- De-escalating conflicts: +0.05 stability
- Fair burden sharing: +0.08 cooperation

**Actions That Damage Reputation**:
- Failed sanctions: -0.20 credibility
- Violating agreements: -0.30 trustworthiness
- Aggressive first strikes: -0.25 stability
- Free-riding in alliances: -0.15 cooperation

**Why Reputation Matters**:
- High reputation (>0.7):
  - Others more likely to join your coalitions
  - Better terms in negotiations
  - Reduced risk premiums on trade (5% GDP benefit)

- Low reputation (<0.3):
  - Difficulty forming alliances
  - Preemptive defensive measures by others
  - Economic isolation effects (-5% to -10% GDP)

### Strategic Resource Dependencies

Some products aren't just commodities—they're strategic weapons. The game tracks vulnerability scores for critical dependencies.

**Vulnerability Calculation**:

Your vulnerability to supply cutoffs depends on:
1. **Import Share**: How much you rely on imports vs. domestic production
2. **Supplier Concentration**: Few suppliers = higher risk (measured by Herfindahl Index)
3. **Substitution Difficulty**: Can you switch to alternatives? (inverse of elasticity)
4. **Strategic Importance**: Military, energy, food security multipliers

**Example**:
Germany's natural gas vulnerability to Russia:
- Import share: 40% of consumption
- Supplier concentration: 0.64 (high)
- Substitution difficulty: High (low elasticity = 1.3)
- Strategic importance: Critical (winter heating + industry)
- **Vulnerability Score: 0.83** (extreme vulnerability)

This affects your strategic options—high vulnerability means you'll think twice before sanctioning that supplier.

## Economic Impacts & Feedback Loops

### Sanction Effectiveness Economics

Sanctions rarely work as intended. The game models realistic effectiveness:

**Success Rates by Type**:
- Comprehensive embargo: 35% (high impact but often circumvented)
- Sectoral sanctions: 30% (focused but substitutable)
- Smart sanctions: 25% (precise but limited impact)
- Symbolic sanctions: 10% (political theater)

**What Determines Success**:
1. **Economic Leverage** = (Your GDP / Target GDP) × Trade Dependence
2. **Coalition Size** = Percentage of target's trade partners participating
3. **Target Resilience** = Domestic production capacity + Alternative suppliers
4. **Enforcement Quality** = Detection capability × Political will

### Cost-Benefit Calculations

Every geopolitical action has economic consequences:

**Imposing Sanctions Costs YOU**:
- Direct trade loss: Value of foregone exports/imports
- Deadweight loss: 15% efficiency loss from trade diversion
- Administrative costs: Monitoring and enforcement
- Retaliation damage: Expected counter-sanctions

**Example Calculation**:
US sanctions on Chinese electronics:
- US exports to China in sector: $50B annually
- Deadweight loss: $7.5B (15% of $50B)
- Alternative suppliers cost premium: 25% = $12.5B
- Chinese retaliation (agriculture): $30B
- **Total Cost to US: $100B annually**

But if successful (30% chance):
- Chinese tech development slowed: $200B value
- Strategic advantage maintained: $150B value
- **Expected Benefit: $105B** (30% × $350B)

**Net Expected Value: +$5B** (marginal positive, high uncertainty)

### Alliance Economics

Joining alliances provides economic benefits but also imposes costs:

**Benefits of Membership**:
- Reduced tariffs within bloc: +2-5% trade volume
- Shared security reduces risk premiums: +1-2% GDP
- Technology and knowledge transfer: +0.5% productivity
- Collective bargaining power: Better terms with third parties

**Costs of Membership**:
- Trade diversion from efficient non-members: -1-3% welfare
- Burden sharing obligations: 0.5-2% GDP for collective actions
- Policy autonomy loss: Must coordinate with allies
- Potential retaliation from excluded countries

### Market Disruption Mechanics

Geopolitical actions create supply shocks that ripple through the economy:

**Immediate Effects**:
1. Sanctioned goods become unavailable from target
2. Prices spike based on elasticity of substitution
3. Countries scramble for alternative suppliers
4. Transport costs increase as trade routes adjust

**Secondary Effects**:
- Input shortages cascade through supply chains
- Inflation from supply constraints
- Investment uncertainty reduces growth
- Currency movements from trade balance shifts

**Example Cascade**:
Russia oil embargo → European energy prices +40% → Industrial costs +15% → Consumer prices +8% → Wage demands +5% → Competitiveness loss -3% → GDP impact -2%

## Strategic Considerations for Players

### When to Sanction

**Favorable Conditions**:
- You have economic leverage (larger economy, critical supplier)
- Target has limited alternatives
- Strong coalition support available
- Clear, achievable political objectives
- Domestic support for economic costs

**Avoid Sanctions When**:
- Target can easily substitute suppliers
- You're highly dependent on target's exports
- No coalition support (unilateral sanctions rarely work)
- Objectives are vague or maximalist
- Your reputation is already damaged

### Coalition Building Strategy

**Building Effective Coalitions**:

1. **Start with Natural Allies**: Countries with aligned interests and values
2. **Offer Side Payments**: Compensate members who bear higher costs
3. **Create Momentum**: Early joiners pressure fence-sitters
4. **Set Clear Objectives**: Vague goals lead to fragmentation
5. **Plan Exit Strategy**: How will sanctions end successfully?

**Managing Free-Riders**:
- Monitor member compliance continuously
- Create verification mechanisms
- Impose costs on defectors (reduce alliance benefits)
- Reward burden-sharers with influence

### Escalation Management

**Controlling Escalation**:
1. **Signal Intentions Clearly**: Ambiguity increases miscalculation risk
2. **Leave Room to Escalate**: Don't start at maximum pressure
3. **Provide Face-Saving Exits**: Allow adversaries to de-escalate with dignity
4. **Build in Pauses**: Time for negotiation between escalation steps
5. **Know Your Red Lines**: What triggers automatic responses?

**De-escalation Tactics**:
- Gradual, reciprocal reduction in sanctions
- Third-party mediation
- Package deals linking multiple issues
- Temporary ceasefires for negotiation
- Face-saving "victories" for both sides

### Long-term Reputation Management

**Building Credibility**:
- **Consistency**: Follow through on threats and promises
- **Proportionality**: Responses match provocations
- **Transparency**: Clear communication of intentions
- **Reliability**: Honor agreements even when costly
- **Restraint**: Don't abuse dominant positions

**Recovering from Reputation Damage**:
- Time heals: 5% recovery per peaceful turn
- Consistent compliance: Multiple small positive actions
- Major gestures: Costly signals of change
- New leadership: Regime change can reset reputation partially
- Coalition participation: Contributing to collective goods

## Module Integration & Data Flow

### Information Inputs

The module receives critical data from across the simulation:

**From Trade Flow Module**:
- Current bilateral trade volumes and dependencies
- Available alternative suppliers and routes
- Trade elasticities and substitution possibilities

**From Country Agents**:
- National objectives and strategic priorities
- Risk tolerance and time preferences
- Domestic political constraints

**From Pricing & Equilibrium Module**:
- Economic impacts of trade disruptions
- Market share shifts from sanctions
- Price effects of supply constraints

**From Energy & Logistics Module**:
- Critical infrastructure vulnerabilities
- Energy supply dependencies
- Transportation chokepoint control

**From Compliance Module**:
- Detected sanctions violations
- Circumvention evidence and patterns
- Enforcement effectiveness metrics

### Decision Outputs

The module generates policy decisions that affect the entire game:

**To Trade Flow Module**:
- Prohibited trade flows (what's sanctioned)
- Tariff schedules by country-product pairs
- Quota restrictions and licensing requirements

**To Country Agents**:
- Available strategic actions this turn
- Current reputation and credibility scores
- Alliance obligations and benefits

**To Pricing & Equilibrium Module**:
- Supply shocks from trade restrictions
- Political risk premiums for instability
- Uncertainty effects on investment

**To Compliance & Detection Module**:
- Active sanctions requiring monitoring
- Coalition enforcement priorities
- Legitimacy scores affecting enforcement

## Calibration & Realism

### Real-World Data Sources

The module is calibrated using extensive empirical data:

**Diplomatic Relations**:
- UN voting similarity indices for alignment
- Alliance membership databases (NATO, CSTO, SCO)
- Bilateral trade agreement networks
- Historical conflict data (GDELT, ICEWS event data)

**Sanctions Effectiveness**:
- Global Sanctions Database (GSDB) for success rates
- US Treasury OFAC sanctions lists
- EU consolidated sanctions regimes
- UN Security Council sanctions history

**Economic Interdependence**:
- UN Comtrade bilateral trade data
- UNCTAD foreign direct investment stocks
- OECD technology trade statistics
- Supply chain vulnerability assessments

**Strategic Resources**:
- Critical minerals assessments (USGS, EU Critical Raw Materials)
- International Energy Agency trade data
- FAO food security statistics
- Defense industrial base reports

### Key Calibrated Parameters

The game uses empirically-grounded parameters:

**Sanction Success Rates** (from historical data):
- Comprehensive embargo: 35%
- Sectoral sanctions: 30%
- Smart sanctions: 25%
- Symbolic sanctions: 10%

**Coalition Dynamics**:
- Coalition effectiveness bonus: 50%
- Free-riding rate: 30% typical
- Coalition fragmentation risk: 20% per period
- Burden sharing inequality: Power factor of 1.5

**Retaliation Parameters**:
- Base retaliation probability: 70%
- Escalation ladder: 5 steps to conflict
- De-escalation probability: 30% per step
- Tit-for-tat forgiveness: 10% noise factor

**Reputation Dynamics**:
- Memory decay: 5% per turn
- Credibility half-life: 10 periods
- Violation penalty: -30% reputation
- Compliance bonus: +10% reputation

**Economic Costs**:
- Sanctions deadweight loss: 15%
- Trade diversion premium: 25%
- Reputation GDP impact: ±5%
- Political risk premium: 2-10% added costs

## Strategic Tips for Players

### Power Projection Strategies

**Economic Hegemon**: Use your market size to force choices—"trade with us or them"
**Resource Controller**: Weaponize critical supplies during crises
**Coalition Builder**: Multiply limited power through collective action
**Reputation Warrior**: Build unmatched credibility for long-term influence
**Chaos Agent**: Destabilize regions for relative advantage

### Common Pitfalls to Avoid

1. **Sanctioning Without Coalition**: Unilateral sanctions rarely succeed
2. **Escalating Without Exit**: Getting trapped in spiraling retaliation
3. **Ignoring Reputation Costs**: Short-term gains, long-term isolation
4. **Overestimating Leverage**: Misjudging your economic importance
5. **Free-Riding Too Often**: Eventually coalitions exclude you

### Advanced Tactics

**The Empty Threat**: Build reputation for toughness without always following through
**The Reverse Sanction**: Restrict your own exports to create leverage
**Coalition Hijacking**: Join coalitions to weaken them from within
**Reputation Arbitrage**: Use high reputation to broker deals between adversaries
**Strategic Ambiguity**: Keep adversaries guessing about your red lines

## Victory Through Geopolitics

While economic dominance is one path to victory, mastering geopolitics offers alternative routes:

**Containment Victory**: Successfully isolate and economically strangle rivals
**Alliance Victory**: Build and maintain dominant coalition controlling majority of global trade
**Reputation Victory**: Become indispensable mediator and trusted partner
**Deterrence Victory**: Credible threats prevent others from challenging you
**Chaos Victory**: Profit from instability you create and control

The Sanctions & Geopolitics Module ensures that economic competition in the UTA simulation includes the full spectrum of strategic statecraft—from peaceful cooperation to economic warfare, always one miscalculation away from catastrophic escalation.