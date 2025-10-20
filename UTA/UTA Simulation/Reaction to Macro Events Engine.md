# Reaction to Macro Events Engine

draft based on (Nails price went up, what about crates?)

# High-level solution

- Detect subsidy signal early.
- Reconstruct downstream exposure.
- Recalibrate costs and rerun impact propagation.
- Apply provisional controls and forensic checks.

# Concrete measures (ordered, actionable)

1. Detect macro input shocks
    - Monitor raw-material price indices (steel coil, iron ore).
    - Flag if domestic producer prices drop >X% vs global benchmark within Y days.
    - Flag if import volumes fall while domestic production rises unusually.
2. Surface downstream anomalies automatically
    - For every product category compute expected unit-cost change = upstream_price_change * share_of_input_in_cost.
    - If observed export price or margin change >> expected by factor Z, mark anomaly cluster.
    - Use rolling-window correlation to find sectors whose export price movements tightly track the steel index.
3. Reconstruct implied input consumption (cheap, fast proxy)
    - Use historical IO coefficients at sector level to estimate typical steel-content per product.
    - Scale coefficients by current production volumes to get implied steel demand.
    - Compare implied demand to actual steel production + imports. Large mismatch implies hidden subsidy reallocation.
4. Dynamic technical-coefficient recalibration
    - When subsidy signal confirmed, temporarily increase steel-content coefficients for downstream sectors by calibrated multiplier.
    - Re-run Leontief propagation to get updated GDP/trade impacts.
    - Log provenance: "synthetic adjustment - triggered by steel subsidy signal."
5. Price pass-through and margin tests
    - Track unit value (export USD per ton/unit) and producer margins per sector.
    - If margins widen across many sectors while input cost collapsed only domestically, suspect hidden cross-subsidies or internal transfer pricing.
6. Firm-level triangulation for high-risk sectors
- Cross-check major downstream exporters' input purchases in customs/firm filings.
    - Look for sudden increases in intra-firm transfers from state-owned steel firms to downstream producers.
1. Sentinel+Sampling escalation
- Maintain a list of downstream sentinel sectors (nails, automotive parts, construction materials).
- On trigger, require higher-fidelity reporting for those sectors for T rounds (invoice-level, bill-of-lading).
1. Apply provisional governance levers
    - Temporarily reduce tariff-credit benefits for products with unresolved anomalies.
    - Offer conditional credits for verified compliance remediation.
    - Publicly publish provisional flags to raise reputational cost of hiding subsidies.

10. Adversarial testing and continuous learning

- Run agent tournaments with cheating agents that simulate steel subsidies and transfer-pricing tricks.
- Update detection thresholds and feature sets from adversarial outcomes.
1. External data fusion to close gaps
    - AIS and port throughput to validate export volumes.
    - Energy consumption & electricity usage to cross-check production scale.
    - Procurement databases for government-backed subsidy flows.