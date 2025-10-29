# Simplified Product Object

**(Core Attributes)**

### **1. Identity & Category**

- Product Name (e.g., “Steel”, “Smartphone”, “Wheat”)
- Category: Raw Material / Intermediate Good / Finished Product
- SubcategoryList: [Raw Material / Intermediate Good / Finished Product]
- Strategic Level: Low / Medium / High (e.g. chips = high)

### **2. Cost Structure** *(mini P&L)*

| Cost Component | Description |
| --- | --- |
| Labor Cost per unit | Wages needed to produce one unit |
| Raw Material Cost | Inputs or supply chain materials |
| Energy Cost | Electricity, fuel, etc |
| Capital/Equipment Cost | Cost of machinery, maintenance (optional aggregate) |
| Transportation Cost | Internal logistics + port fees |
| Shipping + Insurance | Cost to send product internationally |
| Tariff Impact | Tariff rate applied by each trading partner |
| Taxes/Subsidies | Government incentives or penalties |

### **Price & Trade Parameters**

- Base Price (Cost + Markup)
- Markup (%) – adjustable by country strategy
- Current Export Price (calculated)
- Competitiveness Index (relative measure vs other countries)
- Elasticity / Demand Sensitivity (optional now, add later)

# **Country-Level Structure (Built From Products)**

Instead of defining GDP directly, **GDP becomes the result** of product output:

**Country = { list of products }**

Country scoring is derived from:

- Total export revenue = sum over all products
- Trade balance
- Strategic resilience (diversification and dependency on others)

### **Country Metadata (minimal needed)**

- Labor demographic Mix
- Labor cost index (affects all labor components)
- Energy price index matrix (affects all energy cost components)
- Domestic policy variables: subsidies, taxes, export bans
- Trade agreements (affect tariffs and shipping friction)

# **Correct Level of Abstraction**

Each product should be defined by *four strategic vectors*, not by all physical attributes:

1. **Production Elasticity** – how easily supply can increase or decrease
2. **Substitutability** – how many alternatives exist globally
3. **Transport & Storage Sensitivity** – is it a pipeline good, refrigerated good, or digitally shipped good?
4. **Strategic Leverage Index** – does this product create dependency or power?