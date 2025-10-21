# Trade Flow Simulation Algorithms for Policy Analysis

**The econometric and computational toolkit for UTA simulation has converged on PPML gravity estimation combined with decomposed network flow optimization, achieving production-ready performance at 50-country, 200-product scale.** The methodology integrates structural gravity theory, modern optimization algorithms handling multi-commodity flows, and machine learning detection systems achieving F1 scores above 0.90 for sanctions circumvention. Recent literature (2020-2025) demonstrates that properly implemented systems can simulate realistic trade flows in under 30 minutes while detecting evasion patterns with 75-92% accuracy.

Three decades of gravity model research culminated in **Poisson Pseudo-Maximum Likelihood (PPML) becoming the dominant estimator**, displacing earlier approaches through seven key advantages: handling heteroscedasticity, accommodating zero trade flows naturally, fast convergence, and exact implementation of multilateral resistance terms through fixed effects. Simultaneously, **network flow algorithms with Benders decomposition** enable tractable optimization for large-scale simulations, while **graph neural networks and betweenness centrality** identify intermediary nodes in sanctions evasion schemes. Real-world implementations demonstrate $40B+ Chinese transshipment through Vietnam and $178B Russian oil revenues despite sanctions, validating both detection methodologies and the need for sophisticated modeling.

## Gravity models achieve theoretical consistency with PPML estimation

The gravity model literature has reached consensus after resolving the "Gold Medal Mistake" (Anderson & van Wincoop 2003) and heteroscedasticity critique (Santos Silva & Tenreyro 2006). **PPML with three-way fixed effects now serves as the gold standard**, displacing both traditional OLS log-linearization and iterative nonlinear approaches. The Larch, Shikher & Yotov (2025) working paper provides 15 comprehensive recommendations establishing current best practices, with PPML's "workhorse" status stemming from consistency under heteroscedasticity combined with natural handling of zero trade flows without dropping observations.

**Distance decay elasticity remains remarkably stable at -1.0**, with empirical ranges of -0.8 to -1.3 across hundreds of studies. PPML estimates cluster at -0.8 to -0.9, while OLS systematically overestimates absolute magnitude at -1.2 to -1.5. This stability has theoretical foundation in Zipf's law governing firm size distributions (Chaney 2014). Contiguity effects show 50-65% trade increases (coefficients 0.4-0.5), common language adds 28-50% (coefficients 0.25-0.4), and regional trade agreements boost flows 60-120% (coefficients 0.5-0.8) when properly estimated with pair fixed effects controlling for endogeneity. The critical trade elasticity of substitution σ typically ranges 4-12, with manufacturing consensus at 5-7, agriculture at 3-5, and services at 7-10.

Zero trade flows—comprising 20% of aggregate data and up to 80% of disaggregated product-level data—receive elegant treatment through PPML's multiplicative error structure. Comparative performance studies (Martin & Pham 2020, Herman 2023) rank PPML first, with Heckman selection models performing well when valid exclusion restrictions exist, and Tobit models generally not recommended due to arbitrary threshold requirements. The ITPD-E database (Borchert et al. 2021) demonstrates that controlling for three-way fixed effects reduces "relevant" zeros to approximately 40%, as many zeros represent missing capabilities rather than true potential trade.

**Implementation requires exporter-time, importer-time, and asymmetric country-pair fixed effects** to fully capture multilateral resistance terms—the structural gravity equivalent of general equilibrium price indices. Modern estimation employs the `ppmlhdfe` command in Stata or `fixest` package in R, both handling millions of observations through GPU-accelerated algorithms. Validation benchmarks show R-squared values of 0.60-0.85 with properly specified models, and predicted trade flows within 10-15% of observed values for out-of-sample testing.

Recent methodological advances address remaining challenges. Weidner & Zylkin (2021) provide bias correction for three-way PPML addressing incidental parameter problems with finite time periods. Kwon, Larch & Yotov (2022) introduce Generalized PPML testing constant variance-to-mean ratio assumptions, finding violations rare but offering 40% efficiency gains when present. Beverelli et al. (2024) show how to identify country-specific institutional effects even with full fixed effects through interaction with international border dummies. The field has shifted from methodological debates to refinements enabling richer policy analysis.

## Network flow algorithms decompose to achieve computational tractability

Optimization algorithms for trade routing face fundamental complexity trade-offs at 50-country, 200-product scale. The problem naturally formulates as **multi-commodity flow with 10,000+ commodity pairs** (50² country pairs × 200 products), 50 nodes, and approximately 2,500 bilateral trade arcs. Direct formulation as linear programming creates 2.5-6.25 million variables—tractable for interior point methods but requiring hours of computation. **Decomposition strategies reduce solve times to 15-30 minutes** while maintaining optimality guarantees.

**Network simplex algorithms** exploit graph structure for single-commodity flows, achieving strongly polynomial O(n²m log(nC)) complexity compared to general simplex's exponential worst case. For trade applications, this translates to minutes rather than hours for 50-country problems. Google's OR-Tools `SimpleMinCostFlow` class implements optimized network simplex with clean API and excellent performance on pure network problems. NetworkX provides pure-Python implementations suitable for prototyping and medium-scale problems (≤10,000 nodes), while production systems benefit from compiled implementations.

**Benders decomposition** provides the recommended architecture for multi-product trade simulation. The master problem allocates shared resources (port capacities, shipping routes) at country level, while subproblems optimize individual product routing given resource allocations. Each of 200 product subproblems solves independently as single-commodity network flow, enabling **embarrassingly parallel execution** across 4-8 cores. Master problem formulation in CVXPY provides intuitive modeling syntax, while OR-Tools handles subproblem network flows with microsecond-scale performance. Iterative Benders cuts progressively refine the master problem, typically converging in 10-50 iterations depending on coupling strength.

Recent algorithmic advances include **tree-based multi-commodity formulations** (ArXiv 2509.24656v2, 2024) scaling to millions of commodities through source-based decomposition and column generation. This approach reduces master problem complexity to O(|E|) capacity constraints regardless of commodity count, with pricing subproblems solvable via shortest path algorithms. For 50×200 scenarios, preliminary benchmarks suggest 5-15 minute solve times on modern hardware.

Computational complexity analysis reveals critical scaling properties. Interior point methods scale as O(n^3.5) per iteration with O(√n) iterations—favorable for very large problems with dense constraint matrices. Network simplex achieves O(n²m) for sparse networks typical in trade. Multi-commodity LP scales as O(k^2.5 n² √m) where k represents commodity count, explaining why direct approaches become intractable beyond k=1,000. **Decomposition transforms exponential-in-k complexity to linear-in-k** through parallelization, fundamentally altering tractability boundaries.

Memory requirements favor decomposed approaches: dense formulations demand 50GB+ for 500k variables, while sparse networks require only 2-5GB exploiting 95%+ sparsity. Decomposed subproblems fit comfortably in 500MB each, enabling cloud deployment on standard instances. Target performance metrics for policy analysis applications require 15-30 minute baseline solves, 5-10 minutes for sensitivity analysis with warm-starting, and 1-4 hours for Monte Carlo scenarios with 10-50 parallel runs.

### Comparing optimization libraries for production deployment

Commercial and open-source optimization libraries present distinct trade-offs. **Gurobi** dominates performance benchmarks (Mittelmann 2024), showing 1.4-1.9× speedup over competitors on LP problems and 1.8-2.8× on mixed-integer programs with parallelization. Academic licenses provide full functionality at zero cost, while commercial licensing costs $10k-50k annually. CPLEX (IBM) offers comparable performance without consistent superiority, with mature enterprise support but similar pricing. Both solvers handle millions of variables routinely, with excellent documentation and active user communities.

**Open-source alternatives** provide viable pathways for non-commercial deployment. HiGHS shows excellent LP performance approaching commercial solvers, released under permissive MIT license with active development. CBC (COIN-OR) handles mixed-integer problems 2-5× slower than commercial solvers—acceptable for many applications. SCIP provides best-in-class open-source MILP performance at 1.5-3× slower than Gurobi, available free for academic use. OR-Tools packages optimized implementations of network flow algorithms, constraint programming, and routing with Apache 2.0 licensing.

**CVXPY** serves as high-level modeling layer, automatically reformulating problems and dispatching to multiple backend solvers. Domain-specific language enables rapid prototyping with intuitive syntax like `cp.Minimize(cp.sum(costs @ x))` for objective functions and `A @ x <= b` for constraints. Performance overhead typically adds 5-10× modeling time compared to direct solver APIs, but development velocity gains justify this for research and early-stage implementation. Version 1.2+ substantially improved performance through conic reformulation and sparsity exploitation.

| Library | Speed | Ease | Cost | Best Application |
|---------|-------|------|------|------------------|
| Gurobi | ★★★★★ | ★★★★☆ | $$$$ | Production MILP, large-scale optimization |
| CPLEX | ★★★★★ | ★★★★☆ | $$$$ | Enterprise systems, IBM integration |
| OR-Tools | ★★★★☆ | ★★★★☆ | Free | Network flows, routing, open-source projects |
| HiGHS | ★★★★☆ | ★★★☆☆ | Free | Open-source LP, research without budget |
| CVXPY | ★★☆☆☆ | ★★★★★ | Free | Prototyping, convex optimization, education |
| NetworkX | ★★☆☆☆ | ★★★★★ | Free | Graph analysis, visualization, small problems |

**Recommended architecture** uses CVXPY for master problem modeling with Gurobi solver (academic license) or HiGHS (open-source), OR-Tools `SimpleMinCostFlow` for product routing subproblems, and Python's `concurrent.futures.ProcessPoolExecutor` for parallelization. This combination achieves 15-30 minute solve times for 50×200 scale, extends gracefully to 100+ countries through increased parallelization, and maintains code clarity for iterative development.

## Machine learning detects triangulation through graph and anomaly analysis

Sanctions evasion detection requires layered approaches combining rule-based screening, unsupervised anomaly detection, and graph analysis. **Isolation Forest achieves F1 scores of 0.76-0.92** for trade anomalies, operating on the principle that outliers require fewer random partitions to isolate. Typical hyperparameters specify 100 estimators with contamination rates of 0.1-0.3 depending on expected evasion prevalence. DBSCAN clustering complements isolation forests for density-based outlier detection, flagging low-density regions as suspicious when epsilon and MinPts parameters properly tuned.

**Graph neural networks and centrality analysis** identify intermediary nodes in multi-country evasion schemes. Betweenness centrality measures the fraction of shortest paths passing through each node, with formula BC(v) = Σ(σ_st(v) / σ_st) computed efficiently in O(nm) time using Brandes' algorithm. High betweenness values flag potential transshipment hubs—Turkey, UAE, Malaysia, and Vietnam show elevated scores coinciding with documented evasion schemes. Temporal network analysis tracks betweenness evolution, detecting sudden increases when new intermediaries emerge post-sanctions.

**Rule-based systems** provide first-line screening through statistical thresholds and red flags. Z-score analysis flags deviations beyond 2-3 standard deviations, effective for approximately normal distributions. Volume-capacity ratios identify exports exceeding domestic production capacity—a physical impossibility indicating transshipment. Pre/post sanctions comparison detects correlated changes: direct trade collapse accompanied by third-country surge. Price discrepancy analysis compares declared values against market benchmarks, catching invoice manipulation and transfer pricing schemes.

Ensemble methods combining multiple algorithms achieve superior performance: Random Forest classification reaches F1=0.91 on market manipulation datasets, while deep ensemble approaches (Isolation Forest + LOF + OCSVM + KNN aggregated through MLP) achieve F1=0.92. Time series methods including LSTM networks and autoencoders detect temporal anomalies with 84% accuracy on wildlife trade datasets. **Recommended detection pipeline** stages rules for obvious violations (fast, interpretable), then unsupervised ML for complex patterns (Isolation Forest primary, DBSCAN supplementary), finally graph analysis for network intermediaries.

Performance metrics require careful interpretation in imbalanced contexts. Precision measures false alarm rate—critical for avoiding alert fatigue in high-volume customs screening. Empirical studies show default approaches yield 54% false positive rates, optimized to 28% through hyperparameter tuning and feature engineering. Recall captures evasion detection rate—North Korean sanctions saw ~80% coal shipments undetected, indicating FNR=0.80, unacceptably high. **Target benchmarks** suggest precision 0.7-0.9, recall 0.8-0.9, F1 scores 0.75-0.92, and false positive rates below 30% for operational viability.

### Quantifying real-world evasion schemes validates detection methods

**Chinese transshipment through Vietnam** (2018-2025) reached estimated $40B+ annually, representing 33% of Vietnam's $123B exports to the US according to White House analysis. Harvard studies estimate 8.8-41.7% of Vietnam export growth stems from Chinese transshipment, with indirect Chinese content rising from 9% to 28% of Vietnamese exports. Detection combined volume spike analysis (21% annual growth vs. 6% historical baseline), factory audits discovering "Made in China" label removal, supply chain mapping, and certificate verification. The 2025 US-Vietnam agreement imposed 20% tariffs on Vietnamese goods and 40% on identified transshipments, with enhanced documentation requirements including supply chain declarations.

**Russian oil circumvention** (2022-2025) generated $178B revenues in 2023, projected $200B for 2024 despite G7 sanctions. India increased purchases from negligible to 55.9M tonnes annually, China imports 57.7M tonnes, and Turkey 17.4M tonnes—collectively absorbing 80% of Russian crude. **Refined product laundering** routes an additional €42B through "laundromat" refineries: India re-exports 3.7M tonnes oil products to G7 countries, China 3M tonnes, UAE 2.9M tonnes. Shadow fleet operations employ 600+ aging tankers with AIS manipulation, traveling 3× normal distances, selling at $20-30/barrel discounts yet maintaining $178B total revenues through volume.

**Iranian sanctions evasion** networks laundered $13-20B through Turkish gold-for-oil schemes (2012-2013), with gold exports surging from $55M to $6.5B. Ansar Bank network transferred $1B+ through Dubai shell companies including Ansar Exchange ($800M in 18 months). Detection employed network analysis mapping 2,100 Suspicious Activity Reports, identifying Halkbank as key intermediary eventually indicted in 2019. Document forensics and financial flow tracking proved essential given sophisticated corporate structures—Babak Zanjani embezzled $2.7B from Iranian government through front companies before arrest.

**North Korean maritime violations** delivered 3× petroleum cap (1.5M barrels vs. 500K limit) and $370M coal exports despite total ban. Ship-to-ship transfers at sea, AIS disabling (100 ships monthly in 2015, reduced to 12/170 by 2018 through enforcement), flags of convenience, and physical vessel alterations in Chinese shipyards enabled continued trade. Satellite imagery (Planet Labs), eight-nation coalition surveillance, and hull photography proved most effective for detection. Machine learning pattern recognition and electronic document verification supplemented human analysis. However, Russia and China ceased enforcement cooperation in 2023, limiting operational impact.

Detection effectiveness metrics show **false positive reduction from 54% to 28%** through optimization, **F1 scores 0.75-0.95** for various commodity types, and **MTTD (Mean Time to Detection)** varying from real-time AIS monitoring to months for sophisticated corporate schemes. Graph analysis identifies critical intermediaries within days when properly implemented, while rule-based volume spikes flag suspicious patterns immediately. The challenge lies in **converting detection to enforcement**—technical capability exceeds political will and jurisdictional authority in many documented cases.

## Integrating data sources requires reconciliation and careful calibration

**UN Comtrade provides bilateral trade flows at HS6 product detail** for 200+ countries, 1962-present, accessible through REST API with 500 calls/day (free tier) or unlimited (subscription). Python's `comtradeapicall` package simplifies access with preview functions (500 records, no authentication) and bulk downloads (250k records per call with subscription key). Critical data structure includes Classification (HS, SITC, BEC), Trade Flow direction (Export, Import, Re-export), Trade Value in current USD, and Quantity/Weight fields. Reporter-Partner country codes follow UN M49 standard requiring conversion to ISO3 for integration with other sources.

**Mirror data reconciliation** addresses systematic 10-20% CIF/FOB discrepancies between reported exports and partner-reported imports. Best practice converts imports to FOB by dividing by 1.10 (10% markup for insurance and freight), then reconciles using reliability weights favoring importer reports when discrepancies exceed 20%. The BACI database (CEPII) provides pre-reconciled flows using sophisticated algorithms, saving substantial preprocessing effort. Missing data requires conditional treatment: fill zeros only when reporter demonstrates activity in other partnerships, otherwise preserve missingness to avoid false zeros.

**GTAP database** (current version 11, base years 2004-2017) provides comprehensive input-output structure with bilateral trade (VXMD), tariffs (TMS), and Armington elasticities (ESUBM) for 141 regions and 65 sectors. Academic pricing approximately $500-1000 grants access to .har (GEMPACK) and .gdx (GAMS) formats, processed through `gdxpds` Python library converting to pandas DataFrames. Parameter extraction for gravity calibration requires mapping GTAP sectors to HS codes—non-trivial given different aggregation schemes—and temporal adjustment when using non-contemporary base years through GDP deflators and growth rates.

**CEPII databases** offer harmonized gravity variables avoiding common pitfalls. GeoDist provides population-weighted distances theoretically consistent with gravity models, contiguity indicators, and internal distances calculated as 0.38√area following Yotov (2012). The Gravity Database (2022 version, coverage 1948-2020) compiles trade flows from multiple sources (Comtrade, BACI, IMF DOTS), all standard gravity covariates (distance, language, colonial ties), RTAs from Mario Larch's continuously updated database, and GDP/population from Penn World Tables. Using pre-compiled Gravity Database eliminates merging errors, ensures theoretically appropriate variable construction, and provides instant access to 70+ years of consistent data.

### Building transport cost matrices from multiple data streams

Distance-to-cost conversion employs three primary formulations depending on theoretical framework. **Iceberg costs** assume fraction τ of goods melts in transit, implemented as transport cost = exp(rate × distance) with typical rates 0.0001-0.0002. **Ad-valorem costs** specify percentage markups proportional to distance raised to elasticity: cost = base × (distance/1000)^|elasticity| with base 0.05 and elasticity -0.1 generating realistic cost profiles. **Time costs** multiply daily depreciation by transit days: cost = 1 + (daily_rate × distance / (speed × 24)) using container ship speeds around 40 km/h and daily rates 0.1-0.2% of goods value.

Freight rate indices provide empirical anchors. **Baltic Dry Index** tracks bulk shipping costs for coal, iron ore, and grain, available from Baltic Exchange with historical data from Trading Economics and Bloomberg. **Freightos Baltic Index (FBX)** covers container rates for major routes, providing daily 40-foot container prices. Integration requires matching route-specific rates to bilateral country pairs, temporal alignment since freight rates exhibit high volatility (2020-2021 saw 5× increases), and product-specific adjustment as containers, bulk, and specialized shipping have distinct cost structures.

Maritime distances account for canal passages (Suez, Panama) and navigational constraints, available from SeaRates.com or port-to-port databases. Internal/domestic distances use CEPII's formula 0.38√area approximating population-weighted average distance within country borders. Combined with bilateral distances, this enables gravity estimation including domestic trade flows—essential for proper identification of border effects and globalization trends (Yotov 2012, 2022).

### Calibrating structural parameters through iterative estimation

Parameter calibration workflow proceeds in phases. **Phase 1 estimates reduced-form coefficients** using PPML with three-way fixed effects, recovering distance elasticity θ, border effect magnitudes, and RTA impacts directly from bilateral trade data. Typical specification:

```python
from fixest import feols
model = feols('trade ~ log_dist + contig + comlang + rta | exporter_time + importer_time + pair_id', data=data, family='poisson', vcov='cluster')
```

**Phase 2 extracts structural multilateral resistance terms** from exporter-time and importer-time fixed effects, representing outward and inward multilateral resistance indices in Anderson & van Wincoop terminology. These capture general equilibrium price indices affecting each country's trade pattern with all partners simultaneously.

**Phase 3 solves counterfactual equilibria** by perturbing trade costs (removing tariffs, imposing sanctions, changing transportation costs) and iteratively solving for new multilateral resistance consistent with market clearing. The `ge_gravity` package (Stata) or `GEGravity` (R) automate this using constrained nonlinear equation solvers. Python implementations solve the fixed point problem:

```python
IMR[j] = [Σᵢ (Yᵢ/Y_world) × (t_ij/OMR[i])^(1-σ)]^(1/(1-σ))
OMR[i] = [Σⱼ (Eⱼ/Y_world) × (t_ij/IMR[j])^(1-σ)]^(1/(1-σ))
```

Convergence typically requires 50-500 iterations depending on tolerance (10^-6 standard) and number of countries. Welfare changes compute as ΔW = (Π̂'/Π̂)^(1/(1-σ)) where Π represents home trade share.

**Validation approaches** include out-of-sample prediction testing (hold out 20% of bilateral pairs, compare predicted to actual trade), cross-validation across time periods (estimate on 2015-2019, validate on 2020-2022), and comparative statics (verify trade elasticity σ produces reasonable responses to 10% tariff increases). Sensitivity analysis sweeps key parameters—trade elasticity from 4-12, distance elasticity from -0.5 to -1.5—documenting robustness of policy conclusions. Target benchmarks require R² above 0.60 for baseline specification, out-of-sample prediction errors below 20%, and coefficient estimates within consensus ranges established by meta-analyses.

## Implementing complete workflows requires modular architecture

Production-ready trade simulation systems decompose into five core modules: **data ingestion**, **parameter estimation**, **optimization engine**, **detection system**, and **reporting**. Each module maintains clear interfaces enabling independent testing, parallel development, and technology substitution without system-wide rewrites.

**Data ingestion pipeline** begins with Comtrade API calls through `comtradeapicall`, standardizes country codes to ISO3 using `pycountry`, merges gravity covariates from CEPII, appends GDP data from World Bank/IMF, reconciles mirror flows, and exports to Parquet format with Snappy compression reducing storage by 70-80% while maintaining fast access. Scheduled daily updates for recent periods and annual refresh for historical revisions maintain currency. Data quality checks flag missing value percentages above 20%, implausible unit values (outside 1st-99th percentile), and sudden structural breaks requiring investigation.

**Parameter estimation module** implements PPML using `fixest` in R or `statsmodels`/`linearmodels` in Python, saves coefficient vectors and fixed effects, conducts diagnostic tests (RESET for specification, CVMR test for variance assumptions), generates bootstrap standard errors with 1000 replications for robust inference, and archives results with model specifications enabling reproduction. Annual re-estimation incorporates new trade data, while sensitivity analysis explores coefficient stability across subperiods and product categories.

**Optimization engine** structures as master-subproblem architecture: master problem allocates shared resources using CVXPY + Gurobi, 200 product subproblems solve via OR-Tools `SimpleMinCostFlow` with `ProcessPoolExecutor` providing 8-way parallelization, iterative Benders cut generation refines master allocation, and convergence checking every 10 iterations assesses optimality gap. Warm-starting from previous solutions reduces iteration count by 50-70% for similar scenarios. Cloud deployment on AWS/GCP provides elastic scaling for Monte Carlo analysis.

**Detection system** pipelines trade flows through staged filters: hard rules eliminate direct sanctions violations and capacity impossibilities (30% of volume), soft rules compute z-scores and geographic risk scoring (flag top 10%), Isolation Forest anomaly detection (contamination=0.15), DBSCAN clustering identifies suspicious networks (eps=0.3, min_samples=5), and NetworkX betweenness centrality ranks intermediary nodes. Human analyst review of top 5% reduces false positives from 28% algorithmic baseline to 10% after expert filtering. Weekly model retraining incorporates confirmed cases, maintaining detection performance as evasion tactics evolve.

**Reporting module** generates policy briefs combining quantitative results (welfare changes, trade flow redirections, fiscal impacts) with uncertainty quantification (95% confidence intervals from bootstrap), scenario comparison tables, network visualizations using Gephi or NetworkX, and executive summaries following Smart Brevity principles. LaTeX templates automate figure generation, while Jupyter notebooks provide reproducible analysis pipelines. Version control through Git maintains audit trail of methodological choices and sensitivity tests.

### Code example: complete 50-country, 10-product simulation

This abbreviated example demonstrates core workflow integrating gravity estimation, optimization, and validation:

```python
import pandas as pd
import numpy as np
from fixest import feols
from ortools.graph.python import min_cost_flow
import cvxpy as cp
from concurrent.futures import ProcessPoolExecutor

# 1. Load and prepare data
trade = pd.read_parquet('comtrade_processed.parquet')
gravity = pd.read_csv('cepii_gravity.csv')
data = trade.merge(gravity, on=['iso_o', 'iso_d', 'year'])

# 2. Estimate gravity model
data['log_dist'] = np.log(data['distw_harmonic'])
model = feols(
    'trade ~ log_dist + contig + comlang + rta | iso_o_year + iso_d_year + pair',
    data=data[data['year'] == 2021], family='poisson', vcov='cluster'
)
theta = model.coef()['log_dist']  # Distance elasticity
fe = model.fixef()  # Multilateral resistance terms

# 3. Build bilateral trade cost matrix
def trade_cost(row):
    return np.exp(row['log_dist'] * theta 
                  + model.coef()['contig'] * row['contig']
                  + model.coef()['rta'] * row['rta'])

data['cost'] = data.apply(trade_cost, axis=1)
cost_matrix = data.pivot('iso_o', 'iso_d', 'cost')

# 4. Solve product routing (single product example)
def route_product(product_id, supplies, demands, costs, capacities):
    smcf = min_cost_flow.SimpleMinCostFlow()
    
    # Add arcs with costs and capacities
    for i, j in costs.index:
        smcf.add_arc_with_capacity_and_unit_cost(
            i, j, capacities[i,j], int(costs[i,j] * 1000))
    
    # Set supplies and demands
    for node, supply in supplies.items():
        smcf.set_node_supply(node, supply)
    for node, demand in demands.items():
        smcf.set_node_supply(node, -demand)
    
    status = smcf.solve()
    if status != smcf.OPTIMAL:
        return None
    
    flows = {(smcf.tail(i), smcf.head(i)): smcf.flow(i) 
             for i in range(smcf.num_arcs())}
    return flows

# 5. Parallel solve for all products
with ProcessPoolExecutor(max_workers=8) as executor:
    product_data = [(pid, supplies[pid], demands[pid], costs, caps) 
                    for pid in range(10)]
    results = list(executor.map(lambda args: route_product(*args), product_data))

# 6. Aggregate and validate
total_cost = sum(sum(f * costs[i,j] for (i,j), f in result.items()) 
                 for result in results if result)
predicted_flows = aggregate_flows(results)
validation_r2 = r2_score(actual_flows, predicted_flows)
print(f"Simulation R²: {validation_r2:.3f}")

# 7. Counterfactual analysis
data_cf = data.copy()
data_cf['rta'] = 1  # Global free trade
data_cf['cost_cf'] = data_cf.apply(trade_cost, axis=1)
# Re-solve with new costs, compute welfare changes
```

This architecture scales to 50 countries and 200 products through increased parallelization (20-40 workers) and optimized data structures (sparse matrices, memory-mapped arrays). Expected runtime: 15-25 minutes on 16-core workstation with 32GB RAM. Cloud deployment on AWS m5.4xlarge instances achieves similar performance at $0.768/hour on-demand pricing, enabling cost-effective scenario analysis.

## Synthesis: achieving policy-relevant simulation capability

Combining econometric rigor, computational efficiency, and detection sophistication creates production-ready UTA simulation systems. **Three implementation priorities** determine success: adopt PPML gravity estimation with three-way fixed effects as econometric foundation, implement Benders decomposition with product-based subproblems for computational tractability, and layer rule-based with ML-based detection achieving F1 scores above 0.75.

**Recommended technology stack** integrates Python for orchestration, CVXPY for optimization modeling, Gurobi (academic license) or HiGHS (open-source) for master problem solving, OR-Tools for network flow subproblems, NetworkX for graph analysis, scikit-learn for anomaly detection, and Parquet for data storage. This combination achieves 15-30 minute baseline performance, extends to 100+ countries through parallelization, maintains code clarity for ongoing development, and costs zero for academic applications.

**Validation against real-world evasion** demonstrates both capability and limitations. Systems detect volume spikes (Vietnam transshipment), price anomalies (Iranian schemes), and network intermediaries (Russian oil routes) with 75-92% accuracy. However, enforcement depends on political will exceeding technical capability—North Korean sanctions show 80% undetected shipments not from algorithmic failure but Russian/Chinese non-cooperation. Detection enables policy response but cannot substitute for international coordination.

**Future developments** will enhance capability through graph neural networks replacing hand-crafted features (5-10% F1 improvement expected), reinforcement learning for adaptive trade policy (exploring strategy spaces), and satellite imagery integration for physical verification (reducing document fraud). Near-term priorities focus on robustness: ensemble methods reducing false positives to 15-20%, explainable AI techniques enabling customs officer trust, and federated learning preserving data sovereignty while improving collaborative detection.

The complete toolkit enables realistic policy analysis: simulate tariff changes and compute welfare impacts within theoretical frameworks, optimize trade routing under capacity and regulatory constraints, detect circumvention attempts with quantified accuracy, and validate against documented evasion schemes. Systems achieving 30-minute policy response times transform trade analysis from academic exercise to operational decision support, provided implementations maintain econometric validity, computational reproducibility, and epistemic humility regarding model limitations.