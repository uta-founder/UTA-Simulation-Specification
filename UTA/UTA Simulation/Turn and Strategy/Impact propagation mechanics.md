# Impact propagation mechanics

This needs well defined mechanics 

- **Supply Demand Mechanics (elasticities etc)**
- **Direct effects:** bilateral_trade.csv recalculates flows and tariff revenue.
- **IO propagation:** shock vectors run through A-matrix to update output, VA, and imports needs per country. Use standard Leontief methods already implemented in open tools (pymrio/iopy) to avoid reinventing. [GitHub+1](https://github.com/IndEcol/pymrio?utm_source=chatgpt.com)
- **UTA layer:** compliance_history.csv and policy_params.csv compute credits/penalties and redistribute.

# “Borrow, don’t build” where possible

- **Trade flows:** UN Comtrade API or BACI bulk. [comtradeplus.un.org+1](https://comtradeplus.un.org/TradeFlow?utm_source=chatgpt.com)
- **IO tables:** OECD ICIO/WIOD. [OECD+1](https://www.oecd.org/en/data/datasets/inter-country-input-output-tables.html?utm_source=chatgpt.com)
- **Tariffs:** WITS. [World Integrated Trade Solution](https://wits.worldbank.org/?utm_source=chatgpt.com)
- **Ready-made IO tooling:** pymrio, iopy. [GitHub+1](https://github.com/IndEcol/pymrio?utm_source=chatgpt.com)
- **Deep MRIO/GTAP:** use if budget allows or pull older free versions. [gtap.agecon.purdue.edu+1](https://www.gtap.agecon.purdue.edu/databases/?utm_source=chatgpt.com)