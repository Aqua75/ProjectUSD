# Study 05 – Comparative Analysis: ProjectUSD vs. DAI, LUSD, GHO, USDe, USDC
*Structural comparison of stablecoin architectures with regard to autonomy, oracle dependency, stability mechanisms, and governance*  
*(Level-3 Research Format)*

---

## Abstract

Stablecoins form the monetary backbone of DeFi — as unit of account, store of value, and settlement layer.  
This study compares six fundamentally different stablecoin models:

- **ProjectUSD** – autonomous on-chain algorithmic monetary system for PulseChain  
- **DAI** – overcollateralized, governance-driven multi-collateral stablecoin  
- **LUSD** – immutable ETH-only stablecoin with minimal governance  
- **GHO** – Aave’s natively integrated stablecoin using facilitator modules  
- **USDe** – synthetic dollar backed by delta-neutral hedging strategies  
- **USDC** – fully fiat-backed custodial stablecoin  

The analysis evaluates these systems across four core dimensions:

1. **Autonomy** – independence from banks, off-chain infrastructure, and governance  
2. **Oracle dependency** – robustness of price feeds  
3. **Liquidation and stability architecture**  
4. **Governance and mutability of rules**

The resulting comparison highlights technical, economic, and regulatory risks, including stress and black-swan scenarios.

---

# 1. Introduction – Why comparative analysis is essential

Designing an internal unit of account for a blockchain ecosystem requires understanding the architectures, incentives, and systemic weaknesses of existing stablecoins.  
This study explains how ProjectUSD differs from alternative models and why an autonomous, oracle-internal, governance-minimized monetary system is uniquely suited for PulseChain.

---

# 2. Analysis of each system

## 2.1 ProjectUSD

### Design & Objective
ProjectUSD is a fully on-chain, algorithmically regulated monetary system for PulseChain.  
It does **not** attempt to track the US dollar.  
Instead, it defines its own internal unit of value via:

- **Equilibrium price R**  
- **Market price P**  
- **System rate r**, adjusted by the controller  

When P deviates from R, the controller adjusts r.  
High r → new borrowing becomes unattractive.  
Low r → borrowing becomes cheaper and economic activity becomes more attractive.

The system operates using internal signals — not external USD price feeds.

### Core components
- **Vaults** – overcollateralized PLS-backed positions  
- **Stability Pool** – absorbs liquidations and deletes debt  
- **Redemption Engine** – redeems 1 ProjectUSD at R, forming a hard internal price anchor  

### Architecture & Governance
- **Immutable Core** (no admin keys, no upgrades)  
- **Peripheral governance** for optional modules (PSM, AMOs, collateral adapters)

### Oracle
ProjectUSD is **oracle-autonomous**, using only on-chain PulseChain DEX data (Median-TWAP with outlier filters).

---

## 2.2 DAI (MakerDAO)

### Mechanism
- multi-collateral CDPs  
- stability fee, DAI savings rate  
- Peg Stability Module (PSM) enabling USDC ↔ DAI swaps  
- heavy reliance on **Chainlink oracles**

### Governance
- extensive DAO control  
- risk of governance capture  
- parameters frequently adjusted

### External dependencies
- large holdings of USDC and RWAs → substantial reliance on the traditional financial system

---

## 2.3 LUSD (Liquity)

### Mechanism
- ETH-only collateral  
- 110% minimum CR  
- Stability Pool for liquidations  
- redemption enforces price discipline

### Governance
- **immutable**, no upgrades

### Weakness
- limited yield mechanisms → cyclic contraction phases possible

---

## 2.4 GHO (Aave)

### Mechanism
- minted through Aave V3  
- issuance controlled by facilitator modules  
- price stability maintained via Aave’s ecosystem

### Governance
- fully governed by AAVE token holders

### Oracle dependency
- Chainlink feeds for collateral valuation

---

## 2.5 USDe (Ethena)

### Mechanism
- synthetic dollar via delta-neutral hedging (long stETH + short perps)  
- yields derived from funding spreads and staking rewards

### Risks
- dependency on centralized & decentralized derivatives markets  
- funding regime shifts  
- counterparty risk  
- operational complexity

---

## 2.6 USDC (Circle)

### Mechanism
- 1:1 fiat-backed using bank deposits and Treasuries  
- regulated custodial stablecoin

### Risks
- blacklisting  
- seizure risk  
- full reliance on banking and US regulatory environment

---

# 3. Comparison across key criteria

## 3.1 Overview Table

| Criterion | ProjectUSD | DAI | LUSD | GHO | USDe | USDC |
|----------|-------------|-----|------|------|-------|-------|
| Type | On-chain alg. money | Overcollateral CDP | ETH-only, immutable | Aave-native stablecoin | Synthetic / delta-neutral | Fiat IOU |
| Autonomy | High | Medium | High | Medium | Low–Medium | Low |
| Oracle | On-chain Median-TWAP | External | External | Chainlink | Perps + Spot | Off-chain |
| Liquidations | Stability Pool | Auctions | Stability Pool | Aave liquidations | Hedge rebalance | None |
| Redemption | Internal R-based | PSM (USDC) | ETH/USD | Stability modules | Protocol-dependent | 1:1 custodial |
| Governance | Peripheral only | Full DAO | None | Full DAO | Strong centralized | Fully centralized |
| Admin Keys | Core: No | Yes | No | Yes | Yes | Yes |

---

## 3.2 Autonomy

Most autonomous:

- **ProjectUSD**  
- **LUSD**

Both avoid reliance on:

- banking infrastructure  
- centralized custody  
- external price feeds

DAI and GHO possess decentralization but are not autonomous due to:

- heavy oracle dependence  
- governance control  
- real-world asset exposure

USDe is complex and heavily dependent on derivatives markets.  
USDC is not autonomous by design.

---

## 3.3 Oracle Dependency

### ProjectUSD
- uses only on-chain DEX prices  
- robust Median-TWAP with filters  
- immune to off-chain failure

### DAI / LUSD / GHO
- rely on Chainlink  
- subject to oracle lags and keeper dependency

### USDe
- dependent on derivative markets — a fundamentally different risk class

### USDC
- no on-chain oracle; integrity depends on bank reserves

---

## 3.4 Liquidation Architecture

ProjectUSD & LUSD:

- liquidation → Stability Pool → internal collateral redistribution  
- no AMM dumping  
- no auction risk  
- no keeper dependency

DAI & GHO:

- rely on auction/liquidator networks  
- complex interactions in stress periods

USDe:

- liquidation via hedge interruption  
- deeply tied to funding mechanics

USDC:

- no liquidation model (custodial)

---

## 3.5 Governance

ProjectUSD:

- immutable core  
- minimal peripheral governance  
- cannot break via governance mistakes

LUSD:

- governance-free  
- extremely robust, limited flexibility

DAI & GHO:

- governance-intensive  
- require active parameter management

USDe:

- centralized entities and strategies

USDC:

- fully centralized under corporate control

---

# 4. Risk Analysis

## 4.1 Technical Risks

Shared risks:

- smart contract vulnerabilities  
- chain-level instability  
- MEV

ProjectUSD:

- immutable core minimizes governance risks  
- median-TWAP minimizes oracle risks

DAI/GHO:

- upgradeable, but exposed to governance and oracle failures

LUSD:

- immutable, robust but inflexible

USDe:

- inherits risks from CEX/DEX derivatives infrastructure

USDC:

- off-chain failures likely more impactful than technical failures

---

## 4.2 Economic Risks

### Collateral volatility  
Affects ProjectUSD, DAI, LUSD, GHO, and USDe.

### Liquidity  
Lower liquidity amplifies volatility (notable for ProjectUSD early in adoption).

### Model risk (USDe)  
Delta-neutrality can break under extreme funding conditions.

### Redemption risk  
ProjectUSD and LUSD rely on redemption mechanics — robust but dependent on healthy vault structure.

### Bank-run risk  
USDC and indirectly DAI are most vulnerable.

---

## 4.3 Governance and External Environment Risks

### Regulatory exposure
- High: USDC, DAI (via RWAs), GHO  
- Medium: USDe (via CEX dependencies)  
- Low: ProjectUSD, LUSD

### Governance capture
- High: DAI, GHO  
- Medium: ProjectUSD  
- None: LUSD

### Political risk
- High: USDC  
- Low: autonomous models

---

# 5. Stress and Black-Swan Scenarios

## 5.1 Scenario A: Major Crypto Crash (80%)

**ProjectUSD**

- large liquidation waves absorbed by Stability Pool  
- r increases strongly  
- supply contracts  
- system remains solvent  
- redemption maintains R

**LUSD** – similar dynamics

**DAI/GHO**

- oracle lag can trigger faulty liquidations  
- keeper dependency magnifies stress

**USDe**

- hedge may break → potential de-peg

**USDC**

- stable unless coupled with traditional finance distress

---

## 5.2 Scenario B: Oracle or Market Manipulation

**ProjectUSD**

- Median-TWAP resists manipulation  
- rLimiter prevents reflexive overreaction

**DAI/LUSD/GHO**

- Chainlink outage or incorrect feed can trigger mass liquidations

**USDe**

- derivative market manipulation can break hedges

---

## 5.3 Scenario C: Regulatory Pressure

USDC:

- directly exposed

DAI:

- indirectly exposed due to RWA exposure

GHO:

- dependent on Aave’s regulatory status

USDe:

- exposed via exchanges and custodial partners

ProjectUSD & LUSD:

- technically immune to off-chain regulation

---

## 5.4 Scenario D: Derivatives Market Failure (USDe)

- hedge breaks  
- negative funding flips  
- undercollateralization risk  
- de-peg highly likely

ProjectUSD, LUSD, DAI, GHO, USDC largely unaffected.

---

## 5.5 Scenario E: PulseChain Network Disruption

ProjectUSD:

- 100% dependent on PulseChain  
- congestion or reorgs may delay liquidations

Other stablecoins on PulseChain exist only as bridged assets and inherit bridge risks instead.

---

# 6. Conclusion

## 6.1 Positioning of ProjectUSD

ProjectUSD combines features of:

- **LUSD** (immutable core, stability pool, redemption),  
- **DAI** (variable-rate debt model), but **fully automated** without governance.

Differences from USDC & DAI:

- no fiat dependence  
- no real-world assets  
- internal value definition (R)

Differences from USDe:

- no hedging  
- no funding-rate exposure  
- transparent and deterministic

---

## 6.2 Trade-offs

- less flexible than DAI/GHO  
- more autonomous and safer than governance-heavy models  
- more stable and transparent than hedging-based stablecoins  
- less regulatory risk than USDC

---

## 6.3 Relevance to PulseChain

ProjectUSD provides:

- an internal unit of account  
- a stable economic base  
- independence from fiat  
- a deterministic monetary engine for the ecosystem

## 6.4 Outlook

ProjectUSD’s greatest limitation is not conceptual — it is practical:

> **It does not exist yet. It must be built.**

Its eventual success depends on:

- implementation quality  
- ecosystem integration  
- conservative governance of peripheral modules  

Stablecoins will remain foundational to crypto.  
The future will increasingly favor systems that are **autonomous, transparent, and resistant to external failures**.

ProjectUSD is positioned to be such a system on PulseChain.

