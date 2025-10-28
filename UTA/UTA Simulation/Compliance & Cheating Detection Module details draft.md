# Compliance & Cheating Detection Module

## Purpose & Scope

The Compliance & Cheating Detection Module implements the enforcement layer of the UTA framework, identifying violations of trade rules, sanctions circumvention, and strategic manipulation. It models both the incentive structures that drive cheating behavior and the detection mechanisms that uncover violations. The module tracks UTA credit scores, implements audit systems, and calculates enforcement costs and effectiveness. This is the critical "policing" layer that makes the UTA system credible and self-enforcing.

The module operates on two levels: (1) firm-level cheating tactics (transfer pricing, origin falsification, triangulation) and (2) state-level violations (subsidy manipulation, reporting fraud, sanction evasion). It balances detection investment against deterrence effectiveness, creating realistic trade-offs between enforcement strictness and administrative burden.

## Key Components

### 1. Detection Engines
- **Anomaly Detection**: Statistical outlier identification in trade patterns
- **MRIO Consistency Checks**: Input-output table balance verification
- **Partner Report Matching**: Cross-checking bilateral trade reports
- **Forensic Audits**: Deep investigation of flagged entities

### 2. Cheating Taxonomy
- **Triangulation**: Re-routing through third countries to avoid sanctions/tariffs
- **Transfer Pricing**: Manipulating intra-firm prices to shift profits
- **Origin Falsification**: Misrepresenting country of origin
- **Subsidy Hiding**: Concealing state support in cost structures
- **Shadow Fleets**: Using opaque shipping networks for banned goods

### 3. UTA Credit System
- **Credit Score Calculation**: Dynamic reputation metric
- **Violation Penalties**: Credit deductions by offense severity
- **Compliance Rewards**: Credit bonuses for clean records
- **Credit Impacts**: How scores affect market access and costs

### 4. Audit Mechanisms
- **Random Audits**: Baseline deterrence through unpredictability
- **Risk-Based Targeting**: Focus on high-probability violators
- **Triggered Investigations**: Response to anomaly flags
- **Coalition Enforcement**: Coordinated monitoring by alliances

## Data Structures

### Input Data
```python
class ComplianceInputs:
    # Trade Data
    declared_trade: dict[exporter][importer][product] -> {
        'volume': float,
        'value': float,
        'unit_price': float,
        'declared_origin': country,
        'declared_route': list[countries]
    }

    partner_reports: dict[importer][exporter][product] -> {
        'import_volume': float,
        'import_value': float,
        'cif_price': float
    }

    # MRIO Consistency
    input_output_tables: dict[country] -> {
        'intermediate_use': matrix[sector][sector],
        'final_demand': vector[sector],
        'exports': vector[sector],
        'imports': vector[sector]
    }

    # Firm-Level Data
    firm_registry: dict[firm] -> {
        'country': country,
        'sector': sector,
        'capacity': float,
        'ownership_structure': graph,
        'state_affiliation': float,  # 0-1
        'opacity_score': float,      # 0-1
        'propensity_to_cheat': float  # Calibrated parameter
    }

    # Policy Context
    active_sanctions: list[Sanction]
    tariff_schedule: dict[importer][exporter][product] -> float
    subsidy_registry: dict[country][sector] -> float

    # From Other Modules
    energy_routing_anomalies: list[anomaly]  # From Energy & Logistics
    unusual_demand_spikes: list[anomaly]     # From Demand Module
    geopolitical_tensions: dict[(country_i, country_j)] -> float
```

### Internal State
```python
class ComplianceState:
    # UTA Credits
    uta_credits: dict[country] -> float  # Current credit balance
    credit_history: dict[country] -> list[(timestamp, change, reason)]

    # Violation Registry
    violations: list[Violation] where Violation = {
        'id': str,
        'violator': country or firm,
        'type': enum[TRIANGULATION, TRANSFER_PRICING, ORIGIN_FRAUD, SUBSIDY_HIDING, SANCTION_EVASION],
        'severity': float,  # 0-1
        'detected_date': int,
        'evidence_strength': float,  # 0-1
        'status': enum[FLAGGED, UNDER_INVESTIGATION, CONFIRMED, DISMISSED],
        'penalty_applied': float,
        'remediation': str or None
    }

    # Audit State
    audit_queue: list[{
        'target': country or firm,
        'trigger': enum[RANDOM, RISK_BASED, ANOMALY_TRIGGERED],
        'priority': float,
        'resources_allocated': float
    }]

    enforcement_capacity: dict[country or coalition] -> {
        'budget': float,
        'staff': int,
        'technology_level': float,  # 0-1
        'audit_throughput': int     # Audits per period
    }

    # Detection Thresholds (calibrated)
    detection_parameters: {
        'price_variance_threshold': float,
        'volume_spike_threshold': float,
        'mrio_mismatch_tolerance': float,
        'triangulation_margin_threshold': float,
        'partner_report_discrepancy_threshold': float
    }

    # Historical Baselines
    baseline_patterns: dict[(exporter, importer, product)] -> {
        'avg_unit_price': float,
        'std_unit_price': float,
        'avg_volume': float,
        'typical_route': list[countries],
        'seasonal_pattern': vector[12]  # Monthly seasonality
    }
```

### Output Data
```python
class ComplianceOutputs:
    # Detection Results
    flagged_transactions: list[{
        'transaction': trade_flow,
        'anomaly_type': str,
        'confidence': float,
        'recommended_action': enum[AUDIT, MONITOR, IGNORE]
    }]

    confirmed_violations: list[Violation]

    # Credit Updates
    credit_changes: dict[country] -> float
    credit_risk_scores: dict[country] -> float  # Default probability

    # Enforcement Actions
    penalties_imposed: dict[country or firm] -> {
        'fine': float,
        'credit_deduction': float,
        'market_access_restriction': list[restriction],
        'duration': int
    }

    # System Metrics
    detection_rate: float                   # Confirmed violations / actual violations
    false_positive_rate: float              # False flags / total flags
    enforcement_effectiveness: float         # Deterrence impact
    enforcement_cost: dict[enforcer] -> float

    # For Other Modules
    sanctioned_entities: list[country or firm]
    risk_premiums: dict[country] -> float   # Insurance/interest rate markup
    trade_restrictions: dict[(country, country)] -> list[product]
```

## Economic Logic

### 1. Cheating Incentive Calculation

**Expected Profit from Cheating**:
```python
def calculate_cheating_incentive(firm, product, destination, world_state):
    # Baseline profit (compliant)
    compliant_profit = (
        product.price - product.cost
    ) * firm.production_capacity * (1 - world_state.tariff[destination])

    # Profit if cheating (avoiding tariff/sanction)
    if world_state.is_sanctioned(firm.country, destination, product):
        # Triangulation: sell through third country
        transit = find_complicit_transit_country(firm.country, destination)
        cheating_profit = (
            product.price * (1 - TRIANGULATION_DISCOUNT) - product.cost -
            TRIANGULATION_COST
        ) * firm.production_capacity

        detection_probability = estimate_detection_prob(
            firm, product, transit, world_state.enforcement_capacity
        )

    else:
        # Transfer pricing: understate export price to avoid tariff
        understated_price = product.price * (1 - UNDERSTATEMENT_RATIO)
        saved_tariff = (product.price - understated_price) * world_state.tariff[destination]

        cheating_profit = compliant_profit + saved_tariff * firm.production_capacity

        detection_probability = estimate_transfer_pricing_detection(
            understated_price, product.benchmark_price, world_state.audit_intensity
        )

    # Expected penalty if caught
    expected_penalty = detection_probability * (
        world_state.fine_rate * cheating_profit +
        firm.reputation_cost * world_state.uta_credit_value +
        firm.market_access_loss
    )

    # Net expected gain
    net_gain = (cheating_profit - compliant_profit) - expected_penalty

    # Firm cheats if expected gain > risk threshold
    will_cheat = net_gain > firm.risk_threshold

    return {
        'will_cheat': will_cheat,
        'expected_gain': net_gain,
        'detection_probability': detection_probability,
        'chosen_method': 'triangulation' if world_state.is_sanctioned else 'transfer_pricing'
    }
```

### 2. Detection Probability Models

**Triangulation Detection**:
```python
def detect_triangulation(trade_flows, mrio_tables, params):
    flags = []

    for transit_country in countries:
        for product in products:
            # Check re-export ratio
            imports = trade_flows.imports[transit_country][product]
            exports = trade_flows.exports[transit_country][product]
            domestic_production = mrio_tables[transit_country].output[product]
            domestic_consumption = mrio_tables[transit_country].final_demand[product]

            re_export_ratio = exports / (imports + domestic_production)

            # High re-export with low domestic activity
            if (re_export_ratio > params['re_export_threshold'] and
                domestic_production < 0.1 * exports):

                # Check if avoiding sanctions
                for source in trade_flows.import_sources[transit_country][product]:
                    for dest in trade_flows.export_destinations[transit_country][product]:
                        if is_sanctioned(source, dest, product):
                            # Check margin (should be minimal for pass-through)
                            import_price = trade_flows.import_price[source][transit_country][product]
                            export_price = trade_flows.export_price[transit_country][dest][product]
                            margin = (export_price - import_price) / import_price

                            if margin < params['margin_threshold']:
                                confidence = calculate_confidence_score(
                                    re_export_ratio,
                                    domestic_production,
                                    margin,
                                    params
                                )

                                flags.append({
                                    'type': 'triangulation',
                                    'transit': transit_country,
                                    'true_source': source,
                                    'destination': dest,
                                    'product': product,
                                    'confidence': confidence
                                })

    return flags
```

**Transfer Pricing Detection**:
```python
def detect_transfer_pricing(firm_trades, benchmark_prices, params):
    flags = []

    for trade in firm_trades:
        if trade.is_intra_firm:  # Between related parties
            # Compare to arm's length price
            benchmark_price = benchmark_prices[trade.product][trade.destination]
            declared_price = trade.unit_price

            # Check for significant deviation
            deviation = abs(declared_price - benchmark_price) / benchmark_price

            if deviation > params['transfer_pricing_threshold']:
                # Additional checks
                profitability_shift = estimate_profit_shift(
                    firm, trade, benchmark_price, declared_price
                )

                # High-tax to low-tax jurisdiction
                tax_incentive = (
                    world_state.tax_rate[trade.origin] -
                    world_state.tax_rate[trade.destination]
                )

                if tax_incentive > 0 and profitability_shift > params['profit_shift_threshold']:
                    confidence = 0.6 + 0.3 * (deviation / params['transfer_pricing_threshold'])

                    flags.append({
                        'type': 'transfer_pricing',
                        'firm': firm,
                        'trade': trade,
                        'declared_price': declared_price,
                        'benchmark_price': benchmark_price,
                        'deviation': deviation,
                        'confidence': confidence
                    })

    return flags
```

**MRIO Consistency Check**:
```python
def check_mrio_consistency(trade_data, mrio_tables, params):
    inconsistencies = []

    for country in countries:
        for product in products:
            # Production identity: Output = Intermediate Use + Final Demand + Exports
            output = mrio_tables[country].output[product]
            intermediate_use = sum(mrio_tables[country].intermediate_use[product, :])
            final_demand = mrio_tables[country].final_demand[product]
            exports = trade_data.exports[country][product]

            total_use = intermediate_use + final_demand + exports
            residual = abs(output - total_use) / output

            if residual > params['mrio_tolerance']:
                # Investigate input sources
                for input_sector in sectors:
                    imports_declared = trade_data.imports[country][input_sector]
                    mrio_implied_imports = mrio_tables[country].intermediate_use[input_sector, product]

                    import_mismatch = abs(imports_declared - mrio_implied_imports) / imports_declared

                    if import_mismatch > params['import_mismatch_threshold']:
                        inconsistencies.append({
                            'type': 'mrio_inconsistency',
                            'country': country,
                            'product': product,
                            'input_sector': input_sector,
                            'residual': residual,
                            'import_mismatch': import_mismatch,
                            'confidence': min(1.0, residual + import_mismatch)
                        })

    return inconsistencies
```

### 3. UTA Credit Score Dynamics

```python
def update_uta_credits(country, violations, compliance_actions, params):
    # Current credit balance
    current_credits = country.uta_credits

    # Decay factor (credits depreciate over time)
    current_credits *= params['credit_decay_rate']

    # Deductions for violations
    for violation in violations:
        if violation.status == 'CONFIRMED':
            penalty = params['violation_penalty'][violation.type] * violation.severity
            current_credits -= penalty

            # Log the change
            country.credit_history.append({
                'timestamp': world_state.time,
                'change': -penalty,
                'reason': f"Violation: {violation.type}"
            })

    # Bonuses for compliance
    for action in compliance_actions:
        if action.type == 'voluntary_disclosure':
            bonus = params['disclosure_bonus']
            current_credits += bonus
        elif action.type == 'clean_audit':
            bonus = params['clean_audit_bonus']
            current_credits += bonus

    # Threshold effects
    if current_credits < params['credit_threshold_low']:
        country.market_access_restrictions.append('high_risk_premium')
    elif current_credits > params['credit_threshold_high']:
        country.market_access_benefits.append('preferred_trading_partner')

    country.uta_credits = max(0, current_credits)  # Floor at zero

    return country.uta_credits
```

### 4. Audit Resource Allocation

**Risk-Based Audit Selection**:
```python
def select_audit_targets(entities, enforcement_budget, params):
    # Calculate risk scores for all entities
    risk_scores = []

    for entity in entities:
        # Historical violation rate
        violation_history = entity.past_violations.count() / entity.observation_periods

        # Current red flags
        current_flags = entity.anomaly_flags.count()

        # Geopolitical risk
        if isinstance(entity, Country):
            geo_risk = entity.geopolitical_tension_score
        else:  # Firm
            geo_risk = entity.country.geopolitical_tension_score

        # Opacity (harder to monitor = riskier)
        opacity = entity.opacity_score

        # Strategic importance (higher stakes)
        strategic_value = entity.trade_volume * entity.product_criticality

        # Composite risk score
        risk_score = (
            0.3 * violation_history +
            0.3 * current_flags +
            0.2 * geo_risk +
            0.1 * opacity +
            0.1 * (strategic_value / max_strategic_value)
        )

        risk_scores.append((entity, risk_score))

    # Sort by risk descending
    risk_scores.sort(key=lambda x: x[1], reverse=True)

    # Allocate budget
    audits_selected = []
    budget_spent = 0
    audit_cost = params['cost_per_audit']

    for entity, risk in risk_scores:
        if budget_spent + audit_cost <= enforcement_budget:
            # Audit probability increases with risk
            audit_probability = min(1.0, risk * params['audit_sensitivity'])

            if random.random() < audit_probability:
                audits_selected.append(entity)
                budget_spent += audit_cost

    # Add random audits for unpredictability
    random_sample_size = int(params['random_audit_share'] * len(entities))
    random_audits = random.sample(
        [e for e in entities if e not in audits_selected],
        min(random_sample_size, int((enforcement_budget - budget_spent) / audit_cost))
    )

    audits_selected.extend(random_audits)

    return audits_selected
```

### 5. Enforcement Effectiveness

```python
def calculate_enforcement_effectiveness(enforcement_capacity, violations, params):
    # Detection rate
    detected_violations = [v for v in violations if v.status == 'CONFIRMED']
    actual_violations = violations  # In simulation, we know ground truth
    detection_rate = len(detected_violations) / max(1, len(actual_violations))

    # False positive rate
    false_positives = [v for v in violations if v.status == 'DISMISSED']
    false_positive_rate = len(false_positives) / max(1, len(violations))

    # Deterrence effect (reduced cheating over time)
    current_cheating_rate = calculate_cheating_rate(world_state)
    baseline_cheating_rate = params['baseline_cheating_rate']
    deterrence = max(0, baseline_cheating_rate - current_cheating_rate) / baseline_cheating_rate

    # Cost efficiency
    total_penalties_collected = sum([v.penalty_applied for v in detected_violations])
    enforcement_cost = sum([c.budget for c in enforcement_capacity.values()])
    cost_efficiency = total_penalties_collected / max(1, enforcement_cost)

    # Composite effectiveness score
    effectiveness = (
        0.4 * detection_rate +
        0.3 * deterrence +
        0.2 * (1 - false_positive_rate) +
        0.1 * min(1.0, cost_efficiency)
    )

    return {
        'effectiveness': effectiveness,
        'detection_rate': detection_rate,
        'false_positive_rate': false_positive_rate,
        'deterrence': deterrence,
        'cost_efficiency': cost_efficiency
    }
```

## Integration Points

### Inputs From Other Modules

1. **From Trade Flow Module**:
   - Declared bilateral trade volumes and prices
   - Actual vs declared routes
   - Trade flow anomalies

2. **From Energy & Logistics Module**:
   - Unusual routing patterns
   - Shadow fleet activity
   - Infrastructure misuse signals

3. **From Demand Module**:
   - Demand spikes inconsistent with fundamentals
   - Hoarding or stockpiling behavior

4. **From Sanctions & Geopolitics Module**:
   - Active sanctions to enforce
   - Geopolitical risk scores
   - Coalition enforcement priorities

5. **From Country/Firm Agents**:
   - Firm ownership structures
   - State affiliation levels
   - Strategic incentives to cheat

### Outputs To Other Modules

1. **To Trade Flow Module**:
   - Blocked transactions
   - Entities barred from trading
   - Required route disclosures

2. **To Pricing & Equilibrium Module**:
   - Risk premiums for non-compliant countries
   - Credit score impacts on borrowing costs
   - Market access restrictions affecting supply

3. **To Sanctions & Geopolitics Module**:
   - Violation evidence for sanction justification
   - Enforcement effectiveness metrics
   - Coalition burden-sharing data

4. **To Country Agents**:
   - UTA credit scores and changes
   - Audit notices and investigation status
   - Remediation requirements

5. **To Subsidy & Industrial Policy Module**:
   - Detected hidden subsidies
   - State aid violations
   - Required transparency measures

## Implementation Guidance

### Algorithm Flow

```python
def update_compliance(world_state):
    """Main compliance and detection cycle"""

    # Step 1: Collect data for analysis
    trade_data = world_state.trade_flows
    mrio_tables = world_state.input_output_tables
    firm_data = world_state.firm_registry
    sanctions = world_state.active_sanctions

    # Step 2: Run detection algorithms
    anomalies = []

    # Triangulation detection
    anomalies.extend(detect_triangulation(
        trade_data, mrio_tables,
        world_state.detection_params
    ))

    # Transfer pricing detection
    anomalies.extend(detect_transfer_pricing(
        firm_data, world_state.benchmark_prices,
        world_state.detection_params
    ))

    # MRIO consistency checks
    anomalies.extend(check_mrio_consistency(
        trade_data, mrio_tables,
        world_state.detection_params
    ))

    # Partner report matching
    anomalies.extend(check_partner_reports(
        trade_data.exporter_reports,
        trade_data.importer_reports,
        world_state.detection_params
    ))

    # Step 3: Triage anomalies
    flagged = triage_anomalies(
        anomalies,
        confidence_threshold=world_state.flag_threshold
    )

    # Step 4: Select audit targets
    enforcement_budget = sum([
        c.budget for c in world_state.enforcement_capacity.values()
    ])

    audit_targets = select_audit_targets(
        entities=world_state.countries + world_state.firms,
        enforcement_budget=enforcement_budget,
        params=world_state.audit_params
    )

    # Step 5: Conduct audits
    investigation_results = []
    for target in audit_targets:
        result = conduct_audit(
            target, flagged, world_state.enforcement_capacity
        )
        investigation_results.append(result)

    # Step 6: Update violation registry
    for result in investigation_results:
        if result.evidence_strength > world_state.confirmation_threshold:
            violation = create_violation_record(result)
            world_state.violations.append(violation)

            # Apply penalty
            penalty = calculate_penalty(violation, world_state.penalty_params)
            apply_penalty(violation.violator, penalty, world_state)

    # Step 7: Update UTA credits
    for country in world_state.countries:
        country_violations = [v for v in world_state.violations if v.violator == country]
        country_compliance = get_compliance_actions(country)

        new_credits = update_uta_credits(
            country, country_violations, country_compliance,
            world_state.credit_params
        )

    # Step 8: Calculate effectiveness metrics
    effectiveness = calculate_enforcement_effectiveness(
        world_state.enforcement_capacity,
        world_state.violations,
        world_state.effectiveness_params
    )

    # Step 9: Update baselines for future detection
    update_baseline_patterns(trade_data, world_state.baseline_patterns)

    return {
        'flagged_anomalies': flagged,
        'audits_conducted': audit_targets,
        'violations_confirmed': [v for v in world_state.violations if v.status == 'CONFIRMED'],
        'credit_changes': {c: c.uta_credits for c in world_state.countries},
        'effectiveness': effectiveness
    }
```

### Computational Considerations

1. **Anomaly Detection Scaling**:
   - Use statistical process control for real-time monitoring
   - Pre-compute baseline statistics
   - Parallelize detection across products/routes
   - Use sliding windows for temporal patterns

2. **Audit Optimization**:
   - Dynamic programming for budget allocation
   - Risk score caching
   - Batch processing of similar cases

3. **False Positive Management**:
   - Bayesian updating of detection thresholds
   - Machine learning for pattern recognition (future)
   - Manual review queue for edge cases

4. **Performance**:
   - Index trade data by multiple dimensions
   - Cache MRIO computations
   - Incremental updates vs full recalculation

## Calibration Requirements

### Required Data Sources

1. **Violation Data**:
   - WTO trade dispute cases
   - OFAC enforcement actions
   - EU competition investigations
   - Academic studies on trade fraud

2. **Detection Benchmarks**:
   - Customs fraud statistics
   - Transfer pricing case studies
   - Triangulation estimates (academic literature)
   - MRIO validation studies

3. **Penalty Data**:
   - WTO sanction precedents
   - National penalty schedules
   - Credit rating impacts from violations

4. **Cost Data**:
   - Customs administration budgets
   - Audit costs from enforcement agencies
   - Technology investment in monitoring

### Key Parameters to Calibrate

```python
COMPLIANCE_CALIBRATION = {
    # Detection thresholds
    'price_variance_threshold': 0.30,         # 30% deviation flags review
    'volume_spike_threshold': 2.0,            # 2x normal volume
    're_export_threshold': 0.80,              # 80% re-export ratio
    'margin_threshold': 0.05,                 # 5% margin suspicious
    'mrio_tolerance': 0.10,                   # 10% accounting discrepancy
    'transfer_pricing_threshold': 0.25,       # 25% price deviation

    # Violation penalties (UTA credit deductions)
    'violation_penalty': {
        'triangulation': 100,
        'transfer_pricing': 75,
        'origin_falsification': 50,
        'subsidy_hiding': 80,
        'sanction_evasion': 150
    },

    # Detection probabilities (base rates)
    'detection_probability': {
        'triangulation': 0.60,                # With moderate enforcement
        'transfer_pricing': 0.40,
        'origin_fraud': 0.70,
        'subsidy_hiding': 0.30,
        'sanction_evasion': 0.55
    },

    # Enforcement capacity
    'cost_per_audit': 50000,                  # USD
    'audits_per_investigator': 20,            # Per year
    'random_audit_share': 0.15,               # 15% random selection

    # UTA credit parameters
    'credit_decay_rate': 0.98,                # 2% annual decay
    'clean_audit_bonus': 10,
    'disclosure_bonus': 20,
    'credit_threshold_low': 300,              # Triggers restrictions
    'credit_threshold_high': 700,             # Preferred partner status

    # Effectiveness parameters
    'baseline_cheating_rate': 0.15,           # 15% of firms/countries cheat
    'audit_sensitivity': 1.5,                 # Risk multiplier for audit probability
    'confirmation_threshold': 0.75            # Evidence strength to confirm
}
```

### Validation Metrics

1. **Detection Accuracy**: True positive rate > 70%, false positive rate < 20%
2. **Deterrence Effect**: Cheating rate reduction of 40% vs no enforcement
3. **Cost Efficiency**: Penalties collected > 2x enforcement costs
4. **Credit Score Predictiveness**: Default/violation correlation R² > 0.6
5. **Benchmark Comparison**: Detection rates match customs agency performance ±15%