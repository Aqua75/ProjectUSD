# Developer Guidelines – Building ProjectUSD

ProjectUSD is an open blueprint for an autonomous, oracle-free, and self-regulating monetary system on PulseChain.  
These guidelines describe how developers, researchers, and auditors can contribute to building, testing, and securing its architecture.

---

## **1. Philosophy of Development**

ProjectUSD is not a company or a product launch.  
It is a *mathematical organism* — an idea that must be translated into code carefully, transparently, and with immutable integrity.

> 🌀 *"Code first, hype never."*

**Core principles for all development work:**
- No central dependencies or off-chain feeds  
- Minimal and auditable logic  
- Transparent, deterministic behavior  
- Immutability after the Freeze Event  
- Open collaboration and verifiable progress  

---

## **2. Core Components to Implement**

The system architecture is defined by six critical modules:

| Component | Description |
|------------|-------------|
| **Controller** | The economic feedback mechanism that adjusts the system rate (r) based on deviations between market price (P) and equilibrium price (R). |
| **Vaults** | Smart contracts where users deposit PLS collateral to mint ProjectUSD. Includes liquidation logic. |
| **Stability Pool** | Collective liquidity pool that absorbs undercollateralized positions and redistributes PLS to depositors. |
| **Redemption Engine** | Maintains the on-chain equilibrium price R by allowing redemptions of ProjectUSD for PLS. |
| **AMO (Algorithmic Market Operations)** | Optional module that performs liquidity balancing within defined ranges and budgets. |
| **PSM (Peg Stability Module)** | Optional swap mechanism for stablecoins, capped and non-essential for stability. |

Each component must be modular, auditable, and compatible with the **Immutable Core / Periphery** separation described in the whitepaper.

---

## **3. Code Architecture**

### **Immutable Core**
Contains all mission-critical functions and must be *permanently locked* after deployment:
- Vault creation and liquidation logic  
- Controller and rate adjustment mechanism  
- Redemption engine  
- Oracle aggregation (median TWAP)  
- Collateral ratio and liquidation threshold  

After the **Freeze Event**, this core cannot be modified.

### **Periphery Modules**
Optional and upgradeable, managed through transparent on-chain governance:
- Collateral adapters  
- PSM configurations  
- AMO parameters  
- Telemetry and analytics interfaces  

All periphery updates must include:
- Time-locked governance delay  
- On-chain transparency of proposed changes  
- Auditable record of each parameter modification  

---

## **4. Technical Stack & Standards**

| Layer | Recommended Stack |
|-------|-------------------|
| **Smart Contracts** | Solidity ≥0.8.x |
| **Network** | PulseChain Mainnet (EVM-compatible) |
| **Testing Framework** | Hardhat / Foundry |
| **Auditing Tools** | Slither, Echidna, Mythril, or equivalent |
| **Data Feeds** | On-chain TWAP from PulseX pairs (no off-chain oracles) |

**Smart-contract design standards:**
- Follow OpenZeppelin patterns where applicable (access control, math, safety).
- Use **no admin keys**, **no pausable contracts**, **no upgrade proxies** in the Immutable Core.
- Apply **ReentrancyGuard**, **Rate-Limiters**, and **Fail-Safe math** where specified.

---

## **5. Security & Verification**

Before mainnet deployment, all modules must undergo:
- **Formal verification** of mathematical invariants  
- **Independent code audit** by at least one external team  
- **Open bug bounty** or public testing phase  

Security must follow the philosophy:
> *"What cannot be changed, cannot be corrupted."*

---

## **6. Collaboration Workflow**

Developers can contribute via GitHub by:
1. Forking the repository  
2. Creating a new branch (e.g. `feature/controller-module`)  
3. Committing proposed code with documentation and unit tests  
4. Submitting a Pull Request with clear notes  

**Every contribution must include:**
- Purpose and scope  
- Security considerations  
- Dependencies and interactions with existing modules  
- Reference to the corresponding whitepaper section  

---

## **7. Research and Simulation**

Before coding, developers are encouraged to build **mathematical simulations** of the control loop:  
- Relationship between `r`, `R`, and `P`  
- Response to demand shocks  
- Stability under varying collateral conditions  

These simulations (Python, MATLAB, or similar) can be published in the `Drafts/` directory for peer review.

---

## **8. Development Ethics**

ProjectUSD’s credibility relies on transparency and technical honesty.  
All contributors are expected to:
- Respect the immutability principle  
- Avoid speculation or premature tokenization  
- Keep focus on verifiable, testable progress  
- Document everything for future builders  

---

## **9. Summary**

ProjectUSD development is not about speed — it is about precision.  
Every commit, every line of code, and every test must serve the system’s single purpose:  
**autonomous, incorruptible monetary balance.**

> 🧩 *"Not controlled by anyone — and therefore owned by everyone."*
