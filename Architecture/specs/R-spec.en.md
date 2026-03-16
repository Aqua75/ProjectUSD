---
title: "ProjectUSD – R SPEC v2"
status: "Draft"
last_updated: "2026-03-16"
language: "en"
---

# ProjectUSD – R Specification

## 1. Purpose

`R` defines the internal protocol reference price of ProjectUSD.

It is **not a market price** and not derived from external price feeds.  
Instead, `R` is a protocol defined reference value used internally by the system.

`R` serves three fundamental roles:

1. **Controller reference value**  
   The Controller compares the market price `P` to `R` in order to determine the direction and magnitude of system rate adjustments `r`.

2. **Redemption reference price**  
   The Redemption mechanism uses `R` as the internal conversion reference when ProjectUSD is exchanged for PLS collateral from existing Vaults inside the protocol.

3. **Vault reference value**  
   During the creation of ProjectUSD from Vault collateral, `R` acts as the internal valuation reference used to determine the relationship between deposited PLS and the resulting ProjectUSD debt.  
   The exact logic for collateral ratio and maximum debt is defined in the VaultEngine specification.

`R` therefore acts as the **internal equilibrium anchor** of the ProjectUSD system.

---

## 2. Formal Definition

| Property | Definition |
|--------|-------------|
| Variable | `R` |
| Type | internal protocol reference price |
| Unit | `PLS per ProjectUSD Coin` |
| Domain | `R > 0` |
| Accessibility | readable by Controller, Redemption logic, and telemetry systems |

Normative definition:

`R` is the protocol defined internal reference price of ProjectUSD expressed in **PLS per ProjectUSD Coin**.

This value represents the internal system price used for protocol calculations and redemption operations.

---

## 3. Unit Convention

The canonical unit for `R` is:

PLS per ProjectUSD Coin

This unit must be used consistently across all protocol components.

Example interpretation:

R = 0.002 PLS per ProjectUSD

This means:

1 ProjectUSD Coin = 0.002 PLS

All Controller calculations must use the same unit convention for `P`.

---

## 4. Controller Interaction

The Controller measures the deviation between market price `P` and internal reference price `R`.

Deviation signal:

ε = (P - R) / R

Interpretation:

| Condition | Meaning |
|----------|--------|
| P > R | ProjectUSD trades above internal reference value |
| P < R | ProjectUSD trades below internal reference value |
| P ≈ R | system is near equilibrium |

Controller reaction:

if P > R → system rate `r` increases  
if P < R → system rate `r` decreases

The Controller **does not modify `R`**.  
It reacts only to deviations between `P` and `R`.

---

## 5. Redemption Interaction

The Redemption mechanism allows ProjectUSD to be exchanged for collateral using the internal reference price `R`.

Normative redemption conversion:

PLS_out = ProjectUSD_redeemed × R

Example:

R = 0.002 PLS per ProjectUSD  
Redeem = 100 ProjectUSD

Output:

PLS_out = 100 × 0.002 = 0.2 PLS

Redemption therefore establishes the **internal system value** of ProjectUSD independent of external fiat pricing.

The selection of Vaults from which collateral is drawn during Redemption is **not defined in this specification**.

The detailed Redemption procedure is defined in the **Liquidation-Redemption specification**.

---

## 6. System Invariants

The following invariants must always hold.

| ID | Invariant |
|----|-----------|
| R1 | R > 0 |
| R2 | P and R must share the same unit convention when used in controller calculations |
| R3 | R must be defined by deterministic on chain protocol logic |
| R4 | R must not depend on fiat references or off chain price feeds |
| R5 | governance must not manually set or override R |
| R6 | the same current R value must be used consistently across Controller, Redemption, and telemetry |
| R7 | R must not be modified by the Controller |

---

## 7. Storage and Precision

Implementations must define the numeric precision of `R`.

Recommended standard:

fixed point representation with **18 decimals**

Example representation:

R = 0.002 PLS per ProjectUSD  
stored as 0.002 × 10¹⁸

The same precision must be used consistently across:

Controller  
Redemption  
Vault calculations

---

## 8. Initialization

The protocol deployment must define an initial value:

R₀

R₀ is stored in the Immutable Core and serves as the initial Redemption reference price of the system.

Requirements:

R₀ > 0  
consistent with the unit definition  
identical across all modules at deployment

---

## 9. Transparency Requirement

`R` must be externally observable.

Implementations must expose `R` for:

indexing  
monitoring  
audits  
economic analysis

`R` is treated as a **first class system variable** within ProjectUSD telemetry.

---

## 10. Verification

The following verification checks must pass for any implementation.

| Test | Description |
|-----|-------------|
| R-01 | R > 0 holds for all reachable states |
| R-02 | Controller uses the same unit for P and R |
| R-03 | Redemption uses the canonical R representation |
| R-04 | Governance cannot override R |
| R-05 | R is externally readable |

A production implementation must satisfy all invariants and verification tests defined in this specification.
