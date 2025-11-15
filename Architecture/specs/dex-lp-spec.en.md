---
title: "ProjectUSD – DEX-LP SPEC v1"
status: "Draft"
last_updated: "2025-11-15"
author: "Aqua75"
language: "en"
related_whitepaper_sections: ["Ch. 4 – Market Mechanics", "Ch. 7 – Liquidity Layer", "Glossary pp. 20–24"]
---

# ProjectUSD – DEX-LP SPEC v1

## Purpose

The **DEX-LP interface** defines whether and how ProjectUSD interacts  
with decentralized exchanges (DEX) to provide liquidity.

The objective is *not* to turn ProjectUSD into an AMM system, but to:

- ensure price stability through sufficient liquidity,  
- keep the buy/sell spread minimal,  
- prevent liquidity shortages in extreme market situations,  
- optionally allow system-owned LP positions on PulseChain  
  (ProjectUSD/PLS).

The DEX-LP-SPEC becomes active only if governance authorizes  
**system-level LP positions**.  
In the Freeze state, all LP functions are disabled.

---

## 1. DEX Fundamentals in the ProjectUSD Context

ProjectUSD interacts exclusively with:

- **AMM pools on PulseChain** (e.g. PulseX, 1inch routing)  
- Pairs of the form:  
  - ProjectUSD / PLS  
  - ProjectUSD / stable oracle-safe assets (e.g. PLSX)  
  - ProjectUSD / wETH (optional for routing)

There is **no off-chain liquidity** and no CEX integration.

---

## 2. Roles & Actors

| Role            | Description |
|-----------------|-------------|
| **SystemLP**    | Contract module holding LP positions on behalf of the system |
| **Governance**  | Enables/disables LP features, defines LP parameters |
| **DEX Pool**    | AMM pool on PulseChain |
| **LP Provider** | External users adding liquidity (not part of this SPEC) |

---

## 3. Design Goals

### 3.1 Spread Reduction  
High liquidity reduces price deviations.

### 3.2 Target Corridor around R (internal equilibrium price)  
System-LP supplements external LPs to maintain the ProjectUSD/PLS pair  
within a defined price corridor.

### 3.3 Maximum MEV Protection  
According to the Security-SPEC:

- protection against sandwich attacks,  
- no front-running of system LP actions,  
- private RPC endpoints + randomized execution windows.

### 3.4 No Active Trading  
System-LP **must not perform active trades**.  
Its role is strictly passive liquidity provision.

---

## 4. Data Structures

### 4.1 LPStatus

```solidity
struct LPStatus {
    bool enabled;              // whether system-LP is active
    uint256 usdAmount;         // ProjectUSD Coin amount in LP positions
    uint256 plsAmount;         // PLS amount in LP positions
    uint256 lpTokens;          // received LP tokens from the DEX pool
}
```

### 4.2 Global State

```solidity
LPStatus systemLP;
address dexPoolAddress;        // target pool (e.g. ProjectUSD/PLS)
uint256 maxLPExposure;         // maximum allowed LP exposure in ProjectUSD Coin
```

---

## 5. Core Functions

### 5.1 Activation & Parameters

- `enableLP(uint256 maxExposure)`  
  – activates system-LP  
  – sets maximum exposure  

- `disableLP()`  
  – deactivates system-LP  
  – prevents further liquidity additions  
  – withdrawal of existing LP positions remains possible  

### 5.2 Providing Liquidity

- `provideLiquidity(uint256 amountProjectUSD, uint256 amountPLS)`  
  – adds liquidity to the DEX pool  
  – receives DEX-specific LP tokens  
  – updates `systemLP.lpTokens`, `usdAmount`, `plsAmount`  

### 5.3 Removing Liquidity

- `withdrawLiquidity(uint256 lpTokenAmount)`  
  – redeems LP tokens in the DEX  
  – receives PLS & ProjectUSD Coin back  
  – updates the System-LP cache  

### 5.4 Parameter Constraints

- LP may **never** exceed `maxLPExposure`  
- no daily LP changes > defined rate-limit threshold  
- LP functions callable only through Governance or MultiSig  

---

## 6. AMM Interaction

### 6.1 Supported DEX Types

- Constant-Product-AMM (`x*y=k`)  
- Concentrated Liquidity AMM (CLAMM, PulseX v2)  
- Weighted Balancer pools (optional)  

### 6.2 Simulation & Safety Requirements

Each LP action must:

- respect slippage parameters (`maxSlippage`)  
- use private RPC endpoints / relays  
- trigger errors when:  
  - liquidity in the pool is too shallow  
  - pathological AMM states are detected  
  - price deviation exceeds safe bounds (Oracle Deviation Check)  

### 6.3 Internal Benchmark

System checks for every LP action:

`PLS_per_USD_LP ≤ P * (1 + Δ)`

where:

P = oracle price (PLS per ProjectUSD Coin)

Δ = allowed deviation, e.g. 2%

---

## 7. Invariants

| ID | Invariant                                 | Meaning                             |
| -- | ----------------------------------------- | ----------------------------------- |
| L1 | `systemLP.enabled` must be explicitly set | prevents accidental LP activation   |
| L2 | `usdAmount + plsAmount ≤ maxLPExposure`   | prevents system overexposure        |
| L3 | `lpTokens ≥ 0`                            | no negative LP token balances       |
| L4 | LP operations only via Governance         | prevents unauthorized modifications |
| L5 | every LP action triggers slippage checks  | MEV-resilience guarantee            |

---

## 8. Telemetry & KPIs

| KPI               | Description                                    |
| ----------------- | ---------------------------------------------- |
| `LPDepth`         | total liquidity provided by the system         |
| `LPShareSystem`   | system’s share of total DEX liquidity          |
| `ImpermanentLoss` | IL estimate via AMM simulation                 |
| `LPYield`         | yield from PLS/ProjectUSD relative to lpTokens |
| `LPExposure`      | exposure relative to maxLPExposure             |

---

## 9. Open Parameters

| Parameter          | Status | Next Step                 |
| ------------------ | ------ | ------------------------- |
| `maxLPExposure`    | open   | liquidity risk simulation |
| `maxSlippage`      | open   | PulseX optimization       |
| `LPActivationMode` | open   | governance decision       |
| `LPExitMode`       | open   | planned freeze workflow   |

**All parameters are explicitly marked as “design in progress”**,  
until modeling & backtesting are complete.

---

## 10. Verification (Testing & Validation Guide)

**Goal:**  
Demonstrate that system-LP:

- is safely activated/deactivated,  
- cannot operate without authorization,  
- never exceeds exposure limits,  
- keeps LP-token and PLS/ProjectUSD balances accurate.  

**Methods:**

- **UnitTests:**  
  – activation/deactivation  
  – slippage violation attempts  
  – provide/withdraw liquidity  

- **Property-based tests:**  
  – random LP actions under strong volatility  

- **AMM simulation:**  
  – impermanent loss scenarios  
  – price distortion tests  
  – manipulated block sequences  

**Acceptance Criteria:**

- invariants L1–L5 hold in all tests,  
- no LP transaction exceeds exposure limits,  
- LP-position values match DEX pool values exactly.  

---

## 11. Interaction with Other SPECS

- **VaultEngine-SPEC:** may relay collateral/debt to system-LP (optional).  
- **Controller-SPEC:** influences `r_epoch` → system deleveraging may change LP behavior.  
- **Oracle-SPEC:** provides price basis for LP slippage checks.  
- **Security-SPEC:** defines MEV protection & rate limits.  
- **Governance-Freeze-SPEC:** determines when LP must be disabled.  

---

## 12. License & References

© 2025 Aqua75 / ProjectUSD  
License: MIT for code, CC BY-NC-SA 4.0 for documentation  
Reference: ProjectUSD Whitepaper V2.1 (Ch. 7, Glossary pp. 20–24)  
