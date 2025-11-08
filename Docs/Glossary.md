# Glossary – Key Terms of ProjectUSD

---

## **R – Redemption Price (Gleichgewichtspreis)**
The internal reference value around which the market price of ProjectUSD stabilizes.  
It serves as the system’s mathematical anchor and is determined solely by on-chain mechanisms –  
not by external oracles or fiat prices.

---

## **r – System Rate (Interest / Saving Rate)**
The variable control parameter of the Controller.  
It can be positive (interest) or negative (saving rate) and regulates the behavior of borrowers and savers.  

- When **r increases** → money creation becomes more expensive → supply decreases.  
- When **r decreases** → minting and holding become more attractive → demand increases.  

This keeps the market price (P) aligned with the internal equilibrium price (R).

---

## **Vault**
A personal smart-contract vault where users lock native PulseChain assets (e.g. PLS) as collateral  
to mint new ProjectUSD tokens.  
Each vault is fully on-chain, individual, and governed by transparent rules for collateralization,  
liquidation, and repayment.

---

## **Stability Pool**
A collective safety pool where users deposit ProjectUSD to enable liquidations  
and earn rewards.  
When a vault becomes undercollateralized, its debt is covered using the Stability Pool funds,  
and the seized PLS collateral is distributed to depositors.  
This mechanism automatically stabilizes the system.

---

## **Redemption Engine**
The internal price anchor of ProjectUSD.  
Any user can redeem ProjectUSD for PLS at the current equilibrium price R.  
This redemption mechanism creates arbitrage-based feedback:  
price deviations are corrected automatically by market participants.

---

## **AMO – Algorithmic Market Operations**
Optional algorithmic modules that fine-tune liquidity.  
AMOs operate within narrow price bands to reduce arbitrage spreads,  
optimize the system surplus buffer, and manage reserves efficiently.  
All AMO operations are transparent and budgeted.

---

## **PSM – Peg Stability Module**
An optional on-chain basket of other stablecoins (e.g. USDL)  
that helps absorb short-term market friction.  
It is strictly limited by daily swap caps and haircut fees  
and is **never required** for ProjectUSD to function.  
Even without a PSM, the system remains fully autonomous.

---

## **Surplus Buffer**
A collective reserve pool funded by small fees from minting, repayments, and liquidations.  
It acts as an economic safety net to smooth r-rate fluctuations  
and finance long-term saving yields.

---

## **Immutable Core**
The unchangeable core code of ProjectUSD.  
It contains all critical functions (vaults, liquidations, controller, oracle, redemption).  
After the **Freeze Event**, this core can no longer be modified –  
turning ProjectUSD into an autonomous, incorruptible system.

---

## **Freeze Event**
The moment when the core code is permanently frozen.  
After this point, ProjectUSD becomes fully decentralized and self-sustaining,  
independent from governance or developers.

---

## **Controller**
The economic control center of ProjectUSD.  
It measures the price deviation between market price (P) and equilibrium price (R),  
and adjusts the system rate (r) accordingly.  
This keeps the entire system dynamically balanced and self-regulating.

---
