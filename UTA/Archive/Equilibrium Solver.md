# Equilibrium Solver

**Equilibrium Solver Engine** – вычисляет новую мировую цену, объёмы торговли и балансы после каждого хода.

Full Equilibrium 

- Integrate a **market-clearing algorithm** (Walrasian tâtonnement or Newton-Raphson solver).
- Or use **pymrio** to propagate shocks through multi-regional input-output tables (MRIO).
- This simulates full general equilibrium: oversupply affects downstream industries, income effects, GDP feedback loops.

## MVP:

- Price dynamically responds to supply shifts.
- Demand is modeled as function of price and country consumption capability.
- No need to solve full equilibrium.
- Can be implemented as a single function in the model.