## Chapter 5 - Security and Transparency: When Code Replaces Trust

In a world where monetary systems are built on promises, ProjectUSD chooses a different path:

security through mathematics, trust through visibility.

The system is designed so that no single actor - not a person, not a regulator, not even a miner - can control or corrupt it.

Here, security does not mean the absence of risk, but rather the ability to shape risk so that it becomes predictable and limited.

### 5.1 The Principle of Autonomy

True security in DeFi begins where human influence ends.

ProjectUSD follows a simple axiom:

“What cannot be changed cannot be abused.”

The system’s core - Vaults, Liquidations, Redemption, Controller, Oracles - is frozen after its initial deployment phase.

From that moment, no one can stop, rewrite, or adjust it.

Even governance has access only to the outer layer - never to the inner code.

This creates an autonomous monetary system that does not rely on trust in developers, teams, or institutions.

It exists simply because it runs - not because someone permits it to.

### 5.2 On-Chain Transparency

Every number, every process, every metric of ProjectUSD is visible on-chain:

• The current distribution of vault collateralization,

• The live equilibrium price R and system rate r,

• The size of the Stability Pool,

• The liquidation history,

• The state of the Surplus Buffer.

Nothing is hidden. Nothing is proprietary.

Anyone who wants to know how healthy the system is doesn’t need a report - they simply query the smart contract.

This is accounting truth in its purest form.

### 5.3 Protection Against Market Manipulation

DeFi is not a laboratory - it’s a battlefield.

Price feeds, oracles, and liquidity pools are common attack vectors for Miner Extractable Value (MEV), front-running, and sandwiching.

ProjectUSD counters these risks with multi-layered logic:

• Median-TWAP Oracle:

Prices are aggregated from multiple PulseChain pairs (e.g., ProjectUSD/PLS, ProjectUSD/PLSX) to form a time-weighted median.

Short-term pump-and-dump moves lose their impact.

• Outlier Filter:

Pairs with insufficient liquidity or statistical anomalies are automatically excluded.

• Rate Limiter:

Adjustments to the system rate r are capped per epoch (e.g., 50 basis points), preventing sudden interest spikes during market stress.

• Reentrancy & Governance-Capture Protection:

Critical functions are isolated; callbacks are disabled; governance changes are time-locked and fully transparent.

The result is a security model that defends against both technical and economic attacks -

without ever compromising autonomy.

### 5.4 The Surplus Buffer - The Collective Safety Net

Every transaction within ProjectUSD generates small fees that flow into the Surplus Buffer.

This buffer acts as a collective reserve, used to:

• Offset temporary losses from AMO operations,

• Smooth extreme fluctuations in the rate r,

• Or fund long-term savings yields.

The more ProjectUSD circulates, the larger this buffer grows -

a self-reinforcing protection mechanism, fueled by user activity.

### 5.5 Governance as Guardian, Not Ruler

ProjectUSD redefines governance.

It may coordinate, but it cannot control.

After the parameter freeze, its role is limited to maintaining the periphery:

adding new collateral types, adjusting AMO parameters, or managing optional PSM modules.

Every change must go through on-chain voting, with advance notice and full transparency.

Governance, therefore, is not a center of power - it is a guardian of the framework.

It ensures the system can evolve without ever endangering what makes it strong: its incorruptibility.

### 5.6 Security as a Form of Freedom

ProjectUSD proves that security and freedom are not opposites.

A system that limits itself liberates itself from the whims of its creators.

What runs once, runs forever - for as long as PulseChain exists.

Here lies the true promise:

Not “Code is law” - but Code is a contract.

A contract that cannot be broken,

because no one holds the power to break it.
