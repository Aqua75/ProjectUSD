# Study 10 – Multi-Collateral Stress Tests for ProjectUSD
*Systemic analysis of risks, correlation effects, and failure modes in multi-asset collateral models*  
*(Level-3 Research Format)*

---

## Abstract

ProjectUSD is designed as a pure single-collateral system based on PLS, but future expansion phases may theoretically include additional collateral types.  
Understanding whether a multi-collateral architecture can be operated safely — and under which conditions — is essential for long-term protocol evolution.

This study examines:

- systemic risks in multi-collateral designs,  
- correlation effects between different asset classes,  
- liquidation dynamics in cross-collateral environments,  
- stress propagation across collateral clusters,  
- worst-case scenario modeling,  
- and whether ProjectUSD can remain structurally stable under multi-collateral conditions.

The results show that a multi-collateral model is **only viable under strict safety constraints**, ensuring that no death-spiral mechanisms, oracle vulnerabilities, or correlated shock cascades threaten the core system.

---

# 1. Introduction – Why multi-collateral is inherently risky

Many stablecoins adopt multi-collateral architectures to increase flexibility (e.g., DAI).  
However, this comes at significant cost:

- heterogeneous volatility profiles,  
- uneven liquidity depth,  
- dependence on multiple oracles,  
- correlated liquidation cascades,  
- exponentially growing complexity.

ProjectUSD was intentionally designed as a **single-collateral system (PLS)** because this eliminates central risk vectors:

- no cross-asset correlation risk,  
- unified oracle logic,  
- predictable liquidation mechanics,  
- homogeneous risk distribution,  
- simplified stress modeling.

This study evaluates whether and how a multi-collateral architecture could be implemented without compromising systemic safety.

---

# 2. Definitions and system components

## 2.1 Base system (single collateral: PLS)

ProjectUSD operates using:

- PLS-based Vaults,  
- Stability Pool liquidations,  
- redemption for PLS,  
- r-governed monetary dynamics,  
- a Surplus Buffer for long-term stability.

A single-collateral model is **monodimensional** and highly predictable in stress scenarios.

---

## 2.2 Hypothetical multi-collateral extension

Possible additional collateral assets might include:

- wPLS derivatives,  
- liquid staking tokens (LSTs),  
- PulseX LP tokens,  
- potentially bridged external assets (less desirable),  
- other PulseChain-native assets.

Each collateral type introduces its own risk structure:

- distinct volatility  
- distinct liquidity behavior  
- distinct oracle dependencies  
- distinct correlation patterns  

Complexity increases **non-linearly** with each added asset.

---

# 3. Risk categories in multi-collateral systems

## 3.1 Volatility risk

Each asset features:

- different volatility amplitudes,  
- different tail risks,  
- different mean-reversion characteristics.

Multi-collateral architectures create **shared exposure** across volatility clusters.

---

## 3.2 Correlation structure

Core issue:

> **Uncorrelated assets in calm markets often become correlated under stress.**

This produces:

- simultaneous price crashes,  
- amplified liquidation volume,  
- Stress propagation across assets.

Correlation shocks are one of the most dangerous drivers of systemic failure.

---

## 3.3 Oracle risks

Each collateral type requires:

- a distinct price feed,  
- distinct TWAP parameters,  
- distinct median logic,  
- distinct outlier filters.

More oracles → more attack surfaces.

---

## 3.4 Liquidity risk

A collateral asset may become illiquid during volatility spikes:

- wide spreads,  
- insufficient depth,  
- liquidation delays.

This creates **alpha loss** absorbed by the Stability Pool.

---

## 3.5 Complexity risk

More assets →  
more parameters →  
more edge cases →  
more black-swan scenarios →  
higher systemic fragility.

---

# 4. Liquidation dynamics in a multi-collateral system

## 4.1 Advantages of single-collateral liquidation

In the single-collateral model:

- liquidations are homogeneous,  
- the Stability Pool understands its exposure,  
- Surplus Buffer growth is predictable,  
- redemption logic remains stable and simple.

---

## 4.2 Challenges in multi-collateral liquidation

With multiple assets:

- cross-collateral liquidations may overlap,  
- mismatched value transfer risks emerge,  
- the Stability Pool may accumulate undesirable exposure,  
- systemic imbalances propagate.

Worst case:  
A volatile collateral unwinds and destabilizes the Stability Pool.

---

## 4.3 Weighted liquidation models

A theoretical mitigation:

- collateral is transferred with risk-adjusted discounts,  
- volatile assets are discounted more heavily,  
- buffer compensates for mismatched prices.

But such weighting introduces **new attack vectors** and complexity.

---

# 5. Stress tests: multi-collateral failure scenarios

## 5.1 Scenario A – Correlation shock

Two previously low-correlation assets crash simultaneously.

Consequences:

- double liquidation pressure,  
- mixed collateral in the Stability Pool,  
- Surplus Buffer stress,  
- destabilized monetization cycles.

---

## 5.2 Scenario B – Oracle manipulation

An attack on Asset B’s price feed results in:

- incorrect collateral valuation,  
- false liquidation events,  
- mispriced Stability Pool transfers,  
- r-controller disturbances.

---

## 5.3 Scenario C – Illiquid collateral

An asset becomes illiquid during a market crash.

Effects:

- liquidation becomes unprofitable,  
- Stability Pool absorbs toxic collateral,  
- Surplus Buffer depletion,  
- reduced redemption efficiency.

---

## 5.4 Scenario D – Bridge failure for external collateral

If collateral originates from external networks:

- bridge risk becomes systemic,  
- potential total loss of asset backing,  
- oracle desynchronization,  
- unclear redemption pathways.

Such risks violate ProjectUSD’s security philosophy.

---

# 6. Systemic evaluation: Can multi-collateral be safe?

## 6.1 Potential benefits

- broader risk distribution,  
- larger potential collateral base,  
- increased Vault participation,  
- reduced dependency on a single asset.

---

## 6.2 Key drawbacks (currently dominant)

- exponential rise in complexity,  
- new failure modes,  
- higher oracle exposure,  
- unpredictable liquidation outcomes,  
- unstable redemption interactions,  
- increased load on Stability Pool and Surplus Buffer.

---

## 6.3 Core conclusion

A multi-collateral system can be **viable**,  
but only under strict conditions:

- collateral with nearly identical risk profiles,  
- robust on-chain oracle isolation,  
- guaranteed high liquidity,  
- strict per-asset supply caps,  
- dynamic risk weighting,  
- strong buffer reserves.

Without these constraints, systemic risk increases dramatically.

---

# 7. Recommended phased approach for future expansion

ProjectUSD should not introduce multi-collateral support early on.  
Instead, follow a phased roadmap:

## Phase 1 – Pure PLS model (maximum stability)
- minimal attack surface  
- fully predictable risk dynamics  
- ideal environment for controller and oracle optimization

## Phase 2 – Add near-PLS assets
Examples:

- wPLS  
- safe liquid staking derivatives  

These assets closely resemble PLS in risk behavior.

## Phase 3 – Strictly controlled multi-asset extensions
Only possible with:

- hard caps per collateral type,  
- isolated liquidation pools,  
- separate oracle channels,  
- surplus-backed safety margins.

---

# 8. Conclusion

Multi-collateral architectures offer flexibility but significantly increase exposure to systemic vulnerabilities:

- correlation shocks  
- oracle manipulation  
- liquidation cascades  
- illiquidity failures  
- complexity-driven black swans

For ProjectUSD:

> **A single-collateral model provides maximum structural safety.  
> Multi-collateral is only viable under strict risk controls.**

Expansion is possible, but must be:

- isolated,  
- parameterized,  
- algorithmically safe,  
- and kept as simple as possible.

---

# 9. Verification

> ## 📘 Reviewer Checklist
- Are all multi-collateral risk vectors correctly identified?  
- Are liquidation dynamics fully explained?  
- Is the correlation analysis realistic?  
- Are stress scenarios complete and plausible?  
- Are recommendations logically consistent with system design?  

This study forms the basis for advanced security engineering and future multi-asset research within ProjectUSD.
