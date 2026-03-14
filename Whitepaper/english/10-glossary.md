# Glossary - Key Terms of ProjectUSD

R - Equilibrium Price (Redemption Price)
The internal reference value around which the market price of ProjectUSD stabilizes.
It serves as the system’s mathematical anchor, determined solely through on-chain mechanisms - not through external oracles or fiat price feeds.

---

r - System Rate (Interest / Saving Rate)
The variable control parameter of the Controller.
r can be positive (interest rate) or negative (saving incentive) and regulates the behavior of borrowers and savers.

- When r rises → minting becomes more expensive → supply decreases.
- When r falls → holding or minting becomes more attractive → demand increases.

In this way, r maintains equilibrium between the market price (P) and the internal price (R).

---

Vault
A personal smart-contract vault where users deposit PulseChain assets (e.g., PLS) as collateral to mint ProjectUSD.
Each vault is unique, fully on-chain, and governed by clear rules for collateralization, liquidation, and repayment.

---

Stability Pool
A collective safety pool where users deposit ProjectUSD to facilitate liquidations and earn rewards.
When a vault becomes undercollateralized, its debt is repaid with funds from the Stability Pool, and its collateral (PLS) is distributed to depositors.
This process automatically stabilizes the entire system.

---

Redemption Engine
The internal price anchor of ProjectUSD.
Any user can redeem ProjectUSD for PLS at the equilibrium price R at any time.
This redeemability creates an arbitrage-based feedback loop - price deviations are automatically corrected by market participants.

---

AMO - Algorithmic Market Operations
Optional algorithmic modules for fine-tuning liquidity.
AMOs operate within narrow price ranges to reduce arbitrage spreads, manage surpluses, or optimize the system’s reserves (Surplus Buffer).
All AMO activities are transparent and budget-constrained.

---

PSM - Peg Stability Module
An optional on-chain basket of other stablecoins (e.g., USDL) designed to smooth short-term market friction.
It is strictly limited (daily caps, haircuts) and never required for ProjectUSD to function.
Even without a PSM, the system remains fully autonomous.

---

Surplus Buffer
A collective reserve pool funded by fees from minting, repayment, and liquidation processes.
It acts as an economic safety net, smoothing fluctuations in the system rate r and financing long-term savings yields.

---

Immutable Core
The unchangeable core code of ProjectUSD.
It contains all critical functions - Vaults, Liquidation, Controller, Oracles, and Redemption - and becomes permanently locked after the Freeze Event.
This makes ProjectUSD a fully autonomous and incorruptible system.

---

Freeze Event
The moment when the core code becomes permanently frozen.
After the Freeze Event, ProjectUSD is fully decentralized, self-sustaining, and independent of governance or developers.

---

Controller
The economic control center of ProjectUSD.
It measures the price deviation between the market price (P) and the equilibrium price (R),
then adjusts the system rate (r) accordingly.
Through this feedback, it dynamically regulates the entire system and maintains stability.
