---
title: "ProjectUSD – VaultEngine SPEC v1"
status: "Draft"
last_updated: "2025-11-14"
author: "Aqua75"
language: "en"
related_whitepaper_sections: ["Ch. 2 – System Overview", "Ch. 5.1 – Collateral & Vaults", "Ch. 6 – Liquidation & Redemption", "Glossary pp. 18–24"]
---

# ProjectUSD – VaultEngine SPEC v1

## Purpose

The **VaultEngine** is the central accounting system of ProjectUSD.  
It manages:

- all collateralized positions (vaults),  
- the relationship between locked PLS and outstanding ProjectUSD Coins,  
- the interface to Liquidation, Redemption, and Controller.

The VaultEngine itself holds **no external price knowledge** and makes **no** liquidation decisions.  
It only provides consistent, manipulation-resistant state:

- collateral balances per vault  
- debt (in ProjectUSD Coin) per vault  
- system-wide totals and buffers  

Liquidation logic, auctions, and redemptions are defined in  
the `liquidation-redemption-spec` and interact with the VaultEngine  
via well-defined functions.

---

## 1. Core Terms & Parameters

| Term             | Description                                                | Example Value       | Unit                              |
|------------------|------------------------------------------------------------|---------------------|-----------------------------------|
| `VaultID`        | Unique index per vault                                     | 1, 2, 3, ...        | –                                 |
| `owner`          | Address controlling the vault                              | `0xABC…`            | address                           |
| `collateral`     | locked PLS in the vault                                    | 10.0                | PLS                               |
| `debt`           | outstanding debt in ProjectUSD Coin                        | 5.0                 | ProjectUSD Coin                   |
| `MCR`            | minimum collateralization ratio per vault                  | 160 %               | % (value in PLS / debt)           |
| `LiquidationCR`  | threshold at which a vault becomes liquidatable            | 150 %               | %                                 |
| `DebtFloor`      | minimum debt per vault                                     | 100                 | ProjectUSD Coin                   |
| `SystemDebtCap`  | maximum total ProjectUSD Coin debt in the system           | open                | ProjectUSD Coin                   |
| `SurplusBuffer`  | system buffer for fees and surpluses                       | dynamic             | ProjectUSD Coin                   |
| `BadDebt`        | uncollectible debt after liquidation events                | 0                   | ProjectUSD Coin                   |
| `r_epoch`        | per-epoch interest/fee rate provided by the Controller     | 0.0 – 0.05          | 1/epoch                           |

**Legend:**  
“open” marks parameters without a fixed example value.  
These values are design or governance decisions and will be chosen  
through simulation and security analysis.

---

## 2. Roles & Responsibilities

### 2.1 VaultEngine

The VaultEngine guarantees:

- correct accounting of PLS collateral and ProjectUSD Coin debt,  
- enforcement of the minimum collateralization ratio (`MCR`),  
- clean handover to liquidation and redemption modules,  
- deterministic application of the per-epoch rate `r_epoch` provided by the Controller.

### 2.2 External Modules

- **Controller:** provides `r_epoch` and thus influences debt evolution.  
- **Oracle:** provides the price `P` (PLS per ProjectUSD Coin) to the liquidation logic.  
- **Liquidation & Redemption:** perform actions that adjust collateral and debt  
  in the VaultEngine via defined interfaces.  
- **StabilityPool / SurplusBuffer:** receive fees and surpluses and  
  absorb deficits (separate SPEC).

---

## 3. Data Structures

### 3.1 Vault

```solidity
struct Vault {
    address owner;        // owner
    uint256 collateral;   // PLS in wei
    uint256 debt;         // ProjectUSD Coin (internal units)
}
```

### 3.2 Global State

```solidity
mapping (uint256 => Vault) vaults;
uint256 totalCollateral;   // sum of all PLS in vaults
uint256 totalDebt;         // sum of all debt in ProjectUSD Coin
uint256 surplusBuffer;     // system buffer (fees, surpluses)
uint256 badDebt;           // uncollectible residual debt
```

---

## 4. Core Functions (High Level API)

Exact function signatures will be specified in a later Contract SPEC.
Here we only describe behavior and invariants.

### 4.1 Vault Lifecycle

openVault()
– creates a new VaultID with owner = msg.sender,
– initial collateral = 0, debt = 0.

deposit(VaultID id, uint256 amountPLS)
– increases the vault’s collateral,
– increases totalCollateral.

withdraw(VaultID id, uint256 amountPLS)
– decreases the vault’s collateral,
– checks CollateralRatio ≥ MCR afterwards,
– decreases totalCollateral.

### 4.2 Borrowing & Repayment

mint(VaultID id, uint256 amountProjectUSD)
– increases the vault’s debt,
– increases totalDebt,
– checks CollateralRatio ≥ MCR and debt ≥ DebtFloor,
– transfers the newly minted ProjectUSD Coins to the owner.

repay(VaultID id, uint256 amountProjectUSD)
– reduces the vault’s debt (not below 0),
– reduces totalDebt,
– interest portions are settled first, then principal.

### 4.3 Rate Application (Controller Integration)

applyEpochRate(uint256 r_epoch)
– called once per epoch (only by the Controller or an authorized module),
– updates debt of all vaults according to:
debt_next = debt_prev * (1 + r_epoch)
– accumulates the difference debt_next − debt_prev system-wide
in surplusBuffer,
– updates totalDebt.

For efficiency, the implementation may use “global multipliers”
instead of updating each position individually. The invariant, however,
remains the same.

### 4.4 Liquidation & Redemption Hooks

liquidate(VaultID id, LiquidationContext ctx)
– callable only by the liquidation module,
– checks whether CollateralRatio < LiquidationCR,
– adjusts collateral, debt, totalCollateral, totalDebt, surplusBuffer,
and badDebt according to the procedure defined in the
liquidation-redemption-spec.

redeem(uint256 amountProjectUSD, RedemptionContext ctx)
– callable only by the redemption module,
– reduces system-wide totalDebt,
– moves collateral from overcollateralized vaults to the redeemer,
– details see liquidation-redemption-spec.

---

## 5. Collateral Ratio & Liquidation Criteria

### 5.1 Collateral Ratio (CR)

For each vault:

CR = (collateral * P) / debt

collateral in PLS

P in PLS per ProjectUSD Coin

debt in ProjectUSD Coin

### 5.2 Minimum Requirements

Minimum collateralization:
CR ≥ MCR after every user action (mint, withdraw).

Liquidatability:
A vault becomes potentially liquidatable when:
CR ≤ LiquidationCR

The concrete triggering (when, by whom, with which reward)
is defined in the Liquidation SPEC.

---

## 6. Invariants

| ID | Invariant                                | Meaning                                      |
| -- | ---------------------------------------- | -------------------------------------------- |
| V1 | `totalCollateral ≥ Σ vault.collateral`   | No PLS “disappears” in accounting.           |
| V2 | `totalDebt ≥ Σ vault.debt`               | System debt matches the sum of vault debts.  |
| V3 | `CR ≥ MCR` for all active vaults         | All active vaults remain overcollateralized. |
| V4 | `DebtFloor == 0` ⇒ `debt == 0` or ≥ Min  | No dust debts below `DebtFloor`.             |
| V5 | `badDebt` increases only via liquidation | Uncollectible debt cannot emerge “silently”. |
| V6 | `surplusBuffer ≥ 0`                      | Buffer can never become negative.            |

Note:
Σ denotes the sum over all existing vaults.

---

## 7. Telemetry & Metrics

| KPI                | Description                          | Source                |
| ------------------ | ------------------------------------ | --------------------- |
| `SystemCR`         | system-wide collateral ratio         | Subgraph (vaults + P) |
| `AvgVaultCR`       | average CR across all vaults         | subgraph analysis     |
| `DebtDistribution` | distribution of debt by size buckets | analytics / subgraph  |
| `BadDebt`          | amount of uncollectible debt         | VaultEngine events    |
| `SurplusLevel`     | size of the system buffer            | VaultEngine events    |

Recommendation:
- weekly “State of the System” reports analogous to the “State of the Peg” reports from the Controller SPEC.

---

## 8. Open Design Parameters

| Parameter                     | Status                | Next Step                               |
| ----------------------------- | --------------------- | --------------------------------------- |
| `MCR`                         | 150–180 %             | simulation of different market regimes  |
| `LiquidationCR`               | 140–160 %             | alignment with liquidation mechanism    |
| `DebtFloor`                   | open                  | analysis of gas cost vs. fragmentation  |
| `SystemDebtCap`               | open                  | depends on PulseChain liquidity         |
| `r_epoch` granularity         | defined in Controller | shared simulation basis with Controller |
| `FeeSplit` (surplus vs. pool) | open                  | definition in StabilityPool SPEC        |

All parameters are explicitly to be understood as “design in progress”
until simulations and backtests are available.

---

## 9. Verification (Testing & Validation Guide)

Goal:
Demonstrate that the VaultEngine:

fulfills all invariants in Section 6,

cooperates correctly with the Controller,

remains consistent under stress (price crashes, mass liquidations).

Methods:

UnitTests (Foundry)
– creation, funding, and closing of vaults
– tests for mint, repay, deposit, withdraw
– targeted attempts to violate invariants (must revert)

Property-based tests
– random sequences of user actions over many epochs
– ensure totalCollateral and totalDebt remain consistent

SimKit scenarios
– coupled with Controller and Oracle simulations
– price crashes, overload, long sideways phases
– evaluation of SystemCR, BadDebt, SurplusBuffer

Acceptance Criteria:

no invariant from Section 6 is violated in tests,

under extreme price shocks, BadDebt stays within predefined risk bounds,

application of r_epoch leads to traceable, reproducible debt paths.

---

## 10. Interaction with Other SPECS

Controller SPEC: defines how r_epoch is computed.
The VaultEngine only applies this value deterministically.

Oracle SPEC: provides P for CR calculations and liquidation triggers
(via the liquidation module, not directly inside the VaultEngine).

Liquidation-Redemption SPEC: describes in detail how
liquidate() and redeem() interact with the VaultEngine.

StabilityPool SPEC: defines how fees and surpluses from
surplusBuffer are routed into pools or used for system stabilization.

Security SPEC: lists all protection mechanisms (reentrancy, caps, rate limits)
and refers to the concrete checks implemented in the VaultEngine.

---

## 11. License & References

© 2025 Aqua75 / ProjectUSD
License: MIT for code, CC BY-NC-SA 4.0 for documentation
Reference: ProjectUSD Whitepaper V2.1 (Ch. 2, 5.1, 6, Glossary pp. 18–24)
