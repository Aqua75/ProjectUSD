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
| **Periphery Layer** | Optional extensions: Collateral adapters, AMO modules, Peg-Stability mechanisms, and analytics interfaces. |
| **Governance Layer** | Limited to coordination and upgrades of the periphery. No control over the immutable core. |

---

## 🧭 Design Principles

- **On-Chain Autonomy:** No external oracles, no human intervention.  
- **Mathematical Feedback:** Stability arises from algorithmic reaction, not fixed pegs.  
- **Transparency by Code:** Every variable and process verifiable on-chain.  
- **Freeze Event:** Once activated, ProjectUSD becomes immutable and self-sustaining.  

---

## 📘 Reference

All architectural concepts are derived from the  
[ProjectUSD Whitepaper V2.1 – Vision & Architecture of a Self-Regulating Blockchain Economy](https://github.com/Aqua75/ProjectUSD/releases/download/v2.1-EN/ProjectUSD.Whitepaper.V2.1.EN.Englisch.pdf)

---

### 🪙 License
Creative Commons **BY-NC-SA 4.0**  
© 2025 Aqua75 – PulseChain Community Initiative
