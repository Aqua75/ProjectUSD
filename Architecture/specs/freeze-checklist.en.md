---
title: "ProjectUSD – Freeze Checklist v1"
status: "Draft"
last_updated: "2025-11-18"
author: "Aqua75"
language: "en"
related_whitepaper_sections: ["Ch. 8 – Governance & Freeze", "Ch. 9 – Security", "Glossary pp. 24–28"]
---

# ProjectUSD – Freeze Checklist v1

## Purpose

This checklist defines all technical, organizational, and security-relevant steps  
that must be completed **before activating the irreversible freeze**.

Once `activateFreeze()` is executed, ProjectUSD becomes a fully autonomous,  
immutable system with no governance, no admin rights, and no upgrade paths.

A freeze is final – this list ensures that **every prerequisite** is met before  
taking this step.

---

# 1. Technical Requirements (Core System)

## 1.1 Parameter Finalization

All system parameters must be fully set and documented:

- [ ] `MCR` (Minimum Collateral Ratio)  
- [ ] `LiquidationCR`  
- [ ] `DebtFloor`  
- [ ] `SystemDebtCap`  
- [ ] `maxLPExposure`  
- [ ] `maxSlippage`  
- [ ] `RateLimits`  
- [ ] `blockDelay` (oracle safeguard)  
- [ ] `maxDeviation` (price deviation limit)  
- [ ] `N_feeds` (oracle redundancy)

**Goal:** After the freeze, none of these values can ever be changed again.

---

## 1.2 Module Status

All modules must be in their intended final state:

- [ ] VaultEngine fully active  
- [ ] StabilityPool active  
- [ ] Liquidation module active  
- [ ] Oracle stable, feeds synchronized  
- [ ] DEX-LP system in final intended state:  
  - [ ] enabled OR  
  - [ ] cleanly disabled (recommended)  
- [ ] Controller active (`r_epoch` functional)  
- [ ] no experimental modules enabled  

---

## 1.3 Code Finality

- [ ] No proxy contracts  
- [ ] No upgrade paths (`delegatecall`, UUPS, Transparent Proxy)  
- [ ] No admin setters  
- [ ] No external owner roles  
- [ ] Code matches final audited bytecode  
- [ ] Deployment address documented  
- [ ] Code verified on block explorer  

---

# 2. Security & Invariant Checks

## 2.1 System Invariants (must hold)

- [ ] S1: `isFrozen` = false (pre-freeze)  
- [ ] S2: no admin exists  
- [ ] S3: all parameters stable, no moving values  
- [ ] S4: `totalDebt >= 0`  
- [ ] S5: liquidations never produce BadDebt  
- [ ] S6: oracle does not exceed predefined deviation ranges  
- [ ] S7: upgrades are impossible  

---

## 2.2 Security Modules Verified

- [ ] MEV protection enabled  
- [ ] Slippage protection enabled  
- [ ] Oracle deviation checks active  
- [ ] Anti-sandwich mechanisms active  
- [ ] Rate-limit mechanisms correct  
- [ ] Reentrancy guards active  
- [ ] No external calls in critical paths  
- [ ] Liquidation path fully isolated  

---

## 2.3 Gas & Runtime Behavior

- [ ] Liquidations run within safe gas limits  
- [ ] StabilityPool absorbs debt without failure  
- [ ] VaultEngine operations stable  
- [ ] No loops with unbounded iteration  

---

# 3. Test & Audit Requirements

## 3.1 Unit Tests

- [ ] 100% coverage of all core paths  
- [ ] Tests for:  
  - [ ] vault creation  
  - [ ] mint  
  - [ ] repay  
  - [ ] liquidation  
  - [ ] StabilityPool interactions  
  - [ ] oracle behavior  
  - [ ] controller (`r_epoch` computation)  

---

## 3.2 Property-Based Tests

- [ ] random simulations passed  
- [ ] high-volatility scenarios passed  
- [ ] random walk scenarios passed  
- [ ] liquidation storms passed  

---

## 3.3 Formal Analysis

- [ ] reentrancy analysis passed  
- [ ] static code analysis passed  
- [ ] overflow/underflow checks  
- [ ] dead-code / unreachable-code checks  
- [ ] bytecode verified as upgrade-free  

---

## 3.4 External Security Audits

- [ ] internal audit completed  
- [ ] external audit completed  
- [ ] all findings resolved  
- [ ] final audit report published on GitHub  

---

# 4. Oracle & Price Feed Check

- [ ] minimum number of feeds online  
- [ ] medianizer stable  
- [ ] no deviations exceeding `maxDeviation`  
- [ ] block delay stable  
- [ ] fallback feeds tested  
- [ ] DEX safeguard validated  

---

# 5. DEX / LP State (if enabled)

- [ ] LP exposure within `maxLPExposure`  
- [ ] slippage limits respected  
- [ ] PLS and ProjectUSD balances correct  
- [ ] no LP transaction in same block as liquidation  
- [ ] LP system cleanly disableable  

---

# 6. Documentation & Project State

## 6.1 Whitepaper & Specifications

- [ ] whitepaper final  
- [ ] all SPECS final  
- [ ] architecture diagrams final  
- [ ] Freeze SPEC final  
- [ ] Security SPEC final  
- [ ] DEX-LP SPEC final  
- [ ] liquidation/redemption SPECs final  

---

## 6.2 GitHub & Deployment Documentation

- [ ] GitHub structure complete  
- [ ] README final  
- [ ] developer documentation final  
- [ ] freeze checklist linked in repo  
- [ ] RPC and security info documented  
- [ ] version numbers locked  

---

# 7. Organizational Steps (pre-freeze)

- [ ] freeze announcement prepared  
- [ ] community informed about immutability  
- [ ] final technical review session  
- [ ] freeze time selected  
- [ ] monitoring system online  
- [ ] off-chain tools updated  
- [ ] DEX/LP bots disabled (if not needed)  
- [ ] emergency communication plan (informational only)  

---

# 8. Executing the Freeze Transaction

- [ ] verify wallet  
- [ ] verify contract address  
- [ ] document transaction  
- [ ] set safe gas limit  
- [ ] execute `activateFreeze()`  
- [ ] archive transaction hash  
- [ ] confirm `isFrozen = true`  
- [ ] monitoring shows frozen state  

---

# 9. Post-Freeze Verification

- [ ] no governance function available  
- [ ] no setter function executable  
- [ ] no admin function exists  
- [ ] deterministic system behavior  
- [ ] all invariants still satisfied  

---

# 10. License & References

© 2025 Aqua75 / ProjectUSD  
License: MIT for code, CC BY-NC-SA 4.0 for documentation  
Reference: ProjectUSD Whitepaper V2.1 (Ch. 8–9, Glossary pp. 24–28)  
