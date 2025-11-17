---
title: "ProjectUSD – Liquidation & Redemption SPEC v1"
status: "Draft"
last_updated: "2025-11-18"
author: "Aqua75"
language: "en"
related_whitepaper_sections: ["Ch. 6 – Liquidation & Redemption", "Ch. 9 – Security", "Glossary pp. 18–22"]
---

# ProjectUSD – Liquidation & Redemption SPEC v1

## Purpose

This SPEC defines the complete logic for:

1. **Liquidation** (forced closure of an undercollateralized vault)  
2. **Redemption** (exchange of ProjectUSD Coin for collateral at the system price)

Both mechanisms are essential security components of ProjectUSD  
and ensure long-term stability without any central control.

---

# 1. Liquidation (forced closure)

## 1.1 Principle

A vault is liquidated when:

CR < LiquidationCR

Where:

CR = (collateral * OraclePrice) / debt

Goal of liquidation:

- prevent undercollateralized system debt  
- guarantee that every ProjectUSD Coin is fully backed  
- maintain stability through algorithmic rules  
- enforce safety without governance

---

## 1.2 Trigger Condition

Liquidation is triggered when:

```solidity
CR < LiquidationCR
```

The price comes exclusively from the Oracle Medianizer
(not from any DEX price).

---

## 1.3 Liquidation Flow (atomic)

Liquidation happens as a single atomic operation:

Oracle provides latest price

Vault is detected as undercollateralized

StabilityPool absorbs the vault debt

collateral (PLS) is distributed pro-rata

vault is reset to collateral = 0 / debt = 0

event emitted (Liquidation(...))

No intermediate state is externally visible.

---

## 1.4 Interaction with StabilityPool

The StabilityPool performs:

absorbing system debt

distributing collateral to depositors

Algorithm (simplified):

```solidity
absorbDebt(vaultID, debtAmount);
distributeCollateral(proRata);
resetVault(vaultID);
```

No external contracts are called.

---

## 1.5 Security & MEV Protection

Liquidation is protected by:

no external calls

atomic execution

no slippage

no DEX price exposure

no flash-loan dependency

Medianizer prevents spoofed price feeds

liquidation and LP operations cannot happen in the same block

---

## 1.6 Liquidation Reward

ProjectUSD charges no liquidation fee.

Liquidators earn:

the PLS received from the StabilityPool during liquidation

---

## 1.7 Liquidation Invariants

| ID | Invariant                                | Meaning                            |
| -- | ---------------------------------------- | ---------------------------------- |
| L1 | liquidation never creates BadDebt        | system always remains fully backed |
| L2 | liquidation is atomic                    | no partial states                  |
| L3 | only triggered when `CR < LiquidationCR` | no false liquidations              |
| L4 | StabilityPool never goes negative        | pool safety guaranteed             |
| L5 | Oracle controls all liquidation prices   | DEX manipulation impossible        |

---

## 1.8 Telemetry & Monitoring

number of active vaults

liquidation events

absorbed system debt

distributed collateral

average CR of all vaults

oracle deviation indicators

---

## 1.9 Tests (Liquidation)

UnitTests

liquidation when CR < LiquidationCR

no liquidation when CR >= LiquidationCR

StabilityPool debt absorption

CR calculation correctness

atomic execution guaranteed

Property-Based Tests

price-chaos simulations

liquidation storms

oracle outlier scenarios

Static Analysis

no reentrancy possible

no external calls

no unbounded loops

---

## 2. Redemption (system-price collateral exchange)

### 2.1 Principle

Redemption allows users to exchange ProjectUSD Coin
for PLS at the system equilibrium price R, not at market price.

This creates an absolute price floor and maintains peg stability.

1 ProjectUSD → (1 / R) PLS

Where R is defined in Controller-SPEC.

---

### 2.2 Why Redemption is Necessary

creates a guaranteed minimum value

prevents long-term underpricing

removes PLS/ProjectUSD arbitrage zones

keeps market price near R

enables automatic price correction

gives long-term protection to holders

---

### 2.3 Redemption Flow

user sends ProjectUSD Coin to the VaultEngine

system selects the most overcollateralized vault

that vault’s collateral is reduced

that vault’s debt is reduced

user receives PLS at system rate

Redemption is not:

a liquidation

an emergency tool

a governance-controlled price mechanism

It is a pure algorithmic stabilizer.

---

### 2.4 Vault Selection (highest CR first)

Vaults are processed in this order:

highest CR first

then the next highest

etc.

This ensures:

fairness

no individual user is drained disproportionately

natural smoothing of overall collateral structure

---

### 2.5 Security & MEV Protection

no external calls

no DEX exposure

only Oracle price + R determine redemption

optional per-block RedeemLimit

no flash-loan arbitrage possible

atomic execution

---

### 2.6 Redemption Invariants

| ID | Invariant                                  | Meaning                          |
| -- | ------------------------------------------ | -------------------------------- |
| R1 | redemption never creates BadDebt           | full collateralization preserved |
| R2 | vault collateral never becomes negative    | safety for all users             |
| R3 | only overcollateralized vaults are reduced | fairness                         |
| R4 | system value is preserved                  | consistency                      |
| R5 | no DEX price used                          | anti-manipulation                |

---

### 2.7 Telemetry & Monitoring

total redemption volume

number of affected vaults

average CR change

collateral outflow

oracle price movement

equilibrium price R

---

### 2.8 Tests (Redemption)
UnitTests

redemption selects only overcollateralized vaults

CR-ordering correct

atomic execution

correct price computation

Property-Based Tests

extreme price movement

multiple redemption chains

stress redemption

Static Analysis

no external calls

no manipulable loops

---

## 3. Interaction with Other SPECS

VaultEngine-SPEC:
– liquidation and redemption modify vaults atomically

StabilityPool-SPEC:
– absorbs debt during liquidation

Oracle-SPEC:
– provides all CR and redemption prices

Controller-SPEC:
– defines the equilibrium price R

Security-SPEC:
– ensures atomic, manipulation-free execution

Freeze-SPEC:
– liquidation & redemption remain immutable after freeze

---

## 4. License & References

© 2025 Aqua75 / ProjectUSD
License: MIT for code, CC BY-NC-SA 4.0 for documentation
Reference: ProjectUSD Whitepaper V2.1 (Ch. 6, 9, Glossary pp. 18–22)
