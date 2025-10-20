# Behavioral and Systems Analyst - Technical Assignment

## Role
Ensure systemic stability and behavioral realism through game theory and complex systems analysis. Prevent chaotic dynamics and ensure convergence to economically meaningful equilibria.

## Core Deliverables

### 1. Strategic Interaction Formalization
**Game matrices** for key interactions with Nash equilibria:
- Trade wars (tariffs vs free trade)
- Currency wars (devaluation vs stability)
- Sanctions spirals (escalation vs de-escalation)
- Alliance formation (cooperation vs defection)

**Format**: JSON with payoff matrices and equilibrium solutions

### 2. Agent Learning and Adaptation Mechanisms
**Specify algorithms and parameters**:
- Q-learning for strategic policy choices
- Fictitious play for belief formation
- Reinforcement learning parameters
- Learning rate and forgetting parameters
- Belief updating about other agents

**Deliverable**: Pseudo-code + calibration parameters with empirical justification

### 3. System Stability Analysis
**Identify and prevent**:
- Bifurcation points in parameter space
- Conditions for cascading crises
- Dampening mechanisms to prevent divergence

**Deliverables**:
- Stability map (safe vs unstable parameter ranges)
- Automatic stabilization rules
- Critical state thresholds with early warning indicators

### 4. Reputation System
**Components**:
- Reputation calculation formula
- Impact on future interactions (trade costs, alliance probability)
- Reputation recovery mechanisms and time scales
- Role in coalition formation

**Format**: Mathematical specification + numerical examples

### 5. Network Effects and Contagion
**Analysis**:
- Trade network topology and shock propagation channels
- Systemic importance of hub countries (centrality metrics)
- Crisis isolation and quarantine mechanisms
- Contagion thresholds and firebreaks

**Deliverable**: Network metrics + propagation rules (adjacency weights, transmission probabilities)

### 6. Behavioral Heuristics Library
**Decision rules** with application conditions:
- **Tit-for-tat**: Reciprocal tariff retaliation
- **Grim trigger**: Permanent punishment after sanctions violation
- **Bandwagon effects**: Alliance formation dynamics
- **Anchoring**: Price expectation formation
- **Prospect theory**: Loss aversion in policy choices

**Format**: Rule library (JSON) with activation conditions and parameters

### 7. Emergent System Properties
**Monitoring dashboard**:
- Early warning indicators for systemic crises
- Polarization and fragmentation metrics
- Global trade resilience indicators
- Network modularity and clustering coefficients

**Deliverable**: Metric definitions + threshold values for alerts

### 8. Behavioral Parameter Calibration
**Sources**:
- Historical trade conflicts (US-China, EU-US, Japan-US)
- Experimental economics literature
- Behavioral finance empirics

**Requirements**: Parameter ranges with empirical justification and confidence intervals

## Technical Specifications

### Temporal Dynamics
- Discrete vs continuous time choice
- Synchronous vs asynchronous agent updates
- Action coordination mechanisms (simultaneous vs sequential moves)

### Information Structure
- Complete vs incomplete information
- Common knowledge vs private information
- Signaling and screening mechanisms
- Information revelation through actions

### Equilibrium Concepts
- Nash equilibrium
- Subgame perfect equilibrium
- Evolutionary stable strategies (ESS)
- Correlated equilibrium

## Integration with Other Modules

### With Economic Core
- Link strategic behavior to utility functions
- Translate game outcomes to economic parameters

### With Enforcement Module
- Detect deviations from equilibrium strategies
- Model punishment mechanisms

### With Pricing Module
- Expectation formation affects price dynamics
- Strategic behavior in market manipulation

## Delivery Format
1. Theoretical document with game-theoretic analysis (25-35 pages)
2. Behavioral rules library (JSON/Python)
3. Stability test suite (parameter sensitivity analysis)
4. Calibration parameters with sources
5. Jupyter notebook demonstrating dynamics
6. Integration specification with economic core

## Success Criteria
- No explosive growth or collapse under standard scenarios
- Convergence to theoretically predicted equilibria
- Realistic escalation/de-escalation patterns
- Robustness to individual agent manipulation attempts
- Stable long-run dynamics with bounded variability
