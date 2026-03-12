# Study 19 - Analysis of the Optimal Bounds of the System Rate r in the ProjectUSD Protocol
*Scientific examination of the permissible lower and upper bounds of `r` in the Core design of ProjectUSD*  
*(Level-3 Research Format)*

---

## Abstract

This study examines which lower and upper bounds for the system rate `r` in the ProjectUSD protocol are technically, economically, and systemically appropriate. At the center of the analysis is the question of how the bounds of `r` in the ProjectUSD Core can be determined in such a way that controllability, stability, and system robustness are preserved at the same time.

The analysis is based primarily on the normative Core specifications, since these would be binding after the freeze event. Of central importance is the fact that `r` is consistently defined in the documented Core as a nonnegative system rate or debt rate. Against this background, the study examines what consequences would arise if a negative range were hypothetically allowed, and why the documented lower bound at zero is systemically preferable.

The study further shows that a negative `r` in the current design would not simply represent a looser monetary stance, but would mechanically imply a reduction of Vault debt. This would not create a neutral stabilization impulse, but potentially a rule based transfer in favor of borrowers. Although a negative lower bound would extend the controller’s intervention range during underpeg phases, it would not create a guaranteed recovery mechanism. For an immutable protocol, the risks therefore outweigh the benefits.

The study concludes that under the currently documented Core architecture, the bound `0 ≤ r ≤ +20 %` is clearly preferable. Negative values of `r` are not illegitimate in autonomous monetary systems in principle, but in the present design they operate through the wrong channel and therefore should not be part of a frozen Core system.

---

# 1. Introduction

## 1.1 Problem Statement - The Question of the Lower Bound of r

ProjectUSD uses `r` as the central control variable of its internal stabilization mechanism. The controller measures deviations between the market price `P` and the equilibrium price `R` and adjusts the system rate `r` accordingly. This affects Vault incentives, debt dynamics, arbitrage behavior, and thus indirectly monetary stabilization.

The decisive open question, however, is how far `r` may extend downward.

Three basic options structure the analysis:

1. **Option A:** negative floor at `-5 %`  
2. **Option B:** negative floor at `-2 %`  
3. **Option C:** floor at `0 %`

At first glance, a negative range may appear attractive because it would provide the controller with additional room for action during prolonged underpeg phases. But in the current Core design, `r` acts directly on Vault debt. For that reason, the technical and economic meaning of a negative range is far more significant than a mere parameter debate might suggest.

## 1.2 Methodological Basis

This study is based primarily on the normative Core specifications, in particular:

- `controller-spec`
- `vaultengine-spec`
- `liquidation-redemption-spec`
- `Glossary`

These sources are authoritative because they would become binding after the protocol freeze. Studies and conceptual texts are considered additionally, but they do not have the same normative status. From this alone it follows that any hypothetical introduction of negative `r` values would have to be understood not merely as a parameter shift, but as an intervention in types, semantics, and accounting logic.

## 1.3 Two Preliminary Remarks

Two preliminary remarks are decisive for the analysis as a whole.

First, the documentation is now consistent on this point. Both the normative specifications and the revised studies define `r` throughout as a nonnegative system rate or debt rate. A negative value range is therefore not part of the documented Core architecture.

It follows directly that a negative floor cannot be understood as a documented design variant of the existing Core, but only as a hypothetical deviation from the established semantics of `r`.

Second, the transmission channel from `r` to the market price `P` is still not fully specified in mechanical terms. Some formulations suggest: `P < R -> r falls -> P rises`. However, the clearly defined onchain effect of a reduction in `r` in the current Core is only that Vault debt grows more slowly or shrinks. Whether this reliably results in price stabilization also depends on behavior, liquidity, and market conditions. For precisely that reason, the choice of a negative floor is especially sensitive.

---

# 2. System-Theoretical Analysis

## 2.1 Are Negative Rates Legitimate in Principle

Negative interest rates or negative control rates are not fundamentally illegitimate as regulatory instruments. In macroeconomics, negative interest rates have been used to stimulate borrowing, spending, and investment. In crypto as well, systems such as RAI have used positive and negative signals. It follows that an autonomous monetary system can in principle operate with a bidirectional signal.

## 2.2 What Matters Is Not the Sign, but the Transmission Channel

The mere existence of negative values says nothing by itself about their legitimacy in the concrete design. What matters is the point at which the signal acts.

In the case of RAI, the sign acts on redemption rate or target price dynamics, that is, on the internal price anchor. In the case of ProjectUSD, `r` acts directly on Vault debt according to the Core specification:

`debt_next = debt_prev * (1 + r_epoch)`

A negative `r` here would therefore not merely represent a looser monetary stance, but economically a rule based debt reduction. That is a qualitatively different actuator.

## 2.3 Structural Asymmetry of the Controller

A controller with `r ∈ [0, r_max]` is structurally asymmetric. Its range of action is cut off on the lower side. Formally, this yields a saturated controller:

`r_(t+1) = sat(r_t + K * ε_t, r_min, r_max)`

With `r_min = 0`, a persistently negative error `ε < 0` can lead into a region where the desired controller response would lie below the floor. Residual error then appears. The controller would want to loosen further, but cannot.

## 2.4 Interim Conclusion

From a system theoretical perspective, negative `r` can therefore in fact be legitimate, but only if the negative branch operates through a clearly defined channel with a bounded budget and an unambiguous target effect. In the currently documented ProjectUSD Core, this condition is not met. Therefore, the asymmetry of the controller does not by itself imply that negative values are necessary or advisable.

---

# 3. Economic Analysis

## 3.1 Mechanical Effect on Debt

In the current design, `r` is a debt rate. The following therefore applies directly:

`D_(t+1) = D_t (1 + r_t)`

For `r_t < 0`, it follows that:

`D_(t+1) < D_t`

This is not an interpretation, but mechanics. The borrower would owe less in the next epoch than before. A negative value would therefore mean direct relief of existing Vault debt.

## 3.2 Rationally Emerging Arbitrage Strategies

As soon as `r < 0` were allowed, several rational strategies would emerge:

- **Passive carry subsidy:** open a Vault, mint ProjectUSD, and simply hold while the debt declines automatically  
- **Leveraged external deployment:** mint ProjectUSD, use it elsewhere or move it into other assets while the liability declines  
- **Time arbitrage:** mint today and repay later with a smaller remaining debt

All three strategies would become more attractive the longer a negative phase lasted. Negative `r` would therefore not act neutrally, but as a systematic incentive in favor of borrowers.

## 3.3 Subsidy Character and Surplus Buffer

In the VaultEngine design, the difference `debt_next - debt_prev` flows system wide into the `surplusBuffer`. With positive `r`, this buffer grows. With negative `r`, the same logic would have to reduce the buffer. At the same time, `surplusBuffer ≥ 0` is defined as an invariant.

This creates a serious semantic tension. Either:

1. the `surplusBuffer` finances the debt reduction  
2. the implementation implicitly clips negative rates  
3. the invariant is violated

This exact question is not cleanly specified for a negative branch. For an immutable system, that is a central problem.

## 3.4 Long-Term Effect on Supply Dynamics

A frequently underestimated point is that negative `r` does not directly reduce the circulating token supply. It merely reduces the liabilities of borrowers.

This can create two simultaneous effects:

- existing debt is subsidized  
- new borrowing becomes more attractive

As a result, the probability increases that market participants will hold larger or longer running positions. This is especially relevant because stabilization during underpeg phases typically requires additional buybacks and redemption demand rather than weaker repayment pressure.

## 3.5 Magnitude of the Effect

An illustrative epoch calculation shows the scale:

- `r = -2 %` over 20 epochs reduces debt to approximately `0.98^20 ≈ 0.668`, or about **33 %** reduction  
- `r = -5 %` over 20 epochs reduces debt to approximately `0.95^20 ≈ 0.359`, or about **64 %** reduction

This shows that even seemingly small negative floors are by no means small in cumulative terms.

## 3.6 Consequences for Vault Incentives and Holders

If `r < 0` were allowed, Vaults would not merely become cheaper, but potentially turn into subsidy containers. This would shift incentives toward:

- higher desired leverage  
- longer position duration  
- lower urgency of repayment  
- lower willingness to buy back ProjectUSD on the market

Holders would receive no direct benefit from this. The primary beneficiary would be the borrower side, while the system would at the same time be burdened with a smaller buffer, a smaller future fee base, and potentially a larger outstanding debt volume. Economically, this would resemble a transfer from the system’s safety margin to borrowers.

## 3.7 Limiting Mechanisms Are Not Sufficient

Other system mechanisms limit the problem only partially:

- `DELTA_R_MAX` limits speed, not the cumulative transfer  
- minimum collateral ratios limit participation, not the sign of the transfer  
- the Stability Pool absorbs liquidations, not borrower subsidies  
- redemption tightens supply only if tokens are actually bought and redeemed

For that reason, these mechanisms do not transform negative `r` from a subsidy into a neutral signal.

---

# 4. Stress Scenario Analysis

## 4.1 Initial Scenario

The study considers a clear stress scenario:

- `P` remains below `R` for weeks  
- redemption targets are exhausted or practically inactive  
- arbitrage capital is absent  
- market confidence is weak

The real question is then not whether negative `r` could theoretically help, but whether under these conditions it would reliably bring the system back into equilibrium.

## 4.2 Development Without Negative r

Without negative values, the controller lowers `r` step by step to zero and saturates there. From that point onward, it loses additional loosening capacity. This is a real disadvantage because the system loses one degree of freedom.

## 4.3 Development With a Negative Floor

With a negative floor, the controller would gain additional room for action. This additional room can be described approximately as:

`N_extra ≈ |r_min| / Δr_max`

With an illustrative `Δr_max = 50` basis points per epoch, this would imply approximately:

- for **Option B** with `-2 %`, about four additional limiter bound epochs  
- for **Option A** with `-5 %`, about ten additional limiter bound epochs

This is the strongest argument in favor of a negative floor. It expands the active control range of the controller.

## 4.4 Why This Still Does Not Create a Reliable Recovery Mechanism

The decisive point, however, is that even with `r < 0`, the controller could not force recovery.

It:

- does not automatically buy tokens on the market  
- does not execute automatic buybacks  
- does not force redemption demand  
- does not create external arbitrage capital

It changes incentives only. In moderate stress, that may help. In deep stress with weak confidence and weak liquidity, however, this channel remains weak. Worse still, because the only guaranteed mechanical effect of `r < 0` would be borrower relief, the signal could act in the wrong direction precisely in such a situation.

## 4.5 Refined Stress Conclusion

The strong claim that without negative `r` the system has no internal recovery mechanism is therefore too crude. More precisely:

- without negative `r`, the controller loses part of its authority during prolonged underpeg phases  
- with negative `r`, it regains additional authority, but not a guaranteed recovery mechanism

That is where the real trade off lies.

---

# 5. Control-Theoretical Perspective

## 5.1 The Controller as a PI Like Regulator

From a control theoretical perspective, the controller is not a classical PI block, but PI-like, because `r` itself represents the integrated controller state:

`r_(t+1) = r_t + K_p * ε_t`

supplemented by deadband, limiter, and saturation. This architecture explains both the attractiveness of a more symmetric actuator space and the dangers of a negative range.

## 5.2 Saturation at r = 0

A floor at zero creates saturation. In control theory, it is known that saturation worsens performance and causes slower recovery from nonlinear states. In the present system, however, there is no hidden integrator structure with classical windup. `r` itself is the state and is clipped directly. Therefore, the risk of classical windup is lower than in a standard PID with a separate integrator.

## 5.3 What Actually Remains

Even without classical windup, the following remain:

- authority loss due to saturation  
- residual error  
- slower recovery from underpeg states

A negative range would make the actuator space more symmetric, but symmetry in control space is not identical to symmetry in economic welfare effects.

## 5.4 Oscillation Risks

The wider the negative range would be, the greater the risk would become of:

- over loosening in illiquid phases  
- delayed counterreaction due to TWAP or oracle lag  
- rebound oscillation  
- later overshoot if confidence suddenly returns

**Option A** increases this risk much more strongly than **Option B**.

---

# 6. Risk Analysis

## 6.1 Sober Comparison of the Options

The three variants can be compared along the dimensions of control gain, subsidy risk, and suitability for an immutable design:

| Option | Lower Bound | Control Gain in Underpeg | Subsidy Risk | Suitability for Immutable Design |
|---|---:|---|---|---|
| A | -5 % | high | very high | weak |
| B | -2 % | low to moderate | moderate to high | questionable |
| C | 0 % | no negative branch | no debt subsidy branch | strongest |

This comparison condenses the overall analysis very clearly.

## 6.2 Risk 1 - Subsidy Through Negative r

The probability of this risk would be high under Option A and still substantial under Option B once prolonged underpeg phases occur. The damage potential would also be high because:

- buffers could erode  
- borrowers would be systematically favored  
- price effects would remain uncertain  
- the effect could not be corrected afterward in an immutable Core

This makes the risk especially critical for a frozen protocol.

## 6.3 Risk 2 - Loss of Control Authority at r >= 0

A nonnegative range also has a risk. In an underpeg case, the controller can saturate at zero and lose additional loosening capacity. The probability of this problem is, however, more scenario dependent. Moreover, negative `r` does not reliably solve deep crisis situations.

## 6.4 Long Term System Stability

For an immutable system, what matters is not only which controller variant performs better in normal operation. More important is which failure mode is clearer, less exploitable, and structurally more robust.

Option C creates a clear failure mode:

- The controller saturates at zero.

Options A and B, by contrast, would create a second and more dangerous failure mode:

- The protocol would become an automatic and potentially long lasting debt relief mechanism.

For a frozen monetary architecture, this second failure mode is more dangerous.

---

# 7. Recommendation

## 7.1 Clear Recommendation

The study clearly recommends:

`0 ≤ r ≤ +20 %`

This recommendation does not follow from the idea that negative rates are always wrong, but from the fact that in the present architecture they would operate through the wrong transmission channel.

## 7.2 Rationale in One Sentence

ProjectUSD should not implement a negative branch in the form of a negative debt rate in the current Core. If a negative stabilization mechanism were ever desired, it would have to be designed as a separate, explicitly budgeted channel rather than as automatic debt reduction.

## 7.3 Why Not Option A

`-5 %` would be far too aggressive for an immutable debt rate system. The additional control authority would not justify either the scale of cumulative borrower subsidies or the overshoot risks. This option should therefore be rejected.

## 7.4 Why Option B Also Remains Problematic

`-2 %` would be less extreme than Option A, but would still remain problematic under the current Core. It would not merely be parameterization, but real debt forgiveness, without reliably restoring equilibrium in a crisis. Moreover, such a branch would only be discussable at all after a fundamental redesign with explicit funding logic, strict limits, and precise accounting rules.

## 7.5 Why Option C Is Preferable Despite the Asymmetry

Yes, with a floor at zero the controller can saturate. Yes, deep underpeg phases may therefore last longer. Nevertheless, this asymmetry is the smaller risk because it prevents the protocol from automatically paying borrowers during stress phases without delivering a guaranteed stabilizing price effect.

---

# 8. Final Judgment

Negative values of `r` are not fundamentally illegitimate in autonomous monetary systems. As a general principle, bidirectional signal systems can be meaningful. Under the currently documented Core architecture of ProjectUSD, however, negative `r` is not a necessary stabilization component, but an avoidable systemic risk.

This yields the following ranking:

1. **Option C with `0 %`** - clearly preferred  
2. **Option B with `-2 %`** - only after fundamental redesign of the negative branch  
3. **Option A with `-5 %`** - reject

The most important technical conclusion before the freeze goes even deeper than the floor question itself. The sign logic of the transmission channel `r -> P` must be fully specified and internally consistent. As long as the only guaranteed onchain effect of negative `r` would be the reduction of debt, an immutable Core should not include that branch.

---

# 9. Verification

## Reviewer Checklist

- Is there a clear distinction between controller asymmetry and economic symmetry?
- Is the mechanical meaning of `r < 0` as debt reduction correctly described?
- Is it clearly stated that `r` is defined throughout as nonnegative in the documented Core architecture?
- Is the role of the `surplusBuffer` as the central semantic conflict of a hypothetical negative branch correctly described?
- Is the difference between additional controller authority and a genuine recovery mechanism clearly developed?
- Are Options A, B, and C evaluated consistently in terms of control gain, subsidy risk, and immutable design suitability?
- Is the recommendation `0 ≤ r ≤ +20 %` logically derived from the overall analysis?
- Is the final judgment consistent with the documented Core architecture of ProjectUSD?

This study serves as a basis for the decision on the permissible bounds of `r` before the protocol freeze and for the assessment of whether a negative branch should be regarded as a legitimate stabilization mechanism or as a systemic design error.
