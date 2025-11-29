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

### **Core Modules (immutable after freeze)**

- **vaultengine-spec.en.md / .de.md**  
  Logic for vaults, collateral, debt, CR calculation, atomic state transitions.

- **controller-spec.en.md / .de.md**  
  Algorithm for the equilibrium price R and r-epoch updates.

- **oracle-spec.en.md / .de.md**  
  Medianizer, redundancy, block-delay, deviation limits.

- **liquidation-redemption-spec.en.md / .de.md**  
  Liquidation, redemption, invariants, safety rules, atomic flows.

- **stabilitypool-spec.en.md / .de.md**  
  StabilityPool mechanics, debt absorption, collateral distribution.

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

1. **vaultengine-spec**  
2. **controller-spec**  
3. **oracle-spec**  
4. **liquidation-redemption-spec**  
5. **stabilitypool-spec**  
6. **security-spec**  
7. **governance-freeze-spec** → then **freeze-checklist**  
8. **incident-runbook**  
9. **kpi-subgraph-spec**

This order explains:

- economic foundation (VaultEngine)  
- control system (Controller, Oracle)  
- safety & guarantees (Liquidation, StabilityPool, Security)  
- monitoring & diagnostics (Runbook, Subgraph)

---

## 🔒 Core vs Periphery

### **Core (immutable after freeze)**
- VaultEngine  
- Liquidation & Redemption  
- Controller  
- Oracle  
- StabilityPool  

### **Periphery (governance-controlled after freeze)**
- Analytics (Subgraph)  
- DEX-LP modules  
- Frontend / monitoring tools  

---

## 📘 Whitepaper Reference

All SPECS follow the architecture and principles defined in the  
**ProjectUSD Whitepaper V2.1**  
(System equilibrium, invariants, freeze model).

---

## 🪙 License
CC BY-NC-SA 4.0  
© 2025 Aqua75 / ProjectUSD
