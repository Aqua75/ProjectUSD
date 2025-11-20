# Developer Guidelines  
### How to work with the official ProjectUSD specifications

ProjectUSD is a **specification-only repository**.  
It contains no smart contract code and no official implementation.

These guidelines help developers implement ProjectUSD **independently**,  
while respecting architectural boundaries and security expectations.

---

## ⚙️ 1. Follow the Specifications Exactly

Any implementation must follow:

- `/Architecture/specs/README.en.md`
- all module-specific SPEC documents
- the ProjectUSD Whitepaper

Do not modify economic logic, invariants, or core mechanics.

---

## 🔍 2. Transparency Requirements

Implementations should be:

- **open source**
- **publicly verifiable**
- **fully reproducible**
- released under a clear license

Private or closed-source implementations are discouraged.

---

## 🔒 3. Security Requirements

Before launching any implementation:

- request an audit from reputable firms  
- publish audit reports publicly  
- include test coverage  
- consider formal verification  
- follow best practices for Solidity/Vyper security

ProjectUSD does **not** endorse or verify third-party code.

---

## 🚫 4. No Official Implementation

The ProjectUSD repo does not publish or maintain smart contracts.  
Any implementation is **independent** and **not official**.

Do not claim affiliation, endorsement, or partnership.

---

## 🤝 5. Contributing Back

If you find improvements for the **SPECS**, you may:

- open an Issue  
- submit a Pull Request for documentation  
- propose clarifications via GitHub Discussions  

Code contributions for implementations are **out of scope**.

---

## 📩 Contact

Discussion & community support:  
https://t.me/ProjectUSD_Discussion
