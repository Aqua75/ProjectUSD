# Frequently Asked Questions – ProjectUSD

---

## **1. What is ProjectUSD?**
ProjectUSD is not another stablecoin or startup — it is a proposal for a *fully autonomous monetary system* built natively on PulseChain.  
It achieves price stability **without oracles, banks, or centralized control**, using mathematical feedback instead of human intervention.  
It is designed to become the economic foundation of a self-sustaining blockchain economy.

---

## **2. How does ProjectUSD maintain stability without oracles?**
At the heart of the system lies the **internal equilibrium price (R)**.  
When the market price (P) on decentralized exchanges deviates from R,  
the **Controller** automatically adjusts a variable rate **r** (the System Rate).  

- When P > R → r increases → minting new ProjectUSD becomes more expensive → supply contracts.  
- When P < R → r decreases → holding or minting becomes more attractive → demand expands.  

This closed feedback loop constantly pulls the price back toward equilibrium —  
entirely on-chain, without any external price feeds.

---

## **3. What is the Controller and what does it do?**
The Controller is the *economic pulse* of the system.  
It continuously measures the deviation between the market price (P) and the internal redemption price (R),  
and adjusts the system rate (r) to restore balance.  
In short: it is an automated monetary policy written in code — transparent, deterministic, and incorruptible.

---

## **4. What are Vaults, and how do they create ProjectUSD?**
Vaults are on-chain smart contracts where users deposit native PulseChain assets (e.g. PLS) as collateral.  
Based on this collateral, new ProjectUSD can be minted, up to a defined collateral ratio (typically 170% or more).  
If the collateral value falls below the minimum threshold, the vault is automatically liquidated —  
no admin keys, no exceptions, no human intervention.

---

## **5. What is the Stability Pool?**
The Stability Pool acts as the collective safety net of the system.  
Users can deposit ProjectUSD into the pool to earn interest and liquidation rewards.  
When a vault becomes undercollateralized, the pool absorbs its debt and receives its PLS collateral.  
This process removes weak positions and strengthens the system — a self-healing mechanism.

---

## **6. What is the Redemption Engine?**
The Redemption Engine maintains the internal equilibrium.  
Any user can redeem ProjectUSD for PLS at the current redemption price **R**.  
This redeemability creates natural arbitrage forces that anchor the market price to R,  
eliminating the need for external peg mechanisms.

---

## **7. What happens during the Freeze Event?**
The **Freeze Event** is the moment when ProjectUSD becomes truly autonomous.  
Once the system has proven stable (Phase 2 of the roadmap),  
all core parameters — such as collateral ratio, liquidation threshold, controller logic, and redemption mechanism — are frozen.  
From that point forward, the **Immutable Core** can no longer be changed by anyone — not developers, not governance, not the community.  
Code becomes permanent law.

---

## **8. What is the Immutable Core vs. the Periphery?**
- The **Immutable Core** contains all critical economic logic — vaults, liquidations, controller, oracle aggregation, and redemption.  
  Once frozen, it cannot be altered.  
- The **Periphery** is a flexible outer layer that allows safe evolution — such as adding new collaterals, AMOs, or analytical modules.  
  Changes to the periphery are transparent, time-locked, and on-chain governed.

---

## **9. What are AMOs and PSMs?**
- **AMO (Algorithmic Market Operations):**  
  Optional modules that provide liquidity and fine-tune the surplus buffer within defined price bands.  
  Every AMO has a fixed budget and must remain auditable.  

- **PSM (Peg Stability Module):**  
  A small, optional on-chain basket of other stablecoins (e.g. USDL) used to smooth short-term volatility.  
  It operates under strict limits and is never required for ProjectUSD to function.

---

## **10. How does ProjectUSD protect against MEV, front-running, and manipulation?**
ProjectUSD includes multiple defense layers:  
- Median-TWAP price feeds from multiple on-chain pairs  
- Automatic exclusion of illiquid or outlier data  
- Rate-limiters restricting how fast r can change  
- Isolation of critical functions to prevent reentrancy or governance capture  

These safeguards make it resilient against both technical and economic attacks.

---

## **11. Is there a governance or admin key?**
No.  
ProjectUSD is designed to operate **without admin keys, pause buttons, or emergency overrides.**  
After deployment and the Freeze Event, no entity — not even its original creators — can alter or stop the system.  
It belongs to everyone, and to no one.

---

## **12. What is the Surplus Buffer?**
A collective on-chain reserve funded by small fees from minting, redemptions, and liquidations.  
It acts as an internal insurance layer that:
- Smooths r-rate volatility,  
- Covers short-term deficits from AMO operations, and  
- Supports long-term saving mechanisms (DSR).

---

## **13. What risks does ProjectUSD face?**
All risks are openly defined and on-chain measurable:
- **Technical risk:** smart-contract bugs before the Freeze Event.  
- **Economic risk:** strong market crashes in collateral assets (e.g. PLS).  
- **Liquidity risk:** reduced arbitrage volume during low market activity.  
- **Governance risk:** potential manipulation in the periphery layer (minimized through timelocks).  
No financial system is risk-free, but ProjectUSD’s risks are transparent and mathematically bounded.

---

## **14. What makes ProjectUSD different from DAI, LUSD, or UST?**

| Feature | DAI / LUSD | UST | ProjectUSD |
|----------|-------------|-----|-------------|
| Oracle dependency | Yes | Yes | **No (on-chain median TWAP)** |
| External USD peg | Yes | Yes | **No (internal equilibrium R)** |
| Fiat exposure | Yes | No | **No** |
| Autonomous adjustment (r-rate) | Partial | No | **Yes – mathematically regulated** |
| Self-stabilizing loop | No | No | **Yes** |
| Governance-free core | Partial | No | **Yes – immutable after Freeze** |

ProjectUSD replaces trust with transparency and control with code.

---

## **15. How can developers and researchers contribute?**
Anyone can contribute by:
- Building and testing code modules (Controller, Vaults, Stability Pool)  
- Running economic simulations of r–R–P feedback dynamics  
- Translating documentation and whitepapers  
- Designing visual or analytic tools for the ecosystem  

Guidance is provided in [`Docs/Developer_Guidelines.md`](./Developer_Guidelines.md).

---

## **16. What is the long-term vision?**
To make PulseChain a **self-contained economy** with its own autonomous currency —  
a form of digital money that proves its stability rather than promises it.

> 🌀 *"When the code cannot lie, humanity no longer needs to."*
