# Technical Foundation

# ✅**1. Environment & Framework Setup**

- [ ]  Install **Mesa** (agent-based modeling framework in Python)
- [ ]  Set up project structure (modular: agents, model, data, policies, simulation runner)
- [ ]  Define version control (GitHub repo)
- [ ]  Confirm ability to run Mesa visualization server (optional but useful)
    
    ---
    

# ✅ **Phase 2 – Load Real Economic Structure**

*(We are not inventing trade flows—we are pulling real ones.)*

### **2.1 Choose Base Dataset**

- [ ]  Download **WIOD** (World Input-Output Database) or **OECD ICIO** dataset
    
    Purpose: contains real global trade flows between countries and sectors.
    
- [ ]  Select initial **5 starter countries**: e.g. US, China, Canada, Japan, Germany
- [ ]  Extract relevant sectors (start with steel, energy, agriculture, manufacturing, tech)

### **2.2 Load with pymrio (recommended)**

- [ ]  Install **pymrio** (Python package for MRIO tables)
- [ ]  Load MRIO table to extract:
    - Inter-country trade volumes
    - Sector-level production/output
    - Input-output links (how steel feeds into other sectors)

---

# ✅ **Phase 3 – Build the Mesa Model**

### **3.1 Define Agent Structure (Countries as Agents)**

Each country agent will have:

- Production capacity per sector
- Export/import flow per product
- Policy levers (subsidy, tariff, quota, strategic ban)
- Compliance / cheating flag
- Reward function (maximize GDP, credits, influence)

### **3.2 Define Environment (World Model)**

- WorldState holds:
    - Trade matrix (from pymrio)
    - Policy rules (UTA enforcement logic placeholder)
    - Simulation tick counter

---

# ✅ **Phase 4 – Bridge Economic Data and Agent Logic**

### **4.1 Data Integration Tasks**

- [ ]  Map MRIO sectors to “strategic products” (steel is one; refine later)
- [ ]  Assign cost parameters (labor, energy, materials → from World Bank or CIA Factbook)
- [ ]  Initialize each agent with real baseline data (production, exports, imports)

### **4.2 Define Update Logic**

- [ ]  Each step: agents choose policy (e.g., Canada increases steel capacity)
- [ ]  Update world trade matrix accordingly
- [ ]  Recalculate impacts using MRIO multipliers

---

# ✅ **Phase 5 – Prototype Scenario: “Canada Triples Steel Production”**

### **Goal of this milestone**

Be able to run:

```python
world.apply_policy("Canada", action="increase_production", sector="steel", factor=3.0)
simulation.step()
world.get_trade_impacts()

```

# **Outputs:**

- New export volumes
- Price changes (if oversupply)
- Impact on other countries (market share shifts, retaliation probability)
- Changes in UTA credit score