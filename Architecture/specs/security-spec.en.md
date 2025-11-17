---
title: "ProjectUSD – Security SPEC v1"
status: "Draft"
last_updated: "2025-11-17"
author: "Aqua75"
language: "en"
related_whitepaper_sections: ["Ch. 9 – Security & Invariants", "Ch. 8 – Freeze", "Glossary pp. 26–28"]
---

# ProjectUSD – Security SPEC v1

## Purpose

This SPEC defines the complete security model of ProjectUSD.  
It is based on **Hard-Security & Minimal Trust**, meaning:

- no upgrades  
- no admin paths  
- no proxy contracts  
- no dynamic parameters after the freeze  
- no backdoors  
- full immutability and predictability  
- protection against MEV, price manipulation, reentrancy, DoS, and front-running  
- maximum verifiability through static invariants  

Security is **not** achieved through governance but through:

- deterministic rules,  
- mathematical invariants,  
- formal control of data flows,  
- strict access restriction,  
- early parameter finalization,  
- the irreversible freeze.

---

## 1. Security Principles

### 1.1 No trust in individuals or committees  
After the freeze, **no governance** and no admin exists.  
All security guarantees are permanently embedded in the code.

### 1.2 No upgrades  
There are:

- **no proxy contracts**,  
- no upgradeable patterns,  
- no `delegatecall`-based modularity.  

The entire codebase remains immutable.

### 1.3 All parameters are fixed before the freeze  
After freeze, all parameters are fully write-protected:

- MCR  
- LiquidationCR  
- DebtFloor  
- SystemDebtCap  
- maxLPExposure  
- maxSlippage  
- rate limits  

### 1.4 Deterministic security only  
There is no live intervention and no rescue mechanism.  
Security is provided exclusively through:

- mathematical invariants,  
- locked parameters,  
- limits,  
- checks,  
- reverts.

### 1.5 Minimal external attack surface  
No entity with privileged control exists.  
All system actions are 100% public, deterministic, and transparent.

---

## 2. Threat Model

ProjectUSD protects against:

- **reentrancy attacks**  
- **MEV sandwiching** (especially for LP/DEX operations)  
- **oracle manipulation**  
- **flash-loan attacks**  
- **DoS on liquidation paths**  
- **liquidation front-running**  
- **DEX pair price manipulation**  
- **economic manipulation patterns** (e.g., forced BadDebt)  
- **state-change overload** (rate limits)

Not required:

- governance capture  
- admin-key compromise  
- emergency override  

(because these do not exist after the freeze).

---

## 3. System-Wide Security Architecture

### 3.1 Global states

```solidity
bool public isFrozen;
uint256 public lastExecutionTimestamp;
```

### 3.2 No admin roles

```solidity
address public constant ADMIN = address(0);
```

### 3.3 Parameter lockdown

```solidity
require(isFrozen == true);
```

All setters are disabled once:

### 3.4 Rate limits (anti-MEV)

```solidity
mapping(address => uint256) lastAction;
uint256 public rateLimitDelay;
```

Rate limits prevent:
- spam
- flash-loan cascades
- MEV batch manipulations
- excessive per-block activity

### 3.5 Deterministic revert paths

```solidity
require(false, "SECURITY_VIOLATION");
```

All revert messages are immutable.

---

## 4. Protection Mechanisms per Module

### 4.1 VaultEngine

- no reentrancy  
- no external calls inside state-changing operations  
- validation of all vault inputs  
- CR check before every action  
- `totalDebt` consistency control  
- no flash-mint mechanics  

### 4.2 StabilityPool

- no direct access from external contracts  
- only the liquidation module may call `absorbDebt()`  
- PLS distribution proportional, never via gas-heavy loops  
- pool balances must never go negative (invariant SP3)  

### 4.3 Liquidation Module

- uses snapshot data, never live-manipulated prices  
- atomic liquidation sequence:  
  – absorb debt  
  – transfer collateral  
  – reset vault  
- no external calls with untrusted data  

### 4.4 Oracle Module

- median mechanism across multiple feeds  
- strong outlier filtering  
- block-delay cap to prevent spoofing  
- never fewer than `N_feeds`  
- protection against DEX-only price manipulation  

### 4.5 Controller

- deterministic computation of `r_epoch`  
- no live parameter changes  
- no governance influence  
- uninterpreted and immutable  
- no external stimulation paths  

### 4.6 DEX-LP System

- activatable only before freeze  
- anti-MEV slippage boundaries  
- optional use of private RPC via off-chain bot  
- no LP operation allowed in the same block as a liquidation  
- hard cap: `maxLPExposure`  

---

## 5. Security Invariants (System-Wide Rules)

| ID | Invariant                                   | Meaning                   |
| -- | ------------------------------------------- | ------------------------- |
| S1 | `isFrozen` never changes after activation   | freeze is irreversible    |
| S2 | no admin role exists                        | no privileged access      |
| S3 | all parameters remain constant after freeze | full determinism          |
| S4 | `totalDebt >= 0` always true                | accounting consistency    |
| S5 | liquidation never creates BadDebt           | systemic safety           |
| S6 | oracle only changes price-related data      | no external control power |
| S7 | no function allows upgrades                 | no proxy paths            |

---

## 6. Telemetry & Monitoring

After the freeze:

- monitoring is read-only  
- all parameters are static  

**Telemetry includes only key values:**

- `isFrozen`  
- `totalDebt`  
- vault metrics  
- liquidation events  
- StabilityPool data  
- fee developments  
- system-risk indicators (calculated, not parameter-driven)  

---

## 7. Open Design Parameters (relevant only before freeze)

| Parameter            | Status | Description                   |
| -------------------- | ------ | ----------------------------- |
| `rateLimitDelay`     | open   | anti-MEV frequency control    |
| `N_feeds`            | open   | oracle redundancy             |
| `maxDeviation`       | open   | price deviation threshold     |
| `slippageProtection` | open   | LP/liquidation slippage guard |
| `blockDelay`         | open   | anti-spoofing buffer          |

All parameters become final and locked after the freeze.

---

## 8. Verification (Testing & Validation Guide)

**Goal:**  
Demonstrate that after the freeze the system:

- is immutable,  
- behaves deterministically,  
- satisfies all invariants,  
- prevents all critical attack vectors.  

**Methods:**

- **UnitTests:**  
  – vault interactions  
  – liquidations  
  – system-debt changes  
  – slippage violation attempts  

- **Property-based tests:**  
  – random state sequences  
  – extreme volatility scenarios  
  – oracle manipulation attempts  

- **Static analysis:**  
  – guarantee of no upgrade path  
  – reentrancy scans  
  – unreachable-branch verification  

**Acceptance Criteria:**

- S1–S7 are never violated  
- no upgrade possible (verifiable in bytecode)  
- reentrancy impossible  
- liquidation always safe  
- controller behaves deterministically  

---

## 9. Interaction with Other SPECS

- **VaultEngine-SPEC:**  
  – invariant-based mint/burn security  

- **Controller-SPEC:**  
  – deterministic rate computation  

- **Oracle-SPEC:**  
  – manipulation-resistant medianizer  

- **StabilityPool-SPEC:**  
  – protects system-debt through immediate liquidations  

- **DEX-LP-SPEC:**  
  – anti-MEV protection and LP caps  

- **Governance-Freeze-SPEC:**  
  – security model is finalized after freeze  

---

## 10. License & References

© 2025 Aqua75 / ProjectUSD  
License: MIT for code, CC BY-NC-SA 4.0 for documentation  
Reference: ProjectUSD Whitepaper V2.1 (Ch. 9, 8, Glossary pp. 26–28)  
