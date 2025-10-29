# Behavioral Module - Game Mechanics Guide

## Overview

**What This Module Does for Gameplay**

Think of this module as your country's "memory, personality, and learning system." In most economic simulations, countries are mindless calculators that always make perfect decisions. In UTA, your country:

- **Remembers history** - Past betrayals, successful partnerships, and lessons learned
- **Builds a reputation** - Like a credit score that affects how others treat you
- **Learns from experience** - Gets better at strategies that work, abandons ones that fail
- **Reacts emotionally** - Can escalate conflicts, hold grudges, or show restraint
- **Influences others** - Your actions ripple through the network, triggering chain reactions

This creates a living, breathing geopolitical landscape where trust matters, reputation is currency, and yesterday's decisions shape tomorrow's options.

## Core Game Mechanics

### 1. Reputation System - Your Global Credit Score

**What It Does**:
Every country has a reputation score (0-100) that acts like a sovereign credit rating crossed with a poker table read. High reputation = lower trade costs, easier alliances, less scrutiny. Low reputation = expensive trade, isolation, constant surveillance.

**How It Works**:
Your reputation updates every turn based on four behaviors:
- **Compliance** (40% weight) - Did you follow UTA rules and trade agreements?
- **Restraint** (20% weight) - Did you retaliate proportionally or go nuclear?
- **Loyalty** (20% weight) - Did you honor alliance commitments?
- **Transparency** (20% weight) - Did you disclose actions openly or operate in shadows?

Your reputation slowly decays (85% carries over each turn) but recent actions matter most. Think of it like credit card payment history - one missed payment hurts, but consistent good behavior rebuilds trust.

**Strategic Implications**:
- **High reputation (60-100)**: Trade costs drop 20-40%, allies seek you out, you can lead coalitions
- **Mid reputation (40-60)**: Standard interactions, no bonuses or penalties
- **Low reputation (20-40)**: 50% trade cost penalty, limited cooperation, risk premiums everywhere
- **Pariah status (0-20)**: 100% cost increase, credit frozen, only desperate partners will deal

**Example Scenario**:
Germany starts at reputation 75. They catch Turkey cheating on origin rules. Germany could:
- **Option A**: Report to UTA (maintains reputation 75, gains compliance bonus)
- **Option B**: Secretly negotiate side deal (risks -15 if caught, no upside)
- **Option C**: Public sanctions (drops to 68 from "aggressive" label, but signals strength)

### 2. Strategic Personalities - Choose Your Negotiation Style

**What It Does**:
You pick a behavioral "doctrine" that determines how your country responds to others' actions. Like choosing aggressive vs defensive in poker, or rush vs turtle in strategy games.

**How It Works**:
Six core strategies, each with different risk/reward profiles:

#### Tit-for-Tat (The Mirror)
- **Rule**: Whatever you did to me last turn, I do to you this turn
- **Memory**: Only remembers last action
- **Reputation effect**: +5 per turn (seen as fair and predictable)
- **Best against**: Other cooperative players
- **Vulnerable to**: Accidental escalation spirals

#### Grim Trigger (The Grudge Holder)
- **Rule**: One betrayal = permanent maximum retaliation forever
- **Memory**: Never forgets
- **Reputation effect**: -2 per turn in punishment mode (seen as inflexible)
- **Best against**: Deterring cheaters
- **Vulnerable to**: Mistakes locking you into bad equilibria

#### Tit-for-Two-Tats (The Patient Partner)
- **Rule**: Only retaliate after TWO consecutive betrayals
- **Memory**: 2 turns
- **Reputation effect**: +3 per turn (seen as reasonable)
- **Best against**: Noisy environments where accidents happen
- **Vulnerable to**: Systematic exploitation

#### Gradual (The Escalator)
- **Rule**: First betrayal = 1 turn retaliation. Second = 2 turns. Third = 3 turns. Then 2 turns of cooperation attempt.
- **Memory**: Full history with slow decay
- **Reputation effect**: Neutral
- **Best against**: Teaching lessons without permanent warfare
- **Vulnerable to**: Complex coordination failures

#### Bandwagon (The Follower)
- **Rule**: Do what majority (50%+) of your trade partners are doing
- **Memory**: Current consensus only
- **Reputation effect**: Follows group average
- **Best against**: Risk-averse situations, maintaining acceptability
- **Vulnerable to**: Herd behavior off cliffs

#### Contrarian (The Maverick)
- **Rule**: Deliberately oppose majority strategy
- **Memory**: Current consensus to oppose
- **Reputation effect**: +10 if successful, -10 if fails (volatile)
- **Best against**: Exploiting overcrowded strategies
- **Vulnerable to**: High variance, potential isolation

**Strategic Implications**:
You can switch strategies mid-game, but it costs 5 reputation points (like breaking character suddenly raises suspicion).

**Example Scenario**:
USA plays Tit-for-Tat. China imposes 10% tariff (Turn 1). USA mirrors with 10% tariff (Turn 2). China, expecting escalation, sees USA is purely mirroring and switches to Gradual strategy. Both players now know the pattern and can negotiate.

### 3. Learning & Adaptation - Your Country Gets Smarter

**What It Does**:
Countries aren't static. They experiment with strategies, track what works, and optimize over time. Like machine learning for geopolitics.

**How It Works**:

#### The Exploration vs Exploitation Dial
- **High exploration (20% random)**: Try new strategies often, volatile results, discover hidden opportunities
- **Low exploration (5% random)**: Stick with proven winners, stable but potentially suboptimal
- **Default setting**: 10% exploration (one experimental move every 10 turns)

#### The Learning Speed Slider
- **Fast learning (30% update rate)**: Quick adaptation to new information, but prone to overreaction
- **Slow learning (10% update rate)**: Stable beliefs, but slow to adjust to changing environment
- **Default setting**: 10% update rate (moderate adaptation)

#### What Your Country Learns
Every action generates a "score" combining:
- **Economic outcome**: GDP growth, trade balance improvement
- **Reputation change**: Did this help or hurt your standing?
- **Strategic objectives**: Did you achieve your geopolitical goals?

The system tracks which (State, Action) combinations historically produced best scores. Over 10-20 turns, you'll see countries gravitate toward successful strategies.

**Strategic Implications**:
- **Early game**: Everyone's learning. Exploit this with fake patterns (feint aggression, then cooperate).
- **Mid game**: Patterns emerge. Reading others' learning helps predict their moves.
- **Late game**: Optimize learned strategies. Surprise moves have higher impact because they're unexpected.

**Example Scenario**:
Turn 1-5: Japan tries high tariffs → GDP drops 1%, reputation drops to 45. Score: -15.
Turn 6-10: Japan tries moderate tariffs + subsidies → GDP up 2%, reputation steady. Score: +20.
Turn 11+: Japan has "learned" that moderate protection + subsidies beats pure protectionism. Will favor this strategy unless environment changes.

### 4. Crisis Contagion - Economic Shocks Spread Like Viruses

**What It Does**:
When one country experiences a crisis (financial collapse, sanctions, trade war), the shock can spread to connected neighbors. Like dominoes, but with probabilistic transmission.

**How It Works**:

#### The Infection Model
Each crisis has a "transmission probability" (default: 30%). For each country connected by trade:
1. Calculate exposure = (trade with crisis country / your GDP)
2. If exposure exceeds threshold (default: 50% of your reserves), you're "pressured"
3. Roll dice: 30% chance the crisis spreads to you at reduced intensity
4. Your resilience (based on reserves, diversification) reduces impact

#### Resilience Factors
- **Financial reserves**: High reserves (>20% GDP) = 80% resilience
- **Trade diversification**: Many small partners > few large partners = +30% resilience
- **High reputation**: Reputation 70+ = +40% resilience (market confidence)

#### Chain Reaction Limits
- Maximum 10 rounds of spreading (prevents infinite cascades)
- Automatic "firebreaks" activate if 40%+ countries affected
- Early warning system alerts when contagion risk exceeds 50%

**Strategic Implications**:
- **Offensive use**: Target highly connected "hub" countries to maximize cascade
- **Defensive use**: Diversify trade partners, build reserves, maintain high reputation
- **Opportunistic use**: Stay safe during crisis, buy distressed assets, gain market share

**Example Scenario**:
Turkey defaults on debt (reputation crashes to 15).
- **Greece** (15% trade exposure to Turkey): Pressure = 0.15 × 0.6 = 0.09, below threshold (0.10), safe but cautious
- **Bulgaria** (25% trade exposure): Pressure = 0.25 × 0.6 = 0.15, exceeds threshold → 30% chance of contagion
- **Dice roll**: Bulgaria gets unlucky (rolled 22%), hit with 60% intensity crisis
- **Italy** (exposed to Bulgaria): Second-order risk now active...

Game activates dampening: IMF-style support fund opens, reputation decay slowed 50%, crisis contained to 2 countries directly + 4 minor impacts.

### 5. Coalition Formation - Strength in Numbers

**What It Does**:
Countries can form alliances and trade blocs for mutual benefit. Like guild formation in MMOs - more powerful together, but coordination costs and free-rider problems.

**How It Works**:

#### Coalition Value Formula
A coalition's total value =
- **Trade benefits**: All internal trade gets 10% bonus (tariff-free movement)
- **Security benefits**: Combined military power (square root of sum) × shared threat level
- **Coordination costs**: Grows with coalition size² × internal disagreement × friction

Bigger isn't always better. Three aligned powers beat five squabbling nations.

#### Your Share (Shapley Value)
Your slice of the coalition pie depends on:
- What you bring to the table (GDP, military, strategic location)
- What the coalition loses if you leave
- Fair division formula ensures everyone gets at least solo value

#### Stability Check
Coalition stays together only if every member gets more than they'd get alone. Otherwise, someone defects and it collapses.

**Strategic Implications**:
- **Early formation bonus**: First-mover advantage in recruiting best partners
- **Leadership role**: Largest economy typically leads, sets agenda, but bears higher costs
- **Conditional cooperation**: Many players adopt "I'll comply if 80% of members comply" strategy
- **Strategic hedging**: Stay observer without joining, retain flexibility

**Example Scenario**:
USA proposes anti-China coalition to EU, Japan, Australia, India:
- **EU**: 75% acceptance (worried about costs, demands tech sharing)
- **Japan**: 85% acceptance (strong security alignment)
- **Australia**: 90% acceptance (economic dependence on USA)
- **India**: 40% acceptance (still does massive China trade, prefers neutrality)

Coalition forms with USA/EU/Japan/Australia. India stays observer. Coalition implements coordinated 15% tech tariffs. China retaliates with rare earth restrictions. Coalition trade internally increases 12% (trade diversion from China). All members take -5 reputation hit (seen as protectionist bloc).

### 6. Escalation Ladders - Controlled vs Runaway Conflicts

**What It Does**:
Conflicts don't just happen - they escalate step by step. You control whether disputes spiral into trade wars or stabilize at manageable tensions.

**How It Works**:

#### The Escalation Ladder (10 Rungs)
1. **Verbal warning** - Diplomatic note (no economic impact)
2. **Targeted investigation** - Selective enforcement (+5% costs on specific goods)
3. **Symbolic tariff** - 5-10% on narrow category
4. **Broad tariff** - 10-25% on major sector
5. **Strategic embargo** - Block critical goods (chips, energy)
6. **Full trade restriction** - 50%+ tariff across board
7. **Financial sanctions** - Freeze assets, cut off capital flows
8. **Secondary sanctions** - Punish third parties who trade with target
9. **Blockade/disruption** - Physical interference with trade
10. **Military action** - Kinetic conflict (outside this module's scope)

#### Escalation Dynamics
- Each rung up costs you 3-5 reputation points
- Each rung triggers expected retaliation at same or +1 level
- De-escalation (going down ladder) restores 2 reputation per rung
- "Off-ramps" - predefined conditions for backing down without losing face

#### Automatic Cooling Periods
If retaliation chains exceed 5 rounds, system forces 2-turn "cooling period" where no new escalations allowed (like mandatory timeouts in fights).

**Strategic Implications**:
- **Controlled escalation**: Move up one rung at a time, signal willingness to stop
- **Shock and awe**: Jump 3+ rungs immediately for surprise effect (high risk)
- **Strategic ambiguity**: Threaten high rungs, implement low rungs (bluffing)
- **De-escalation credibility**: Publicly define off-ramps before escalating (preserves reputation)

**Example Scenario**:
USA discovers China semiconductor dumping:
- **Turn 1**: USA at Rung 2 (investigation), reputation 65
- **Turn 2**: USA jumps to Rung 4 (25% tariff on chips), reputation 60, China retaliates at Rung 4
- **Turn 3**: USA at Rung 5 (embargo on advanced chips), reputation 55, China at Rung 6 (broad restrictions)
- **Turn 4**: Early warning triggers - 4 rounds deep, approaching forced cooling
- **Turn 5**: Both players define off-ramps (USA: "remove if subsidy ends", China: "remove if tariff drops to 10%")
- **Turn 6**: Negotiation begins, both climb down to Rung 3, reputation recovers +4

## Turn-by-Turn Behavioral Factors

### What Affects Your Decision Each Turn

Every turn, your behavioral module processes:

1. **Memory Check**: What did other countries do last 1-10 turns (depending on your strategy)?
2. **Belief Update**: What strategies do you think they're playing? Update your mental model.
3. **Learning Signal**: Did your last action produce good or bad results? Update strategy scores.
4. **Reputation Calculation**: Apply compliance, restraint, loyalty, transparency weights → new reputation.
5. **Network Scan**: Is any crisis brewing nearby? Calculate contagion exposure.
6. **Strategy Selection**: Based on updated beliefs and learned values, choose action:
   - 90% of time: Best known action (exploitation)
   - 10% of time: Random experiment (exploration)
7. **Coalition Check**: If in alliance, verify partners' compliance, adjust loyalty score.
8. **Escalation Review**: Are you in active conflict? Where on ladder? Off-ramp available?

### The Information You See

**Public Information** (everyone sees):
- All countries' current reputation scores
- Public coalition memberships
- Official tariff and sanction announcements
- Trade volumes (aggregate level)

**Private Information** (only you see):
- Your Q-learning table (which strategies you've learned work best)
- Your beliefs about others' strategies (are they Tit-for-Tat or Grim Trigger?)
- Your exploration rate and learning speed settings
- Your planned escalation paths and off-ramps

**Inferred Information** (you can deduce):
- Others' likely strategies by observing action patterns
- Coalition stability by watching for defections
- Crisis contagion paths by mapping trade network
- Reputation trends by tracking behavior changes

## Strategic Opportunities

### How Savvy Players Exploit Behavioral Mechanics

#### 1. Reputation Arbitrage
**The Play**: Deliberately sacrifice short-term reputation for long-term gain.
**Example**: Drop from 60 to 45 reputation by aggressive move, capture strategic industry, then slowly rebuild over 10 turns while reaping industry benefits.
**Risk**: Contagion exposure during low-reputation period.

#### 2. Strategy Signaling
**The Play**: Loudly announce your strategy (e.g., "I'm playing Grim Trigger"), then follow through.
**Example**: Announce "one strike and you're out" policy. First violation, permanent embargo. Others learn to never test you.
**Risk**: You're locked in - must follow through even when costly.

#### 3. Learning Exploitation
**The Play**: Feed opponents fake patterns early, then switch once they've "learned" the wrong lesson.
**Example**: Cooperate for 5 turns while opponent learns "they're friendly." Turn 6, defect for massive one-time gain before they adapt.
**Risk**: Reputation destruction, opponents switch to Grim Trigger against you.

#### 4. Coalition Surfing
**The Play**: Join coalitions for benefits, exit before costs materialize.
**Example**: Enter tech alliance for IP sharing, extract value for 3 turns, exit claiming "changed strategic priorities" before burden-sharing requirements kick in.
**Risk**: -20 loyalty score, difficult to join future coalitions.

#### 5. Crisis Opportunism
**The Play**: Position yourself as safe haven during contagion events.
**Example**: When Turkey-Greece crisis hits, maintain high reputation (70+) and diversified trade. Capital and trade flows redirect to you. Gain 15% market share.
**Risk**: None if positioned defensively; high resilience prevents contagion.

#### 6. Escalation Chicken
**The Play**: Rapidly escalate to high rung, bet opponent blinks first.
**Example**: Jump from Rung 1 to Rung 6 (financial sanctions) immediately. If opponent backs down, gain dominance. If they match, both lose.
**Risk**: Mutual destruction if both players are stubborn. Reputation cost even if you win.

#### 7. Reputation Recovery Timing
**The Play**: Plan reputation dips during low-stakes periods, recover before critical moments.
**Example**: Execute controversial moves during global boom (attention elsewhere). Rebuild reputation before election year or crisis when you need allies.
**Risk**: Unexpected crisis during low-reputation window leaves you vulnerable.

#### 8. Bandwagon Manipulation
**The Play**: If you're large economy, shift strategy knowing Bandwagon players will follow.
**Example**: USA switches to protectionism. 40% of global GDP follows. Now you're in majority, Bandwagon countries join your bloc, further tipping balance.
**Risk**: Creates polarized world, reduces overall trade efficiency.

## Common Player Mistakes

### Behavioral Traps and How to Avoid Them

#### Mistake 1: Reputation Neglect
**The Trap**: Ignoring reputation score, focusing only on GDP and trade balance.
**Why It Hurts**: Low reputation raises all trade costs 50-100%, erasing economic gains. Triggers crisis contagion vulnerability.
**Avoidance**: Check reputation each turn. If below 50, implement transparency boost and compliance signals.

#### Mistake 2: Overescalation
**The Trap**: Responding to small provocation with maximum retaliation (Rung 1 → Rung 8).
**Why It Hurts**: -25 reputation, triggers coalition against you, locks into costly conflict.
**Avoidance**: Climb escalation ladder one rung at a time. Define off-ramps before climbing.

#### Mistake 3: Grim Trigger Lock-In
**The Trap**: Using Grim Trigger strategy, then triggering permanent punishment after accident.
**Why It Hurts**: Trapped in suboptimal equilibrium forever. Both sides lose indefinitely.
**Avoidance**: Use Gradual or Tit-for-Two-Tats for more forgiveness. Reserve Grim Trigger for existential threats only.

#### Mistake 4: Learning Too Slowly
**The Trap**: Keeping learning rate at 5%, taking 30+ turns to adapt to changed environment.
**Why It Hurts**: Opponents learn faster, discover optimal strategies first, exploit your rigidity.
**Avoidance**: Increase learning rate to 15-20% during uncertain periods. Slow to 5-10% once stable pattern emerges.

#### Mistake 5: Coalition Free-Riding
**The Trap**: Join coalition, minimize contributions, hope others carry burden.
**Why It Hurts**: Loyalty score drops, coalition kicks you out, lose all benefits including reputation bonus.
**Avoidance**: Contribute proportionally to Shapley value. If coalition demands exceed value, negotiate or exit honorably.

#### Mistake 6: Ignoring Network Position
**The Trap**: Concentrating trade with few large partners (e.g., 80% trade with one country).
**Why It Hurts**: High contagion exposure. If that partner hits crisis, you're automatically infected.
**Avoidance**: Diversify trade. No single partner above 30% of trade volume. Monitor network centrality metrics.

#### Mistake 7: Exploration Addiction
**The Trap**: Setting exploration rate to 30%, constantly experimenting with random strategies.
**Why It Hurts**: Volatile outcomes, partners can't predict you, reduces cooperation, wastes learning potential.
**Avoidance**: Explore heavily (20%) for first 10 turns, then drop to 5-10% once you've mapped strategy space.

#### Mistake 8: Reputation Hoarding
**The Trap**: Maintaining reputation 90+ by never taking controversial actions.
**Why It Hurts**: Miss strategic opportunities. Other players exploit your predictability.
**Avoidance**: Reputation is a resource to spend, not hoard. Optimal range: 60-75. Dip to 50 for high-value moves, rebuild to 70.

#### Mistake 9: Bandwagon Following into Crisis
**The Trap**: Using Bandwagon strategy, following majority over cliff.
**Why It Hurts**: If consensus is wrong (e.g., everyone escalates trade war), you crash with the herd.
**Avoidance**: Monitor "systemic stress index." If above 0.6, override Bandwagon with independent judgment.

#### Mistake 10: Belief Ossification
**The Trap**: Forming fixed beliefs about opponents' strategies (e.g., "China always defects"), ignoring contradicting evidence.
**Why It Hurts**: Opponents change strategies, but you don't notice. Cooperation opportunities missed.
**Avoidance**: Weight recent observations heavily (30% update rate for beliefs). Reassess opponent strategy every 5 turns.

## Integration with Other Systems

### How Behavioral Mechanics Connect to Other Modules

#### With Pricing & Market Equilibrium
**Connection**: Your reputation directly impacts transaction costs.
- Reputation 80: Transaction costs × 0.6 (40% discount)
- Reputation 50: Transaction costs × 1.0 (baseline)
- Reputation 20: Transaction costs × 1.5 (50% penalty)

**Gameplay Impact**: High reputation means your goods are cheaper to trade. Markets trust you, reducing friction. Low reputation adds "risk premium" to every transaction.

#### With Trade Flow Module
**Connection**: Coalition memberships determine preferential tariff rates.
- Inside coalition: 10% tariff reduction on all intra-coalition trade
- Outside coalition: Standard MFN (Most Favored Nation) rates
- Sanctioned/low reputation: Additional 20-100% penalty tariff

**Gameplay Impact**: Being in the "right" coalition can triple your effective market access. Outside looking in? You're paying premium rates.

#### With Sanctions & Geopolitics Module
**Connection**: Escalation ladder position determines sanction severity and retaliation probability.
- Rung 1-3: Diplomatic, minimal economic impact
- Rung 4-6: Moderate sanctions, 10-30% trade reduction
- Rung 7-9: Severe sanctions, 50-90% trade reduction

**Gameplay Impact**: Sanctions aren't binary (on/off). They escalate gradually. Behavioral strategy determines whether you climb or descend the ladder.

#### With Compliance & Cheating Detection
**Connection**: Reputation affects detection probability and investigation frequency.
- Reputation 80+: 50% baseline detection rate (trusted, less scrutiny)
- Reputation 50: 100% baseline detection rate (standard)
- Reputation 20-: 200% detection rate (constant surveillance)

**Gameplay Impact**: Cheating when your reputation is low is suicide - you'll get caught. High reputation gives cover for occasional rule-bending.

#### With Demand Module
**Connection**: Crisis contagion affects consumer confidence and demand elasticity.
- Normal state: Demand responds predictably to price
- Crisis state: Panic buying (hoarding) or demand collapse (uncertainty)
- Contagion: Demand shocks spread through network

**Gameplay Impact**: Financial crises don't just hit the origin country - they depress demand across connected partners. Your exports drop even if your economy is fine.

#### With Currency Strategy Module
**Connection**: Devaluation strategies interact with reputation system.
- Small devaluation (< 5%): No reputation impact, export boost
- Medium devaluation (5-10%): -3 reputation, triggers retaliation probability
- Large devaluation (> 10%): -10 reputation, triggers currency war game

**Gameplay Impact**: Competitive devaluation is a multiplayer game. If everyone devalues, no one gains advantage. Behavioral strategies determine whether escalation happens.

#### With Agent Intelligence Module
**Connection**: Q-learning values inform AI strategy suggestions.
- AI reads your Q-table: "Your learned optimal strategy is X"
- AI reads opponents' observed patterns: "China likely playing Gradual strategy"
- AI suggests coalitions: "High Shapley value opportunity with EU/Japan"

**Gameplay Impact**: The AI isn't omniscient - it learns alongside you. Early game, suggestions are exploratory. Late game, AI has decoded the meta and offers refined advice.

## Quick Reference: Behavioral Cheat Sheet

### Reputation Score Guide
- **90-100**: Superpower status, can lead coalitions, 40% cost reduction
- **70-89**: Strong standing, preferred partner, 20% cost reduction
- **50-69**: Normal country, standard rates, no bonuses or penalties
- **30-49**: Risky partner, 25% cost penalty, limited cooperation
- **10-29**: Pariah state, 75% cost penalty, isolated
- **0-9**: Failed state, 100% cost penalty, embargo risk

### Strategy Selection Quick Guide
| If Opponent Is... | Your Best Counter | Why |
|------------------|------------------|-----|
| Aggressive (frequent defection) | Grim Trigger | Deter with permanent punishment threat |
| Cooperative (consistent cooperation) | Tit-for-Tat | Mutual cooperation, occasional forgiveness |
| Unpredictable (random) | Gradual | Controlled escalation, built-in forgiveness |
| Weak reputation (< 40) | Exploit (defect) | Low-cost target, limited retaliation capability |
| Strong reputation (> 70) | Cooperate | Building relationship pays off long-term |
| Leading coalition | Bandwagon | Join winning side, share benefits |

### Learning Settings by Game Phase
| Game Phase | Exploration Rate | Learning Rate | Why |
|-----------|----------------|--------------|-----|
| Early (Turns 1-10) | 20% | 15% | Discover strategy space, rapid adaptation |
| Mid (Turns 11-30) | 10% | 10% | Refine strategies, moderate adaptation |
| Late (Turns 31+) | 5% | 5% | Optimize learned strategies, stability |
| Crisis/Uncertainty | 15% | 20% | Environment changed, relearn fast |

### Crisis Contagion Risk Assessment
**Check These Three Factors:**
1. **Trade concentration**: Is 30%+ of your trade with any single partner? (High risk)
2. **Reserve buffer**: Are reserves below 10% of GDP? (High risk)
3. **Network centrality**: Are you trading with 8+ crisis-affected countries? (High risk)

**Risk Mitigation Priority**:
- 3 high-risk factors: URGENT - diversify immediately, build reserves, hedge exposure
- 2 high-risk factors: WARNING - implement defensive measures next 3 turns
- 1 high-risk factor: MONITOR - prepare contingency plans
- 0 high-risk factors: SAFE - consider opportunistic expansion

### Escalation Ladder Decision Tree
```
Small dispute (< $10B impact):
  → Rung 1-2: Verbal warning, investigation
  → Off-ramp: Apology + compensation

Medium dispute ($10-50B impact):
  → Rung 3-5: Targeted tariffs, sector embargo
  → Off-ramp: Negotiated settlement + policy change

Large dispute (> $50B or strategic assets):
  → Rung 6-8: Broad sanctions, financial restrictions
  → Off-ramp: Mediation + third-party guarantees

Existential threat:
  → Rung 9-10: Blockade, military action
  → Off-ramp: International coalition + security guarantees
```

### Coalition Value Quick Calc
**Does This Coalition Make Sense?**
1. Add up internal trade among all members → A
2. Multiply by 1.10 (10% efficiency bonus) → B
3. Add square root of combined military power → C
4. Subtract (# members)² × 0.1 × heterogeneity → D
5. Net value = B + C - D

**If your share (Shapley value) exceeds what you'd get solo + 20%, join. Otherwise negotiate better terms or stay independent.**

### Red Flags: System Instability Alerts
**If You See These Indicators, Reduce Risk Exposure:**
- Average global reputation below 45 → Cooperation breakdown likely
- Trade volume down 30%+ from baseline → Crisis cascade possible
- 5+ round retaliation chain → Forced cooling period incoming
- 40%+ countries in crisis → Systemic contagion mode
- Polarization index above 0.7 → Bloc formation, fragmentation ahead

### One-Turn Behavioral Checklist
Every turn, ask yourself:
1. Did my reputation move 5+ points? (Check causes, adjust strategy)
2. Are any neighbors in crisis? (Calculate contagion exposure)
3. Did opponents change strategies? (Update beliefs, adjust counter)
4. Am I in escalation chain 3+ rounds deep? (Plan off-ramp or prepare for forced cooling)
5. Is exploration rate appropriate for current uncertainty? (Adjust as needed)
6. Does my coalition still provide net positive value? (Check Shapley value vs solo alternative)
7. What did I learn this turn? (Update Q-values for state-action pairs)

---

## Final Thought: Behavioral Mechanics as Strategic Depth

In simpler economic games, optimal strategy is often "always defect" or "always cooperate." In UTA, the behavioral module ensures context matters:

- **Against weak opponents**: Exploit
- **Against strong reputations**: Cooperate to build trust
- **In stable periods**: Optimize learned strategies
- **In crises**: Explore aggressively for new approaches
- **As leader**: Signal clearly, build reputation
- **As challenger**: Strategic defection with calculated risk

Your country isn't just an economy - it's a learning entity with memory, reputation, and evolving strategy. Master the behavioral layer, and you master the meta-game behind the economics.

The best players don't just optimize GDP. They optimize reputation trajectory, coalition positioning, learning speed, and crisis resilience simultaneously. That's the art of behavioral economics in UTA.
