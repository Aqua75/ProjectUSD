# Study 01 – Controller Dynamics & Price Feedback Mechanism in ProjectUSD
*Scientific Analysis of the Algorithmic Monetary Feedback Loop in an Autonomous On-Chain System*  
*(Level-3 Research Format)*

---

## Abstract

ProjectUSD is a fully on-chain, algorithmic monetary system on PulseChain. Its price stability is not derived from external oracles, banks, governance, or discretionary human intervention, but from an **internal feedback loop** between:

- the market price **P**,  
- the equilibrium price **R**,  
- and the system rate **r**.

This study analyzes the mathematical structure of this controller, which measures deviations between the market price and the equilibrium price and adjusts **r** to influence the economic behavior of borrowers, holders, and arbitrageurs.

We develop a formal model for price deviation, derive convergence conditions, and discuss four core scenarios: overvaluation, undervaluation, extreme volatility, and low liquidity.

---

# 1. Introduction – Algorithmic Feedback Instead of Centralized Monetary Control

ProjectUSD replaces classical central banking mechanisms with **deterministic, immutable logic**.

The feedback loop operates as follows:

1. DEX markets determine the spot price **P**.  
2. The oracle produces a smoothed value via Median-TWAP.  
3. The controller measures the deviation between **P** and **R**.  
4. The system rate **r** is adjusted accordingly.  
5. Changes in **r** affect supply, demand, borrowing incentives, and arbitrage.  
6. These forces guide **P → R** over time.

This creates an internal regulatory cycle that maintains monetary equilibrium without external influence.

---

# 2. System Overview

## 2.1 Core Components of ProjectUSD

### **Vaults**
- Users deposit PLS as collateral  
- mint ProjectUSD  
- undercollateralized positions are liquidated automatically

### **Stability Pool**
- absorbs liquidations  
- burns ProjectUSD supply  
- distributes PLS gains to pool participants

### **Redemption Engine**
- allows redemption of ProjectUSD at **R**  
- creates an arbitrage-driven internal price anchor  
- reduces the weakest vaults

Together, these components form a closed monetary mechanism when combined with the controller.

---

## 2.2 Definition of Key Variables

- **Rₜ** – equilibrium price (redemption price)  
- **Pₜ** – market price from the oracle  
- **rₜ** – system rate (interest / savings rate)  
- **εₜ** – relative price deviation  

$$
\varepsilon_t = \frac{P_t - R_t}{R_t}
$$

- **EpochLength** – number of blocks per controller update

---

## 2.3 The Controller as a Regulator

> ## 📘 Definition – Controller Logic  
> The controller converts price deviations into adjustments of **r**, guiding **P → R**.

### 1. Price Deviation

$$
\varepsilon_t = \frac{P_t - R_t}{R_t}
$$

### 2. Deadband Check

$$
|\varepsilon_t| < \varepsilon_{\text{db}} \Rightarrow \Delta r_t = 0
$$

### 3. Proportional Adjustment

$$
\Delta r_t = K_p \cdot \varepsilon_t
$$

### 4. Rate Limiter

$$
\Delta r_t^{\text{clamped}} =
\max\left(-\delta r_{\max}, \min(\delta r_{\max}, \Delta r_t)\right)
$$

### 5. New System Rate

$$
r_{t+1} = \text{clip}(r_t + \Delta r_t^{\text{clamped}}, 0, r_{\text{cap}})
$$

---

# 3. Mathematical Analysis

## 3.1 Price Deviation

> ## 📘 Definition – Relative Peg Deviation

$$
\varepsilon_t = \frac{P_t - R_t}{R_t}
$$

---

## 3.2 Proportional Control Function

$$
\Delta r_t =
\begin{cases}
0, & |\varepsilon_t| < \varepsilon_{\text{db}} \\
K_p \varepsilon_t, & \text{otherwise}
\end{cases}
$$

---

## 3.3 Simplified Dynamic Model

> ## 📘 Model – Linear Price Approximation

Approximate deviation based on supply Sₜ and demand Dₜ:

$$
\varepsilon_t \approx \alpha \cdot \frac{S_t - D_t}{D_t}
$$

Rate impact:

$$
\Delta S_{t+1} \approx -\beta_s \Delta r_t
$$

$$
\Delta D_{t+1} \approx +\beta_d \Delta r_t
$$

Recursive deviation dynamics:

$$
\varepsilon_{t+1} \approx (1 - \kappa K_p)\varepsilon_t
$$

> ## 📘 Theorem – Convergence Condition  
> The controller stabilizes the system **if and only if**:
>
> $$
> 0 < \kappa K_p < 2
> $$

---

# 4. Simulation Scenarios

## 📊 Scenario 1 – Overvaluation (P > R)

When the market price stands above the equilibrium price:

- r increases  
- new borrowing becomes less attractive  
- users mint and sell additional ProjectUSD  
- P gradually moves downward toward R  

This scenario describes a controlled downward convergence of the market price toward the internal equilibrium value.

---

## 📊 Scenario 2 – Undervaluation (P < R)

When the market price is below the equilibrium price:

- r decreases  
- redemption arbitrage generates additional demand  
- P rises toward R  

This scenario illustrates an upward adjustment driven by arbitrage demand and reduced economic pressure on borrowers.

---

## 📊 Scenario 3 – Extreme Volatility

During sudden market shocks or rapid price fluctuations:

- the oracle (Median-TWAP) smooths the incoming price data  
- the controller reacts intentionally with delay to avoid overshooting  
- arbitrage rapidly corrects short-lived deviations  

This scenario highlights the interplay between smoothed oracle data, delayed controller response, and fast market-driven correction.

---

## 📊 Scenario 4 – Low Liquidity

In illiquid or potentially manipulated market conditions:

- illiquid or anomalous pools are filtered out  
- the controller may temporarily limit its activity  
- redemption becomes the primary stabilizing mechanism  

This scenario shows how the system relies on internal redemption dynamics when external market data becomes unreliable.

---

# 5. Discussion

## 5.1 Arbitrage as the Transmission Mechanism

Arbitrageurs translate controller incentives into market action:

- **P < R:**  
  Buy ProjectUSD → redeem at R → profit → P rises.

- **P > R:**  
  Mint ProjectUSD → sell above R → repay debt later → P falls.

---

## 5.2 Market Psychology

> ## 📘 Observation – Expectations as Amplifiers

- Confidence stabilizes  
- Fear magnifies deviations  

Transparent metrics (e.g., peg deviation, half-life) strengthen credibility.

---

## 5.3 Reaction Times

- **Seconds–Minutes:** DEX noise  
- **Epoch scale:** controller updates  
- **Weeks:** structural reallocation of collateral, debt positions, and pool deposits  

---

# 6. Limitations & Risks

## 6.1 Delays
- Oracle TWAP delay  
- controller epoch delay  
- human behavioral delay  

## 6.2 Oracle Bias
- liquidity bias  
- stale data  
- need for filtering mechanisms  

## 6.3 Stress Conditions
- liquidation cascades  
- dominance of forced sales over normal market behavior  
- rate limiter saturation  

## 6.4 Parameter Risk
- Kₚ too high → oscillation  
- Kₚ too low → sluggish reversion  
- problematic combinations with EpochLength  

## 6.5 Psychological Risks
- overconfidence  
- panic reflexivity  

---

# 7. Conclusion

The controller is a core component of ProjectUSD’s autonomous stability architecture.  
It measures deviations between **P** and **R** and adjusts **r** to influence the incentives of borrowers, savers, and arbitrageurs.

In combination with:

- redemption  
- the stability pool  
- oracle filtering  

the system forms a closed feedback loop designed to bring **P → R** over time.

Robust stability requires careful parameter calibration, sufficient liquidity, and efficient arbitrage.

---

# 8. Next Steps

- Construction of a dedicated simulation framework (SimKit)  
- systematic stress testing  
- parameter calibration (Kₚ, ε_db, δr_max, EpochLength)  
- monitoring metrics such as PegDeviation, HalfLife(P → R), LimiterHit-Rate  
- extending models to nonlinear AMM behavior  

---

# 9. Verification

> ## 📘 Reviewer Checklist

- Parameter consistency with official specifications  
- correctness of all mathematical derivations  
- reproducibility of scenario results  
- coherence across controller ↔ oracle ↔ redemption ↔ stability pool  
- validation that in realistic parameter ranges:
  
$$
0 < \kappa K_p < 2
$$
