# The Heart of ProjectUSD - A Simple Explanation of P, R and r

## Introduction

The three variables **P**, **R**, and **r** form the foundation of price stability in ProjectUSD.
Together they ensure that the market price repeatedly moves around a stable internal value.
They are simple to understand but economically deep, and this combination is exactly what makes the system unique.

This article explains the three variables as clearly as possible, without unnecessary mathematical complexity.
Unlike traditional stablecoins, ProjectUSD requires neither:

- an external USD peg
- oracles
- banks
- governance decisions

Stability emerges **purely through internal feedback**.
This feedback is created by the interaction of **P**, **R**, and **r**.

**It is important to understand one key point:**

**ProjectUSD simultaneously has two prices:**
a **market price P** and an **internal equilibrium price R**.

The market price **P** can fluctuate, while **R** serves as a stable reference point.
The role of the system is to repeatedly guide the market price **P** back toward this equilibrium price **R**.

---

## 1. P - the market price

**P** is the actual trading price of ProjectUSD on PulseX.

- It arises purely from supply and demand.
- It can lie above or below the equilibrium price **R**.
- It behaves like the price of any other token: volatile, fast, and dynamic.

**In short:**

**P = what the market is doing right now.**

The system does not judge P.
It only measures the deviation from R, and the controller reacts to that deviation.

---

## 2. R - the internal equilibrium price

**R** is the internal equilibrium price of the system, the reference value around which the market price moves over time.

What matters most is what R **is not**:

- R does not come from a USD oracle.
- R does not come from external prices such as PLS or PLSX.
- R is not set by teams, governance, or humans.
- R is not pegged to the dollar.

Instead, R is a **purely internal, mathematically derived value** that emerges from the structure of the system.

You can think of R as a fixed center point around which the market price moves.

R is the price at which ProjectUSD can always be **redeemed internally for PLS**.
This redeemability creates a natural value anchor and ensures that the market price P cannot deviate from the system value for long.

---

## 3. The price deviation ε

There is almost always a small difference between P and R.

This **relative** deviation is defined as:

**ε = (P − R) / R**

- ε > 0 → P lies relatively above R (overvaluation)
- ε < 0 → P lies relatively below R (undervaluation)

The magnitude of ε determines how strongly the controller adjusts r.

---

## 4. r - the system rate (corrective force)

**r** is the most important variable in the entire system.
It is **not interest**, **not a reward**, **not inflation**, and **not a governance variable**.

r is the **corrective force** that repeatedly pulls P back toward the equilibrium price R.

### When P > R

- r increases
- minting becomes more expensive
- holding becomes less attractive
- arbitrage and supply cool down the price

→ **P moves downward toward R**

### When P < R

- r decreases
- holding becomes more attractive
- arbitrage becomes profitable
- demand increases

→ **P moves upward toward R**

**In short:**

**r is the automatic counterforce that corrects every deviation.**

---

## 5. Why R is not completely fixed - but extremely stable

R is not an absolutely fixed value.
It can change, but:

- only slowly
- never abruptly
- never depending on external markets
- exclusively for internal reasons

The reason is that debt, collateral, and redemptions are dynamic.
For the system to remain in long term equilibrium, R must also be able to adjust gently.

You can think of R as a **slowly moving reference point**, while P represents the fast market price.

---

## 6. How R is actually formed

R emerges from the **internal states of the system**, in particular:

- the redemption logic (Redemption Engine)
- the collateral and debt of all vaults
- liquidation dynamics
- internal system drift
- debt reduction and the surplus buffer structure

This makes R a **book accurate internal fair value** that has nothing to do with external prices.

R is the value at which the system can always issue ProjectUSD, guaranteed by mathematics, not by promises.

---

## 7. How ProjectUSD is created

ProjectUSD can enter circulation in two ways:

**1. Purchase on the DEX**

Users can buy ProjectUSD directly on PulseX.
The price in this case corresponds to the market price **P**.

**2. Minting through vaults**

Users can **deposit PLS into a vault in the ProjectUSD system and mint new ProjectUSD**.

In this process, ProjectUSD is created as a **collateralized debt position**, at the equilibrium price **R**.

The equilibrium price **R** is the fixed system price of ProjectUSD.
At this price ProjectUSD is created during minting, and at this price it can later be redeemed again for **PLS**.

---

## 8. R and internal purchasing power

R does not only stabilize the internal value of ProjectUSD.
It also stabilizes the **purchasing power of the token within the PulseChain economy**.

1 ProjectUSD always represents a **constant unit of economic activity** inside the system.
External price changes play no role in this internal measure.

A detailed analysis of internal purchasing power can be found in the separate article:

[“ProjectUSD - and the Secret of Purchasing Power”](https://github.com/Aqua75/ProjectUSD/blob/main/Articles/projectusd-and-purchasing-power/projectusd-and-purchasing-power.en.md)

---

## 9. Summary

- **P** is volatile and reflects the market.
- **R** is the internal equilibrium price, stable, slow moving, and systemic.
- **r** is the automatic corrective force that repeatedly guides P back toward R.

This is why ProjectUSD works:

- without a peg
- without oracles
- without governance
- without USD
- purely algorithmic
- fully on chain

**ProjectUSD stabilizes itself because r continuously drives P back toward R.**

This creates an autonomous monetary system that enables a stable internal economy on PulseChain.
