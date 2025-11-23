# Glossary – Key Terms of the ProjectUSD Specification

This glossary defines the core terms of the ProjectUSD specification.  
The modules described here show how the components function in an eventual implementation,  
assuming an external development team translates the specification into code.

---

# 🔹 Fundamental System Variables

## **R – Redemption Price**
The internal reference value around which the system stabilizes.  
R defines the mathematical equilibrium and is derived exclusively from  
on-chain measurable quantities — without oracles or fiat references.

---

## **P – Market Price**
The external trading price of ProjectUSD on decentralized exchanges.  
P is the exogenous signal the system reacts to in order to maintain stability.

---

## **r – System Rate**
The variable control parameter of the specification.  
r regulates incentives, demand, debt behavior, and price reactions by  
offsetting deviations between the market price P and the equilibrium price R.  
A higher r increases the cost of money creation; a lower r increases the attractiveness  
of holding and minting.

---

# 🔹 Core System Modules

## **Vault (Collateral Module)**
A module that defines how collateral is deposited, how debt is created,  
and how risks are processed.  
The Vault model specifies collateralization, liquidation rules,  
and the issuance of new units.

---

## **Stability Pool**
A collective risk buffer for undercollateralized positions.  
The Stability Pool absorbs the debt of liquidated vaults and distributes their  
collateral according to the rules defined in the specification.  
It ensures continuous removal of weak positions.

---

## **Redemption Engine**
The specified price-anchoring mechanism.  
The Redemption Engine generates arbitrage signals that pull the market price P  
back toward the equilibrium price R.

---

## **Liquidation Mechanism**
The mechanism that processes undercollateralized vaults and redistributes  
their collateral.  
It ensures that no unbacked debt remains in the system and that  
risk resolution is transparent and rule-based.

---

## **Controller**
The mathematical control system that evaluates the relationship between P, R, and r  
and adjusts the system rate accordingly.  
The Controller maintains dynamic equilibrium across the system.

---

# 🔹 Extension Modules

## **AMO – Algorithmic Market Operations**
Optional algorithmic modules that operate within defined parameters to  
provide liquidity, reduce arbitrage spreads, or optimize the surplus buffer.  
AMOs follow strict, rule-based behavior and operate only within  
narrow economic boundaries.

---

## **PSM – Peg Stability Module**
An optional mechanism for handling short-term market friction.  
The PSM uses limited amounts of external stablecoins as a buffer  
without creating dependency on their price logic.  
It is supplemental and not required for the core architecture.

---

## **Surplus Buffer**
An internal economic buffer that stores system surpluses and smooths  
r-rate fluctuations.  
The surplus buffer stabilizes long-term savings dynamics and absorbs  
transient imbalances.

---

# 🔹 Structural and Security Concepts

## **Immutable Core**
The defined, unchangeable core of all critical mechanisms.  
Once frozen, the Immutable Core remains permanent and protects the system  
from governance manipulation and external interference.

---

## **Freeze Event**
The point at which the core of the system becomes permanently frozen  
and cannot be modified anymore.  
The Freeze Event ensures stability, incorruptibility, and long-term autonomy.

---

## **Periphery Layer**
A flexible outer layer of non-critical components such as AMOs,  
analytical tools, and additional collateral models.  
The Periphery can evolve over time with transparent and restrictive  
change mechanisms.

---

## **TWAP – Time-Weighted Average Price**
A price reference calculated from on-chain trading data.  
TWAP filters out short-term manipulation and serves as a stable input  
for internal analysis.

---

## **MEV Resilience**
A set of design principles that ensure stable outcomes even when  
validators attempt to reorder or manipulate transactions.  
This includes price-protection logic, liquidation design,  
and controlled transitions between P and R.

---

# 🔹 Economic Mechanisms

## **Debt Position**
The obligation created when new units are minted.  
Every debt position is collateral-backed and subject to liquidation rules.

---

## **Collateral Ratio**
The ratio between collateral value and outstanding debt within a vault.  
The specification defines minimum thresholds that guarantee system safety  
and prevent undercollateralization.

---

## **Redemption Spread**
The difference between the market price P and the redemption price R.  
The spread determines the direction and strength of arbitrage activity.

---

## **Savings / Interest Dynamics**
The internal dynamics through which r creates saving incentives  
or increases the cost of debt.  
These dynamics form the core of the autonomous monetary mechanism.

---

# 🔹 System Properties

## **Autonomous Monetary Policy**
A fully rule-based, algorithmic monetary policy with no governance  
and no external price feed dependencies.

---

## **On-Chain Transparency**
All rules, parameters, and transitions are measurable, open-source,  
and auditable by anyone.  
The system relies entirely on verifiable mathematics.

---

## **Decentralized Stability**
System stability arises from internal feedback loops, arbitrage pressure,  
and rule-based adjustments — not from outside support or discretionary intervention.

---
