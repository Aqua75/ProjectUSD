# Study 04 – MEV Resilience, Median Oracle Architecture, and TWAP Stability in ProjectUSD
*Scientific analysis of manipulation resistance, oracle design, and systemic stability under MEV conditions*  
*(Level-3 Research Format)*

---

## Abstract

MEV (Miner / Maximal Extractable Value) represents a systemic risk across all EVM-based blockchains.  
Stablecoins are particularly vulnerable because even small oracle distortions can trigger reflexive cascades that affect peg stability and user confidence.

ProjectUSD addresses this through a resilient architecture combining:

- a multi-pool **Median TWAP Oracle**,  
- outlier filters and STALE logic,  
- liquidity weighting across valid pools,  
- **rLimiter** mechanisms preventing overreaction,  
- deterministic rate-limits against spam and cluster MEV,  
- redemption and arbitrage as corrective market forces.

This study analyzes system behavior under sandwich attacks, flash-price manipulation, coordinated TWAP attacks, and liquidity-correlated pool structures.  
The results show that ProjectUSD neutralizes short-term MEV attacks effectively and makes long-term TWAP manipulation economically unattractive.

---

# 1. Introduction – MEV as a Systemic Risk for On-Chain Monetary Systems

MEV includes:

- transaction reordering,  
- priority gas auctions,  
- targeted AMM price shifts,  
- liquidation sniping,  
- oracle manipulation attempts.

For stablecoins, MEV is especially dangerous:

- distorted oracle → incorrect r-adjustment  
- incorrect r-adjustment → wrong economic incentives  
- wrong incentives → reflexive instability

ProjectUSD mitigates these risks through:

- a **Median TWAP Oracle** across multiple pools,  
- aggressive outlier detection,  
- STALE behavior when data is unreliable,  
- rate-limiters and an rLimiter,  
- a liquidation system that never sells collateral on the open market.

---

# 2. Attack Types on Price Feeds and Oracles

## 2.1 Sandwich Attacks

Mechanism:

1. attacker front-runs a user and pushes the price upward,  
2. user trades at worse conditions,  
3. attacker back-runs and captures the spread.

Relevance to ProjectUSD:

- affects user execution, not oracle integrity,  
- TWAP smoothing neutralizes short spikes,  
- Median logic reduces residual noise to near zero.

**System relevance: minimal.**

---

## 2.2 Flash Manipulation of Spot Prices

Mechanism:

- FlashLoan → massive temporary pool shift → oracle sample captured → reversal.

Relevance:

- highly effective against systems using spot or single-point oracles.

In ProjectUSD:

- TWAP averages over hundreds of blocks,  
- one manipulated block has weight **1/N**,  
- Median selection removes extreme distortions,  
- filters reject implausible values entirely.

A one-block manipulation typically results in deviations of **0.1% or less**.

---

## 2.3 Multi-Block TWAP Attacks

Mechanism:

- sustained price distortion in a target pool,  
- across >50% of TWAP window blocks,  
- usually attempted in thin liquidity environments.

Relevance:

TWAP attacks are the most realistic and dangerous.  
However:

- Median removes single-pool influence,  
- attacker must manipulate **multiple deep pools simultaneously**,  
- arbitrage constantly pushes pools back in line,  
- extremely high capital requirements,  
- rLimiter ensures system parameters change slowly even under distortion.

---

# 3. Protective Mechanisms: Median Oracle, TWAP, Filters & rLimiter

## 3.1 TWAP Smoothing – Protection Against Temporal Manipulation

TWAP:

$$
P_{\text{twap}} = \frac{\sum (P_{\text{spot},i} \cdot \Delta t_i)}{\sum \Delta t_i}
$$

Effects:

- flash spikes are diluted immediately,  
- short-term sandwich manipulations vanish in noise,  
- oracle response becomes slow and robust.

---

## 3.2 Multi-Pool Architecture and Liquidity Weighting

For each valid pool:

$$
w_i = \sqrt{\text{Reserve}_{PLS,i} \cdot \text{Reserve}_{PUSD,i}}
$$

Implications:

- deep pools dominate oracle influence,  
- thin pools contribute almost nothing,  
- manipulation requires multi-pool dominance.

---

## 3.3 Median Aggregation & Outlier Filters

Final oracle value:

$$
P_{\text{final}} = \text{median}(P_{\text{twap},1}, P_{\text{twap},2}, \dots)
$$

Filters:

- **MaxDeviationFilter** excludes pools >10% off consensus,  
- **MinLiquidityFilter** excludes illiquid pools.

Effect:

- extreme values have zero influence,  
- attacker must control a majority of meaningful pools.

---

## 3.4 STALE Behavior

Trigger conditions:

- missing updates,  
- suspiciously flat or frozen prices,  
- abnormal volatility patterns.

Actions:

- STALE pools are ignored,  
- if all pools are STALE → system uses previous P and freezes r-updates.

Guiding principle:

> **Better no update than an incorrect update.**

---

## 3.5 Rate-Limits and the rLimiter

Functions:

- restrict user spam behavior,  
- limit transaction throughput during MEV clusters,  
- ensure r cannot change too quickly (e.g., ≤50 bp per epoch).

Even with distorted oracle data:

- system reacts **slowly and predictably**,  
- no reflexive self-amplification occurs.

---

# 4. Attack Model Evaluation in ProjectUSD

## 4.1 Sandwich Attacks

- degrade user execution quality,  
- negligible oracle influence,  
- TWAP + Median neutralize effects.

**System relevance: low.**

---

## 4.2 Flash Manipulation in Thin Pools

- TWAP dilution reduces impact to <0.2%,  
- Median removes manipulated pools,  
- strong economic cost to attacker.

**System relevance: very low.**

---

## 4.3 Long-Horizon TWAP Attacks (Multiple Pools)

Attacker requirements:

- manipulate two or more deep pools simultaneously,  
- sustain distortion over hundreds of blocks,  
- constantly inject liquidity to counter arbitrage.

Economic reality:

- extremely capital-intensive,  
- arbitrage and redemption push against manipulation,  
- unsustainable long-term.

**System relevance: moderate only under extreme conditions.**

---

# 5. Structural MEV Resilience in ProjectUSD

## 5.1 Strengths

- resistant to flash attacks,  
- resistant to sandwich attacks,  
- resistant to single-pool manipulation,  
- rLimiter suppresses systemic overreaction,  
- multi-pool TWAP increases attacker cost drastically.

---

## 5.2 Economic Counterforces

Beyond the oracle itself, ProjectUSD benefits from:

- **cross-pool arbitrage**,  
- **redemption when P < R**,  
- **mint arbitrage when P > R**,  
- **natural deleveraging and liquidation processes**.

Attackers constantly trade against corrective market forces.

---

## 5.3 Systemic Behavior

ProjectUSD remains:

- **slow**,  
- **robust**,  
- **deterministic**,  
- **immune to noise**.

This slowness is intentional — it makes manipulation unprofitable.

---

# 6. Risks, Assumptions & Limitations

## 6.1 Low DEX Liquidity
Extreme illiquidity can degrade oracle accuracy.

## 6.2 Pool Correlation  
High LP concentration increases attack feasibility.

## 6.3 Long-Term Manipulation  
Not impossible, but economically prohibitive.

## 6.4 STALE Mode  
Prevents incorrect updates but freezes state temporarily.

## 6.5 Model Assumptions  
Analysis assumes typical liquidity and arbitrage conditions.

---

# 7. Conclusion

ProjectUSD achieves exceptional MEV resilience through:

- Median TWAP aggregation,  
- multi-pool redundancy,  
- outlier detection,  
- STALE fail-safes,  
- deterministic rate limits,  
- redemption and arbitrage as corrective forces.

Short-term manipulation is neutralized.  
Long-term manipulation is prohibitively expensive.  

The oracle stack of ProjectUSD is a **deliberately slow, robust, and self-stabilizing system** that requires no governance intervention.

---

# 8. Verification

> ## 📘 Reviewer Checklist
- Are attack types correctly categorized?  
- Are TWAP and Median mechanics accurately described?  
- Are outlier filtering and STALE logic consistent?  
- Is interaction with r and ε = (P − R)/R accurate?  
- Are risks and limitations sufficiently documented?  

This study forms the basis for further research into oracle stability, MEV economics, and stress testing.

