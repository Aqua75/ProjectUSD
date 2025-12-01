# Study 02 – Liquidation Cascades and the Role of the Stability Pool in Stress Scenarios
*Scientific analysis of liquidation mechanics, risk transfer, and system stability under extreme market conditions*  
*(Level-3 Research Format)*

---

## Abstract

Liquidations are a central mechanism in ProjectUSD:  
they remove undercollateralized positions, destroy ProjectUSD supply, and transfer PLS collateral to Stability Pool participants.

This study investigates the system’s behavior during single liquidations, serial liquidations, and full liquidation cascades under stress conditions. Special focus is placed on:

- the interaction between Collateral Ratio (CR), price movements, and the liquidation threshold  
- the role of the Stability Pool as a shock absorber  
- the dynamics during strong price declines  
- the characteristics of cascades and their natural limits  
- the built-in mechanisms that prevent systemic instability

The analysis shows: liquidations are not a failure mode — they are a fundamental self-stabilizing force that keeps the system healthy during severe market conditions.

---

# 1. Introduction – Liquidations as a Stability Mechanism

In ProjectUSD, liquidations serve to:

- remove undercollateralized vaults  
- eliminate excess system debt  
- ensure that total collateral always exceeds total obligations  
- transfer PLS collateral to Stability Pool participants  
- reduce circulating ProjectUSD supply

Unlike centralized systems, ProjectUSD makes fully **algorithmic**, **deterministic** decisions — without governance, committees, or human intervention.

The liquidation module is designed to:

- intervene **early** (when CR falls below threshold)  
- execute **instantly**  
- leave behind **no bad debt**  
- avoid **market sell pressure**  
- require **no external backstops**  

Liquidations are therefore an active health mechanism, not an error state.

---

# 2. System Components and Key Concepts

## 2.1 Liquidation Threshold (LT)

The liquidation threshold defines when a vault becomes undercollateralized.  
Typically:

- **CR below 110% → liquidatable**  
- Vault is closed  
- Stability Pool pays off the debt  

---

## 2.2 Collateral Ratio (CR)

> ## 📘 Definition – Collateral Ratio
> The Collateral Ratio of a vault is defined as:
>
> $$
> CR = \frac{\text{Value of PLS Collateral}}{\text{ProjectUSD Debt}}
> $$

The CR determines whether a position is safe, risky, or subject to liquidation.

---

## 2.3 Stability Pool

The Stability Pool:

- absorbs liquidations  
- receives PLS collateral  
- deletes the corresponding ProjectUSD debt  
- prevents the creation of “toxic debt”  
- protects the system core during market stress

It functions as the **first line of defense** in down markets.

---

## 2.4 Liquidator Reward

Each liquidation produces a reward for Stability Pool participants, since they receive PLS collateral at an effective discount.

This creates a strong economic incentive to keep funds in the Stability Pool.

---

# 3. Dynamics of Single Liquidations

A single liquidation occurs when:

1. the PLS price drops  
2. a vault’s CR falls below the liquidation threshold  
3. the Stability Pool holds enough ProjectUSD to cover the debt  
4. the system automatically liquidates the vault

Process:

- Stability Pool pays the vault’s ProjectUSD debt  
- the vault is removed  
- collateral is transferred to the Stability Pool  
- a reward is realized  
- circulating ProjectUSD decreases  

This mechanism strengthens the system:

- **more collateral per remaining ProjectUSD**  
- **lower system debt**  
- **cleaner risk distribution**

---

# 4. Serial Liquidations (Normal Stress Phases)

During moderate price declines, liquidations typically occur in sequence:

- multiple vaults drop below LT one after another  
- the Stability Pool processes them individually  
- the collateral-to-debt ratio improves after each event  
- market conditions gradually stabilize

Economic properties:

- Stability Pool participants receive multiple rewards  
- ProjectUSD supply contracts  
- the system remains fully solvent  
- no systemic bad debt is created

Serial liquidations are typical in normal stress conditions.

---

# 5. Liquidation Cascades (Severe Price Crashes)

A liquidation cascade emerges when:

- the PLS price falls very quickly  
- many vaults cross the liquidation threshold simultaneously  
- the Stability Pool absorbs debt in rapid succession  

Characteristics of a cascade:

- **high liquidation frequency per block**  
- **rapid transfer of PLS to Stability Pool participants**  
- **strong contraction of ProjectUSD supply**  
- **removal of weak collateral positions**

Cascades are intense, but they lead to a **cleaner and more robust system state** after the crash.

---

# 6. Why Cascades Do Not Destabilize the System

In centralized architectures, cascades may cause systemic failure.  
In ProjectUSD, they serve the opposite purpose:  
they are a **self-correcting mechanism** that removes structural fragility.

Multiple properties ensure the system remains safe:

---

## 6.1 Negative Equity Cannot Occur

The system can **never** end up with more debt than collateralized value.  
Each liquidation removes both:

- collateral  
- and debt  

This prevents system-wide debt accumulation.

---

## 6.2 Stability Pool Absorbs the Shock

The Stability Pool:

- receives PLS  
- destroys ProjectUSD debt  

This results in:

- higher collateral coverage  
- lower supply  
- safer remaining debt positions

Cascades **strengthen** collateralization.

---

## 6.3 Redemption as an Additional Stability Layer

If P drops below R, redemption arbitrage activates:

- buy ProjectUSD  
- redeem for PLS  
- weak vaults are closed  
- the system rebalances

Redemption continues to function even during cascades.

---

## 6.4 Liquidations Do Not Create Sell Pressure

A critical property:

- liquidations **do not sell** PLS on the market  
- no forced dumping occurs  
- PLS is transferred internally  
- market price P remains unaffected by liquidation execution  

This prevents spiraling price declines.

---

## 6.5 System-Wide Rebalancing Is Self-Stabilizing

After a cascade, the system typically ends up with:

- higher overcollateralization  
- stronger vault structures  
- lower supply  
- risk concentrated in the most robust participants  

The system is **safer after a cascade** than before the crash.

---

# 7. User Roles and Incentives

## 7.1 Stability Pool Participants  
- receive PLS rewards  
- absorb liquidation shocks  
- benefit from discounted collateral  

## 7.2 Vault Users  
- take market risk  
- may be liquidated  
- contribute to deleveraging events  

## 7.3 Arbitrageurs  
- stabilize P → R  
- accelerate recovery after stress  

---

# 8. Conclusion

Liquidations are a fundamental stabilizing force in ProjectUSD.  
They:

- prevent systemic bad debt  
- strengthen collateralization  
- reallocate risk efficiently  
- support natural deleveraging  
- perform extremely well under stress  

Liquidation cascades are not a system defect — they are an essential reset mechanism that enhances long-term resilience after strong market movements.

---

# 9. Verification

> ## 📘 Reviewer Checklist
- Is the description consistent with the official specification?  
- Are liquidation flows internally coherent?  
- Does no negative equity arise at any point?  
- Is the role of the Stability Pool accurately modeled?  
- Are stress scenarios logically reproducible?  

This document provides the structural foundation for further studies on stress resilience, shock propagation, and the interplay between liquidations, the controller, and redemption dynamics.
