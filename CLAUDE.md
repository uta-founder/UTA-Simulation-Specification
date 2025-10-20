# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

The **Unified Trade Authority (UTA)** is a comprehensive geo-economic simulation platform designed to model next-generation global trade governance. This repository contains documentation and specifications for building an agent-based modeling system that simulates countries, firms, trade flows, and enforcement mechanisms under a unified rule-based framework.

The project aims to replace the current fragmented system of uncoordinated sanctions and weaponized tariffs with a transparent, rules-based architecture featuring credit systems, AI-driven monitoring, and strategic economic gameplay.

## Repository Structure

- **`UTA/UTA Simulation/`** - Core simulation design specifications
  - Module specifications for different economic systems (trade, sanctions, compliance, energy, etc.)
  - Technical foundation documents outlining implementation approach
  - Agent intelligence and behavior specifications
  - `TechnicalAssigments(TZ)/` - Role-specific technical assignments (in Russian) for economists, strategists, military analysts, financial strategists, energy analysts, and behavioral analysts

- **`UTA/Post Simulation Work (papers, PhDs and tournaments)/`** - Research and validation phase documentation
  - Plans for academic papers, stress testing, and policy advocacy
  - Intellectual network building strategies

- **`Unified Trade Authority.md`** - High-level manifesto and core components of the UTA framework

- **`CLEANUP_SUMMARY.md`** - Documentation of repository cleanup (removed Notion GUIDs, updated links, identified empty files needing content)

## System Architecture (Planned)

### Core Technical Stack (Not Yet Implemented)
- **Framework**: Mesa (Python agent-based modeling)
- **Economic Data**: WIOD (World Input-Output Database) or OECD ICIO datasets
- **Data Processing**: pymrio for multi-regional input-output tables
- **Countries**: Modeled as strategic agents with production, trade, and policy capabilities
- **Firms**: Micro-level agents representing producers with capacity, elasticity, and cheating propensity
- **Products**: Simplified objects with cost structures, strategic importance, and supply-demand parameters

### Key Simulation Components

1. **Agent System**
   - Country agents with GDP, production capacity, trade flows, policy levers, and compliance status
   - Firm agents with production capacity, market share, state affiliation, and strategic decision-making
   - Two-level interaction: states set policy, firms execute with potential for circumvention

2. **Economic Modules**
   - **Equilibrium Solver**: Market-clearing with price discovery (Walrasian or Newton-Raphson)
   - **Supply-Demand-Price System**: CGE-level realism with elasticities
   - **Trade Flow Module**: Bilateral trade with transport costs and tariffs
   - **Subsidy & Industrial Policy**: State interventions with propagation effects
   - **Pricing & Market Equilibrium**: Dynamic price adjustments based on supply shocks

3. **Enforcement & Compliance**
   - Tariff-credit system (violations issue credits; compliance earns credits)
   - Detection engines for shadow fleets, commodity laundering, sanctions evasion, currency manipulation
   - Probabilistic cheating and discovery mechanics
   - Enforcement capacity as a strategic investment

4. **Geopolitical Layer**
   - Alliance formation and bloc dynamics
   - Sanctions and counter-sanctions
   - Strategic resource dependencies
   - Reputation and influence metrics

5. **UI Concepts** (Not Implemented)
   - Global Dashboard: Live compliance, trade flows, alerts
   - Nation Control Panel: Strategy input and risk forecasting
   - Treaty & Alliance Marketplace: Diplomatic negotiation hub
   - Economic Metrics Lab: Deep analytics and stress tests
   - Agent Management Console: AI agent configuration and monitoring
   - Leaderboard: Economic dominance and credibility scoring

## Economic Modeling Principles

### Product Modeling
Products are defined by **four strategic vectors**:
1. **Production Elasticity**: How quickly supply responds to incentives
2. **Substitutability**: Availability of alternatives
3. **Transport & Storage Sensitivity**: Logistics complexity (pipeline, refrigerated, digital)
4. **Strategic Leverage Index**: Dependency and power implications

### Country Behavior
Countries operate under different **behavioral regimes**:
- **Cooperative**: Maximize shared benefits (e.g., EU internal trade)
- **Protectionist**: Defend domestic markets (e.g., US-China tariffs)
- **Aggressive**: Seek unilateral advantages (e.g., steel dumping)
- **Survival**: Maintain currency stability (e.g., capital controls)

### Firm-State Interaction
- States set rules and incentives (tariffs, subsidies, bans, procurement)
- Firms optimize profits within constraints (produce, reroute, reprice, hide origin, exploit transfer pricing)
- Detection system catches anomalies: export volume-price ratios, input-output mismatches, sudden margin shifts
- Key parameters per firm: `capacity`, `capex_lead_time`, `margin_target`, `export_share`, `opacity_score`, `propensity_to_cheat`

### Detection Signatures for Cheating
- Export price-volume anomalies
- Input import vs. final product export mismatches
- Triangulation (re-routing through third countries)
- Transfer pricing exploitation
- Sudden margin swings
- Partner report asymmetries

## Development Phases

### Phase 1-2: Foundation (Current Documentation Stage)
- Environment setup with Mesa framework
- Load real economic data (WIOD/OECD ICIO)
- Select starter countries (US, China, Canada, Japan, Germany)
- Extract key sectors (steel, energy, agriculture, manufacturing, tech)

### Phase 3: Core Model
- Define country agents with production capacity, trade flows, and policy levers
- Build world model with trade matrices and enforcement logic
- Integrate MRIO data with agent decision-making

### Phase 4: Prototype Scenarios
- Implement basic policy actions (e.g., "Canada triples steel production")
- Calculate trade impacts, price changes, market share shifts
- Demonstrate UTA credit score changes

### Phase 4.5: Research & Validation (Future)
- Publish peer-reviewed papers
- Add advanced financial layer (derivatives, CDS, sovereign debt, FX markets)
- Conduct adversarial tournaments
- Stress testing and systemic risk analysis
- Policy advocacy and institutional engagement

### Phase 5: Policy Influence (Future)
- Public conferences and outreach
- Policy briefs and workshops
- Positioning UTA as a credible successor framework

## Key Technical Challenges

1. **Equilibrium Solving**: Balance between full CGE realism and computational tractability
2. **Firm-Level Detail**: Represent enough granularity to catch circumvention without modeling every SKU
3. **Detection Engine**: Probabilistic audit with ratio tests and anomaly detection
4. **Agent Intelligence**: LLM-based strategic reasoning with economic grounding
5. **Data Calibration**: Real trade flows, elasticities, lead times, and cost structures
6. **Cheating Mechanics**: Realistic incentive structures where short-term cheating is costly long-term

## Important Notes

### No Code Yet
This repository currently contains **specifications and design documents only**. No implementation code exists. The technical foundation describes using:
- Mesa for agent-based modeling
- pymrio for MRIO data processing
- Python as the primary language
- Modular architecture separating agents, model, data, policies, and simulation runner

### Multilingual Documentation
Technical assignments (TZ) are primarily in Russian, reflecting the international nature of the project team. Core architectural documents are in English.

### Agent-Driven Strategy Development
The vision includes "agentic coding" where players can propose new strategies in natural language, which are then:
1. Analyzed for feasibility and impact
2. Presented as strategy flowcharts
3. Converted to executable code upon approval
4. Saved and optionally shared (algorithmic trading with known algorithms)

### Realism Requirements
- Use real trade data (WIOD, OECD ICIO)
- Calibrate elasticities from empirical research
- Model actual sectoral dependencies
- Validate against historical episodes
- Maintain economic constraints (supply, demand, cost structure, CGE equilibrium)

### Strategic Design Philosophy
- Not a game UI but a "geo-economic simulation dashboard"
- Modeled after trading terminals, IMF dashboards, strategic command centers
- Serious, data-rich, high-stakes feel
- Credible enough for policy evaluation

## Development Workflow (When Implementation Begins)

**Setup**:
```bash
# Install Mesa framework
pip install mesa

# Install pymrio for MRIO data
pip install pymrio

# Download WIOD or OECD ICIO dataset
# (specific commands depend on data source)
```

**Project Structure** (Recommended):
```
UTA/
├── agents/          # Country and firm agent definitions
├── model/           # World model and simulation engine
├── data/            # MRIO tables, cost parameters, calibration
├── policies/        # Policy action implementations
├── enforcement/     # Detection and compliance engines
├── equilibrium/     # Market clearing and price discovery
├── simulation/      # Simulation runner and orchestration
├── ui/              # Visualization and dashboard (optional)
└── tests/           # Unit and integration tests
```

**Running Simulations** (Future):
```python
# Load world model with real trade data
world = WorldModel.from_mrio("wiod_data.pkl")

# Initialize countries
world.add_countries(["US", "China", "Canada", "Japan", "Germany"])

# Apply policy scenario
world.apply_policy("Canada", action="increase_production",
                   sector="steel", factor=3.0)

# Run simulation step
world.step()

# Analyze results
impacts = world.get_trade_impacts()
credits = world.get_uta_credits()
```

## Research Integration

When implementing components, refer to the detailed specifications in:
- `UTA Simulation/Technical Foundation.md` - Setup and phases
- `UTA Simulation/Economists.md` - Economic formalization requirements
- `UTA Simulation/Firm vs State Actions.md` - Two-level agent interaction
- `UTA Simulation/Equilibrium Solver.md` - Market clearing approaches
- `UTA Simulation/Simplified Product Object.md` - Product data model

Each major module has a corresponding specification file describing inputs, outputs, and economic logic.
