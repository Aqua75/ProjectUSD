## Chapter 4 - The Architecture: Building an Incorruptible System

A system can only be as strong as its architecture.

In ProjectUSD, every component has been designed to be incorruptible - immune to manipulation by people, external data, or governance majorities.

Everything that keeps the system alive exists on-chain, fully verifiable, and without any privileged access.

### 4.1 Vaults - The Foundation of Money Creation

Vaults are personal smart-contract vaults where users deposit native PulseChain assets - primarily PLS - as collateral.

Based on these deposits, they can mint new ProjectUSD tokens.

The maximum mintable amount depends on the required Collateral Ratio (CR) - typically 170% or higher.

If the collateral value falls below the minimum threshold, the vault is automatically liquidated.

No person, team, or authority can halt or alter this process - every action follows the same immutable rule.

Vaults are thus the birthplaces of money within the system.

Anyone can open one, anyone can close one, and every action is dictated purely by code.

### 4.2 The Stability Pool - Security Through Collective Behavior

The Stability Pool acts as ProjectUSD’s collective safety net.

Users can voluntarily deposit ProjectUSD tokens here to earn interest and liquidation bonuses.

When a vault falls below its required collateralization level, its debt is automatically repaid using funds from the Stability Pool.

In return, the pool participants receive the vault’s PLS collateral - plus a small bonus - while the excess ProjectUSD supply is burned.

The result:

• Weak positions disappear,

• Strong hands gain additional collateral,

• And the entire system becomes more stable.

This creates a self-healing cycle that absorbs market stress instead of amplifying it.

### 4.3 The Redemption Engine - The Inner Price Anchor

The most important stability mechanism is the Redemption Engine.

It allows any user to redeem ProjectUSD for PLS at the current equilibrium price R.

Redemptions always target the least-collateralized vaults first - those closest to liquidation.

This principle establishes a natural market order:

overextended debt positions are automatically reduced,

arbitrageurs smooth out price deviations,

and confidence in redeemability permanently anchors the price to R.

No external oracle feed, no manual intervention, no black box - only open, deterministic logic.

### 4.4 The Core - Immutable by Design

At the center of ProjectUSD lies the Immutable Core - the system’s unchangeable heart.

It contains all essential functions:

• Vault logic and liquidation mechanisms

• Redemption Engine

• Controller and r-rate management

• Internal parameters such as Collateral Ratio and Liquidation Threshold

• Median Oracle aggregation for price stability

After the so-called Freeze Event, this core becomes permanently locked.

From that moment on, no one - not developers, not the DAO, not the community - can modify or stop it.

ProjectUSD becomes a truly autonomous organism: once launched, it lives indefinitely.

### 4.5 The Periphery - Controlled Flexibility

To enable innovation, ProjectUSD includes a periphery layer.

Here, modules can be added or replaced without endangering the system’s core.

Examples include:

• New collateral adapters

• Peg Stability Modules (PSM) for optional on-chain swaps

• Algorithmic Market Operations (AMO) for liquidity management

• Telemetry and analytics interfaces

All changes occur via timelocks and on-chain voting, publicly visible and time-delayed.

This keeps governance open but never dangerous.

### 4.6 A System Without a Plug

There is no admin key, no “pause button,” no emergency access.

ProjectUSD cannot be frozen or deleted.

The system is not just decentralized - it is autonomous.

Once deployed, it belongs to no one - and therefore to everyone.

This incorruptibility is not a byproduct but the goal itself:

a monetary system that requires no control,

because it is already perfectly balanced at its core.
