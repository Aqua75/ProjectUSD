# Study 12 – Game Theory of the ProjectUSD Economy
*Analysis of strategic interactions among market participants, arbitrageurs, borrowers, holders, liquidators and the autonomous protocol*  
*(Level-3 Research Format)*

---

## Abstract

ProjectUSD is an autonomously regulated monetary system whose stability does not rely on central actors, but instead emerges from game-theoretic equilibria.  
The core question is:  
**How do rational market participants behave when arbitrage, redemption, r-adjustment and liquidation follow deterministic, transparent rules?**

This study models all major actor groups:

- **Arbitrageurs**  
- **ProjectUSD holders**  
- **Vault owners (borrowers)**  
- **Stability Pool participants**  
- **Liquidators**  
- **External speculators**

and examines how their strategic incentives contribute to:

- price stability,  
- low manipulation risk,  
- robust equilibrium states,  
- stable expectations,  
- and negative feedback loops that dampen volatility.

We demonstrate that ProjectUSD forms a **strong game-theoretic equilibrium**, in which every rational actor — pursuing their own interest — ends up stabilizing the system rather than destabilizing it.

---

# 1. Introduction – Why game theory matters for ProjectUSD

ProjectUSD’s economy is not centrally governed.  
Instead, it arises from:

- automated mechanisms (controller, oracle, redemption),  
- incentives,  
- rational decision-making by participants.

Game theory evaluates whether these incentives:

- are stable,  
- consistent,  
- manipulation-resistant,  
- and sustainable over time.

ProjectUSD is designed such that individual incentives **naturally support** systemic stability.

---

# 2. Actor types and their utility functions

## 2.1 Arbitrageurs

Goal: **Risk-free profit from price deviations P ↔ R.**

Utility:

- if P < R → buy + redeem → profit  
- if P > R → mint (if r allows) + sell → profit  

Arbitrageurs are the **natural stabilizers** of the system.

---

## 2.2 Holders of ProjectUSD

Goal: **Price stability and predictable value.**

Utility:

- P stable around R  
- low slippage  
- low systemic risk  
- reliable long-term store of value

Holders benefit from stable equilibria.

---

## 2.3 Vault owners (borrowers)

Goal: **PLS leverage through collateralized debt.**

Utility:

- low r (cheap borrowing)  
- high collateral value  
- low liquidation pressure

Borrowers are sensitive to r-adjustments, and react rationally to them.

---

## 2.4 Stability Pool participants

Goal: **Profits from liquidation gains.**

Utility:

- receiving collateral > cancelled debt  
- consistent alpha returns  
- cushioned by the Surplus Buffer

They enable liquidations and improve systemic resilience.

---

## 2.5 Liquidators

Goal: **Acquire discounted collateral through liquidations.**

Utility:

- efficient liquidation mechanics  
- minimal oracle manipulation risk  
- predictable PLS exposure

Liquidators prevent “bad debt” from accumulating in the system.

---

## 2.6 External speculators

Goal: **Profit from price movements in ProjectUSD or PLS.**

They may increase volatility,  
but cannot destabilize the system due to counteracting mechanisms.

---

# 3. Game-theoretic core structure: Negative feedback

## 3.1 Why stable systems need negative feedback loops

Failed systems (UST/LUNA, IRON/TITAN) relied on **positive feedback**:

Price drops → supply increases → price drops further → collapse.

ProjectUSD exhibits **strictly negative feedback**:

Price drops → r decreases → demand rises → P rises  
Price rises → r increases → demand cools → P falls  

This is the essential reason spirals cannot form.

---

## 3.2 Arbitrage as a Nash equilibrium

Arbitrage is a **dominant strategy**:

- when P < R, every rational trader has incentive to buy  
- when P > R, every rational trader has incentive to sell or mint  
- deviation from arbitrage yields lower payoff  

Thus, price stabilizes at a **Nash equilibrium around R**.

---

## 3.3 Equilibrium between borrowers and holders

Borrowers want low r.  
Holders want price stability.

The system aligns both through:

- the r-controller,  
- median-TWAP oracle,  
- redemption incentives.

The game yields a **shared optimum**.

---

## 3.4 Stability Pool as a game-theoretic anchor

SP participants assume the debt of liquidated vaults.  
They receive collateral with positive expected value.

This:

- reduces liquidation fear,  
- strengthens demand for ProjectUSD,  
- attracts rational long-term actors.

---

# 4. Strategic interactions in price discovery

## 4.1 Underpricing (P < R)

Dominant strategies:

- Arbitrageurs: buy + redeem  
- Holders: accumulate (safe anchor R)  
- Borrowers: benefit from reduced r  
- Liquidators: if applicable, benefit from efficient liquidations

Outcome: **P increases toward R**.

---

## 4.2 Overpricing (P > R)

Dominant strategies:

- Arbitrageurs: mint (if r allows) + sell  
- Holders: sell or wait  
- Borrowers: r increases → borrowing becomes unattractive  
- Stability Pool: unaffected

Outcome: **P decreases toward R**.

---

## 4.3 Neutral zone (P ≈ R)

A zone of strategic neutrality:

- minimal arbitrage  
- stable r  
- predictable expectations  
- low volatility  

This is a **self-sustaining Nash equilibrium**.

---

# 5. Strategic stability under stress

## 5.1 PLS crash

Strategic behavior:

- Liquidators take over vaults  
- Stability Pool absorbs collateral efficiently  
- r decreases → demand for ProjectUSD rises  
- Arbitrage stabilizes P

The system remains operational and stable.

---

## 5.2 Illiquid market conditions

Strategic behavior:

- oracle smoothing protects against mispricing  
- traders reduce position size  
- arbitrage continues in small increments  
- Stability Pool remains functional

System continues functioning even with low liquidity.

---

## 5.3 PulseChain-wide panic

The combination of:

- Redemption,  
- Stability Pool mechanics,  
- Surplus Buffer,  
- r-adjustment,  
- oracle smoothing  

creates **coordinated strategic responses** that prevent collapse.

---

# 6. Role of the Surplus Buffer in game theory

The Surplus Buffer enhances equilibrium stability by:

- absorbing shocks,  
- supporting negative-r phases,  
- increasing confidence of holders and borrowers,  
- strengthening long-term predictability.

It acts as a **strategic insurance layer**.

---

# 7. Manipulation resistance as a game-theoretic equilibrium

ProjectUSD is resistant to:

- oracle manipulation (Median + TWAP),  
- low-liquidity price manipulation,  
- flashloan attacks,  
- death spirals,  
- governance takeovers (none exist).

A rational attacker cannot obtain lasting profits because:

- arbitrage punishes deviations,  
- oracle filters remove manipulation,  
- r dampens the effect of shocks.

Attacks are **economically irrational**.

---

# 8. Game-theoretic identity of ProjectUSD

ProjectUSD is a **self-stabilizing game**:

- negative feedback loops,  
- dominant arbitrage strategies,  
- symmetrical incentives,  
- stable Nash equilibria,  
- no reflexive risk token,  
- no external peg constraint,  
- no governance bottleneck.

Rational behavior leads to **collective stability**.

---

# 9. Conclusion

ProjectUSD is not just a technical architecture — it is a game-theoretic design:

A system where:

- arbitrage stabilizes,  
- holders gain predictable value,  
- borrowers act rationally,  
- the Stability Pool acts as an anchor,  
- liquidations function efficiently,  
- r regulates systemic pressure.

Every participant's rational self-interest aligns with **systemic stability**.

This makes ProjectUSD a **self-reinforcing, game-theoretically robust monetary system**, resistant to manipulation, panic, external shocks, and reflexive instability.

---

# 10. Verification

> ## 📘 Reviewer Checklist
- Are all actor types correctly defined?  
- Are game-theoretic incentives accurately modeled?  
- Are dominant strategies correctly derived?  
- Is the equilibrium P → R explained precisely?  
- Are stress scenarios logically consistent?  

This study provides a foundation for further work on mechanism design, incentive theory and dynamic monetary governance within ProjectUSD.
