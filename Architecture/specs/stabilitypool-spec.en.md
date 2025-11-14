---
title: "ProjectUSD – StabilityPool SPEC v1"
status: "Draft"
last_updated: "2025-11-15"
author: "Aqua75"
language: "en"
related_whitepaper_sections: ["Ch. 6 – Liquidation & Redemption", "Ch. 7 – Stability Layer", "Glossary pp. 22–24"]
---

# ProjectUSD – StabilityPool SPEC v1

## Purpose

The **StabilityPool** is a central safety mechanism in the ProjectUSD system.  
It serves to:

- absorb system-wide debt (ProjectUSD Coin) during liquidations,  
- receive PLS collateral from liquidated vaults,  
- accept surpluses and fees from the VaultEngine,  
- prevent or strictly limit BadDebt.

The StabilityPool enables an **instant, loss-minimizing liquidation model**,  
that works without auctions or external bidders and is therefore:

- fast,  
- manipulation-resistant,  
- gas-efficient.

---

## 1. Core Concept

The StabilityPool follows one simple principle:

> **Liquidity Providers (LPs) deposit ProjectUSD Coins into the pool.  
> When a vault is liquidated, the pool absorbs its debt –  
> and receives that vault’s collateral in return.**

This allows the system to:

- liquidate instantly without complex auction mechanics,  
- avoid BadDebt (debt is covered by available deposits),  
- grant LPs a gain in PLS (collateral bought below market value).

This ensures high stability even in severe market downturns.

---

## 2. Roles & Actors

| Role                  | Description |
|-----------------------|-------------|
| **Depositor (LP)**    | Deposits ProjectUSD into the pool & receives PLS from liquidations |
| **StabilityPool**     | Aggregates liquidity for debt absorption |
| **VaultEngine**       | Provides collateral and debt values, increases `surplusBuffer` |
| **Liquidation Module**| Executes liquidations and calls pool functions |
| **Controller**        | Indirectly involved through `r_epoch` and system debt dynamics |

---

## 3. Data Structures

### 3.1 StabilityPool

```solidity
struct StabilityPool {
    uint256 totalDeposits;      // total ProjectUSD deposits
    uint256 totalPLSClaimable;  // total PLS owed to LPs (not yet withdrawn)
}
```

### 3.2 Individual Depositors

```solidity
mapping (address => uint256) deposits;      // ProjectUSD Coin
mapping (address => uint256) PLS_credits;   // allocated PLS from liquidations
```
---

## 4. Core Functions (High Level API)

### 4.1 Deposit & Withdrawal

deposit(uint256 amountProjectUSD)
– increases deposits[msg.sender],
– increases totalDeposits.

withdraw(uint256 amountProjectUSD)
– decreases the deposit (if sufficient),
– decreases totalDeposits,
– LP additionally receives accumulated PLS_credits.

### 4.2 Liquidation Integration

When liquidation(VaultID) is triggered in the VaultEngine:

The liquidation module calls:
absorbDebt(VaultID id, uint256 debt, uint256 collateralPLS)

The StabilityPool absorbs the debt:
totalDeposits -= debt

The collateral is fully allocated to LPs:
totalPLSClaimable += collateralPLS

Distribution is proportional to deposit share:

LP_share = deposits[LP] / totalDeposits_before

PLS_credits[LP] += LP_share * collateralPLS

### 4.3 Surpluses from VaultEngine

When the VaultEngine collects system fees:

surplusBuffer grows

these fees may be directed to the StabilityPool
(the exact mechanism is defined in StabilityPool v2)

---

## 5. Liquidation Logic (Interaction with VaultEngine)

A vault becomes liquidatable when:

CR ≤ LiquidationCR

The liquidation module:

reads debt and collateral from the VaultEngine,

calls absorbDebt() in the StabilityPool,

sets the vault in the VaultEngine to debt = 0, collateral = 0,

updates totalDebt and totalCollateral.

The StabilityPool is never responsible for:

price computation,

liquidation triggers,

penalty definitions.

These are defined in the Liquidation SPEC.

---

## 6. Invariants

| ID | Invariant                                           | Meaning                          |
| -- | --------------------------------------------------- | -------------------------------- |
| S1 | `totalDeposits ≥ 0`                                 | pool can never go negative       |
| S2 | `deposits[LP] ≥ 0`                                  | no negative LP balances          |
| S3 | `totalPLSClaimable ≥ Σ PLS_credits[LP]`             | accounting consistency           |
| S4 | `absorbDebt()` only callable via liquidation module | protection against direct misuse |
| S5 | liquidations never create BadDebt                   | pool absorbs all debt            |

---

## 7. Telemetry & KPIs

| KPI                  | Description                                          |
| -------------------- | ---------------------------------------------------- |
| `PoolCoverageRatio`  | `totalDeposits / totalDebt`                          |
| `LiquidityAvailable` | ProjectUSD in the pool available for debt absorption |
| `PLSRewards`         | PLS credited but not yet withdrawn                   |
| `LiquidationVolume`  | cumulative absorbed debt                             |
| `AvgRewardPerLP`     | average PLS reward per LP                            |

---

## 8. Open Design Parameters

| Parameter          | Status | Next Step                         |
| ------------------ | ------ | --------------------------------- |
| `MinDeposit`       | open   | gas cost analysis                 |
| `RewardDelay`      | open   | anti-flash-arbitrage logic        |
| `PoolFeeShare`     | open   | in connection with SurplusBuffer  |
| `DistributionMode` | open   | linear vs. per-epoch distribution |

All parameters are explicitly marked as “design in progress”
and will be finalized through simulation and backtesting.

---

## 9. Verification (Testing & Validation Guide)

Goal:
Ensure that:

liquidations work without BadDebt,

LPs receive correct proportional PLS payouts,

the pool’s accounting remains stable and consistent.

Methods:

UnitTests (Foundry):
– deposit & withdrawal,
– multiple simultaneous LPs,
– debt absorption under various scenarios.

Property-based tests:
– random LP movements during long liquidation sequences.

SimKit scenarios:
– severe price crashes → many vaults liquidated,
– long high-volatility stress phases.

Acceptance Criteria:

all invariants (S1–S5) hold in all simulations,

no remaining system debt (BadDebt = 0),

all LPs receive exactly proportional PLS credits.

---

## 10. Interaction with Other SPECS

VaultEngine-SPEC: provides collateral and debt data.

Controller-SPEC: influences system debt evolution via r_epoch.

Oracle-SPEC: indirectly relevant as price basis for liquidation thresholds.

Liquidation-SPEC: defines triggers and liquidation mechanics.

Security-SPEC: validates deposit/withdraw logic, caps & safety checks.

---

## 11. License & References

© 2025 Aqua75 / ProjectUSD
License: MIT for code, CC BY-NC-SA 4.0 for documentation
Reference: ProjectUSD Whitepaper V2.1 (Ch. 6, 7, Glossary pp. 22–24)
