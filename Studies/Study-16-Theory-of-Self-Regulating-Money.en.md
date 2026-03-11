# Study 16 – The Theory of Self-Regulating Money  
*Philosophy of autonomous money, monetary theory, decentralization and system autonomy in the context of ProjectUSD on PulseChain*  
*(Level-3 Research Format)*

---

## Abstract

This study develops an academic-philosophical theory of self-regulating money and examines under which conditions a monetary system without an institutional center can be considered stable, legitimate and functional. Drawing on classical and modern monetary theories, stability is not understood as mere price fixation, but as a performative outcome of expectations, feedback loops and institutional guarantees.

Subsequently, concepts from systems theory and cybernetics are applied to monetary orders. Autonomy appears not as isolation, but as the capacity to process disturbances through internal control loops without relying on discretionary intervention.

In the fourth chapter, ProjectUSD is examined as a case study: a fully on-chain designed, algorithmic monetary system for PulseChain that seeks to generate stability through an internal equilibrium price R, a variable system rate r, vault-based collateral, a Stability Pool and a Redemption mechanism, complemented by an Immutable Core after a freeze event, where immutability functions as a monetary constitution.

The conclusion formulates criteria under which ProjectUSD can be regarded as a paradigmatic design of autonomous money and identifies philosophical tensions: autonomy versus adaptability, transparency versus complexity, and the question of whether stability without an external nominal anchor is more than internal coherence.

---

# 1. Introduction

## 1.1 Problem statement – money between trust, power and technology

Money is never merely a neutral medium of exchange. It is simultaneously an institution, an infrastructure and a political technology. Whoever issues money implicitly defines rules: which forms of collateral count, which debt relations are accepted, who is rescued in a crisis and who is not. Historically, this power was exercised by the state through taxation and legal tender laws, or by the banking system through credit creation and the lender of last resort function.

Decentralized financial systems aim to circumvent this power architecture. Yet especially in the case of stablecoins, a paradox becomes visible: stability is often purchased at the cost of centralization, custodians, bank accounts, blacklists and regulatory points of control. The ProjectUSD whitepaper addresses this paradox by formulating a counterposition: a fully on-chain, algorithmic monetary system that seeks price stability without banks and without central intervention, while explicitly positioning itself not as a product announcement but as a conceptual blueprint.

Philosophically, this shifts the question from “Is this already real?” to “What kind of money would be conceivable if control were fully delegated to rules?”

## 1.2 Guiding questions

This study investigates five guiding questions:

1. What is money in theoretical terms – function, origin and legitimacy  
2. What does stability mean – fixation to an external benchmark or internal dynamic balance  
3. What does autonomy mean in systems, and is an autonomous monetary system possible at all  
4. How does ProjectUSD translate the idea of autonomy into mechanisms – R, r, vaults, Stability Pool, Redemption, Immutable Core  
5. What normative consequences arise when code becomes a monetary order – responsibility, freedom, justice and error tolerance

## 1.3 Method and scope

Methodologically, this is a philosophical analysis with a systems-theoretical approach and an interpretive reading of the primary source, the ProjectUSD Whitepaper V2.1. The text is not treated as a narrow technical specification, but as the outline of a monetary constitution and as a program of a specific philosophy of money: instead of promises there is code, instead of trust there is transparency.

Scope limitation: This study is neither an investment analysis nor a formal security audit. It addresses concepts, assumptions and internal tensions, not short-term market opportunities.

---

# 2. Monetary theory

## 2.1 Functions of money – medium of exchange, unit of account, store of value

In classical economics, money is defined by three core functions:

1. Medium of exchange  
2. Unit of account  
3. Store of value

Philosophically, it is crucial to note that these functions are not natural facts, but rest on collective expectations and institutional guarantees. Money functions because a sufficient number of actors expect it to be accepted as money tomorrow as well.

Money thus becomes a social contract, not necessarily in a legal sense. In crypto systems, this contract can be technically encoded: rules become execution conditions. ProjectUSD articulates this perspective as a substitution of trust with visibility and deterministic logic.

## 2.2 Theories of origin – commodity, state and credit

Historically, monetary theory is divided into three major narratives:

- Commodity money and barter theories: money emerges from market processes to facilitate exchange  
- Chartalism and state theory: money is primarily a state token, acceptance is enforced via taxation and law  
- Credit theories: money is fundamentally a debt-credit relationship, created by banks through balance sheets and institutional trust

ProjectUSD cuts across these traditions. It is not state-issued, not tied to bank balance sheets and not strictly commodity money, yet it employs collateral-based logic through vaults that resemble security intuitions. Money creation is tied to overcollateralized positions, typically around 170 percent or more.

Philosophically, this can be understood as an attempt to realize credit money without banks: debt is formalized via smart contracts, while security is enforced through liquidation mechanics and collective buffers such as the Stability Pool.

## 2.3 Stability as a normative category

Stability is not merely a price concept, but also an argument about welfare and justice. Unstable units of account generate redistribution by distorting calculation and contractual relations. Traditionally, stability is therefore anchored to an external nominal reference: gold, a state inflation target or a currency basket.

ProjectUSD proposes a different definition: stability as oscillation around an internal equilibrium price R, with deviations dampened through an endogenous adjustment of the system rate r. This stability is not identical to an external parity. The whitepaper explicitly emphasizes that ProjectUSD is not intended as a fiat replica, but as an independent digital unit of account.

The concept thus shifts: “stable” no longer means external parity, but internal coherence and redeemability.

## 2.4 Rule binding versus discretion – an old debate in a new form

Monetary orders historically oscillate between discretion, situational intervention, and rule binding. ProjectUSD radicalizes rule binding: no admin key, no pause button, no discretionary intervention. After the freeze event, the core is intended to become immutable.

Philosophically, this reflects the thesis that arbitrariness is the fundamental problem of money. The solution is not better rulers, but the exclusion of rulership through immutability. Yet rule binding remains ambivalent. It protects against abuse of power, but may remove the capacity to react to genuine system failures.

The conflict is not technical, but political-philosophical: do we want a form of money that cannot be rescued, even when rescue might be desirable?

---

# 3. Autonomous systems

## 3.1 Autonomy – not isolation, but self-regulation

In systems theory and cybernetics, autonomy does not primarily mean isolation, but the ability to reproduce essential states through internal processes. An autonomous system processes disturbances through feedback, not through external command.

ProjectUSD embodies this idea. Deviations between market price P and internal price R lead to adjustments of the system rate r within predefined bounds, influencing the incentives of borrowers, arbitrageurs and liquidity providers. The controller functions as a feedback loop: measure, compare, correct.

## 3.2 Feedback and homeostasis

Many biological and technical systems stabilize themselves not through rigidity, but through dynamics, through homeostasis. The whitepaper adopts this metaphor: stability does not arise from fixation, but from movement, the system “breathes” through counterforces in response to price deviations.

Philosophically, this is notable: stability is understood as a process, not a state. Money becomes less a thing and more an operating regime.

## 3.3 Autopoiesis and structural coupling

Autopoiesis theories emphasize that autonomous systems are operationally closed, yet structurally coupled to their environment. They perceive the environment only through their own sensors and respond only through their own operations.

Applied to ProjectUSD, “oracleless” does not mean absence of environmental input, but absence of external authority. The system uses on-chain price references, median and TWAP across DEX pairs, as its internal perception. There is no external arbiter, only a self-defined measurement process.

Autonomy thus becomes a question of epistemic interface: not no data, but no foreign authority.

## 3.4 Complexity, reflexivity and limits of control

Autonomous systems in markets are reflexive: expectations influence outcomes, outcomes influence expectations. A control loop can stabilize or generate oscillations, overshoot, inertia or panic.

ProjectUSD addresses this risk through rate limiters, limiting changes in r per epoch, and through manipulation filters such as median TWAP and outlier filtering. Yet one limitation remains: no rule set can fully eliminate the social dimension of markets. Psychological factors, panic and irrational behavior mark the limits of algorithmic perfection.

Autonomy is therefore gradual, not absolute.

## 3.5 Governance – guardian or sovereign

Who is allowed to change rules? ProjectUSD designs a two-layer order:

- Immutable Core: core functions such as vaults, liquidations, redemption and controller become immutable after the freeze  
- Periphery: adjustable via timelocks and voting, including modules such as AMO and PSM

Governance acts as a guardian, not a sovereign. Philosophically, this corresponds to a constitutional model: there is a constitution that limits political processes.

Decentralization thus means not only distribution of power, but architectural restriction of power.

---

# 4. ProjectUSD in context

## 4.1 System concept – autonomous money for an autonomous chain

The whitepaper positions ProjectUSD as the missing component of a self-sufficient DeFi economy on PulseChain: a value anchor that functions as autonomously as the chain itself. The core thesis is that stability does not require trust if feedback replaces human control.

Money appears not as a product, but as a system organ. ProjectUSD describes itself as the heart of the economy and as a mini central bank without humans.

Philosophically, this is a translation of central banking functions into code:

- control of money creation through vaults and r  
- crisis mechanisms via the Stability Pool and liquidations  
- redeemability and anchoring through redemption at R

## 4.2 R and r – endogenous reference instead of external peg

At the center lies the internal equilibrium price R as the reference around which the market price P is intended to oscillate. The control variable r is a non negative system rate that adjusts borrowing conditions and influences the incentives to mint or repay ProjectUSD.

The mechanism implies a cybernetic thesis: stability emerges when incentives are structured such that deviations become unattractive. Not command, but a field of incentives in which actors, driven by self-interest, contribute to restoring equilibrium.

The critical question is value itself. If R is not tied to an external benchmark, value becomes an internal reference point of the system. ProjectUSD explicitly emphasizes this independence. Philosophically, this can be read as an attempt to create a monetary sphere in which unit of account and stability emerge from system logic itself.

The term “stablecoin” thus becomes potentially misleading. It is closer to an algorithmic unit of account with a stability objective than to a fiat mirror.

## 4.3 Vaults, Stability Pool and Redemption – institutions without institutions

ProjectUSD organizes money creation and stability through three core institutions encoded in smart contracts:

1. Vaults: users deposit collateral, primarily PLS, and mint ProjectUSD subject to minimum collateralization; below the threshold, automatic liquidation occurs  
2. Stability Pool: users deposit ProjectUSD to absorb liquidations and receive collateral and bonuses in return; supply is reduced through burns and stress is absorbed  
3. Redemption Engine: anyone can redeem ProjectUSD against PLS at the equilibrium price R, with the weakest vaults reduced first

Philosophically, this translates classical institutions:

- the vault as an individualized balance sheet  
- the Stability Pool as collective insurance logic  
- redemption as redeemability, the core of monetary legitimacy

In traditional monetary theory, redeemability is political or institutional, taxation or bank reserves. Here it becomes procedural: redeemability is a function of the protocol, not a promise by an institution.

## 4.4 Immutable Core and freeze event – monetary constitutionalism

The Immutable Core is the centerpiece. After the freeze event, no one can change core logic or core parameters. There is no admin key and no kill switch.

Philosophically, this represents the strongest normative claim: autonomy through immutability. Money becomes a permanent rule rather than an ongoing political decision.

The ambivalence is clear:

- positive: minimization of arbitrariness, reduction of capture risk, maximum predictability  
- negative: immutability makes errors permanent; smart contract bugs are irreversible, requiring uncompromising quality before the freeze

This reproduces a classic dilemma of political philosophy in technical form: adaptable fallibility with abuse risk versus rigidity with irreversible error costs.

ProjectUSD tends to answer in favor of rigidity and shifts responsibility to the pre-freeze phase: audits, verification and testing.

## 4.5 Oracleless yet measured – an epistemic distinction

The whitepaper emphasizes “without oracles” while simultaneously describing median TWAP, outlier filters and price aggregation across multiple DEX pairs. This is less a contradiction than an epistemic distinction:

- “without oracles” means without off-chain authority and without bank-backed fiat reference feeds  
- “oracle” in a technical sense refers to internal on-chain measurement of the system environment to smooth manipulation

Philosophically, the protocol cannot not observe the world. It can only decide how it observes and which observation forms are considered legitimate. ProjectUSD chooses observation from within its own system and applies filters against manipulation.

## 4.6 Security and transparency – accounting truth as a norm

ProjectUSD treats transparency as a substitute for trust. Metrics such as R, r, vault distribution, pool size and histories are intended to be observable on-chain.

The normative shift is clear:

- traditional systems require trust in reports, institutions and auditors  
- on-chain systems rely on immediate verifiability; those who want to know, query the contract

Yet transparency is not identical to comprehensibility. A complex protocol can be fully transparent and still epistemically exclusive. This raises the question: does transparency truly replace trust, or does it merely replace blind trust with technical authority.

Whether transparency replaces trust depends less on data availability than on socially shared interpretability.

## 4.7 PulseChain context – sovereignty through a native unit of account

The whitepaper argues that PulseChain requires its own stable currency to avoid dependence on centralized stablecoins, which may introduce blacklisting, regulatory intervention or systemic failure into the ecosystem.

Philosophically, this is an argument about sovereignty: a system is only as autonomous as its unit of account. Without its own money, a chain remains dependent, economically and politically. ProjectUSD can thus be read as an attempt to establish monetary independence, not merely technical decentralization.

## 4.8 Risks and limits – honesty as part of the philosophy of money

Notably, the whitepaper explicitly names risks: smart contract bugs, MEV, oracle bias in illiquid phases, collateral volatility, psychological market reactions, governance capture in the periphery and legal uncertainty.

The core claim is that perfect safety does not exist. The difference lies in where risks reside and whether they are visible. ProjectUSD shifts risk from humans to code in order to make it explicit, measurable and fair.

This represents an ethics of explicit rules: the goal is not absence of risk, but absence of hidden, discretionary decisions.

---

# 5. Conclusion

## 5.1 Results stated as theses

1. Self-regulating money is philosophically plausible if stability is understood as dynamic feedback rather than rigid parity; ProjectUSD designs stability as a control loop around R with bounded adjustments of the system rate r 
2. Autonomy does not mean freedom from the environment, but the capacity to process environmental disturbances through internal operations; ProjectUSD operationalizes this through on-chain measurement, rule adjustment and redeemability  
3. Immutability via Immutable Core and freeze event constitutes monetary constitutionalism; it limits power but increases the cost of irreversible errors  
4. Transparency only partially replaces trust; it enables verification but does not automatically create shared understanding; expertise and expectation coordination remain necessary  
5. By its own claim, ProjectUSD is not a fiat replica but an independent unit of account for a closed economy, shifting the debate from peg maintenance to system coherence

## 5.2 Open questions – philosophical and systemic

- The nominal anchor question: if R is endogenous, how is stability measured outside the system; is internal redeemability sufficient as a legitimacy core  
- The justice question: who bears losses in stress phases – vault owners, pool participants, arbitrageurs; is the distribution normatively fair or merely rule-compliant  
- The governance question: can peripheral governance remain secure as economic incentives grow; capture risk  
- The epistemic question: how can transparency avoid becoming rule by those who can interpret data

## 5.3 Closing thought

ProjectUSD articulates a radical thesis: money can exist as an autonomous system if it is constructed as an incorruptible rule regime, a contract that cannot be broken.

Philosophically, this is more than DeFi engineering. It is an attempt to replace the political question of money with an architectural answer: not better rule, but less rule.

Whether this shift succeeds depends not only on code, but on the social reality surrounding it: markets, expectations, liquidity, crises and the human tendency, even in the most transparent systems, to search again for authorities. Autonomous money therefore does not abolish the political; it reformulates it – from sovereignty as a person or institution to sovereignty as a protocol.

---

# 6. References

## Primary source

- ProjectUSD – An autonomous monetary system for PulseChain. Whitepaper V2.1 EN, vision and architecture of a self-regulating blockchain economy. Conceptual blueprint, chapters on autonomous money, R and r mechanics, architecture, security, roadmap, risks and philosophy

## Classical and modern reference lines

- Aristotle: Nicomachean Ethics, exchange, measure, money as convention  
- Georg Simmel: The Philosophy of Money, money as a form of social mediation  
- Carl Menger: Principles of Economics, origin of money  
- John M. Keynes: A Treatise on Money, The General Theory, money, uncertainty and expectations  
- Friedrich A. Hayek: Denationalisation of Money, private money, currency competition  
- Niklas Luhmann: The Economy of Society, money as a medium of communication  
- Norbert Wiener: Cybernetics, feedback and control  
- Humberto Maturana, Francisco Varela: Autopoiesis and Cognition, operational closure and structural coupling

---

# 7. Verification

> ## 📘 Reviewer checklist

- Are the guiding questions clearly addressed and logically connected  
- Is the distinction between stability as parity and stability as feedback clearly articulated  
- Are systems-theoretical concepts correctly transferred – autonomy, feedback, homeostasis, autopoiesis  
- Is ProjectUSD described precisely and consistently with the whitepaper, especially R, r, vaults, Stability Pool, Redemption and Immutable Core  
- Are tensions and open questions clearly named without prematurely resolving them  
- Is the overall argument consistent with the ProjectUSD design and its stated limits

This study provides the foundation for a philosophical and systematic classification of ProjectUSD as a design of autonomous money and for deriving normative criteria against which later technical and economic tests can be evaluated.
