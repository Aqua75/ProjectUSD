# Study 07 – The Breathing Dynamics of ProjectUSD: How r-Adjustment Absorbs Market Volatility
*Analysis of dynamic price stability through controller logic, arbitrage, and supply–demand reactions*  
*(Level-3 Research Format)*

---

## Abstract

ProjectUSD is a fully on-chain, autonomously regulated monetary system operating on PulseChain.  
Unlike fiat-backed stablecoins, its stability does not depend on external collateral but on a **dynamic feedback mechanism** that measures price deviations and adjusts the system rate **r** to activate counterbalancing economic forces.

This study examines the system’s **breathing dynamics**:  
How relative price deviations (ε = (P − R) / R), controller reactions (Δr), arbitrage via redemption, and supply–demand feedback loops collectively absorb volatility.  
We model the regulatory circuit, analyze stress behavior, and identify limits and boundary conditions for system stability.

---

# 1. Introduction – The Role of Dynamic Stability

## 1.1 Motivation

Conventional stablecoins rely on external collateral, central entities or money markets.  
Their stability is **imported** — dependent on fiat institutions, regulatory environments or off-chain infrastructure.

ProjectUSD follows a fundamentally different paradigm:

- no USD peg  
- no banks  
- no off-chain oracle dependency  
- no governance over the core monetary mechanism  

Its stability arises from **feedback dynamics**:  
The system measures price deviations and adjusts incentives to pull the market back toward equilibrium.

---

## 1.2 Dynamic vs. static stability

**Static stability**  
– Price remains tightly fixed around a target value  
– Requires external guarantees or rigid pegs

**Dynamic stability**  
– Price is allowed to move, but counteracting forces restore equilibrium  
– Similar to a damped oscillator

ProjectUSD intentionally relies on **dynamic stability**:

- R = internal equilibrium price  
- P = median TWAP market price  
- ε = relative price deviation  
- r = system rate regulating economic expansion or contraction

---

## 1.3 Research question

> How does ProjectUSD absorb market volatility through r-adjustment, arbitrage, and redemption — and under what conditions can this breathing mechanism fail?

This study analyzes:

- formal modeling of the regulatory loop  
- low- and high-volatility behavior  
- interaction between controller, supply dynamics and arbitrage  
- systemic limits and potential failure modes  

---

# 2. Model: Price deviations & r-response functions

## 2.1 Core variables

- **R** – equilibrium (redemption) price  
- **P** – market price (Median-TWAP)  
- **ε** – relative price deviation:  
  $$
  \varepsilon_t = \frac{P_t - R}{R}
  $$
- **r** – system rate  
- **t** – epoch index  

---

## 2.2 Oracle model: Filtering before control

The oracle uses:

- multiple DEX pools  
- liquidity weighting  
- TWAP per pool  
- median aggregation  
- outlier filters  
- STALE protections  

Final price:

$$
P = \text{median}(P_{\text{twap},1}, \dots, P_{\text{twap},n})
$$

The oracle produces a **smoothed, manipulation-resistant** signal for the controller.

---

## 2.3 Controller logic: ε → r

Relative deviation:

$$
\varepsilon_t = \frac{P_t - R}{R}
$$

If |ε| is within the deadband → r remains unchanged.

Otherwise:

$$
\Delta r_t = K_p \cdot \varepsilon_t
$$

Clamped:

$$
\Delta r_t = \text{clamp}(\Delta r_t,\ -\delta r_{\max},\ +\delta r_{\max})
$$

New system rate:

$$
r_{t+1} = r_t + \Delta r_t
$$

Interpretation:

- **ε > 0 (P > R)** → r increases → debt becomes expensive → minting slows → P decreases  
- **ε < 0 (P < R)** → r decreases → debt becomes cheaper → demand rises → P increases  

---

## 2.4 Supply and demand as functions of r

Approximate linearized forms:

**Minting supply:**

$$
E(r) \approx E_0 - \alpha_r (r - r_0)
$$

**Market demand:**

$$
D(r) \approx D_0 + \beta_r (-r)
$$

**Price impact through total quantity Q:**

$$
P(Q) \approx P^* - \gamma (Q - Q^*)
$$

Thus, r influences price indirectly through shifting supply and demand curves.

---

## 2.5 Local stability analysis

With small Kₚ and moderate price sensitivity:

$$
r_{t+1} = r_t + K_p \varepsilon_t
$$

$$
P_{t+1} = P^* - c(r_t - r^*) + u_t
$$

Eigenvalue analysis shows:

- damped oscillations are possible  
- monotonic convergence under well-chosen parameters  
- stability depends on Kₚ, deadband width, δr_max, arbitrage strength, and oracle smoothing  

---

# 3. Dynamics in volatile markets

## 3.1 Arbitrage & redemption as fast corrective forces

**P < R:**

- arbitrageurs buy ProjectUSD  
- redeem at R  
- supply contracts  
- P moves upward toward R  

**P > R:**

- minting (if r permits)  
- sell above R  
- supply expands → P falls  

Arbitrage = **fast mechanism**  
Controller = **slow systemic stabilizer**

---

## 3.2 Oracle as volatility filter

TWAP + median:

- dampen noise  
- prevent overreaction  
- shield the controller from manipulation  
- create a stable control input  

---

## 3.3 r as shock absorber during PLS volatility

Because ProjectUSD is valued in PLS, external USD volatility does not directly destabilize the system.

During a major PLS downturn:

1. vault liquidations occur  
2. ProjectUSD supply contracts  
3. P temporarily falls  
4. ε < 0 → controller lowers r  
5. demand rises  
6. P stabilizes near R  

---

# 4. Stress scenarios: low, medium, high

## 4.1 Low stress

- small price deviations  
- arbitrage quickly restores equilibrium  
- r remains stable or moves only slightly  
- P stays tightly centered around R  

---

## 4.2 Medium stress (intraday volatility)

- ε oscillates noticeably  
- r adjusts across several epochs  
- minor overshooting possible  
- redemption strengthens correction  

---

## 4.3 High stress (market panic, PLS crash)

Sequence:

1. liquidation cascades  
2. supply contraction  
3. temporary downward pressure on P  
4. arbitrage activates  
5. r decreases aggressively  
6. P returns to R corridor  

Thus, ProjectUSD generates **endogenous damping** against severe shocks.

---

# 5. Analysis of the breathing mechanism

## 5.1 Expansion (inhalation phase)

When P < R → ε < 0:

- r decreases  
- borrowing becomes attractive  
- demand increases  
- redemption reduces circulating supply  
- P rises toward R  

---

## 5.2 Contraction (exhalation phase)

When P > R → ε > 0:

- r increases  
- borrowing becomes expensive  
- demand falls  
- minting slows  
- P declines toward R  

---

## 5.3 Deadband & rate limiter

Deadband:

- prevents noise amplification  
- avoids unnecessary r-fluctuations  

Rate limiter:

- constrains Δr  
- protects against reflexive instability  
- produces a **smooth breathing rhythm** rather than volatility spikes  

---

## 5.4 Surplus buffer as long-term stabilizer

The surplus buffer:

- accumulates fees  
- supports negative-r phases  
- provides long-term system resilience  
- acts like a stored energy reserve for stabilization  

---

# 6. Limits & risks

## 6.1 Technical risks
- smart contract vulnerabilities  
- STALE oracle conditions freeze r updates  
- chain-level instability  

## 6.2 Economic risks
- low DEX liquidity → slow arbitrage  
- panic markets may override rational incentives  
- parameter setting (Kₚ, δr_max) crucial  

## 6.3 Open design questions
- optimal r-range  
- long-term average r behavior  
- interaction with future PSM/AMO modules  

---

# 7. Conclusion

ProjectUSD does not stabilize through rigid pegging but through an **adaptive, breathing equilibrium**.  
The relative price deviation ε, the controller response Δr, arbitrage, redemption, and supply dynamics form a feedback circuit that:

- absorbs shocks  
- restores equilibrium  
- produces systemic stability  

This breathing dynamic makes ProjectUSD a **self-stabilizing on-chain monetary system**, operable without external oracles, banks or governance intervention.

---

# 8. Verification

> ## 📘 Reviewer Checklist
- Is the correct formula for ε used consistently?  
- Is the ε → r controller mapping correctly described?  
- Are supply- and demand-based effects modeled coherently?  
- Are stability assumptions plausible?  
- Is the breathing mechanism logically complete?  

This study provides the foundation for further research on system dynamics, parameter optimization, and stress scenario simulation.
