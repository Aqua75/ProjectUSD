[← Chapter 9](09-chapter-9.md) | [Contents](README.md)

---

# Glossary - Key Terms of ProjectUSD

**R - Equilibrium Price (Redemption Price)** <br>
The internal reference value around which the market price of ProjectUSD stabilizes.<br>
It serves as the system’s mathematical anchor, determined solely through on-chain mechanisms - not<br>
through external oracles or fiat price feeds.

---

**r - System Rate (Interest / Saving Rate)** <br>
The variable control parameter of the Controller.<br>
**r** is the system rate and regulates the behavior of borrowers and savers.

- When **r** rises → minting becomes more expensive → supply decreases.
- When **r** falls → holding or minting becomes more attractive → demand increases.

In this way, **r** maintains equilibrium between the market price (**P**) and the internal price (**R**).

---

**Vault** <br>
A personal smart-contract vault where users deposit PulseChain assets (e.g., PLS) as collateral to mint<br>
ProjectUSD.
Each vault is unique, fully on-chain, and governed by clear rules for collateralization, liquidation, and<br>
repayment.

---

**Stability Pool** <br>
A collective safety pool where users deposit ProjectUSD to facilitate liquidations and earn rewards.<br>
When a vault becomes undercollateralized, its debt is repaid with funds from the Stability Pool, and its<br> collateral (PLS) is distributed to depositors.<br>
This process automatically stabilizes the entire system.

---

**Redemption Engine** <br>
The internal price anchor of ProjectUSD.<br>
Any user can redeem ProjectUSD for PLS at the equilibrium price **R** at any time.<br>
This redeemability creates an arbitrage-based feedback loop - price deviations are automatically<br>
corrected by market participants.

---

**AMO - Algorithmic Market Operations** <br>
Optional algorithmic modules for fine-tuning liquidity.<br>
AMOs operate within narrow price ranges to reduce arbitrage spreads, manage surpluses, or optimize<br>
the system’s reserves (Surplus Buffer).<br>
All AMO activities are transparent and budget-constrained.

---

**PSM - Peg Stability Module** <br>
An optional on-chain basket of other stablecoins (e.g., USDL) designed to smooth short-term market<br>
friction.<br>
It is strictly limited (daily caps, haircuts) and never required for ProjectUSD to function.<br>
Even without a PSM, the system remains fully autonomous.

---

**Surplus Buffer** <br>
A collective reserve pool funded by fees from minting, repayment, and liquidation processes.<br>
It acts as an economic safety net, smoothing fluctuations in the system rate r and financing long-term<br>
savings yields.

---

**Immutable Core** <br>
The unchangeable core code of ProjectUSD.<br>
It contains all critical functions - Vaults, Liquidation, Controller, Oracles, and Redemption - and<br>
becomes permanently locked after the Freeze Event.<br>
This makes ProjectUSD a fully autonomous and incorruptible system.

---

**Freeze Event** <br>
The moment when the core code becomes permanently frozen.<br>
After the Freeze Event, ProjectUSD is fully decentralized, self-sustaining, and independent of<br>
governance or developers.

---

**Controller** <br>
The economic control center of ProjectUSD.<br>
It measures the price deviation between the market price (**P**) and the equilibrium price (**R**),<br>
then adjusts the system rate (**r**) accordingly.<br>
Through this feedback, it dynamically regulates the entire system and maintains stability.

---

[← Chapter 9](09-chapter-9.md) | [Contents](README.md)
