# Currency Strategist Technical Assignment

## Role Definition
Design currency policy framework for sovereign agents in UTA simulation. Define rules, tools, and strategic levers for monetary policy—not implementation code.

## Core Principles
- **Hybrid model**: Interest-rate-driven valuation with carry trade mechanics
- **Instruments**: Vanilla forwards only (no complex derivatives)
- **Risk modeling**: Sovereign risk premium index instead of CDS
- **No full Wall Street simulation**: Focus on state-level strategic decisions

## Deliverables

### 1. Currency Policy Toolkit
Define available policy instruments with specifications:
- Policy interest rate setting
- Forward guidance mechanisms
- FX intervention (rule-based vs covert)
- Reserve ratio adjustments
- Capital controls
- Forward contract offerings
- Capital flow taxation

**Format**: JSON schema with parameters, constraints, detection signatures

### 2. Macroeconomic Impact Matrix
For each policy tool, specify:
- Intended outcomes
- Side effects
- Carry agent reactions (institutional/hedge fund/shadow)
- Cross-country spillovers
- UTA compliance impacts

**Format**: CSV with coefficients, confidence bands, lag structures

### 3. Observable Metrics Dashboard
Define game-visible indicators:
- Exchange rates (spot + forward)
- Interest rates
- Reserve balances
- Capital flow indices
- Risk premium indices
- UTA compliance scores

**Format**: Metric definitions with update frequencies, calculation formulas

### 4. Behavioral Archetypes
Create policy regime templates:
- Currency stabilizer
- Export maximizer
- Devaluation aggressor
- Financial hub model
- Dollarized/pegged regime

**Format**: Parameter sets per archetype with transition conditions

### 5. Detection & Enforcement Framework
Specify violation thresholds and detection logic:
- Manipulation signatures
- Acceptable vs unacceptable tactics
- Detection probabilities by method
- Penalty escalation ladder

**Format**: Rule engine specification with pseudo-code

## Technical Requirements
- All formulas must be CGE-compatible
- Parameters must be calibratable from IMF IFS, BIS data
- Include confidence intervals for all estimates
- Provide historical validation examples
- Ensure Mesa framework compatibility

## Integration Points
- Links to trade module via exchange rate pass-through
- Connects to enforcement via manipulation detection
- Feeds into country agent decision-making
- Impacts firm-level cost structures

## Expected Output Format
1. Technical specification document (20-30 pages)
2. Parameter tables (CSV/JSON)
3. Detection rule engine (pseudo-code)
4. Historical calibration examples
5. Scenario test suite (min 6 scenarios)