# ProjectUSD Architecture  

The **ProjectUSD Architecture** defines the structural and functional foundation of the system.  
It describes how on-chain components interact to maintain equilibrium, autonomy, and transparency.

---

## 🧩 Core Components

- **Vaults** – The foundation of money creation.  
  Users lock native PulseChain assets (e.g., PLS) as collateral to mint ProjectUSD.  

- **Stability Pool** – Collective safeguard that absorbs undercollateralized positions  
  and redistributes their collateral among depositors.  

- **Redemption Engine** – Maintains the internal equilibrium price (R)  
  by allowing 1:1 redemption in PLS at the internal reference value.  

- **Controller** – The autonomous feedback algorithm that regulates the system rate (r),  
  adjusting supply and demand dynamically.  

---

## 🧱 Architectural Layers

| Layer | Description |
|-------|--------------|
| **Immutable Core** | Contains the unchangeable logic: Vaults, Controller, Liquidations, and Redemption. Once frozen, it cannot be altered or paused. |
| **Periphery Layer** | Optional extensions: collateral adapters, analytics modules, and other non-core features. |
| **Governance Layer** | Limited to coordination and upgrades of the periphery. No control over the immutable core. |

---

## 🧭 Design Principles

- **On-Chain Autonomy:** No external oracles, no human intervention.  
- **Mathematical Feedback:** Stability arises from algorithmic reaction, not fixed pegs.  
- **Transparency by Code:** Every variable and process verifiable on-chain.  
- **Freeze Event (Core only):** Once activated, only the **Immutable Core** becomes unchangeable; peripheral modules remain adjustable through timelocked governance.

---

## 📂 Technical Specifications (SPECS)

The complete set of technical specifications – covering every core module,  
security concept, freeze mechanism, stability logic, liquidation engine,  
Subgraph KPIs, and diagnostic procedures – is available in:

**➡ `/Architecture/specs/`**

Two full entry points exist:

- 🇬🇧 **SPECS Overview (English)**  
  `/Architecture/specs/README.md`

- 🇩🇪 **SPECS Übersicht (Deutsch)**  
  `/Architecture/specs/README.de.md`

These files provide:

- a full module overview  
- direct links to all specifications  
- recommended reading order  
- core vs periphery structure  
- references to the ProjectUSD Whitepaper  

The SPECS folder represents the **complete technical foundation** of ProjectUSD  
for developers, auditors, and researchers.

---

## 📘 Reference

All architectural concepts are derived from the  
[ProjectUSD Whitepaper V2.1 – Vision & Architecture of a Self-Regulating Blockchain Economy](https://github.com/Aqua75/ProjectUSD/releases/download/v2.1-EN/ProjectUSD.Whitepaper.V2.1.EN.Englisch.pdf)

---

### 🪙 License
Creative Commons **BY-NC-SA 4.0**  
© 2026 Aqua75 – PulseChain Community Initiative
