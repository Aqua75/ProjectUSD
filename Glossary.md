# ProjectUSD – Glossary (English)
### Complete definitions of all core system terms, variables, mechanisms and models

This glossary contains all relevant terms from:
- the ProjectUSD architecture  
- the SPEC documents  
- the Whitepaper  
- the P-R-r model  
- the Controller logic  
- the VaultEngine  
- Liquidation & Redemption  
- the studies and research articles  

This version replaces all earlier glossaries.

---

# 🧩 Fundamental Concepts

**ProjectUSD**  
An autonomous, algorithmic monetary system on PulseChain without oracles, governance, admin keys or upgradeability. The system follows fully deterministic rules.

**Autonomous Monetary Policy**  
The rule-based mechanism through which ProjectUSD maintains long-term purchasing power. It is entirely algorithmic and free of human intervention.

---

# 🧠 Core Variables: P, R, r

## **R – Internal Value Unit (Purchasing Power Anchor)**  
The internal reference metric against which the value of ProjectUSD is stabilized.  
R determines:
- the redemption price  
- the Controller’s stability target  
- the system’s internal equilibrium  

R is immutable and forms the foundation of purchasing power stability.

---

## **r – System Debt Rate**  
An internal parameter that regulates the cost of system debt.

r influences:
- the growth rate of outstanding vault debt
- borrowing incentives
- supply elasticity through minting activity

The Controller dynamically adjusts r in response to deviations between market price P and equilibrium value R.

The system rate is bounded:

0 ≤ r ≤ r_cap

---

## **P – Market Price / Market Demand Impulse**  
P is the market-generated price impulse, derived from the observed TWAP price of the ProjectUSD–PLS AMM pair.

P represents:
- market price movements  
- demand or supply shocks  
- external market realities  

P is the **only external factor** in the P-R-r model.

---

# 🔢 P-R-r Model

The central economic model of ProjectUSD.  
It describes the interaction between:

- **P** – market price impulse  
- **R** – internal value unit (price anchor)  
- **r** – system debt rate  

The model explains:
- price stability  
- demand absorption  
- epoch transitions  
- supply and savings dynamics  
- long-term value consistency  

---

# 🕒 Epochs & Controller Phases

## **R-Epoch (Restore)**  
The phase in which the system actively corrects price deviations and enforces the value anchor R.  
Typical characteristics:
- increased redemption activity  
- strong Controller intervention  
- return of price towards R  

---

## **r-Epoch (Rebalance)**  
The structural adjustment phase.  
The Controller modifies r to prevent future stress and re-establish balance.

---

## **Epoch Transition**  
The automatic transition between R-Epoch and r-Epoch, triggered by:

- market price movements (P)  
- deviations from R  
- structural stress  
- Controller metrics  

---

# 🏛 Architecture Terms

**Immutable Core**  
The permanently unchangeable modules: VaultEngine, Controller, StabilityPool, Redemption, Liquidation, TWAP module.

**Freeze Event**  
The moment the Core is permanently frozen. No upgrades are possible thereafter.

**Deterministic Execution**  
All operations produce identical results for identical inputs.

**No Admin Key**  
No key exists that could modify parameters or intervene in system behavior.

---

# 🏦 VaultEngine & Collateral

**Vault**  
A user position consisting of collateral and generated debt.

**Collateral Ratio (CR)**  
Collateral value divided by debt.

**Minimum Collateral Ratio (MCR)**  
Lower bound; falling below triggers liquidation.

**Debt Ceiling**  
Maximum allowed system debt (global or per collateral group).

**System Debt**  
All issued ProjectUSD units.

**Debt Expansion / Debt Contraction**  
Increase or decrease of total debt driven by Controller mechanisms.

**Collateral Bucket**  
A group of collateral types sharing common parameters.

**Debt Floor**  
The minimum amount of debt required for a valid vault.

---

# 💥 Liquidation & Redemption

**Liquidation**  
Forced closure of a vault when CR < MCR.

**Pro-Rata Liquidation**  
Distribution of an undercollateralized vault proportionally among StabilityPool participants.

**Liquidation Penalty**  
A surcharge paid into the StabilityPool.

**Liquidation Discount**  
The discount at which Stability Providers acquire collateral during liquidation.

**Soft Liquidation / Hard Liquidation**  
Different liquidation modes depending on system stress.

---

## **Redemption**  
Exchange of ProjectUSD for PLS at the value anchor R.

**Redemption Queue**  
Order in which vaults are processed during redemption.

**Redemption Spread**  
Optional systemic adjustment that slightly modifies redemption execution.

**Redemption Density**  
Intensity of redemption activity across multiple blocks.

---

# 🏦 StabilityPool

**StabilityPool**  
A liquidity pool that absorbs liquidations and receives collateral in return.

**Stability Provider (SP)**  
Users who deposit ProjectUSD into the StabilityPool and earn liquidation gains.

**Stability Pool Utilization**  
The extent to which the pool is engaged in liquidation events.

---

# 📊 Oracle, Pricing & TWAP

**Oracleless Design**  
No external oracles; pricing relies exclusively on on-chain data.

**TWAP (Time-Weighted Average Price)**  
Time-weighted average price from the AMM.

**TWAP Window**  
The time interval used to compute the TWAP.

**Oracle Window Shift**  
The rolling forward of the TWAP window to incorporate new data.

**Deviation Limit**  
Maximum tolerable deviation between TWAP and system parameters.

**Deviation Trigger**  
Trigger that activates the R-Epoch.

---

# 🛡 Security & Invariants

**Atomicity**  
Operations either execute entirely or revert entirely.

**Invariants**  
Rules that must never be violated (e.g., CR ≥ MCR).

**State Transition Function**  
Formal definition of all valid state transitions.

**Fail-Safe Mode**  
A protective mode entered under extreme anomalies.

**Invariant Enforcement Layer**  
A layer ensuring that invariants are always upheld.

**Deterministic Path**  
A sequence of operations that always yields identical results under identical inputs.

---

# 📈 Analytics & Monitoring Metrics

**Epoch Tracker**  
Tracks R- and r-epoch states.

**Collateral Health Index**  
Measure of average collateralization strength.

**Redemption Pressure Index**  
Metric representing redemption-induced stress.

**System Stress Level**  
Macro indicator for system-wide stress.

**Controller Saturation**  
A state in which the Controller cannot adjust r any further.

**Supply Elasticity Envelope**  
The permitted dynamic range within which the supply can elastically adjust.

---

# 👥 Organizational Terms

**SPEC (Specification)**  
Formal technical description of a system module.

**Independent Implementation**  
An external implementation independent of this repository.

**Open-Source Blueprint**  
The full set of SPECS, articles and studies.

**Incident Runbook**  
Documentation for diagnosing anomalies in third-party implementations.

---

# 📌 Final Note

This glossary forms the complete definitional foundation of ProjectUSD  
and ensures that all modules, SPECS, articles and studies can be understood consistently.
