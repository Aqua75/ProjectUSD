---
title: "ProjectUSD – Incident Runbook v1"
status: "Draft"
last_updated: "2025-11-19"
author: "Aqua75"
language: "en"
related_whitepaper_sections: ["Ch. 8 – Freeze", "Ch. 9 – Security", "Glossary pp. 24–28"]
---

# ProjectUSD – Incident Runbook v1

## Purpose

This Incident Runbook defines all possible incident types for ProjectUSD  
and describes the required **diagnostic and monitoring procedures**.

**Important:**  
After the freeze activation, ProjectUSD has:

- no admins  
- no emergency functions  
- no intervention mechanisms  
- no upgrade paths  

This runbook therefore documents **diagnosis only**, not action.  
There are **no system interventions** after freeze — only:

- correct diagnosis  
- pattern detection  
- state verification  
- interpretation of scenarios  
- transparent documentation for post-mortems  

---

# 1. Incident Classification

ProjectUSD distinguishes five categories of incidents:

## 1.1 Technical Incidents (Smart Contracts / Blockchain)

- unusual gas spikes  
- extremely low block production  
- chain reorgs / forks  
- RPC failures  
- subgraph delays  
- system state temporarily inaccessible  

## 1.2 Economic Incidents (Market / Liquidation / Redemption)

- sudden PLS price crashes  
- liquidation waves  
- redemption spikes  
- liquidation delays  
- abnormal CR distributions  
- unusually high system debt levels  

## 1.3 Oracle Incidents

- missing price updates  
- strong deviations between feeds  
- median diverges abnormally from DEX prices  
- single-feed outliers  

## 1.4 StabilityPool and Vault Health Incidents

- StabilityPool approaching empty capacity  
- multiple negative CR vaults in rapid sequence  
- increased risk of BadDebt  
- extreme shifts in vault CR structure  

## 1.5 Offchain / Infrastructure Incidents

- frontend monitoring unavailable  
- subgraph unreachable  
- API rate limits  
- delayed event indexing  

---

# 2. Severity Levels

ProjectUSD uses three severity classes:

## SEV-0 (Critical)
- potential threat to system observability  
- oracle price missing for extended periods  
- massive liquidation queueing  
- extremely low block production  
- StabilityPool approaching zero  
- system state cannot be queried  

→ **Immediate diagnosis, continuous monitoring, documentation**

## SEV-1 (High)
- unusual CR distributions  
- redemption queueing  
- single oracle feed down  
- subgraph delayed  
- network congestion  

→ Increase monitoring cadence

## SEV-2 (Informational)
- higher-than-normal volatility  
- occasional liquidation delays  
- RPC slowdowns  
- UI temporarily offline  

→ Observe and document

---

# 3. Incident Types & Runbooks

## 3.1 Oracle Outage (SEV-0 / SEV-1)

**Symptoms:**

- `OraclePrice` not updated for > X seconds  
- medianizer shows stale value  
- missing feed data  

**Diagnosis Steps:**

- check `priceUpdateTimestamp`  
- compare feed deviations  
- compare medianizer vs DEX TWAP (diagnostic only)  
- verify `blockDelay` behavior  

**Interpretation:**  
System remains stable — liquidation/redemption simply pause until price updates resume.

---

## 3.2 Liquidation Congestion (SEV-0)

**Symptoms:**

- many vaults with `CR < LiquidationCR`  
- few liquidation events  
- StabilityPool absorbs debt intermittently  

**Diagnosis:**

- inspect mempool and gas conditions  
- verify block production  
- inspect LiquidationLogs  
- check StabilityPool capacity  
- check trend of `totalDebt`  

**Interpretation:**  
Network limitation only.  
System remains correct — liquidation executes once blocks resume.

---

## 3.3 Redemption Spike (SEV-1)

**Symptoms:**

- excessive redemptions in short time  
- top-collateralized vaults losing CR quickly  
- pressure on equilibrium price `R`  

**Diagnosis:**

- check redemptions per block  
- inspect CR structure  
- evaluate `RedeemLimit` (if configured)  
- examine redemption volume  

**Interpretation:**  
System functioning normally — redemption stabilizes price.

---

## 3.4 StabilityPool Near Empty (SEV-0)

**Symptoms:**

- low `SurplusBuffer`  
- depleted PLS reserves in StabilityPool  
- liquidation rewards small  

**Diagnosis:**

- check current PLS in pool  
- check recent liquidation load  
- examine CR distribution  

**Interpretation:**  
System remains functional.  
Liquidations continue — rewards adjust downward.

---

## 3.5 Extreme Volatility (SEV-1)

**Symptoms:**

- PLS price moves > 20 % within < 1 hour  
- large number of vaults drop into risk zone  
- redemption volume increases sharply  

**Diagnosis:**

- check oracle update cadence  
- verify block time  
- inspect recent liquidation logs  
- analyze CR structure shifts  

**Interpretation:**  
System behaves as intended — no intervention possible or required.

---

## 3.6 Network / Blockchain Instability (SEV-0)

**Symptoms:**

- long periods without new blocks  
- transactions stuck for minutes  
- chain reorganizations  

**Diagnosis:**

- inspect block explorer  
- check `block.number` progression  
- confirm subgraph indexing delay  
- watch gas price fluctuations  

**Interpretation:**  
System becomes temporarily inert but remains safe —  
liquidation/redemption paused until network resumes.

---

## 3.7 Monitoring / Subgraph Outage (SEV-2)

**Symptoms:**

- UI does not display vaults  
- outdated charts  
- slow or blocked indexing  

**Diagnosis:**

- check via direct RPC calls  
- inspect on-chain events  
- verify subgraph indexing lag  

**Interpretation:**  
Display problem only — protocol is unaffected.

---

# 4. System Diagnosis Protocol

For every incident, record:

- incident timestamp  
- block number  
- oracle values  
- CR distribution  
- StabilityPool status  
- number of liquidations  
- number of redemptions  
- `totalDebt`  
- gas conditions  
- transaction logs  
- impacted vault IDs  

These enable accurate post-mortem analysis.

---

# 5. Decision Matrix (Diagnosis Only)

Because ProjectUSD is immutable after freeze,  
this runbook defines only:

- how to detect issues  
- how to interpret system behavior  
- how to monitor state transitions  
- how to communicate incidents  
- how to document findings  

There are **no corrective actions**.

---

# 6. Communication

For significant incidents, communicate:

- incident type  
- current system behavior  
- expected protocol response  
- what users may observe  
- external contributing factors (network, oracle, volatility)  

Transparency only — no action.

---

# 7. Post-Mortem Process

After a high-severity incident:

- create a post-mortem report  
- document the root cause  
- note block ranges  
- compare oracle feeds  
- inspect liquidation / redemption logs  
- record learnings  

This supports trust and long-term protocol transparency.

---

# 8. License & References

© 2025 Aqua75 / ProjectUSD  
License: MIT for code, CC BY-NC-SA 4.0 for documentation  
References: ProjectUSD Whitepaper V2.1 (Ch. 8–9, Glossary pp. 24–28)  
