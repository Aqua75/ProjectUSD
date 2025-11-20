# ProjectUSD Glossary  
### Definitions of all key concepts and terms

This glossary provides precise definitions for all terminology used in the  
ProjectUSD architecture, SPECS, and whitepaper.

---

## 🧩 Core Concepts

**ProjectUSD**  
A fully autonomous monetary system for PulseChain based on algorithmic equilibrium.

**Equilibrium Price (R)**  
Internal reference value that governs redemption and system stability.

**r-Epoch**  
Periodic system update where the controller adjusts global parameters.

**Freeze Event**  
One-time process that makes the core immutable permanently.

**Immutable Core**  
VaultEngine, Controller, Oracle, Liquidation/Redemption, StabilityPool.

---

## 🏦 Vault & Collateral Terms

**Vault**  
User-owned position holding collateral and debt.

**Collateral Ratio (CR)**  
Collateral value / debt, expressed as a percentage.

**Minimum Collateral Ratio (MCR)**  
Threshold below which liquidation occurs.

**System Debt**  
Total outstanding ProjectUSD supply in the system.

---

## 🔄 Stability & Liquidation

**Stability Pool**  
Collective buffer absorbing undercollateralized vaults.

**Liquidation**  
Forced settlement when a vault falls below MCR.

**Redemption**  
Exchange of ProjectUSD for underlying PLS at equilibrium price R.

---

## 🔒 Security & Invariants

**Atomicity**  
Every state change must complete fully or revert.

**Invariants**  
Economic and logical rules that must always remain true.

**Deviation Limit**  
Maximum allowed difference between oracle sources.

---

## 📈 Analytics & Monitoring

**Subgraph KPIs**  
Metrics used for vault health, system stability, oracle behavior, and incidents.

**Incident Runbook**  
Procedure for diagnosing unexpected events in independent implementations.

---

## 👥 Community / Development Terms

**Self-Starter**  
A contributor who acts independently without coordination.

**Part-Time Steward**  
A community member offering recurring support (non-technical).

**Specification (SPEC)**  
Technical blueprint defining required system behavior.

