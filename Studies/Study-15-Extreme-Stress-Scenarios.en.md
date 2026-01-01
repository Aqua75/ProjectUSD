# Study 15 – Extreme Stress Scenarios  
*Extreme stress testing, worst case scenarios and Black Swan resilience*  
*(Level-3 Research Format)*

---

## Abstract

ProjectUSD is designed as a fully on-chain, autonomous monetary system without admin keys, without a pause mechanism and with an immutable core after the freeze event.  
This architecture maximizes credibility and neutrality, but shifts the full responsibility for stability and survivability to **mechanics, parameter choices and market incentives**.

This study examines the robustness of ProjectUSD under extreme but plausible stress conditions:

- 90 percent price crash of the primary collateral PLS  
- sudden liquidity exodus from DEXs  
- chain reorgs and unstable finality  
- MEV extreme phases including front running and sandwiching  
- combined cascade scenarios

The objective is to analyze under which conditions ProjectUSD survives systemically, where its structural limits lie, and which measures increase Black Swan resilience.

---

# 1. Introduction – Why extreme stress tests are essential

ProjectUSD follows a clear design philosophy:

- full on-chain autonomy  
- no admin key  
- no pause button  
- immutable core after the freeze event  
- governance limited to a peripheral layer

Classical emergency interventions are intentionally excluded.  
Stability must emerge from:

- overcollateralization  
- liquidation mechanics  
- the Stability Pool  
- the Redemption Engine  
- a feedback controller via the interest rate r

Extreme stress testing is therefore not optional, but a **mandatory prerequisite** for a credible system.

---

## 1.1 System components under stress

Four core mechanism blocks are particularly critical in Black Swan scenarios:

**Vaults and liquidations**  
Users primarily deposit PLS as collateral. If the collateral ratio falls below the liquidation threshold, the vault is forcibly liquidated.

**Stability Pool**  
The Stability Pool absorbs debt from liquidated vaults and receives their collateral in return. Excess supply is burned. The goal is stress absorption rather than escalation.

**Redemption Engine**  
ProjectUSD can always be redeemed against collateral at the equilibrium price R. The weakest vaults are reduced first, acting as an internal price anchor.

**Controller and interest rate r**  
Deviations between market price P and equilibrium price R adjust r. Higher r discourages demand, lower r incentivizes minting. Adjustments are deliberately rate limited.

---

# 2. Stress scenarios

## 2.1 Scenario matrix

Five primary scenarios are defined:

**S1 – 90 percent PLS crash**  
Abrupt collapse of the primary collateral price within a short time window.

**S2 – Liquidity exodus**  
Mass withdrawal of DEX liquidity and sharply reduced trading volume.

**S3 – Reorg storm**  
Series of chain reorgs with unstable transaction finality.

**S4 – MEV supercycle**  
Extremely elevated MEV activity with front running, sandwiching and backrunning.

**S5 – Four Horsemen cascade**  
Combination of all above effects with self reinforcing feedback loops.

---

## 2.2 Stress parameters

Scenarios are modeled using parameter vectors:

- PLS price processes with jumps and aftershocks  
- DEX liquidity drops between 70 and 95 percent  
- oracle delay and noise  
- reorg depth and frequency  
- MEV intensity and adversarial block share

---

## 2.3 Success criteria

A scenario is considered passed if:

1. **Solvency** is preserved or deficits are clearly socialized  
2. **Peg resilience** holds with deviations remaining temporary  
3. **Functionality** of liquidations and redemptions is maintained  
4. **Manipulation resistance** against oracle and MEV attacks persists

---

# 3. Simulation framework

This study is conceptual. Concrete parameters are intentionally not finalized and must be calibrated prior to implementation.

---

## 3.1 State variables

- vaults with collateral, debt and collateral ratio  
- Stability Pool balance  
- total supply  
- DEX liquidity and price impact  
- oracle state  
- controller interest rate r  
- surplus buffer

---

## 3.2 Liquidation logic

Undercollateralized vaults are liquidated. The Stability Pool absorbs their debt and receives collateral.

**Open core question**  
What happens if the Stability Pool is insufficient?

Possible fallback options:

- external liquidations  
- debt redistribution  
- coverage via the surplus buffer

Without an explicit rule, worst case solvency cannot be proven.

---

## 3.3 Redemption mechanics

Redemptions contract supply and support the peg, but remove collateral from the weakest vaults. In illiquid conditions, this can amplify stress.

---

## 3.4 Oracle and network model

- median TWAP oracle with outlier filtering  
- increased lag under low liquidity  
- reorgs can distort oracle windows and transaction ordering

---

## 3.5 MEV layer

- sandwiching  
- front running  
- backrunning of liquidations and redemptions

Protective measures exist but do not guarantee full immunity.

---

## 3.6 KPIs

- peg deviation and recovery time  
- liquidation volume  
- Stability Pool depletion  
- oracle error  
- r volatility  
- estimated MEV extraction  
- user cost via gas and slippage

---

# 4. Scenario analysis

## 4.1 S1 – 90 percent PLS crash

A 90 percent price collapse scales every collateral ratio by a factor of 0.1.

Example:

- 300 percent CR becomes 30 percent  
- maintaining 170 percent would require roughly 1700 percent beforehand

Result:  
Such a crash liquidates nearly all normally leveraged vaults.

---

## 4.2 Stability Pool under extreme stress

- rapid depletion of the Stability Pool  
- concentration of collateral among SP depositors  
- psychological risk of a Stability Pool run

---

## 4.3 Redemption during the crash

Redemption supports the peg but can further weaken the collateral base, especially with oracle lag and illiquid markets.

---

## 4.4 S2 – Liquidity exodus

Reduced volume slows arbitrage. Oracle data becomes lagged and noisy. Peg deviations may persist longer.

---

## 4.5 S3 – Reorg storm

Reorgs can:

- revert liquidations  
- reorder execution priority  
- distort oracle windows

Without a pause mechanism, reorg resilience must be solved architecturally.

---

## 4.6 S4 – MEV supercycle

MEV primarily causes:

- value leakage  
- higher user costs  
- additional liquidity drain

The peg may hold formally while confidence erodes.

---

## 4.7 S5 – Cascade

Protective mechanisms may work against each other:

- liquidations  
- oracle lag  
- MEV  
- reorgs

Peg recovery time increases significantly. Trust becomes the critical variable.

---

# 5. Measures and design implications

## 5.1 Conservative design before freeze

- guarded launch  
- low debt caps  
- no AMOs or PSMs  
- intensive on-chain monitoring

---

## 5.2 Mitigating single collateral risk

- higher recommended collateral ratios  
- explicit fallback liquidation rules  
- long term collateral diversification

---

## 5.3 Measures against liquidity exodus

- deep reference trading pairs  
- PSM strictly as a shock absorber  
- tightly budgeted AMOs

---

## 5.4 Reorg resilience

- reorg safe oracle windows  
- idempotent liquidations  
- clear backlog fairness rules

---

## 5.5 MEV resilience

- batching  
- commit reveal for large redemptions  
- MEV aware execution  
- transparent on-chain telemetry

---

## 5.6 Surplus buffer

- clearly defined activation rules  
- hard caps  
- no implicit bailout guarantee

---

# 6. Conclusion

ProjectUSD is designed as a self regulating, autonomous monetary system. Precisely because no human intervention is possible, Black Swan risks must be fully addressed before the freeze event.

Key conclusions:

- single collateral systems are structurally stressed by 90 percent crashes  
- liquidity exodus prolongs peg deviations  
- MEV creates friction even without formal peg failure  
- reorgs represent a serious execution risk

The conservative path outlined in the whitepaper guarded launch followed by freeze remains the only credible approach to managing these risks.

---

# 7. Verification

> ## 📘 Reviewer checklist

- Are the stress scenarios realistic and complete  
- Are cascade effects logically consistent  
- Are open design questions clearly identified  
- Is the reasoning aligned with the ProjectUSD design  
- Can the scenarios be translated into simulations and testnet tests

This study serves as the foundation for formal simulations, audits and testnet stress testing prior to a final freeze event.
