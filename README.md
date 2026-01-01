# ProjectUSD  
### Autonomous Monetary System for PulseChain

**Language:** 🇬🇧 English | [🇩🇪 German](./README.de.md)

> *"When the code cannot lie, humanity no longer needs to."*

---

## 🌐 What is ProjectUSD?

ProjectUSD is a **fully on-chain, algorithmic monetary system** designed for PulseChain.  
It achieves economic stability **without banks, without governance, without oracles,  
and without centralized intervention of any kind.**

It represents the next evolution of decentralized finance:  
a **self-regulating economic engine** powered solely by transparent, immutable logic.

---

## 📘 Whitepaper V2.1

**Available Editions:**

- 🇩🇪 [Download German Edition (PDF)](https://github.com/Aqua75/ProjectUSD/releases/download/v2.1-DE/ProjectUSD.Whitepaper.V2.1.German.pdf)  
- 🇺🇸 [Download English Edition (PDF)](https://github.com/Aqua75/ProjectUSD/releases/download/v2.1-EN/ProjectUSD.Whitepaper.V2.1.EN.Englisch.pdf)
- 🇪🇸 [Download Spanish Edition (PDF)](https://github.com/Aqua75/ProjectUSD/releases/download/v2.1-es/ProjectUSD_Whitepaper_V2.1_ES_Espanol.pdf)
- 🇫🇷 [Download French Edition (PDF)](https://github.com/Aqua75/ProjectUSD/releases/download/v2.1-FR/ProjectUSD_Whitepaper_V2.1_FR_Francais.pdf)
- 🇧🇷 [Download Brazilian Edition (PDF)](https://github.com/Aqua75/ProjectUSD/releases/download/v2.1-PT-BR/ProjectUSD_Whitepaper_V2.1_pt-BR_Portugues.pdf)
- 🇮🇹 [Download Italian Edition (PDF)](https://github.com/Aqua75/ProjectUSD/releases/download/v2.1-IT/ProjectUSD_Whitepaper_V2.1_IT_Italiano.pdf)
- 🇵🇱 [Download Polish Edition (PDF)](https://github.com/Aqua75/ProjectUSD/releases/download/v2.1-PL/ProjectUSD_Whitepaper_V2.1_PL_Polski.pdf)
- 🇳🇱 [Download Dutch Edition (PDF)](https://github.com/Aqua75/ProjectUSD/releases/download/v2.1-NL/ProjectUSD_Whitepaper_V2.1_NL_Nederlands.pdf)
- 🇨🇳 [Download Chinese Edition (PDF)](https://github.com/Aqua75/ProjectUSD/releases/download/v2.1-CN/ProjectUSD_Whitepaper_V2.1_CN_Chinese.pdf)
- 🇯🇵 [Download Japanese Edition (PDF)](https://github.com/Aqua75/ProjectUSD/releases/download/v2.1-JA/ProjectUSD_Whitepaper_V2.1_JA_Japanese.pdf)
- 🇷🇺 [Download Russian Edition (PDF)](https://github.com/Aqua75/ProjectUSD/releases/download/v2.1-RU/ProjectUSD_Whitepaper_V2.1_RU_Russian.pdf)
- 🇮🇳 [Download Hindi Edition (PDF)](https://github.com/Aqua75/ProjectUSD/releases/download/v2.1-HI/ProjectUSD_Whitepaper_V2.1_HI_Hindi.pdf)
- 🇹🇷 [Download Turkish Edition (PDF)](https://github.com/Aqua75/ProjectUSD/releases/download/v2.1-TR/ProjectUSD_Whitepaper_V2.1_TR_Turkish.pdf)
- 🇻🇳 [Download Vietnamese Edition (PDF)](https://github.com/Aqua75/ProjectUSD/releases/download/v2.1-VI/ProjectUSD_Whitepaper_V2.1_VI_Vietnamese.pdf)
- 🇮🇩 [Download Indonesian Edition (PDF)](https://github.com/Aqua75/ProjectUSD/releases/download/v2.1-ID/ProjectUSD_Whitepaper_V2.1_ID_Indonesian.pdf)
- 🇰🇷 [Download Korean Edition (PDF)](https://github.com/Aqua75/ProjectUSD/releases/download/v2.1-KR/ProjectUSD_Whitepaper_V2.1_KR_Korean.pdf)
- 🇸🇦 [Download Arabic Edition (PDF)](https://github.com/Aqua75/ProjectUSD/releases/download/v2.1-AR/ProjectUSD_Whitepaper_V2.1_AR_Arabic.pdf)
- 🕉 [Download Sanskrit Edition (PDF)](https://github.com/Aqua75/ProjectUSD/releases/download/v2.1-SA/ProjectUSD_Whitepaper_V2.1_SA_Sanskrit.pdf) *(Experimental)*

---

## 🧩 Technical Architecture

ProjectUSD is built from five immutable core modules:

- **VaultEngine** – Collateral, debt, and CR logic  
- **Controller** – Autonomous equilibrium engine (R & r-epochs)  
- **Oracle** – Medianized, deviation-safe pricing  
- **Liquidation & Redemption Engine** – Stability enforcement  
- **StabilityPool** – Collective risk absorption  

---

> ### 🔍 Clarification: Internal TWAP Oracle  
> The “Oracle” module in ProjectUSD is **not** an external price oracle.  
> It does **not** use Chainlink, Pyth, DIA, APIs, or any off-chain data.  
>  
> Instead, it is a **pure on-chain TWAP reader** that derives price information  
> exclusively from the ProjectUSD/PLS AMM pool on PulseChain.  
>  
> - no external dependencies  
> - no governance updates  
> - no admin intervention  
> - fully deterministic and on-chain  
>  
> This ensures that ProjectUSD remains an **autonomous, oracle-free monetary system** while still allowing the controller to observe its own AMM-based market behavior.

---

A detailed architectural explanation is available at:

➡ `/Architecture/README.md`

---

## 🚀 Quickstart for Developers

For developers, auditors, and researchers who want to enter directly into the technical foundations of ProjectUSD, the following documents serve as the primary entry points:

### **1. Architecture Overview**
➡ [`/Architecture/README.md`](./Architecture/README.md)  
A high-level introduction to the system architecture, core modules, and internal data flows.

### **2. Complete Specifications (SPECS)**
➡ [`/Architecture/specs/README.md`](./Architecture/specs/README.md)  
The formal, audit-ready specifications of all core components:

- VaultEngine  
- Controller  
- Oracle  
- Liquidation & Redemption  
- StabilityPool  
- Security  
- Governance & Freeze  
- KPI Subgraph  
- Incident Runbook  

### **3. Developer Playbook**
➡ [`/Developer_Playbook/README.md`](./Developer_Playbook/README.md)  
A practical guide for development workflow, standards, conventions, and recommended best practices.

### **4. Glossary**
➡ [`/Glossary.md`](./Glossary.md)  
Definitions of terms, mechanisms, variables, economic concepts, and formula notation used throughout the system.

---

## 📂 Full Technical Specification Library (SPECS)

ProjectUSD contains one of the most complete SPEC frameworks in decentralized finance:

➡ `/Architecture/specs/README.md`  
➡ `/Architecture/specs/README.de.md`

This section provides the **entire audit-ready blueprint** of the system, including:

- VaultEngine SPEC  
- Controller SPEC  
- Oracle SPEC  
- Liquidation & Redemption SPEC  
- StabilityPool SPEC  
- Security SPEC  
- Governance & Freeze SPEC  
- Freeze Checklist  
- KPI Subgraph SPEC  
- Incident Runbook  
- DEX-LP SPEC (optional)

All specifications are **modular**, **consistent**, and available in **English and German**.

---

## 📚 Research Library

ProjectUSD provides two curated document collections that extend beyond the technical specifications and deepen the economic foundations of the system.

### 📝 Articles

➡ [`/Articles`](./Articles)  
Analytical essays and conceptual papers covering topics such as:
- internal value units and purchasing power  
- the meaning of the name ProjectUSD  
- the P R r model  
- theoretical principles of autonomous monetary systems  

These texts provide the conceptual framework behind the design and help explain the reasoning that informs the SPECS.

### 📑 Studies

➡ [`/Studies`](./Studies)  
Formal research studies covering subjects such as:
- stability mechanisms and anti reflexivity  
- system game theory  
- collateral models and stress simulations  
- liquidity and arbitrage behaviour  
- long term surplus development  
- gas usage and efficiency models  

These studies provide quantitative models, conceptual frameworks and analytical insights into the structural behaviour of the ProjectUSD system.

---

## 📌 Status  
🧩 *Completed architecture & full SPEC blueprint — now open for developers, auditors, and investors.*

---

## 🔗 Discussion & Development

Join the ProjectUSD community on Telegram:

➡ https://t.me/ProjectUSD_Discussion

---

## ⚠️ Implementation Notice

This repository contains the official ProjectUSD specifications only.

Smart contract implementations may be developed by independent teams.
Whether a specific implementation is secure can only be evaluated through:

- **open audits**,  
- **peer review**,  
- **open-source transparency**,  
- **formal verification**,  

— not through this document.

ProjectUSD does not publish smart contracts and does not designate any implementation as official.

Users should rely only on implementations that have undergone verification
by **reputable auditors** and whose source code is fully transparent.

---

## 🏷️ ProjectUSD – Name & Attribution Policy

ProjectUSD is an original open-source concept published by  
**Aqua75 / PulseChain Community Initiative**  
under the **Creative Commons BY-NC-SA 4.0** license.

This license applies to all documentation, specifications, studies, whitepapers and media in this repository.

However, the **name “ProjectUSD” and the ProjectUSD logo** are protected identifiers of the original PulseChain-based design.

### Allowed Use of the Name “ProjectUSD”

Implementations deployed on **PulseChain** must:

1. fully comply with the official ProjectUSD specification, and  
2. pass the consolidation process  

to use the name **“ProjectUSD”**.

### Independent Forks

All other implementations — on PulseChain or elsewhere — must be clearly labeled as **independent forks**, and must include the attribution:

> Based on the “ProjectUSD” concept by Aqua75 / PulseChain Community Initiative  
> https://github.com/Aqua75/ProjectUSD

Unauthorized use of the name or logo outside the PulseChain context  
violates the license terms.

© 2026 Aqua75 — All rights reserved for the name and logo **“ProjectUSD”**.

---

## 🪙 License

Creative Commons **BY-NC-SA 4.0**  
© 2025 Aqua75 – PulseChain Community Initiative
