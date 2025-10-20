# Repository Cleanup Summary

## Completed Tasks

### 1. File Renaming (GUID Removal)
All Notion-exported files with GUID suffixes have been cleaned up:

**Files Renamed:**
- `Agent Intelligence Module 292eaf87a2fd80d38039dceb2eb5b87d.md` → `Agent Intelligence Module.md`
- `Compliance & Cheating Detection Module 292eaf87a2fd80f4969bc61dd92d6486.md` → `Compliance & Cheating Detection Module.md`
- `Demand Module 292eaf87a2fd8044948ed030c430d795.md` → `Demand Module.md`
- `Energy & Logistics Module 292eaf87a2fd808fb10dd797e0a67914.md` → `Energy & Logistics Module.md`
- `Equilibrium Solver 292eaf87a2fd80df86e2fac7392c07d8.md` → `Equilibrium Solver.md`
- `Firm vs State Actions 292eaf87a2fd8073935bfa44b5569ae2.md` → `Firm vs State Actions.md`
- `Impact propagation mechanics 292eaf87a2fd807bb9f0d48c18d6a8fe.md` → `Impact propagation mechanics.md`
- `Pricing & Market Equilibrium Module 292eaf87a2fd80fa975fe4df2aeb0bba.md` → `Pricing & Market Equilibrium Module.md`
- `Reaction to Macro Events Engine 292eaf87a2fd800d945fd84be21f292e.md` → `Reaction to Macro Events Engine.md`
- `Sanctions & Geopolitics Module 292eaf87a2fd807f9727f741430e49d1.md` → `Sanctions & Geopolitics Module.md`
- `Simplified Product Object 292eaf87a2fd8016853df725a5adc1b5.md` → `Simplified Product Object.md`
- `Subsidy & Industrial Policy Module 292eaf87a2fd80bdbef4dc6a6f28d1e7.md` → `Subsidy & Industrial Policy Module.md`
- `Technical Foundation 292eaf87a2fd80f283cff73b34317811.md` → `Technical Foundation.md`
- `Trade Flow Module 292eaf87a2fd80c1ac80ff16e7c75d65.md` → `Trade Flow Module.md`
- `Post Simulation Work (papers, PhDs and tournaments 292eaf87a2fd80b3b782e2481a2e188e.md` → `Post Simulation Work (papers, PhDs and tournaments).md`
- `Intellectual Network 292eaf87a2fd80f98f8ff6ebdbfb417f.md` → `Intellectual Network.md`

### 2. Link Updates
All internal markdown links have been updated to reflect the new clean filenames:

**Files Updated:**
- `UTA/UTA Simulation.md` - Fixed 14 component links
- `Unified Trade Authority.md` - Fixed 2 phase links
- `UTA/UTA Simulation/Технические Задания.md` - Fixed 6 technical assignment links
- `UTA/Post Simulation Work (papers, PhDs and tournaments).md` - Fixed 1 link

---

## Nearly Empty Files (Requiring Content)

### Critical Module Specifications (Single-line placeholders)

These files contain only brief one-line descriptions in Russian and need full specification content:

#### 1. **Trade Flow Module** (`UTA/UTA Simulation/Trade Flow Module.md`)
- **Current:** "реальные объёмы импорта/экспорта между странами по секторам."
- **Translation:** "actual import/export volumes between countries by sectors."
- **Needed:** Full specification of bilateral trade flows, transport costs, tariff calculations, trade matrix structure

#### 2. **Demand Module** (`UTA/UTA Simulation/Demand Module.md`)
- **Current:** "внутренняя и внешняя потребность в товарах, эластичность, замещения."
- **Translation:** "domestic and foreign demand for goods, elasticity, substitutions."
- **Needed:** Demand functions, price elasticities, income elasticities, substitution matrices, consumption patterns

#### 3. **Sanctions & Geopolitics Module** (`UTA/UTA Simulation/Sanctions & Geopolitics Module.md`)
- **Current:** "ограничения, тарифы, эмбарго, ответные меры."
- **Translation:** "restrictions, tariffs, embargoes, countermeasures."
- **Needed:** Sanctions implementation logic, geopolitical constraints, alliance mechanics, retaliatory measures, red lines

#### 4. **Energy & Logistics Module** (`UTA/UTA Simulation/Energy & Logistics Module.md`)
- **Current:** "стоимость транспорта, топлива, инфраструктурные chokepoints"
- **Translation:** "transport costs, fuel, infrastructure chokepoints"
- **Needed:** Energy pricing, transportation cost models, chokepoint identification, shipping routes, pipeline dependencies

#### 5. **Compliance & Cheating Detection Module** (`UTA/UTA Simulation/Compliance & Cheating Detection Module.md`)
- **Current:** "как страны манипулируют системой и как их можно поймать"
- **Translation:** "how countries manipulate the system and how they can be caught"
- **Needed:** Detection algorithms, anomaly identification, audit mechanisms, penalty structures, probabilistic discovery

#### 6. **Pricing & Market Equilibrium Module** (`UTA/UTA Simulation/Pricing & Market Equilibrium Module.md`)
- **Current:** "расчёт равновесных цен через CGE (Walrasian clearing)"
- **Translation:** "calculation of equilibrium prices via CGE (Walrasian clearing)"
- **Needed:** Market clearing algorithms, price adjustment mechanisms, Walrasian/Newton-Raphson solver details, convergence criteria

#### 7. **Subsidy & Industrial Policy Module** (`UTA/UTA Simulation/Subsidy & Industrial Policy Module.md`)
- **Current:** "эффект господдержки на себестоимость и конкурентоспособность."
- **Translation:** "effect of government support on cost and competitiveness."
- **Needed:** Subsidy calculation methods, cost structure impacts, competitiveness metrics, policy instrument models

### Technical Assignment Documents (Minimal content)

#### 8. **Энергетический аналитик** (`UTA/UTA Simulation/TechnicalAssigments(TZ)/Энергетический аналитик.md`)
- **Current:** Only title "Энергетический аналитик" (Energy Analyst)
- **Needed:** Complete technical assignment for energy analyst role including:
  - Energy market modeling requirements
  - Oil, gas, electricity, renewables specifications
  - Infrastructure and chokepoint analysis
  - Energy dependency calculations
  - Price volatility modeling

#### 9. **Поведенческий и системный аналитик** (`UTA/UTA Simulation/TechnicalAssigments(TZ)/Поведенческий и системный аналитик.md`)
- **Current:** Only 3 lines: title + "Теория игр, системы с нелинейной динамикой" + "Модель должна быть устойчива, не ломаться от хаоса"
- **Translation:** "Game theory, systems with nonlinear dynamics" + "Model must be stable, not break from chaos"
- **Needed:** Complete technical assignment including:
  - Game theory frameworks to apply
  - Behavioral economics considerations
  - Stability analysis requirements
  - Complex systems dynamics
  - Chaos prevention mechanisms

---

## Recommended Todo List for Content Population

### Phase 1: Core Economic Modules (Highest Priority)
These are essential for the MVP and should be completed first:

1. **Demand Module**
   - Define demand functions (Cobb-Douglas, CES, or custom)
   - Specify elasticity parameters (price, income, cross-price)
   - Document substitution patterns between products
   - Create demand calibration methodology

2. **Pricing & Market Equilibrium Module**
   - Select and document equilibrium solver (Walrasian tâtonnement vs Newton-Raphson)
   - Define convergence criteria and stopping rules
   - Specify price adjustment speed parameters
   - Document how to integrate with pymrio for IO propagation

3. **Trade Flow Module**
   - Define bilateral trade matrix structure
   - Specify transport cost calculations (distance, mode, fuel)
   - Document tariff application logic
   - Create trade flow calibration process from WIOD/OECD data

### Phase 2: Policy & Intervention Modules
Essential for simulating strategic country behavior:

4. **Subsidy & Industrial Policy Module**
   - Define subsidy types (direct, tax breaks, soft loans, procurement)
   - Specify cost impact calculations
   - Document competitiveness index changes
   - Create subsidy detection thresholds

5. **Sanctions & Geopolitics Module**
   - Define sanction types and implementation
   - Specify alliance formation mechanics
   - Document red line triggers
   - Create retaliation logic and escalation ladders

### Phase 3: Strategic Infrastructure
Critical for realism and strategic gameplay:

6. **Energy & Logistics Module**
   - Define energy product types (oil, gas, coal, electricity, renewables)
   - Specify chokepoint catalog (Strait of Hormuz, Suez, etc.)
   - Document transportation cost models
   - Create energy dependency metrics

7. **Compliance & Cheating Detection Module**
   - Define cheating strategy catalog
   - Specify detection algorithms (ratio tests, anomaly detection)
   - Document audit mechanics and probabilities
   - Create penalty structures and credit adjustments

### Phase 4: Technical Assignments
Complete role-specific requirements:

8. **Энергетический аналитик (Energy Analyst)**
   - Document energy sector modeling requirements
   - Specify data sources and calibration
   - Define energy-economy interaction mechanics
   - Create energy shock scenarios

9. **Поведенческий и системный аналитик (Behavioral & Systems Analyst)**
   - Define game-theoretic frameworks
   - Specify behavioral economics integration
   - Document stability analysis procedures
   - Create complexity and chaos mitigation strategies

---

## Implementation Priority Ranking

**Tier 1 (MVP Blockers):**
1. Demand Module
2. Pricing & Market Equilibrium Module
3. Trade Flow Module

**Tier 2 (Strategic Gameplay):**
4. Subsidy & Industrial Policy Module
5. Sanctions & Geopolitics Module

**Tier 3 (Enhanced Realism):**
6. Energy & Logistics Module
7. Compliance & Cheating Detection Module

**Tier 4 (Role Specifications):**
8. Энергетический аналитик
9. Поведенческий и системный аналитик

---

## Content Structure Recommendations

Each module specification should include:

1. **Overview** - Purpose and scope
2. **Mathematical Formulation** - Core equations and algorithms
3. **Data Requirements** - Input parameters and calibration sources
4. **Implementation Notes** - Python/Mesa integration guidance
5. **Testing Scenarios** - Example use cases
6. **References** - Academic papers and data sources

Each technical assignment should include:

1. **Role Description** - Expert domain and responsibilities
2. **Key Questions** - What this expert must answer
3. **Deliverables** - Specific outputs (formulas, parameters, logic)
4. **Data & Tools** - Required resources
5. **Integration Points** - How this connects to other modules
