# Study 03 – The Redemption Engine as the Internal Price Anchor of ProjectUSD
*Scientific analysis of the internal value reference, arbitrage dynamics, and the role of redemption in maintaining equilibrium*  
*(Level-3 Research Format)*

---

## Abstract

The redemption engine is the core mechanism that gives ProjectUSD an internal and stable measure of value. While the market price P is determined by supply and demand, the redemption system defines the equilibrium price R and ensures that:

- ProjectUSD always has a clearly defined internal value,  
- arbitrage consistently pushes the system toward R,  
- P cannot drift away from R for long without triggering economic correction forces.

This study explains the mechanics of redemption, its interaction with the oracle, the arbitrage-driven mean reversion of P → R, and its role in stress scenarios. The analysis shows that redemption is not merely a feature — it is the economic foundation that differentiates ProjectUSD from fiat-anchored stablecoins and externally referenced systems.

---

# 1. Introduction – Why Redemption Is the Internal Price Anchor

ProjectUSD has:

- **no fiat peg**,  
- **no external USD oracle**,  
- **no governance body** defining its value.

Instead, the system’s value emerges from:

- the equilibrium price **R**,  
- the redemption engine,  
- arbitrage incentives,  
- the market’s economic response to these incentives.

Redemption answers the key question:

> *“How much PLS corresponds to 1 ProjectUSD within the system itself?”*

Thus, R functions as an internal value reference, independent of external markets.

---

# 2. Technical Foundations of the Redemption Engine

## 2.1 Definition of the Equilibrium Price R

> ## 📘 Definition – Redemption Price \(R\)
> The equilibrium price R represents the internal value at which 1 ProjectUSD can be redeemed for PLS through the system.

R does not depend on fiat, USD price feeds, or governance decisions.

---

## 2.2 Core Principle of Redemption

When a user redeems ProjectUSD:

1. the system targets the **weakest vaults** (lowest CR),  
2. their PLS collateral is transferred to the redeemer,  
3. the vault’s debt is reduced or erased,  
4. the vault becomes safer or is closed,  
5. the ProjectUSD supply decreases.

Important:

- No PLS is sold on the open market.  
- No price impact on DEX liquidity.  
- Redemption operates **entirely inside the protocol**.

---

## 2.3 System-Level Effects

Redemption produces:

- higher collateralization  
- reduction of ProjectUSD supply  
- removal of weak-risk positions  
- internal redistribution of collateral  
- a **stable, deterministic reference value**

---

# 3. Arbitrage Dynamics Between Market Price P and Equilibrium Price R

Redemption creates an economic gradient that arbitrageurs exploit.  
The dynamic is deterministic and self-balancing.

---

## 3.1 Case 1 – P < R (Undervaluation)

If ProjectUSD trades below its internal value:

- arbitrageurs buy PUSD cheaply,  
- redeem it for PLS worth R,  
- realize a profit,  
- supply decreases,  
- P moves upward toward R.

Persistent undervaluation is impossible as long as redemption is available.

---

## 3.2 Case 2 – P > R (Overvaluation)

If PUSD trades above R:

- users mint additional ProjectUSD,  
- sell it for a premium,  
- later repay their vault debt,  
- supply expands temporarily,  
- P moves downward toward R.

Overvaluation is also self-correcting.

---

## 3.3 Result: R Functions as an Attractor

R is:

- the internal value anchor,  
- the reference point for arbitrage,  
- the long-term equilibrium target,  
- independent of external markets.

R is not advisory — it is an *economic attractor*.

---

# 4. Oracle Interaction

## 4.1 Oracle Input Relevant to Redemption

The oracle provides:

- Median-TWAP PLS prices,  
- smoothed values,  
- manipulation resistance,  
- STALE mode during illiquid phases.

While redemption itself does not use the oracle price directly, the oracle determines:

- vault collateral values,  
- CR calculations,  
- selection of vaults during redemption.

---

## 4.2 Oracle Filtering as Manipulation Protection

If a pool becomes illiquid or manipulated:

- oracle filtering excludes it,  
- STALE mode prevents corrupted inputs,  
- redemption logic remains valid,  
- R remains a clean and reliable reference.

Thus, redemption is protected from short-term oracle anomalies.

---

# 5. Mathematical Foundation of Price Reversion

A central question:

> *“How does redemption ensure that P always converges back toward R?”*

---

## 5.1 Relative Deviation εₜ

> ## 📘 Definition – Relative Price Deviation
> $$
> \varepsilon_t = \frac{P_t - R_t}{R_t}
> $$

Positive εₜ indicates overvaluation, negative indicates undervaluation.

---

## 5.2 Arbitrage-Driven Mean Reversion

Redemption creates:

- demand when P < R,  
- supply when P > R,  
- monotonic reversion toward R.

Arbitrage never pushes the price *away* from R.

---

## 5.3 Stability Through Supply Reduction

Every redemption reduces the circulating ProjectUSD supply.

This results in:

- higher collateral per remaining unit,  
- a safer system profile,  
- stronger tendency toward equilibrium.

---

# 6. Redemption in Stress Scenarios

## 6.1 Strong Price Declines

During rapid PLS declines:

- many vaults lose CR,  
- redemption reduces their debt,  
- system collateralization increases,  
- arbitrage remains active,  
- P stabilizes.

---

## 6.2 Oracle Disruptions

If oracle feeds fail:

- redemption proceeds using the last valid values,  
- STALE mode prevents manipulation,  
- collateral is not mispriced,  
- arbitrage resumes once data normalizes.

---

## 6.3 Gas Spikes

Redemption remains functional because:

- logic is simple and deterministic,  
- operations are bounded in complexity,  
- transactions remain predictable even under congestion.

---

# 7. Redemption as a Game-Theoretic Mechanism

Redemption creates a strategic ecosystem:

- arbitrageurs profit whenever P ≠ R,  
- vault users take leverage risk,  
- Stability Pool users benefit from system stress,  
- the protocol becomes stronger after every imbalance.

The equilibrium condition:

> *Arbitrage eliminates long-term deviations of P from R.*

---

# 8. Conclusion

The redemption engine is the monetary foundation of ProjectUSD.  
It provides:

- an internal value measure,  
- arbitrage-driven stability,  
- supply correction,  
- resilience under stress,  
- a deterministic equilibrium,  
- a self-regulating market dynamic.

Without redemption, ProjectUSD would have no internal price anchor.  
With it, ProjectUSD behaves as a fully autonomous on-chain monetary system.

---

# 9. Verification

> ## 📘 Reviewer Checklist
- Is R correctly defined and used?  
- Are arbitrage pathways logically consistent?  
- Is no external fiat reference required at any point?  
- Does the mechanism remain valid during stress conditions?  
- Is the monotonic reversion P → R correctly described?  

This document provides the foundation for further studies on arbitrage, market mechanics, and the interaction between redemption, the controller, and the Stability Pool.
