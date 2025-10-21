# Financial and Currency Strategist - Technical Assignment

## Role
Design currency policy framework and formalize currency manipulation detection mechanisms for UTA simulation. Define policy instruments, detection indicators, and economic impact coefficients.

## Core Deliverables

### 1. Currency Policy Toolkit
Define policy instruments with parameters and detection signatures:
- Policy interest rate setting
- Forward guidance mechanisms
- FX intervention (rule-based vs covert)
- Reserve ratio adjustments
- Capital controls (flow restrictions, taxation)
- Forward contract offerings
- Trade invoicing shifts

**Format**: JSON schema with constraints, detection thresholds, UTA compliance impacts

### 2. Currency Manipulation Catalog
**Minimum**: 15 manipulation types (CSV/JSON)

**Fields**: action_id, description, scope, detectability_score, expected_duration, typical_targets

**Examples**:
- Stealth devaluation via FX swaps
- Export subsidies + sterilization
- Forced devaluation from capital flight
- Trade invoicing asymmetry exploitation

### 3. Detection Indicator System
**Required indicators** with formulas, baselines, thresholds (short/medium/long-term), confidence scores:

- **Reserve pressure** = -Δ(official_reserves) / monthly_imports
  - Thresholds: low 0.02, med 0.05, high 0.12
- **FX intervention intensity** = central_bank_net_sales_fx / money_base
- **Trade invoicing asymmetry** = |exports_A_to_B - imports_B_from_A| / max(...)
  - Flag when >0.15 for 3 months
- **Capital flow spike** = rolling_30d(net_portfolio_inflow) / GDP_month
  - Flag when >0.5% GDP

**Format**: Machine-readable formulas with calibration parameters

### 4. Detection Rule Engine
**Specification**: Pseudo-code with false-positive reduction measures

**Example**:
```
IF (Δreserves > X AND FX_interventions_reported < Y)
OR (trade_receipts_mismatch > Z)
THEN flag WITH score S
```

**Escalation rules**:
- Score 0.2-0.4 → monitoring
- Score 0.4-0.7 → temporary UTA benefit restrictions
- Score >0.7 → formal audit + credit penalties

### 5. Economic Impact Coefficients
**Table**: action_id → direct effects with min/median/max + confidence

Effects on:
- Export volume (%)
- Import prices (%)
- Inflation (%)
- CGE variables (real wages, interest rates)
- Trade balance
- Capital flows

### 6. Macroeconomic Impact Matrix
For each policy tool, specify:
- Intended outcomes
- Side effects and spillovers
- Cross-country transmission channels
- Carry trade agent reactions
- UTA compliance impacts
- Lag structures

**Format**: CSV with coefficients and confidence bands

### 7. Behavioral Archetypes
Policy regime templates with parameters and transition conditions:
- **Currency stabilizer**: Minimize volatility
- **Export maximizer**: Undervaluation strategy
- **Devaluation aggressor**: Competitive devaluation
- **Financial hub model**: Capital market openness
- **Dollarized/pegged regime**: Fixed exchange rate defense

### 8. Scenario Packages
**Minimum**: 8 scenarios with:
- Timeline and parameter values
- Contagion channels
- Country category (small/medium/great power)
- Concealment tactics (behavioral patterns only)
- Expected detection probability
- Economic gain vs reputational cost

### 9. Data Requirements
**Mandatory sources**:
- IMF International Financial Statistics (IFS)
- BIS statistics
- SWIFT aggregates
- Central bank reports
- FX reserve flows
- Balance of payments

**Format**: Data schema + update frequency specifications

### 10. Integration Specification
- API/CSV contract for passing flags to CGE/Mesa core
- Schema: flags, scores, timestamps, provenance
- Translation rules: flag → temporary parameter adjustments in economic model

### 11. Adversarial Test Suite
- 6 cheating patterns against detection logic
- Expected model responses
- Calibration guidance

## Currency Policy Modes
1. **Managed float**: Smooth exchange rate management
2. **Sterilized support**: Intervention with liquidity neutralization
3. **Capital controls**: Flow restrictions and taxation
4. **Trade-invoicing shift**: Currency of settlement changes
5. **Reserve accumulation/decumulation**: Strategic reserve management

## Simulation Parameters
Required agent attributes:
- reserves_level (USD)
- fx_rate_index ∈ [0,1]
- intervention_score ∈ [0,1]
- capital_control_index ∈ [0,1]
- invoicing_share_USD, invoicing_share_local
- detection_risk ∈ [0,1]
- reputational_cost_score ∈ [0,1]

## Observable Metrics Dashboard
Game-visible indicators:
- Exchange rates (spot + forward)
- Interest rates
- Reserve balances
- Capital flow indices
- Risk premium indices
- UTA compliance scores

**Format**: Metric definitions with update frequencies and formulas

## Technical Requirements
- **Temporal horizons**: intraday/daily/weekly/monthly resolution
- **Hybrid model**: Interest-rate-driven valuation with carry trade mechanics
- **Instruments**: Vanilla forwards only (no complex derivatives)
- **Risk modeling**: Sovereign risk premium index instead of CDS
- **All formulas**: CGE-compatible and Mesa-implementable
- **Parameters**: Calibratable from IMF IFS, BIS data
- **Uncertainty**: Confidence bands for all signals
- **Validation**: Historical cases without revealing tactics
- **Reproducibility**: Jupyter/Colab with sample data

## Integration Points
- Trade module: Exchange rate pass-through effects
- Enforcement module: Manipulation detection flags
- Country agents: Policy decision-making
- Firm agents: Cost structure impacts via input prices

## Delivery Format
1. Technical document with formulas (30-40 pages)
2. CSV/JSON parameter tables and detection rules
3. Jupyter notebook with examples and calibration
4. Evaluation matrix (evasiveness_score, economic_gain, reputation_cost)
5. Scenario test suite (minimum 6 scenarios)
6. Historical validation examples

## Success Criteria
- Detection system catches manipulation without excessive false positives
- Economic impacts match historical elasticities
- Parameters calibratable from public data
- Integration with CGE core maintains equilibrium properties
