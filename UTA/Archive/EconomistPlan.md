# UTA Economist Module - Developer Guide
Source of requirements: uploaded assignment. 
## 0. Quickstart
- Install deps
- Data pull commands
- How to run calibration and smoke tests

## 1. Fundamental Economic Variables
- Table: macro indicators by country and sector
- Definitions and dependency formulas
- Data mapping from WIOD and OECD ICIO

## 2. CGE Equilibrium Core
- Market clearing equations
- Supply-demand functions
- Price elasticities and substitution matrices
- Algorithm: Newton-Raphson or Walrasian auctioneer
- Convergence proof sketch and guardrails

## 3. Policy Impact Matrix
- 15+ instruments with direct and spillover effects
- CSV schema with min, median, max, CI, lags
- Example calibration from WTO notifications

## 4. Production Networks
- Simplified ICIO matrix
- Leontief inverse and shock propagation
- Lead times and capacity constraints
- Bottleneck detection algorithm

## 5. Country Behavioral Models
- Utility variants and calibration by archetype
- Action space and reaction functions
- Regime transitions
- Expectation formation rules

## 6. Cheating Detection
- Signatures, thresholds, and false positive mitigation
- Mirror statistics usage

## 7. Alliance Economics
- Coalition formation
- Stability analysis with Shapley value sketch

## 8. UTA Credit System
- Earning, penalties, redemption, transferability
- Equilibrium properties

## 9. Integration With Other Roles
- Strategists, currency analyst, military analyst

## 10. Technical Specs and Performance
- Iteration limits, tolerance, complexity
- Failure modes and recovery

## 11. Validation and Sensitivity
- Gravity equation reproduction
- Balassa-Samuelson check
- Elasticity backtests
- Sensitivity for top parameters

## 12. Mesa Integration
- Agent class template
- Scheduler and environment
- State logging and audit

## 13. Appendices
- Glossary
- Units and symbols
- Data provenance table
- CSV and JSON schemas