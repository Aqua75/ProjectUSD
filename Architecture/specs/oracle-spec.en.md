```markdown
title: "ProjectUSD – Oracle SPEC v1"
status: "Draft"
last_updated: "2025-11-14"
author: "Aqua75"
language: "en"
related_whitepaper_sections: ["Ch. 4 – Price Signals", "Ch. 5.2 – MedianTWAP", "Glossary pp. 22–24"]
ProjectUSD – Oracle SPEC v1

## Purpose

The oracle provides the market price P of the ProjectUSD Coin in PLS to the controller.
It is the primary external input for the error signal:

`ε = P − R`

Because ProjectUSD operates entirely without off-chain price feeds, banks, or centralized data sources,
the oracle must:

operate fully on-chain

resist manipulation

remain functional during low-liquidity conditions

incorporate multiple DEX pools

fail safely without creating instability

This document describes the v1 design:
MedianTWAP across multiple DEX pools, weighted by liquidity.

---

## 1. Core Principles

The ProjectUSD Oracle (v1) is built on four fundamental ideas:

TWAP (Time-Weighted Average Price)
→ smooths out individual trades and short-term manipulation attempts.

Multiple Pools
→ reduces attack surface by combining several independent price sources.

Liquidity Weighting
→ deeper pools carry more informational weight than shallow ones.

Median Filtering
→ eliminates outliers (e.g., manipulated pools).

---

## 2. Data Sources (DEX Pools)

The oracle uses only PulseChain DEX pools that trade ProjectUSD Coin against PLS.

Defined as:

- Pool1: ProjectUSD/PLS (DEX A)
- Pool2: ProjectUSD/PLS (DEX B)
- Pool3: ProjectUSD/PLS (DEX C)

...

Restrictions:

- only pools with sufficient historical liquidity
- only pools with valid reserve structure (no empty or paused pairs)
- only pools using constant-product logic (x * y = k) or V3 √K liquidity model

---

## 3. Price Computation per Pool

### 3.1 Instant Price (Spot)

Spot price of an AMM pool:
`P_spot = (Reserve_PLS / Reserve_ProjectUSD)`

### 3.2 TWAP per Pool

Each pool computes a TWAP over N blocks:
`P_twap = Σ (P_spot_i * Δt_i) / Σ Δt_i`

Parameters:

TWAPWindow = 900–3600 blocks

MinObservations = 3

### 3.3 Liquidity Weighting

Each pool receives a weight proportional to its depth:
`w_i = sqrt(Reserve_PLS_i * Reserve_ProjectUSD_i)`

This prevents shallow pools from distorting the result.

---

## 4. Aggregation Across Pools

### 4.1 Weighted Price

Per-pool weighted price:
`P_weighted_i = P_twap_i * w_i`

Aggregated price:
`P_agg = (Σ P_weighted_i) / (Σ w_i)`

### 4.2 Median Filtering

The final stabilization uses a median across all valid TWAP values:
`P_final = median(P_twap_1, P_twap_2, ..., P_twap_n)`

Rationale:

robust against outliers

resistant to single-pool manipulation

ideal across varying liquidity profiles

Final oracle output:
`P = P_final`
Unit: PLS per ProjectUSD Coin (market price)

---

## 5. Fail-Safe / STALE Mode

A pool is considered STALE if:

no new observations within STALEWindow

reserves remain unchanged despite DEX activity

TWAP cannot be computed

an on-chain reserve slot error is detected

Rules:

STALE pools are ignored for the current epoch.

If all pools become STALE → oracle outputs `P = P_prev` (freeze).

The controller then sets `Δr = 0`
(see Controller SPEC).

This prevents a broken pool from destabilizing the system.

---

## 6. Safety Mechanisms

- Time dilation – minimum TWAP duration to prevent flash manipulation
- Reserve Check – validates that `x * y` remains within stable bounds
- MaxDeviationFilter – pools deviating >10% from the median are disqualified
- MinLiquidityFilter – pools below LiquidityFloor are ignored
- STALE Marker – automatic tagging of faulty pools

---

## 7. Integration with the Controller

Per-epoch process:

- Oracle collects TWAP data from all pools.
- Filters are applied (STALE, MinLiquidity, MaxDeviation).
- Median is computed.
- Value is published as P.
- Controller reads P and computes `ε = P − R`.
- Controller produces the new r_next.

All values are logged on-chain, e.g.:

OracleUpdate(P, poolsUsed, block.number)

---

## 8. Open Parameters (Design in Progress)

| Parameter        | Status          | Next Step                           |
| ---------------- | --------------- | ----------------------------------- |
| `TWAPWindow`     | 900–3600 blocks | calibration via SimKit              |
| `LiquidityFloor` | open            | analyze historical PulseX liquidity |
| `MaxDeviation`   | 10 %            | empirical confirmation required     |
| `PoolWhitelist`  | dynamic         | depends on DEX landscape            |
| `STALEWindow`    | open            | define realistic block duration     |

Note: All elements clearly marked as “Design in Progress,” per quality standard.

---

## 9. Verification (Testing & Validation Guide)

Goal:
Demonstrate that P remains stable, robust, and manipulation-resistant through TWAP + median filtering.

Methods:

SimKit Backtests
– TWAP response to large trades
– simulated liquidity drops
– flash manipulation tests

Manipulation Tests
– sandwich attacks
– fake-liquidity pools
– single-pool attacks

TelemetryAudit
– compare P_twap vs. P_spot
– deviation from per-pool median
– STALE-status monitoring

Acceptance Criteria:

median deviation < 1% across 90% of epochs

no flash-manipulation window within TWAPWindow

oracle failure results in controlled `Controller-Δr = 0`

---

## 10. Planned Enhancements

This section intentionally describes future features that are not part of the v1 design.

Potential extensions:

MAD Filter (Median Absolute Deviation)
→ stronger outlier detection

Volatility Channel (internal PLS-volatility indicator)
→ filtering extreme market phases

Multi-stage smoothing
→ combination of MedianTWAP and predictive bands

These features will be added only after backtesting and simulation.

---

## 11. License & References

© 2025 Aqua75 / ProjectUSD
License: MIT for code, CC BY-NC-SA 4.0 for documentation
Reference: ProjectUSD Whitepaper V2.1 (Ch. 4, 5.2, Glossary pp. 22–24)
