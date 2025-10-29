# Agent Intelligence Module

## Overview

The Agent Intelligence Module serves as the **Strategic Command Orchestrator** - the interface between high-level player vision and detailed simulation mechanics. Players act as visionary leaders who issue strategic directives ("Conquer Egypt!", "Dominate semiconductor supply chain", "Build Asian trade coalition") without concerning themselves with implementation details.

The module orchestrates specialist subagents, aggregates their analyses, and delivers executive summaries that enable decision-making at the strategic level while ensuring all actions are grounded in rigorous economic, military, and geopolitical modeling.

---

## Core Concept: The Visionary Leader Model

### Player Role
- Issues **high-level strategic directives** in natural language
- Reviews **executive summaries** (2-page reports with key metrics, risks, costs, timelines)
- Makes **approve/reject/modify decisions** based on synthesized intelligence
- **Never** deals with implementation details, formulas, or low-level mechanics

### Agent Intelligence Module Role
- **Interprets** strategic intent from natural language
- **Spawns** necessary specialist subagents dynamically
- **Coordinates** parallel analysis across economic, military, diplomatic, and behavioral domains
- **Aggregates** specialist outputs into coherent strategic assessment
- **Extends game rules** when strategies require novel mechanics
- **Generates** executive decision packages for player approval

---

## Architecture

### 1. Input Processing Layer

**Input**: Natural language strategic directive

**Examples**:
- "Conquer Egypt!"
- "Sanction Russia's energy sector to collapse their economy"
- "Form a semiconductor trade bloc with Taiwan, South Korea, and Japan"
- "Launch a currency war against the United States"
- "Dominate global steel production through subsidies and dumping"

**Processing Steps**:
1. **Intent Extraction**: Parse directive using LLM to identify:
   - Strategic objective (conquer, sanction, form alliance, manipulate market, etc.)
   - Target entities (countries, sectors, products, trade routes)
   - Implied constraints (timeframe, cost tolerance, escalation limits)
   - Success metrics (control, market share, price impact, compliance)

2. **Scope Analysis**: Determine which game systems are affected:
   - Military/territorial control
   - Trade flows and tariffs
   - Currency/financial markets
   - Industrial policy and subsidies
   - Sanctions and compliance
   - Energy and logistics
   - Geopolitical relationships and coalitions

3. **Novelty Detection**: Identify if strategy requires:
   - **Standard mechanics** (already in game rules) → Use existing modules
   - **Rule extension** (new but compatible mechanics) → Generate new rules
   - **Core modification** (fundamental new gameplay) → Flag for human review

---

### 2. Subagent Spawning System

**Dynamic Agent Creation**: Based on scope analysis, spawn necessary specialist agents

#### Subagent Registry

##### **Economist Agent**
- **Triggers**: Any strategy affecting trade, production, prices, subsidies
- **Responsibilities**:
  - Run CGE equilibrium analysis for proposed actions
  - Calculate GDP impact, sectoral employment effects, price changes
  - Estimate deadweight losses, consumer/producer surplus shifts
  - Model supply chain disruptions and elasticity effects
  - Forecast trade balance and current account changes
- **Outputs**: Economic impact matrix (GDP delta, inflation, trade flows, welfare)

##### **Geopolitical Strategist Agent**
- **Triggers**: Territorial actions, alliance formation, sanctions, diplomatic moves
- **Responsibilities**:
  - Assess alliance formation probabilities
  - Model third-party reactions (bandwagoning, balancing, neutrality)
  - Evaluate reputation costs and trust erosion
  - Calculate UTA credit system impacts
  - Identify escalation pathways and de-escalation options
- **Outputs**: Geopolitical risk matrix (alliance shifts, retaliation probability, escalation ladder)

##### **Military Analyst Agent**
- **Triggers**: Military actions (blockades, cyberattacks, invasions, shows of force)
- **Responsibilities**:
  - Calculate military costs (operational, equipment, casualties)
  - Estimate success probabilities based on force ratios
  - Model duration and attrition dynamics
  - Assess detection/attribution probabilities
  - Evaluate counter-escalation risks
- **Outputs**: Military feasibility assessment (cost, duration, success probability, escalation risk)

##### **Financial and Currency Strategist Agent**
- **Triggers**: Currency manipulation, capital controls, reserve policy, bond issuance
- **Responsibilities**:
  - Model exchange rate impacts of interventions
  - Calculate capital flow responses
  - Estimate reserve adequacy and sustainability
  - Assess contagion risks to financial sector
  - Forecast interest rate and inflation effects
- **Outputs**: Financial stability report (FX impact, reserve drain, capital flight risk, inflation)

##### **Energy Analyst Agent**
- **Triggers**: Actions affecting energy production, trade, sanctions on energy exporters
- **Responsibilities**:
  - Model energy supply disruptions and price shocks
  - Calculate transport cost changes and logistics bottlenecks
  - Assess strategic reserve adequacy
  - Estimate transition costs for alternative suppliers
  - Evaluate energy security vulnerabilities
- **Outputs**: Energy security assessment (supply risk, price impact, transition costs)

##### **Behavioral and Systems Analyst Agent**
- **Triggers**: All strategies (systemic stability check mandatory)
- **Responsibilities**:
  - Identify potential system instabilities (cascading failures, runaway dynamics)
  - Model other agents' likely responses using game theory
  - Calculate Nash equilibria and predict counter-strategies
  - Assess reputation effects on future cooperation
  - Monitor network contagion risks
- **Outputs**: Systemic risk report (stability indicators, predicted responses, equilibrium analysis)

##### **Compliance and Detection Analyst Agent**
- **Triggers**: Cheating strategies (origin laundering, subsidy concealment, sanctions evasion)
- **Responsibilities**:
  - Calculate detection probabilities based on enforcement spending
  - Model forensic trail visibility (data opacity, transaction complexity)
  - Estimate penalties if caught (UTA credits, tariffs, sanctions)
  - Assess expected value of cheating (gains vs. risk-adjusted costs)
  - Recommend compliance vs. evasion strategies
- **Outputs**: Compliance risk-reward analysis (detection probability, penalty severity, expected payoff)

---

### 3. Coordination and Task Delegation

**Orchestrator Workflow**:

```
Strategic Directive Input
    ↓
[Intent Extraction + Scope Analysis]
    ↓
[Spawn Subagents: Economist, Strategist, Military, etc.]
    ↓
[Parallel Execution]
    ├─→ Economist: Run CGE impact model
    ├─→ Strategist: Assess geopolitical reactions
    ├─→ Military: Calculate operational costs
    ├─→ Financial: Model currency effects
    ├─→ Energy: Evaluate supply security
    ├─→ Behavioral: Check system stability
    └─→ Compliance: Assess detection risk
    ↓
[Aggregation Layer]
    ↓
[Conflict Resolution & Synthesis]
    ↓
[Executive Summary Generation]
    ↓
[Present to Player: 2-Page Decision Package]
```

**Coordination Mechanisms**:
- **Parallel execution**: All subagents run simultaneously for speed
- **Shared context**: All agents access same game state snapshot (prices, trade flows, alliances, etc.)
- **Cross-agent dependencies**: Military costs feed into Economist GDP calculations; Currency impacts feed into Trade flow projections
- **Conflict resolution**: If subagents produce contradictory assessments, flag conflicts and present alternative scenarios

---

### 4. Rule Extension for Extraordinary Strategies

**When**: Player proposes strategy not covered by existing game rules

**Process**:
1. **Gap Identification**: Subagent identifies missing mechanics
   - Example: "Conquer Egypt" requires territorial control mechanics not yet in simulation

2. **Rule Generation**:
   - Subagent drafts new rule specification grounded in economic/military theory
   - Defines state changes (territory ownership, resource control, population)
   - Specifies integration with existing modules (trade flows rerouted, GDP recalculated)
   - Proposes parameter values with empirical justification

3. **Validation**:
   - Check consistency with CGE equilibrium constraints
   - Ensure no explosive dynamics or undefined edge cases
   - Verify compatibility with existing rule set

4. **Flowchart Generation**:
   - Convert rule logic to Mermaid flowchart for visual approval

5. **Code Generation**:
   - Use agentic coding to implement rule as executable Python code
   - Integrate with Mesa agent framework and CGE solver

6. **Rule Library Update**:
   - Add to permanent rule set
   - Tag as "player-generated" with disclosure flag
   - Allow sharing with other players (algorithmic transparency)

**Example**: "Conquer Egypt" Extension
- **New Rule**: "Territorial Annexation Mechanics"
  - Military victory → ownership transfer → Egypt's GDP added to conqueror's economy
  - Trade flows recalculated (Egypt-origin exports now show as conqueror's exports)
  - Factor markets integrated (Egypt's labor/capital added to conqueror's factor supply)
  - UTA penalty: -5000 credits for territorial aggression
  - Reputation cost: -80 with all countries, enables counter-coalitions

---

### 5. Aggregation and Synthesis Layer

**Inputs**: Reports from all spawned subagents

**Aggregation Process**:
1. **Extract Key Metrics** from each subagent report:
   - Economist: GDP delta, inflation, trade balance change
   - Strategist: Alliance shift probability, retaliation risk
   - Military: Cost, duration, success probability
   - Financial: FX impact, reserve drain
   - Energy: Supply disruption magnitude
   - Behavioral: System stability score
   - Compliance: Detection probability, penalty exposure

2. **Conflict Identification**:
   - Flag contradictions (e.g., Economist predicts +2% GDP, but Energy predicts oil shock causing -3% GDP)
   - Resolve using sensitivity analysis or present both scenarios

3. **Scenario Generation**:
   - **Base Case**: Most likely outcome
   - **Best Case**: Upper bound of favorable outcomes
   - **Worst Case**: Cascading failures and worst-case reactions
   - **Expected Value**: Probability-weighted across scenarios

4. **Risk-Adjusted Scoring**:
   - Calculate expected utility: E[Utility] = Σ P(scenario) × Utility(scenario)
   - Identify risk factors (high variance, tail risks, irreversible commitments)

5. **Strategic Alternatives**:
   - If strategy has low expected value or high risk, propose alternatives
   - Example: Instead of "Conquer Egypt" (high cost, low success), suggest "Economic Dominance via Belt & Road Infrastructure Investment"

---

### 6. Executive Summary Generation

**Format**: 2-Page Decision Package for Player

#### **Page 1: Strategic Overview**

**DIRECTIVE**: [Restate player's input]
*Example: "Conquer Egypt to control Suez Canal trade route"*

**EXECUTIVE SUMMARY**: [3-4 sentence strategic assessment]
*Example: "Military annexation of Egypt would cost $450B over 18 months with 65% success probability. Economic gains (+$120B GDP from Suez control) are offset by sanctions, coalition formation, and UTA penalties (-$380B net present value). Recommend alternative: Negotiate preferential Suez access rights via infrastructure investment at 1/10th the cost."*

**KEY METRICS**:
| Metric | Value | Confidence |
|--------|-------|------------|
| Net Economic Impact (20yr NPV) | -$380B | 75% |
| Military Cost | $450B | 80% |
| Success Probability | 65% | 60% |
| Duration | 18 months | 70% |
| Escalation Risk | 85% (regional war) | 65% |
| UTA Credit Penalty | -5000 credits | 95% |
| Reputation Loss | -80 (global avg) | 90% |

**RISK FACTORS**:
- **Critical**: 85% probability of counter-coalition (NATO, Arab League)
- **High**: Oil supply disruption → global price shock (+$40/barrel)
- **Medium**: Domestic opposition and war fatigue
- **Low**: Nuclear escalation (5% if conflict extends to Israel/Iran)

**STRATEGIC ALTERNATIVES**:
1. **Negotiate Suez Access Rights**: Cost $45B, Success 90%, NPV +$220B
2. **Build Alternative Route (Land Bridge)**: Cost $120B, 15-year timeline, NPV +$80B
3. **Economic Sanctions + Regime Change Support**: Cost $15B, Success 35%, NPV +$60B (if successful)

---

#### **Page 2: Detailed Impact Analysis**

**ECONOMIC IMPACT** (from Economist Agent):
- GDP: +$120B from Suez control, -$500B from sanctions and war costs = **-$380B net**
- Trade Balance: -$60B/year during conflict (import surge for military supplies)
- Inflation: +4.5% (war spending + oil shock)
- Employment: -1.2M jobs in export sectors (due to sanctions)

**GEOPOLITICAL IMPACT** (from Strategist Agent):
- **Counter-Coalition Probability**: 85% (NATO + Arab League + possibly China/Russia)
- **Alliance Erosion**: Lose preferential trade with EU (-$80B/year)
- **UTA Status**: Expelled from T3C, lose all trade credits (worth $200B)

**MILITARY ASSESSMENT** (from Military Agent):
- **Force Requirements**: 250,000 troops, 400 aircraft, 2 carrier groups
- **Operational Cost**: $450B (18-month campaign)
- **Casualty Estimate**: 8,000-15,000 KIA, 40,000-60,000 WIA
- **Success Factors**: Air superiority (high), urban warfare (medium), insurgency suppression (low)

**FINANCIAL IMPACT** (from Currency Strategist):
- **Currency**: -15% depreciation (capital flight + sanctions)
- **Reserves**: -$200B drawdown to defend currency
- **Borrowing Costs**: +300 bps (sovereign spread widening)

**ENERGY SECURITY** (from Energy Analyst):
- **Oil Price Shock**: +$40/barrel (Suez closure during conflict)
- **Global Impact**: -0.8% world GDP (if conflict extends >6 months)
- **Strategic Reserve**: Adequate for 90 days (domestic consumption)

**SYSTEMIC RISKS** (from Behavioral Analyst):
- **Stability Score**: 3/10 (high instability)
- **Contagion Risk**: Regional arms race, refugee crisis (5M displaced)
- **Equilibrium Shift**: Move from cooperative trade to bloc fragmentation

**COMPLIANCE ASSESSMENT** (from Compliance Agent):
- **Detection**: 100% (overt military action)
- **Attribution**: 100% (no plausible deniability)
- **Penalties**: UTA expulsion, global sanctions, ICC prosecution

---

**RECOMMENDATION**: **REJECT** current strategy. Pursue Alternative #1 (Negotiate Suez Access Rights) with 4:1 better risk-adjusted return.

**DECISION REQUIRED**:
- [ ] Proceed with Directive as specified
- [ ] Proceed with Alternative #1 (Recommended)
- [ ] Proceed with Alternative #2
- [ ] Proceed with Alternative #3
- [ ] Request further analysis on: _______________
- [ ] Abandon strategy entirely

---

## Integration with Game Systems

### Inputs from Game State
- Current prices (all products, all countries)
- Trade flows (bilateral matrices)
- Alliance structures and reputation scores
- Military capabilities and deployments
- UTA credit balances
- Compliance history and enforcement spending
- Energy flows and strategic reserves

### Outputs to Game Engine
- **Approved Strategy** → Executable action sequence
- **Rule Extensions** → Added to permanent game mechanics
- **State Changes** → Territory, GDP, trade flows, alliances updated via CGE propagation
- **Event Log** → All strategic decisions recorded for learning/adaptation

### Feedback Loop
- **Post-Implementation Monitoring**: Track actual vs. predicted outcomes
- **Learning**: Update prediction models based on realized results
- **Strategy Library**: Store successful strategies for reuse/sharing

---

## Example Walkthroughs

### Example 1: "Conquer Egypt!"

**Input**: Natural language directive

**Spawned Agents**:
- Economist (trade flow impact, GDP calculation)
- Military Analyst (operational planning, costs)
- Geopolitical Strategist (coalition response)
- Energy Analyst (Suez Canal control value)
- Financial Strategist (sanctions impact, currency defense)
- Behavioral Analyst (regional stability)

**Rule Extension Required**:
- **Territorial Annexation Mechanics** (new rule)
- **Post-Conflict Integration Module** (GDP consolidation, factor market merger)

**Output**: 2-page decision package (shown above) with **REJECT** recommendation

**Alternative Approved**: "Negotiate Suez Access Rights" → Standard trade agreement mechanics (no rule extension needed)

---

### Example 2: "Sanction Russia's energy sector to collapse their economy"

**Input**: Natural language directive

**Spawned Agents**:
- Economist (global energy price impact, substitution elasticities)
- Energy Analyst (supply rerouting, LNG capacity constraints)
- Geopolitical Strategist (Russia's counter-sanctions, China's support)
- Financial Strategist (ruble collapse, capital controls)
- Compliance Analyst (sanctions evasion via shadow tankers)
- Behavioral Analyst (European energy crisis, political backlash)

**Rule Extension Required**: None (sanctions mechanics already exist)

**Output**: 2-page decision package
- **Economic Impact**: -$180B to Russia GDP, +$60/barrel oil price (hurts sanctioning countries -$120B)
- **Success Probability**: 60% (Russia finds alternative buyers in China/India)
- **Blowback Risk**: European energy crisis, domestic political backlash
- **Recommendation**: **APPROVE** with modifications (exemptions for humanitarian goods, gradual phase-in)

---

### Example 3: "Form a semiconductor trade bloc with Taiwan, South Korea, and Japan"

**Input**: Natural language directive

**Spawned Agents**:
- Economist (trade creation vs. diversion, welfare analysis)
- Geopolitical Strategist (China's response, US support)
- Behavioral Analyst (coalition stability, trust mechanisms)

**Rule Extension Required**:
- **Sectoral Trade Bloc Mechanics** (tariff preferences limited to semiconductors, not full FTA)

**Output**: 2-page decision package
- **Economic Impact**: +$45B/year from improved supply chain coordination
- **Geopolitical Risk**: China retaliates with rare earth export ban (-$30B)
- **Formation Probability**: 75% (conditional on US security guarantees)
- **Recommendation**: **APPROVE** (net positive, manageable risks)

---

## Technical Implementation

### LLM Integration
- **Model**: GPT-4 or Claude for intent parsing and report generation
- **Prompting Strategy**:
  - System prompt defines specialist agent roles
  - Few-shot examples for each agent type
  - Structured output formats (JSON for metrics, Markdown for summaries)

### Subagent Architecture
- **Framework**: LangGraph or CrewAI for multi-agent orchestration
- **Memory**: Shared vector store for game state context
- **Tool Use**: Each subagent has access to:
  - CGE solver (Economist)
  - Game theory solver (Behavioral Analyst)
  - Military simulation (Military Analyst)
  - Network analysis tools (Strategist)

### Code Generation Pipeline
- **Input**: Natural language rule specification from subagent
- **Processing**: LLM converts to pseudocode → Python implementation
- **Validation**: Unit tests auto-generated, integration tests with CGE solver
- **Deployment**: Add to Mesa agent action space, update game state transition functions

### Executive Summary Template
- **Format**: Markdown → PDF rendering
- **Visualization**: Auto-generate charts (cost breakdown, risk matrix, timeline)
- **Interactivity**: Hyperlinks to detailed subagent reports (for players who want deep dives)

---

## Success Criteria

1. **Player Satisfaction**: Players spend <5 minutes reviewing decision packages, feel informed enough to decide
2. **Accuracy**: Predicted outcomes match realized outcomes with R² > 0.7
3. **Coverage**: 95%+ of player directives handled without human-in-the-loop rule creation
4. **Speed**: Generate 2-page decision package in <60 seconds
5. **Economic Rigor**: All recommendations pass CGE equilibrium validation
6. **Transparency**: All assumptions, data sources, and calculations auditable

---

## Future Enhancements

### Phase 1: MVP (Current Specification)
- Fixed subagent roster (7 specialist types)
- Manual rule extension approval
- Text-based decision packages

### Phase 2: Advanced Intelligence
- **Dynamic subagent generation**: Create new specialist types on-demand
- **Multi-turn dialogue**: Player can ask follow-up questions, request sensitivity analysis
- **Counterfactual analysis**: "What if China had supported Russia?" scenario branches

### Phase 3: Full Autonomy
- **Auto-approval for low-risk strategies**: Skip player review for routine actions
- **Proactive recommendations**: Agent suggests strategies unprompted based on game state
- **Meta-learning**: Improve prediction models by learning from all players' outcomes across games

---

## Alignment with UTA Vision

This module embodies the core UTA principle: **Strategic agency with economic accountability**

- Players exercise **genuine strategic choice** (not constrained to pre-defined actions)
- All choices face **real economic consequences** (grounded in CGE equilibrium)
- **Transparency and disclosure** (strategies become shared algorithms)
- **Adaptive rules** (game evolves with player creativity)
- **Credible analysis** (rigorous modeling, not hand-waived narratives)

The Agent Intelligence Module transforms UTA from a simulation into a **strategic laboratory** where leaders explore geo-economic futures with the rigor of academic research and the accessibility of a strategy game.
