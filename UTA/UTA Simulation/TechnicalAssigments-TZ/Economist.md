# Economist - Technical Assignment

## Role
Formalize core economic mechanisms for UTA simulation. Define fundamental variables, equilibrium systems, behavioral models, and calibration approaches ensuring CGE-level realism.

## Core Deliverables

### 1. Fundamental Economic Variables
**Minimal macroeconomic indicators** per country:
- Production capacity by sector (key sectors: energy, transport, steel, IT, agriculture, defense)
- Consumption patterns (household, government, investment)
- Strategic power metrics beyond GDP (tech leadership, currency dominance, trade centrality)
- Country utility functions (growth, influence, security trade-offs)

**Format**: Variable definitions + dependency formulas + data sources (WIOD, OECD ICIO)

### 2. CGE Equilibrium Module
**Price formation mechanisms**:
- Market clearing equations (Walrasian auctioneer or Newton-Raphson iterative)
- Supply-demand functions (national and global markets)
- Price elasticities (short-run vs long-run by sector)
- Cross-price effects and substitution matrices

**Deliverable**: Mathematical core suitable for Mesa implementation with convergence guarantees

### 3. Policy Impact Matrix
**Map state actions to economic outcomes** (minimum 15 instruments):

| Policy | Direct Effect | Spillovers | Detection Trigger | UTA Impact |
|--------|---------------|------------|-------------------|------------|
| Tariff +10% | Import -X%, Price +Y% | Partner retaliation probability | Trade asymmetry >Z | Credit -N |
| Export subsidy | Market share +X% | Price distortion, dumping | Margin anomaly | Credit penalty |
| Industrial policy | Capacity +X% in T years | Competitor displacement | Production surge | Neutral if disclosed |
| Capital controls | Capital outflow -X% | Investment reduction | Flow anomaly | Penalty if severe |

**Format**: CSV with coefficients (min/median/max), confidence bands, lag structures

### 4. Production Networks
**Strategic sector dependencies**:
- Input-output linkages (simplified ICIO matrix: 10-15 key sectors)
- Shock propagation mechanisms (Leontief inverse)
- Lead times for capacity expansion by sector
- Bottleneck identification (critical nodes in production network)

**Format**: Adjacency matrix + elasticity parameters + capacity constraints

### 5. Country Behavioral Models

#### 5.1 Utility Functions
**2-3 variants by country type**:
- **GDP maximizer**: U = α·GDP_growth - β·inflation - γ·unemployment
- **Strategic autonomy**: U = δ·(1/import_dependence) + ε·export_diversity + ζ·tech_leadership
- **Hegemonic**: U = η·market_share + θ·currency_dominance + ι·normative_influence

**Calibration**: By country archetype (resource, industrial, tech, financial hub, survival)

#### 5.2 Action Space
**Complete policy toolkit**:
- **Trade**: Tariffs, quotas, export restrictions, dumping
- **Industrial**: Subsidies, tax breaks, procurement preferences, SOE support
- **Monetary**: Interest rates, capital controls, FX intervention
- **Strategic**: Sanctions, embargos, resource monopolization, standard-setting
- **Covert**: Data manipulation, hidden subsidies, transfer pricing

#### 5.3 Reaction Functions
**Response rules** (decision trees with probabilities):
```
IF (market_share_loss > 10% for 2 quarters) THEN
  P(tariff_increase) = 0.7
  P(export_subsidy) = 0.5
  P(currency_devaluation) = 0.3
```

#### 5.4 Behavioral Regimes
| Regime | Goal | Typical Actions | Transition Trigger |
|--------|------|-----------------|-------------------|
| Cooperative | Mutual gains | Lower tariffs, harmonize standards | Trust index > threshold |
| Protectionist | Defend domestic market | Raise barriers, local content rules | Import surge >X% |
| Aggressive | Unilateral advantage | Dumping, subsidies, currency manipulation | Excess capacity + export opportunity |
| Survival | Crisis management | Capital controls, default risk mitigation | Debt/GDP >Y%, reserves <Z months |

#### 5.5 Expectation Formation
**Mechanisms**:
- **Rational expectations**: Model-consistent forecasts (computationally expensive)
- **Adaptive learning**: Weighted historical average with decay
- **Bounded rationality**: Simple heuristics (rules of thumb)

**Deliverable**: Expectation update equations + parameters (learning rates, forecast horizons)

### 6. Cheating Detection
**Hidden manipulation signatures**:
- Export price anomalies vs production costs (unit value indices)
- Input-output mismatches (import inputs vs export products)
- Transfer pricing exploitation (intra-firm trade mispricing)
- Statistical reporting discrepancies (mirror trade statistics)

**Format**: Detection rules + confidence thresholds + false-positive mitigation

### 7. Alliance Economics
**Coalition game formulation**:
- Economic complementarity measures (trade intensity, factor endowments)
- Power asymmetry indices (GDP ratios, bargaining power)
- Dependency ratios (bilateral trade as % of GDP)
- Influence metrics (network centrality)

**Deliverable**: Coalition formation conditions + stability analysis (core, Shapley value)

### 8. UTA Credit System
**Credit mechanics**:
- **Earning**: compliance_score × trade_volume × time_in_compliance
- **Penalties**: violation_severity × detection_probability × strategic_importance
- **Redemption**: Market access benefits, preferential tariff rates, fast-track dispute resolution
- **Transferability**: Limited secondary market (prevent gaming)

**Format**: Complete credit economy specification with equilibrium properties

## Integration Requirements

### With Strategists
- Translate strategic archetypes to utility function parameters
- Map geopolitical imperatives to economic constraints

### With Currency Analyst
- Exchange rate pass-through to trade flows
- Capital flow effects on production and investment

### With Military Analyst
- Economic costs of conflict and disruption
- Supply chain vulnerability propagation

## Technical Specifications
- **Computational tractability**: Equilibrium solvable in <10 iterations for standard scenarios
- **Data calibration**: Parameters from WIOD, OECD ICIO, WTO, IMF IFS
- **Convergence**: Guaranteed under standard conditions (convex preferences, continuous production)
- **Mesa compatibility**: Agent decision logic implementable as Python methods

## Validation Requirements
- **Stylized facts**: Reproduce gravity equation, Balassa-Samuelson effect
- **Historical elasticities**: Match empirical trade and production elasticities
- **Business cycles**: Generate realistic fluctuations (no explosive paths)
- **Accounting identities**: Satisfy GDP = C + I + G + NX; trade balance sums to zero globally

## Delivery Format
1. Technical document with equations and economic theory (50-60 pages)
2. Parameter tables (CSV/JSON) with sources and confidence intervals
3. Calibration code (Python/Jupyter) with data loading and estimation
4. Test scenarios with known outcomes (historical validation)
5. Integration specifications for Mesa framework
6. Sensitivity analysis for key parameters (elasticities, adjustment speeds)

## Success Criteria
- Economic realism without computational explosion
- Strategic depth without arbitrary mechanics
- All parameters calibratable from real data
- Clear documentation for implementation team
- Model passes historical scenario tests
