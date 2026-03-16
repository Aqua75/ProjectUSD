# ProjectUSD – SPECS Overview

This README provides a complete orientation for all technical specifications
(SPECS) of ProjectUSD.  
It serves as the entry point for developers, auditors, researchers, and
community members.

## 📚 Purpose of the SPECS

The SPECS define **every component of the protocol** at a professional,
audit-level standard.  
ProjectUSD is a fully autonomous and immutable system after freeze, which makes
a transparent and modular specification set essential.

## 🧩 Module Overview

The SPECS are organized into the following categories:

### Core Modules (immutable after freeze)

- vaultengine-spec.en.md / .de.md  
  Logic for vaults, collateral, debt accounting and CR calculations.

- R-spec.en.md / .de.md  
  Definition of the internal system reference price R used by Controller and Redemption.

- controller-spec.en.md / .de.md  
  Control algorithm for the system rate r based on deviations between market price P and internal reference price R.

- oracle-spec.en.md / .de.md  
  Market price feed P, medianizer logic, redundancy and safety limits.

- liquidation-redemption-spec.en.md / .de.md  
  Liquidation and redemption flows, vault selection rules and safety invariants.

- stabilitypool-spec.en.md / .de.md  
  StabilityPool mechanics, debt absorption and collateral redistribution.

### **Security & Freeze**

- **security-spec.en.md / .de.md**  
  Security model: MEV protection, reentrancy protection, atomicity.

- **governance-freeze-spec.en.md / .de.md**  
  Immutability model, freeze process, removal of governance.

- **freeze-checklist.en.md / .de.md**  
  Step-by-step checklist to prepare the immutable freeze event.

### **Monitoring, Analytics & Incident Handling**

- **kpi-subgraph-spec.en.md / .de.md**  
  KPI and data model for the Subgraph (vault KPIs, system KPIs, oracle KPIs, incident KPIs).

- **incident-runbook.en.md / .de.md**  
  Diagnostic procedures for all major incident types.

### **Periphery (optional and flexible)**

- **dex-lp-spec.en.md / .de.md**  
  Optional DEX-LP integration module.

---

## 🗂️ Recommended Reading Order (for developers)

1. vaultengine-spec  
2. R-spec  
3. controller-spec  
4. oracle-spec  
5. liquidation-redemption-spec  
6. stabilitypool-spec  
7. security-spec  
8. governance-freeze-spec → then freeze-checklist  
9. incident-runbook  
10. kpi-subgraph-spec

This order explains:

- economic foundation (VaultEngine)  
- control system (Controller, Oracle)  
- safety & guarantees (Liquidation, StabilityPool, Security)  
- monitoring & diagnostics (Runbook, Subgraph)

---

## 🔒 Core vs Periphery

### **Core (immutable after freeze)**
- VaultEngine  
- R  
- Controller  
- Oracle  
- Liquidation & Redemption  
- StabilityPool

### **Periphery (governance-controlled after freeze)**
- Analytics (Subgraph)  
- DEX-LP modules  
- Frontend / monitoring tools  

---

## 📘 Whitepaper Reference

All SPECS follow the architecture and principles defined in the  
**ProjectUSD Whitepaper V2.2**  
(System equilibrium, invariants, freeze model).

---

## 🪙 License
CC BY-NC-SA 4.0  
© 2026 Aqua75 / ProjectUSD
