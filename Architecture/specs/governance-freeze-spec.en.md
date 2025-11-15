---
title: "ProjectUSD – Governance & Freeze SPEC v1"
status: "Draft"
last_updated: "2025-11-16"
author: "Aqua75"
language: "en"
related_whitepaper_sections: ["Ch. 8 – Governance & Freeze", "Glossary pp. 24–26"]
---

# ProjectUSD – Governance & Freeze SPEC v1

## Purpose

This SPEC defines the governance model of ProjectUSD **before** the freeze  
and the system logic **after** the freeze activation.

The freeze is:

- **absolutely irreversible**,  
- **permanent**,  
- **without backdoors**,  
- **without emergency keys**,  
- **without upgrade mechanisms**.

After freeze activation, ProjectUSD becomes a fully autonomous,  
immutable protocol — comparable to a mathematically defined,  
algorithmically fixed asset.

Governance exists only until the **one-time governance freeze event**.

---

## 1. Principles of ProjectUSD Governance (before freeze)

### 1.1 Minimal Governance

Governance exists only to:

- define parameters before the freeze,  
- activate or deactivate system modules,  
- complete risk and security assessments,  
- prepare the freeze.

It **must not**:

- set prices,  
- perform market interventions,  
- influence algorithmic logic,  
- manipulate the Controller or Oracle.

### 1.2 Governance rights are temporary

Governance is a **temporary helper module**.

Once the freeze is activated:

- all governance rights end,  
- all governance functions are disabled,  
- all parameters become write-protected.

### 1.3 No delegation model

There are:

- no voting rights,  
- no token-based governance,  
- no governance tokens.

Governance is a purely technical setup module.

---

## 2. Governance Permissions (before freeze)

| Area                 | Permission | Description |
|----------------------|------------|-------------|
| Parameter setup      | allowed    | adjust system parameters until freeze |
| Module activation    | allowed    | enable/disable individual components |
| DEX-LP management    | allowed    | only before freeze |
| Security parameters  | allowed    | rate limits, slippage limits |
| Freeze activation    | allowed    | one-time trigger |

**Not allowed:**

- controlling prices  
- controlling liquidations  
- influencing Controller or Oracle  
- altering VaultEngine logic  
- any change after freeze

---

## 3. Freeze Mechanism (core architecture)

### 3.1 Type: Fully irreversible freeze (Variant 1)

The freeze is:

- **not reversible**,  
- **not negotiable**,  
- **not overridable**,  
- **not breakable by emergency keys**,  
- **not reversible by MultiSig**.

There is **no mechanism** to break or undo the freeze.

### 3.2 Activation by Governance

Governance calls:

- `activateFreeze()`  

This causes:

- sets global flag `isFrozen = true`  
- fully disables all governance modules  
- permanently disables all setter functions in all core modules  
- removes all admin roles  
- removes all external control paths

### 3.3 Effects on the system

After `isFrozen = true`:

- system parameters become absolutely write-protected  
- contracts become permanently immutable  
- the DEX-LP system is disabled  
- governance functionality no longer exists  
- all security control paths operate automatically  
- every mutating admin function remains permanently disabled

---

## 4. Governance Functions (before freeze)

### 4.1 Parameter setup

- `setMCR()`  
- `setLiquidationCR()`  
- `setDebtFloor()`  
- `setSystemDebtCap()`  
- `setRateLimits()`  
- `setMaxLPExposure()`  
- `setMaxSlippage()`  

These functions exist only **before** the freeze and are permanently disabled after activation.

### 4.2 Module control

- `enableLP()` / `disableLP()`  
- enable/disable individual pools  
- enable/disable analytical modules  
- release or block experimental features (only before freeze)

### 4.3 Security & risk controls

- setting security boundaries  
- updating MEV protection parameters  
- configuring caps & rate limits  

These parameters define **only safety limits**, not economics or pricing logic.

---

## 5. Technical Architecture of the Freeze

### 5.1 Global variable

```solidity
bool public isFrozen;
```

### 5.2 Freeze trigger

```solidity
function activateFreeze() external onlyGovernance {
    require(!isFrozen, "ALREADY_FROZEN");
    isFrozen = true;
    _disableGovernance();
    _lockAllParameters();
    _disableAdminFunctions();
}
```

### 5.3 Parameter lockdown

```solidity
function _lockAllParameters() internal {
    // permanently disable all setters
}
```

### 5.4 Governance deactivation

```solidity
function _disableGovernance() internal {
    // remove all roles
    // delete governance privileges
}
```

### 5.5 Admin function deactivation

```solidity
function _disableAdminFunctions() internal {
    // disable all admin paths
    // no upgrades, no parameter modifications
}
```

After the freeze, no contract code exists that
allows mutations or upgrades.

---

## 6. Invariants

| ID | Invariant                                  | Meaning                       |
| -- | ------------------------------------------ | ----------------------------- |
| G1 | `isFrozen` is always TRUE after activation | freeze is irreversible        |
| G2 | all governance functions are disabled      | no changes possible           |
| G3 | all parameter setters are disabled         | system remains fixed          |
| G4 | no admin roles exist                       | no central control            |
| G5 | controller/oracle remain algorithmic       | governance cannot change them |

---

## 7. Telemetry & Monitoring

After the freeze:

- monitoring is read-only  
- no parameter is modifiable  
- only on-chain metrics are shown  

**Telemetry includes:**

- `isFrozenFlag`  
- system debt  
- collateral distribution  
- liquidation data  
- vault status  
- surplus data  

---

## 8. Open Design Parameters (only before freeze)

| Parameter       | Status | Description              |
| --------------- | ------ | ------------------------ |
| `MCR`           | open   | minimum collateral ratio |
| `LiquidationCR` | open   | liquidation threshold    |
| `DebtFloor`     | open   | minimum debt             |
| `maxLPExposure` | open   | system LP exposure limit |
| `maxSlippage`   | open   | LP slippage limit        |
| `RateLimits`    | open   | anti-MEV thresholds      |

All parameters become final after the freeze.

---

## 9. Verification (Testing & Validation Guide)

**Goal:**  
Verify that:

- the freeze is activated safely,  
- no parameter changes are possible afterwards,  
- all mutation paths are disabled,  
- no governance or admin role exists.  

**Methods:**

- **UnitTests:**  
  – activation of `activateFreeze()`  
  – verify all setters revert  
  – verify governance is removed  

- **Static analysis:**  
  – verify no upgrade path exists  
  – verify no unprotected mutation functions exist  

- **Property-based tests:**  
  – random mutation attempts  

**Acceptance Criteria:**

- all invariants G1–G5 hold in 100% of tests,  
- freeze cannot be undone,  
- no function permits state changes after freeze,  
- system behaves strictly deterministically.  

---

## 10. Interaction with Other SPECS

- **VaultEngine-SPEC:**  
  – remains immutable after freeze  

- **Controller-SPEC:**  
  – algorithmic, not governance-driven  

- **Oracle-SPEC:**  
  – governance-independent medianizer  

- **StabilityPool-SPEC:**  
  – no parameters modifiable after freeze  

- **DEX-LP-SPEC:**  
  – system LP is fully disabled  

- **Security-SPEC:**  
  – all limits adjustable only before freeze  

---

## 11. License & References

© 2025 Aqua75 / ProjectUSD  
License: MIT for code, CC BY-NC-SA 4.0 for documentation  
Reference: ProjectUSD Whitepaper V2.1 (Ch. 8, Glossary pp. 24–26)  
