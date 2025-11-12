---
title: "ProjectUSD – Controller SPEC v1"
status: "Draft"
last_updated: "2025-11-12"
author: "Aqua75"
language: "en"
related_whitepaper_sections: ["Ch. 3 – Feedback Loop (R/r)", "Ch. 5.3 – Rate Limiter & Security Stack", "Glossary p. 20–21"]
---

# ProjectUSD – Controller SPEC v1

## Purpose

The Controller is the core of the system.  
It translates the **error signal ε = P − R** (the difference between market price *P* and internal equilibrium price *R*) into a new **system rate r**, which affects all vaults and stability mechanisms.  
ProjectUSD replaces external peg promises with **feedback-based stabilization**.

---

## 1. Core Terms & Parameters

| Parameter | Description | Example | Unit |
|------------|-------------|----------|------|
| `R` | Equilibrium price (ProjectUSD → PLS) | 1.0000 | PLS per internal USD |
| `P` | Market price (ProjectUSD on DEX / MedianTWAP) | 0.998–1.002 | PLS per USD |
| `ε` | Deviation = P − R | — | PLS per USD |
| `r` | System rate (interest/debt rate per epoch) | 0 – 0.05 | 1/epoch |
| `EpochLength` | Duration of one control cycle (e.g. 3600 blocks) | — | Blocks |
| `Kp` | Proportional gain of the controller | 0.5 – 1.5 | — |
| `Deadband` | Range within which ε is ignored | 0.001 (0.1%) | relative |
| `δr_max` | Maximum rate change per epoch (rate limiter) | 50 bp | — |
| `SurplusBuffer` | System buffer for smoothing r via fees | — | ProjectUSD |
| `LimiterHit%` | Share of epochs hitting the δr_max boundary | — | % of epochs |

---

## 2. Algorithmic Principle

```solidity
function controllerStep() external {
    epsilon = P - R;

    if (abs(epsilon / R) < Deadband) return; // no change

    delta_r = Kp * (epsilon / R);

    // Rate limiter
    delta_r = clamp(delta_r, -δr_max, +δr_max);

    r_next = r_prev + delta_r;

    emit ControllerUpdate(epsilon, r_next, block.number);
}
```
Explanation:

- Positive ε (P > R) → r increases → borrowing becomes more expensive → issuance slows down → P decreases.
- Negative ε (P < R) → r decreases → borrowing becomes cheaper → issuance rises → P increases.
- Result: P oscillates around R – stability through movement, not fixation.

---

## 3. Invariants

| ID | Condition | Meaning |
|----|------------|----------|
| I1 | &#124;P−R&#124;/R ≤ 2 % over N epochs in equilibrium | Peg remains within defined tolerance |
| I2 | &#124;Δr&#124; ≤ δr_max always | Rate limiter works correctly |
| I3 | `r ≥ 0` and `r ≤ r_cap` | No negative or explosive interest rates |
| I4 | `SurplusBuffer ≥ 0` | Buffer can never become negative |
| I5 | `LimiterHit% < 25 %` | System operates mostly within normal bounds |

---

## 4. Telemetry & Metrics

| KPI            | Description                        | Source                |
| -------------- | ---------------------------------- | --------------------- |
| `PegDeviation` | |P − R| / R in basis points        | MedianTWAP aggregator |
| `HalfLife_P→R` | Time for deviation to halve        | Controller log        |
| `rVolatility`  | Std. deviation of r over 30 epochs | r history             |
| `LimiterHit%`  | Epoch ratio where Δr = δr_max      | Controller log        |
| `SurplusLevel` | Level of the system’s fee buffer   | Accounting module     |

---

## 5. Integration in the System

- Controller queries Oracle Aggregator (MedianTWAP) once per epoch.

- The result (P) is processed by controllerStep().

- The resulting r_next is propagated to the VaultEngine and StabilityPool.

- Fee flows go to the SurplusBuffer and may smooth future r updates.

---

## 6. Safety Mechanisms

- Limiter: Prevents jumps greater than δr_max per epoch.
- Deadband: Filters DEX price noise.
- Failsafe: If Oracle status = STALE → Δr = 0.
- Transparency: All variables (r, ε, P, R) are public on-chain.
- AuditLog: Each rule update is logged with block number, ε, and r_next.

---

## 7. Tests (Minimum Requirements)

| Test ID | Description                  | Objective                                             |
| ------- | ---------------------------- | ----------------------------------------------------- |
| C-01    | Convergence test at ε = +1 % | r increases and peg returns within T epochs           |
| C-02    | Limiter test                 | Δr never exceeds δr_max                               |
| C-03    | Deadband test                | ε within band → r unchanged                           |
| C-04    | Oracle fail mode             | If status = STALE → Δr = 0                            |
| C-05    | Telemetry consistency        | All KPIs are logged and non-negative                  |
| C-06    | Stress simulation            | PLS −50 % → r reacts within limits and restores P → R |

---

## 8. Open Parameters (Design in Progress)

| Parameter     | Status                               | Next Step                                      |
| ------------- | ------------------------------------ | ---------------------------------------------- |
| `Kp`          | Simulation parameter (not finalized) | Backtesting on ±5 %, ±10 % deviation scenarios |
| `δr_max`      | Depends on chain volatility          | Empirical derivation from testnet runs         |
| `Deadband`    | Currently 0.1 %                      | Evaluation based on DEX noise profiles         |
| `EpochLength` | 3600 blocks                          | Validation in SimKit                           |
| `r_cap`       | 5 % per epoch                        | Open – economic trade-off evaluation           |

---

## 9. Verification (Testing & Validation Guide)

**Goal:**  
Demonstrate that the controller drives **P → R** within a defined half-life, without overshoot or undershoot.

**Methods:**

- **SimKit (Backtest)**  
  – Feed PLS price series with ±30 %, ±50 %, ±70 % shocks  
  – Apply `controllerStep()` once per epoch  
  – Metrics: half-life, limiter hit %, r volatility  

- **UnitTests (Foundry)**  
  – Run ε, deadband, and limiter test cases C-01 – C-04  

- **TelemetryAudit**  
  – Correlate ε → Δr in Subgraph  
  – Publish weekly *State of the Peg* reports  

**Acceptance Criteria:**  
Median peg deviation < 100 bp over 30 epochs; half-life ≤ 10 epochs; LimiterHit % < 25 %.

---

## 10. Notes & Risks

- The controller stabilizes the internal equilibrium price R only; the external USD value of PLS remains volatile.
- In cases of sustained low DEX liquidity, the oracle fallback and limiter mechanisms activate.
- Psychological panic behavior can extend deviations, but the system remains measurably stable.

---

## 11. License & References

© 2025 Aqua75 / ProjectUSD
License: MIT for code, CC BY-NC-SA 4.0 for documentation
Reference: ProjectUSD Whitepaper V2.1 (Ch. 3, 5.3, Glossary p. 20–21)



















