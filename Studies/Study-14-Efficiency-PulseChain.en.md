# Study 14 – Efficiency of ProjectUSD on PulseChain  
*Gas and energy efficiency, scalability and comparison with Ethereum*  
*(Level-3 Research Format)*

---

## Abstract

ProjectUSD is a fully on-chain, autonomous monetary system.  
For practical use as the **base money of PulseChain**, efficiency is as crucial as its monetary architecture:

- How gas-efficient is the system?  
- Can it scale with tens of thousands of vaults, Stability Pool deposits, liquidations and redemptions?  
- How does a deployment on PulseChain differ from an equivalent deployment on Ethereum?  
- What energy efficiency does a PoS-based L1 provide for a high-usage stablecoin system?

This study analyzes:

- gas models of Ethereum and PulseChain,  
- gas profiles of typical ProjectUSD interactions,  
- system scalability under heavy usage,  
- PulseChain energy efficiency,  
- optimization vectors inside the ProjectUSD core.

The results show:  
**ProjectUSD is architecturally ideal for PulseChain — highly scalable, extremely cheap in gas, energy-efficient and mass-market friendly.**

---

# 1. Introduction – Efficiency as a core requirement

ProjectUSD integrates:

- collateralized vaults  
- the Stability Pool  
- the redemption engine  
- the r-controller  
- a Median-TWAP oracle  

into a fully autonomous system with no governance, no admin keys and no external pegs.

For real usability, the system must be:

- **gas-efficient**,  
- **scalable**,  
- **energy-efficient**,  
- **friendly for small users**,  
- **network-friendly**.

This study answers the question:  
> How efficient is ProjectUSD on PulseChain, and how does it compare to Ethereum?

---

# 2. Gas models

## 2.1 Gas fundamentals on EVM chains

Gas fee = **GasUsed × GasPrice**

- **GasUsed** = computational effort  
- **GasPrice** = market cost of blockspace  

EIP-1559 introduces:

- Base Fee (burned)  
- Priority Tip (validator reward)

Protocol efficiency has two layers:

1. **Code efficiency** (design choices)  
2. **Chain efficiency** (network cost model)

ProjectUSD directly influences layer 1, indirectly layer 2.

---

## 2.2 Ethereum gas model

Key characteristics:

- Proof of Stake  
- ~12–13s block time  
- ~30–60M gas block limit  
- DeFi interactions cost 3–50+ USD  
- Complex operations (vaults, liquidations) can cost **10–100 USD**

MakerDAO and Liquity required optimizations such as:

- liquidation buffers  
- minimum debt thresholds  
- batch liquidations  
- aggressive storage optimizations

Ethereum **forces larger trade sizes** due to high gas.

---

## 2.3 PulseChain gas model

Key characteristics:

- Proof of Stake  
- ~10–11s real block time  
- extremely low gas price  
- typical TX: **0.001–0.01 USD**  
- fee burn enabled  
- EVM opcode costs identical, but blockspace is vastly cheaper

PulseChain enables:

- small vault sizes  
- inexpensive liquidations  
- inexpensive arbitrage  
- cheap redemptions  
- mass adoption

---

## 2.4 Gas profiles of typical ProjectUSD actions

Based on Liquity/Maker comparisons:

**Open / Close Vault**  
→ 400k–900k gas

**Adjust Collateral or Debt**  
→ 200k–600k gas

**Stability Pool Deposit/Withdraw**  
→ 200k–500k gas

**Liquidation of a Vault**  
→ 800k–1.5M gas (batching lowers cost per vault)

**Redemption**  
→ similar to liquidation path

**Oracle / r-Update**  
→ extremely low gas (lazy updates)

**Key insight:**  
Gas usage is similar to Liquity —  
**the advantage arises from PulseChain’s ultra-low gas prices**.

---

# 3. Comparison: Ethereum vs PulseChain

## 3.1 Protocol parameter comparison

| Feature | Ethereum (2025) | PulseChain (2025) |
|--------|------------------|--------------------|
| Consensus | PoS | PoS |
| Block time | ~12–13s | ~10–11s |
| TX cost | $0.03 → $50+ | $0.001–$0.01 |
| Fee burn | Yes | Yes |
| Gas limit | ~30–60M | similar, but cheaper to utilize |

---

## 3.2 Example – Vault Opening (800,000 gas)

**Ethereum (10 Gwei, 3000 USD/ETH)**  
→ ~24 USD  
(at 30 Gwei ≈ 72 USD)

**PulseChain**  
→ 0.04–0.40 USD

**Conclusion:**  
→ **Ethereum is 50–200× more expensive** than PulseChain.

Small users are excluded on Ethereum —  
PulseChain enables **universal accessibility**.

---

## 3.3 System-wide gas footprint

Assumptions:

- 50,000 vaults  
- 200,000 vault interactions/year  
- 20,000 Stability Pool actions  
- 5,000 liquidations/redemptions  

Total usage:  
→ ~112B gas/year  
→ <0.1% of total annual capacity of an EVM chain

**Conclusion:**  
ProjectUSD scales effortlessly on PulseChain.

---

## 3.4 Energy efficiency

**Ethereum PoS:**  
~0.0026 TWh/year (very efficient)

**PulseChain PoS:**  
similar architecture → similar energy profile

ProjectUSD efficiency metrics:

- more liquidations per kWh  
- more arbitrage corrections per kWh  
- high stability-per-energy ratio  
- fee burn couples usage with ecosystem value

---

# 4. Optimizations

## 4.1 Core-level optimizations

- storage slot packing  
- splitting frequently vs infrequently updated variables  
- minimizing SSTORE  
- event logging instead of storage  
- batch liquidations  
- sorted data structures for weakest vaults  
- off-chain view computations

---

## 4.2 Protocol-level optimizations

- pull-based reward mechanisms  
- lazy r computation  
- gas compensation for liquidators  
- low-frequency median-TWAP updates  
- strict separation of core vs peripherals

---

## 4.3 PulseChain-specific optimizations

- multicall bundling  
- optional gas subsidies for small users  
- exploiting low-load network phases  
- fee burn alignment

---

## 4.4 Hypothetical Ethereum deployment

If ProjectUSD were deployed on Ethereum:

- minimum debt per vault must be far higher  
- liquidations become risky during gas spikes  
- small users excluded  
- redemptions only profitable for large actors

PulseChain:

- low fees → inclusivity  
- stable liquidation incentives  
- arbitrage active even for small deviations  
- mass-adoption friendly

---

# 5. Conclusion

### **Gas Efficiency**
ProjectUSD uses a minimal, immutable architecture that:

- requires few transactions  
- allows low-cost liquidations and redemptions  
- benefits enormously from PulseChain’s low gas price

### **Scalability**
On PulseChain, ProjectUSD supports:

- tens of thousands of vaults  
- thousands of liquidations/year  
- <0.1% network load

### **Energy Efficiency**
PoS chains are extremely energy-efficient;  
PulseChain leverages this with high economic throughput per kWh.

### **Ethereum vs PulseChain**
ProjectUSD *could* run on Ethereum —  
but PulseChain is **orders of magnitude more efficient**:

- user-friendly  
- capital-efficient  
- mass-market ready  
- stability-enhancing  
- energy-efficient  
- gas-efficient

ProjectUSD is therefore an **ideal high-efficiency monetary system** for PulseChain.

---

# 6. Verification

> ## 📘 Reviewer Checklist
- Are gas profiles accurately described?  
- Is the Ethereum vs PulseChain comparison technically correct?  
- Are scalability assumptions reasonable?  
- Are energy-efficiency statements accurate?  
- Is the analysis aligned with the ProjectUSD system design?

This study forms the basis for technical evaluations, benchmarking and future prototype testing of ProjectUSD on PulseChain.
