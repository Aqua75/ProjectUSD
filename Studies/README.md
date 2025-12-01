# ProjectUSD Research Studies  
*A structured collection of technical, economic and system-level analyses of the ProjectUSD architecture*

---

## Overview

This directory contains the complete set of **ProjectUSD Research Studies**, a continuously expanding body of work designed to formally document, evaluate and analyze the architecture, mechanics and economic properties of ProjectUSD — an autonomous, oracle-independent, self-regulating monetary system built for PulseChain.

Each study follows a unified **Level-3 Research Format**, ensuring:

- formal structure  
- logical consistency  
- verifiable claims  
- clear separation of theory, mechanism design and empirical reasoning  
- professional readability for developers, researchers and auditors  

Every study is available in **German (.de.md)** and **English (.md)**.

---

## Purpose of the Research Series

The ProjectUSD Studies serve three goals:

### **1. Technical Documentation**  
To provide precise, implementation-ready specifications of the system’s core mechanics such as:

- controller logic (r-adjustment)  
- redemption flows  
- liquidation and Stability Pool mechanics  
- oracle and TWAP design  

### **2. Economic and Game-Theoretic Evaluation**  
To analyze how actors behave within the system and how incentives generate negative feedback loops, stability and manipulation resistance.

### **3. Comparative and Stress-Test Analysis**  
To examine ProjectUSD under extreme market conditions and compare it with other decentralized and centralized stablecoin systems.

---

## Contents

Below is the chronological list of all research studies:

### **01 – Controller Dynamics**  
Mechanics of price deviation ε and the r-adjustment feedback loop.

### **02 – Liquidation Cascades**  
Stress behavior of vault liquidations and Stability Pool dynamics.

### **03 – The Redemption Engine**  
Internal price anchor and equilibrium restoration mechanism.

### **04 – MEV Resistance & Median-TWAP Stability**  
Oracle smoothing, manipulation protection and MEV robustness.

### **05 – Comparison: ProjectUSD vs DAI, LUSD, GHO, USDe, USDC**  
Decentralization, risk, architectural and economic comparison.

### **06 – PulseChain as a Closed Economy**  
Impact of endogenous value systems without external fiat ties.

### **07 – Breathing Dynamics of r**  
How r-adjustment absorbs volatility through countercyclical pressure.

### **08 – Surplus Buffer & Long-Term System Health**  
Why autonomous savings layers strengthen long-run stability.

### **09 – Why ProjectUSD Cannot Develop Death Spirals**  
Structural analysis of negative feedback vs reflexive collapse.

### **10 – Multi-Collateral Stress Tests**  
System behavior under correlated collateral shocks and tail events.

### **11 – Liquidity Analysis of ProjectUSD Trading Pairs**  
Market microstructure, arbitrage and pair-level behavior.

### **12 – Game Theory of the ProjectUSD Economy**  
Strategic incentives of all actor types and Nash equilibrium formation.

### **13 – Decentralization Comparison**  
Structural decentralization vs governance-based systems.

### **14 – Efficiency of ProjectUSD on PulseChain**  
Gas costs, scalability, and performance benchmarking vs Ethereum.

---

## File Naming Convention

All documents follow the format:

- Study-XX-Short-Title.de.md
- Study-XX-Short-Title.en.md


This ensures:

- clear structure  
- easy navigation  
- alphabetical sorting  
- SEO-optimized URLs  
- direct readability for developers and researchers  

---

## Contribution & Review

The studies are designed to be:

- technically precise  
- logically verifiable  
- auditable  
- self-consistent  

If you wish to contribute improvements, propose corrections or request deeper analysis, please open an Issue or Pull Request in the main repository.

All contributions must follow:

- academic rigor  
- source-based reasoning  
- neutrality  
- consistency with the immutable ProjectUSD architecture  

---

## License and Attribution

ProjectUSD is an original open-source concept published by  
**Aqua75 / PulseChain Community Initiative**  
under the **Creative Commons BY-NC-SA 4.0** license.

This license applies to all:

- whitepapers  
- research studies  
- translations  
- specifications  
- media assets  
- diagrams and explanatory materials  

contained in this repository and its official releases.

While the concept may be studied, extended or implemented under the same license terms,  
the **name “ProjectUSD” and the ProjectUSD logo** are protected identifiers of the original PulseChain-based design.

### Use of the Name “ProjectUSD”

Any implementation deployed on **PulseChain** must:

1. fully comply with the official ProjectUSD specification, and  
2. pass the consolidation process  

in order to use the name **“ProjectUSD”**.

All other implementations — on PulseChain or elsewhere — **must be clearly labeled as independent forks**, and must include a visible attribution:

> Based on the “ProjectUSD” concept by Aqua75 / PulseChain Community Initiative  
> https://github.com/Aqua75/ProjectUSD

Unauthorized use of the name or logo outside the PulseChain context  
constitutes a breach of the license terms.

© 2025 Aqua75 – All rights reserved for the name and logo **“ProjectUSD”**.

---

## Contact & Further Reading

For discussions, questions, clarification or collaboration regarding ProjectUSD,  
please use the official community discussion group:

**Telegram (ProjectUSD Discussion Group)**  
https://t.me/ProjectUSD_Discussion

This channel is the central contact point for:

- research-related questions  
- technical clarifications  
- architectural discussions  
- feedback on studies or documentation  

Since this repository is maintained in a curated and consolidated form,  
external Pull Requests are not part of the workflow.  
All inquiries should be directed to the discussion group above.

### Key Documentation

- **Whitepaper (English)**  
  `ProjectUSD.Whitepaper.V2.1.EN.Englisch.pdf`

- **Architecture & Module Specifications**  
  `/Architecture/`

- **Developer Playbook**  
  `/Developer_Playbook/`

- **Research Studies (Deutsch & Englisch)**  
  `/Studies/`

- **Articles & Concept Papers**  
  `/Articles/`
