# Chapter 5 - Security and Transparency: When Code Replaces Trust

In a world where monetary systems are built on promises, ProjectUSD chooses a different path:<br>
**security through mathematics, trust through visibility**.

The system is designed so that no single actor - not a person, not a regulator, not even a miner - can<br>
control or corrupt it.<br>
Here, security does not mean the absence of risk, but rather the ability to shape risk so that it becomes<br> **predictable and limited**.

---

### 5.1 The Principle of Autonomy

True security in DeFi begins where human influence ends.<br>
ProjectUSD follows a simple axiom:

“What cannot be changed cannot be abused.”

The system’s core - Vaults, Liquidations, Redemption, Controller, Oracles - is frozen after its initial<br>
deployment phase.<br>
From that moment, no one can stop, rewrite, or adjust it.<br>
Even governance has access only to the outer layer - never to the inner code.

This creates an **autonomous monetary system** that does not rely on trust in developers, teams, or institutions.<br>
It exists simply because it runs - not because someone permits it to.

---

### 5.2 On-Chain Transparency

Every number, every process, every metric of ProjectUSD is visible on-chain:

- The current distribution of vault collateralization,
- The live equilibrium price **R** and system rate **r**,
- The size of the Stability Pool,
- The liquidation history,
- The state of the Surplus Buffer.

Nothing is hidden. Nothing is proprietary.<br>
Anyone who wants to know how healthy the system is doesn’t need a report - they simply query the smart contract.<br>
This is accounting truth in its purest form.

---

### 5.3 Protection Against Market Manipulation

DeFi is not a laboratory - it’s a battlefield.<br>
Price feeds, oracles, and liquidity pools are common attack vectors for Miner Extractable Value (MEV),<br>
front-running, and sandwiching.<br>
ProjectUSD counters these risks with multi-layered logic:

- **Median-TWAP Oracle:**<br>
Prices are aggregated from multiple PulseChain pairs (e.g., ProjectUSD/PLS,<br>
ProjectUSD/PLSX) to form a time-weighted median.<br>
Short-term pump-and-dump moves lose their impact.
- **Outlier Filter:**<br>
Pairs with insufficient liquidity or statistical anomalies are automatically excluded.
- **Rate Limiter:**<br>
Adjustments to the system rate r are capped per epoch (e.g., 50 basis points), preventing sudden<br>
interest spikes during market stress.<br>
- **Reentrancy & Governance-Capture Protection:**<br>
Critical functions are isolated; callbacks are disabled; governance changes are time-locked and<br>
fully transparent.

The result is a security model that defends against both technical and economic attacks -<br>
without ever compromising autonomy.

---

### 5.4 The Surplus Buffer - The Collective Safety Net

Every transaction within ProjectUSD generates small fees that flow into the **Surplus Buffer**.<br>
This buffer acts as a collective reserve, used to:

- Offset temporary losses from AMO operations,
- Smooth extreme fluctuations in the rate **r**,
- Or fund long-term savings yields.

The more ProjectUSD circulates, the larger this buffer grows -<br>
a self-reinforcing protection mechanism, fueled by user activity.

---

### 5.5 Governance as Guardian, Not Ruler

ProjectUSD redefines governance.<br>
It may **coordinate**, but it cannot **control**.

After the parameter freeze, its role is limited to maintaining the periphery:<br>
adding new collateral types, adjusting AMO parameters, or managing optional PSM modules.<br>
Every change must go through on-chain voting, with advance notice and full transparency.

Governance, therefore, is not a center of power - it is a guardian of the framework.<br>
It ensures the system can evolve without ever endangering what makes it strong: its incorruptibility.

---

### 5.6 Security as a Form of Freedom

ProjectUSD proves that security and freedom are not opposites.<br>
A system that limits itself liberates itself from the whims of its creators.<br>
What runs once, runs forever - for as long as PulseChain exists.

Here lies the true promise:<br>
Not “Code is law” - but **Code is a contract**.<br>
A contract that cannot be broken,<br>
because no one holds the power to break it.
