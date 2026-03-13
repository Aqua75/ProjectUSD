# Chapter 4 - The Architecture: Building an Incorruptible System

A system can only be as strong as its architecture.<br>
In ProjectUSD, every component has been designed to be **incorruptible** - immune to manipulation by<br>
people, external data, or governance majorities.<br>
Everything that keeps the system alive exists **on-chain**, fully verifiable, and without any privileged access.

---

### 4.1 Vaults - The Foundation of Money Creation

Vaults are personal smart-contract vaults where users deposit native PulseChain assets - primarily **PLS** -<br>
as collateral.<br>
Based on these deposits, they can mint new ProjectUSD tokens.

The maximum mintable amount depends on the required **Collateral Ratio** (CR) - typically 170% or higher.<br>
If the collateral value falls below the minimum threshold, the vault is automatically liquidated.<br>
No person, team, or authority can halt or alter this process - every action follows the same immutable rule.

Vaults are thus the **birthplaces** of money within the system.<br>
Anyone can open one, anyone can close one, and every action is dictated purely by code.

---

### 4.2 The Stability Pool - Security Through Collective Behavior

The Stability Pool acts as ProjectUSD’s collective safety net.<br>
Users can voluntarily deposit ProjectUSD tokens here to earn interest and liquidation bonuses.<br>

When a vault falls below its required collateralization level, its debt is automatically repaid using funds<br>
from the Stability Pool.<br>
In return, the pool participants receive the vault’s PLS collateral - plus a small bonus - while the excess<br>
ProjectUSD supply is burned.

The result:

- Weak positions disappear,
- Strong hands gain additional collateral,
- And the entire system becomes more stable.

This creates a self-healing cycle that absorbs market stress instead of amplifying it.

---

### 4.3 The Redemption Engine - The Inner Price Anchor

The most important stability mechanism is the **Redemption Engine**.<br>
It allows any user to redeem ProjectUSD for PLS at the current equilibrium price **R**.<br>
Redemptions always target the least-collateralized vaults first - those closest to liquidation.

This principle establishes a natural market order:<br>
overextended debt positions are automatically reduced,<br>
arbitrageurs smooth out price deviations,<br>
and confidence in redeemability permanently anchors the price to **R**.

No external oracle feed, no manual intervention, no black box - only open, deterministic logic.

---

### 4.4 The Core - Immutable by Design

At the center of ProjectUSD lies the Immutable Core - the system’s unchangeable heart.<br>
It contains all essential functions:

- Vault logic and liquidation mechanisms
- Redemption Engine
- Controller and **r-rate** management
- Internal parameters such as Collateral Ratio and Liquidation Threshold
- Median Oracle aggregation for price stability

After the so-called **Freeze Event**, this core becomes permanently locked.<br>
From that moment on, no one - not developers, not the DAO, not the community - can modify or stop it.<br>
ProjectUSD becomes a truly autonomous organism: once launched, it lives indefinitely.

---

### 4.5 The Periphery - Controlled Flexibility

To enable innovation, ProjectUSD includes a periphery layer.<br>
Here, modules can be added or replaced without endangering the system’s core.

Examples include:

- New collateral adapters
- Peg Stability Modules (PSM) for optional on-chain swaps
- Algorithmic Market Operations (AMO) for liquidity management
- Telemetry and analytics interfaces

All changes occur via **timelocks** and **on-chain voting**, publicly visible and time-delayed.<br>
This keeps governance open but never dangerous.

---

### 4.6 A System Without a Plug

There is no admin key, no “pause button,” no emergency access.<br>
ProjectUSD cannot be frozen or deleted.<br>
The system is not just decentralized - it is **autonomous**.<br>
Once deployed, it belongs to no one - and therefore to everyone.<br>
This incorruptibility is not a byproduct but the goal itself:<br>
a monetary system that requires no control,<br>
because it is already perfectly balanced at its core.
