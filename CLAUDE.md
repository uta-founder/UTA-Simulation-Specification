# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is the **UTA (Unified Trade Authority) Simulation Specification** repository - a comprehensive economic simulation modeling global trade enforcement, geopolitical strategy, and agent-based decision-making. The project aims to create a credible, policy-relevant geo-economic modeling platform grounded in rigorous Computable General Equilibrium (CGE) theory.

**Key Goal**: Model countries as strategic agents that produce, trade, subsidize, manipulate currency, form alliances, or cheat under rules enforced by a Unified Trade Authority System with real economic consequences.

## Project Structure

```
UTA-Simulation-Specification/
├── UTA/
│   ├── UTA Simulation.md                    # Main entry point - overview of all components
│   └── UTA Simulation/
│       ├── Technical Foundation.md          # Implementation roadmap & data setup
│       ├── Country Move.md                  # Complete action space for countries
│       ├── Firm vs State Actions.md         # Distinction between firm-level and state actions
│       ├── Impact propagation mechanics.md  # How effects cascade through the system
│       ├── Reaction to Macro Events Engine.md
│       ├── Simplified Product Object.md
│       ├── UIParams.md                      # High-level UI specification
│       │
│       ├── [Economic Modules]
│       ├── Demand Module.md                 # ✅ Production-ready (780 lines)
│       ├── Pricing & Market Equilibrium Module.md  # ✅ Production-ready (908 lines)
│       ├── Trade Flow Module.md             # ✅ Comprehensive spec
│       ├── Subsidy & Industrial Policy Module.md   # ✅ Complete
│       ├── Sanctions & Geopolitics Module.md       # ✅ Complete
│       ├── Energy & Logistics Module.md            # ✅ Complete
│       ├── Compliance & Cheating Detection Module.md  # ✅ Complete
│       ├── Agent Intelligence Module.md     # Brief - agentic LLM strategy implementation
│       │
│       ├── WhitePapers/                     # Academic-level implementation guides
│       ├── DeepResearchPrompts/             # Research prompts for deep dives
│       ├── Personas/                        # Research personas (e.g., Dr. Maya Patel)
│       └── TechnicalAssigments-TZ/          # Expert assignments (Economist, Energy Analyst, etc.)
│
├── SpecOps/                                 # Project management & validation
│   ├── VALIDATION-REPORT-Phase1-Complete.md # Comprehensive progress report
│   ├── cge-game-logic-implementer-BASE1-todo.md  # 42-day implementation roadmap
│   └── GameContentTodo.md                   # Original task list
│
└── Unified Trade Authority.md               # Original manifesto & thesis

```

## Development Phases

The project follows a structured 42-day implementation plan across 4 phases:

### Phase 1: Core Economic Modules (Days 1-12) ✅ COMPLETE
- Demand Module (Armington CES, LES demand system)
- Pricing & Market Equilibrium Module (Walrasian clearing, CGE solver)
- Equilibrium Solver integration with pymrio

**Status**: Phase 1 is production-ready with comprehensive specifications (~1688 lines of spec)

### Phase 2: Policy & Intervention Modules (Days 13-20)
- Subsidy & Industrial Policy Module
- Sanctions & Geopolitics Module

### Phase 3: Strategic Infrastructure (Days 21-30)
- Energy & Logistics Module
- Compliance & Cheating Detection Module

### Phase 4: Agent Intelligence & Behavioral (Days 31-42)
- Agent Intelligence Module (LLM-driven strategy generation)
- Behavioral & Systems Analyst integration
- Game-theoretic formalization

## Key Economic Frameworks

### CGE (Computable General Equilibrium) Foundation
The simulation is built on rigorous CGE theory:
- **Armington Aggregation**: CES function for origin-differentiated products
- **Walrasian Market Clearing**: Supply = Demand for all products in all countries
- **Zero-Profit Conditions**: P = MC under perfect competition
- **Factor Market Clearing**: Full employment of labor and capital
- **Walras' Law**: Budget constraints satisfied across all agents

### Data Sources
- **WIOD** (World Input-Output Database)
- **OECD ICIO** (Inter-Country Input-Output tables)
- **UN Comtrade** (bilateral trade flows)
- **World Bank** (national accounts, elasticities)
- **GTAP Database** (substitution elasticities: 1.3-5.0 range)

### Key Parameters
- Substitution elasticities: 1.3 (strategic goods) to 5.0 (commodities)
- Income elasticities: 0.3 (necessities) to 2.0 (luxuries)
- Solver tolerance: 1e-6 (0.0001% relative excess demand)
- Convergence: R² > 0.90 for trade share replication

## Module Integration Architecture

**Central Hub**: Pricing & Market Equilibrium Module
- Receives excess demand/supply from all sectors
- Sends equilibrium prices to all agents
- Iterative Gauss-Seidel or tâtonnement convergence

**Integration Flow**:
1. Demand Module → quantities demanded → Pricing Module
2. Pricing Module → equilibrium prices → Demand Module
3. Trade Flow Module ↔ bilateral flows ↔ Demand & Pricing
4. Sanctions Module → trade restrictions → Trade Flow
5. Subsidy Module → cost adjustments → Pricing
6. Energy Module → transport costs → Trade Flow

## Custom Claude Agents

This repository uses specialized Claude agents (`.claude/agents/`):

### `uta-simulation-architect`
**Purpose**: Analyze UTA simulation specifications for completeness, identify gaps in economic modeling logic, validate consistency between modules, propose game mechanics grounded in economic theory.
**Use when**: Reviewing module specifications, identifying missing components, validating cross-module consistency

### `cge-game-logic-implementer`
**Purpose**: Translate country specifications and policy changes through CGE model, propagate effects with mass-balance and equilibrium constraints, convert policy descriptions into formal human-readable rules.
**Use when**: Implementing policy rules, propagating economic effects, validating economic consistency

### `uta-simulation-TZ-fixer`
**Purpose**: Refine technical assignments (TZ) for human experts.
**Use when**: Working with files in `TechnicalAssigments-TZ/` directory

### `deep-research-orchestrator`
**Purpose**: Conduct comprehensive research with persona development and structured investigation.
**Use when**: Creating research prompts, developing personas, deep-diving into economic concepts

## Working with Specifications

### Reading Module Specifications
Each module follows a standard structure:
1. **Economic Foundation** - Theory, formulas, assumptions
2. **Implementation Specification** - Algorithms, data structures, pseudocode
3. **Calibration & Data** - Parameter ranges, data sources, calibration procedures
4. **Integration Points** - Inputs from/outputs to other modules
5. **Strategic Gameplay** - Player-facing elements
6. **Example Scenarios** - Concrete numerical walkthroughs

### When Modifying Specifications
- Maintain economic rigor (ground in CGE/trade theory)
- Provide clear mathematical formulations
- Specify realistic parameter ranges from empirical literature
- Define integration points explicitly
- Include 2+ numerical example scenarios
- Ensure consistency across modules


## Implementation Technology Stack

### Core Framework
- **Mesa** (agent-based modeling framework in Python)
- **pymrio** (Python package for Multi-Regional Input-Output tables)

### Data Processing
- WIOD/OECD ICIO data loading and transformation
- Input-output coefficient extraction
- Bilateral trade matrix construction

### Solver Approaches
1. **MVP**: Simple Tâtonnement (Walrasian price adjustment)
2. **Intermediate**: Newton-Raphson with Jacobian
3. **Advanced**: PATH Solver (Mixed Complementarity)
4. **Recommended**: Hybrid Gauss-Seidel + Damped Tâtonnement

### Agent Intelligence
- LLM integration for strategy parsing
- Agentic coding: players propose strategies → analyzed → flowchart → approved → implemented as code
- Strategy sharing (like algorithmic trading with disclosed algorithms)

## Git Workflow

**Main Branch**: `main`

**Current Status** (per git status at session start):
- Phase 1 complete, validation report available
- Archive cleanup completed (old Russian specifications removed)
- Core modules production-ready

## Validation & Testing

### Economic Validation
Test model's ability to replicate historical shocks:
- 2018 US-China tariffs
- 2022 Russia energy cutoffs to Europe
- 2020 pandemic supply chain disruptions
- **Target**: R² > 0.8 for scenario replication

### Convergence Metrics
- Market clearing: |Z/Q| < 0.0001 for all markets
- Walras' Law: |Σ P*Z| < 0.001 * World GDP
- Zero profit: P ≈ MC (±1% tolerance)
- Factor market clearing: ±0.1%
- Global trade balance: ±0.001% of world GDP

## Key Concepts

### UTA System Components
1. **Tripartite Council (T3C)**: Three-bloc governance
2. **Tariff-Credit Enforcement**: Replace tariffs with credit system
3. **Detection Engines**: Shadow fleets, commodity laundering, sanctions evasion
4. **Strategic Benefits**: Trade credits, compliance rewards, enforcement mechanisms

### Strategic Gameplay Elements
Players (countries) can:
- Adjust tariffs, subsidies, quotas, sanctions
- Manipulate currency (interest rates, FX intervention, reserves)
- Implement industrial policy (R&D, SOE mandates)
- Form alliances, coalitions, trade agreements
- Execute military actions (blockades, cyberattacks, deterrence)
- Cheat (origin laundering, transfer pricing) with detection risk
- Use UTA credits and file disputes

### Military & Non-Kinetic Actions
All military actions have parameter vectors:
`{economic_impact, detection_prob, attribution_prob, UTA_penalty, escalation_risk, duration}`

Examples:
- Naval blockade: -80% throughput, 100% detection, -1000 credits, 80% escalation risk
- Cyber sabotage: variable impact, 60% detection, 40% attribution, -500 credits (if proven)
- Show of force: -5% throughput, 100% visible, -50 credits, 15% escalation

## Documentation Standards

### For Economic Modules
- Use LaTeX-style math notation in markdown
- Provide both theoretical foundations and implementation guidance
- Include parameter calibration procedures
- Specify data requirements explicitly
- Show numerical examples with full calculations

### For Research Outputs
- **White Papers**: Academic-level, full mathematical rigor
- **Deep Research Prompts**: For creating white papers, MBA-friendly (flowcharts not formulas)
- **Personas**: Research specialists (e.g., Dr. Maya Patel - Chief Research Translator)

### Excluded Content
Per `.gitignore`:
- `/SpecOps` (project management, not for general distribution)
- `/UTA/UTA Simulation/DeepResearchPrompts` (internal research scaffolding)

## Future Work

Per `UTA Simulation/Post-SimulationWork.md`:
- Academic papers based on simulation results
- PhD dissertation opportunities
- Policy tournaments and scenario competitions
- Real-world adoption pathway (see `Unified Trade Authority.md`)

## References

**Key Documents to Read First**:
1. `UTA/UTA Simulation.md` - Start here for overview
2. `SpecOps/VALIDATION-REPORT-Phase1-Complete.md` - Progress status
3. `SpecOps/cge-game-logic-implementer-BASE1-todo.md` - Implementation roadmap
4. `UTA/UTA Simulation/Technical Foundation.md` - Setup instructions

**For Economic Context**:
- Demand Module and Pricing & Market Equilibrium Module are reference implementations
- Trade Flow Module shows comprehensive bilateral trade modeling
- Country Move.md defines complete strategic action space
