---
title: "ProjectUSD – KPI Subgraph SPEC v1"
status: "Draft"
last_updated: "2025-11-19"
author: "Aqua75"
language: "en"
related_whitepaper_sections: ["Ch. 6 – Liquidation & Redemption", "Ch. 7 – System Architecture", "Ch. 9 – Security", "Incident Runbook"]
---

# ProjectUSD – KPI Subgraph SPEC v1

## Purpose

This SPEC defines all Key Performance Indicators (KPIs)  
that the ProjectUSD Subgraph must index, aggregate and expose  
for dashboards, risk monitoring, incident analysis, and auditing.

The KPI Subgraph is used for:

- system monitoring  
- economic stability evaluation  
- liquidation and redemption analytics  
- oracle integrity monitoring  
- vault structure analysis  
- incident detection  
- post-mortem documentation  

Because ProjectUSD becomes fully immutable after the freeze,  
the KPI Subgraph is the **primary long-term observability tool**.

---

# 1. Architecture & Data Flow

## 1.1 Data Sources

The Subgraph consumes on-chain data from:

- VaultEngine  
- StabilityPool  
- Liquidation module  
- Redemption module  
- Oracle (Medianizer)  
- Controller (equilibrium price `R`)  
- Module events  
- Block metadata  

No external APIs.  
No DEX price queries.

---

## 1.2 Indexing Layers

The Subgraph indexes three levels:

- **Vault-level KPIs** (micro-level)  
- **System-wide KPIs** (macro-level)  
- **Incident KPIs** (diagnostics)  

---

# 2. Vault KPIs (Micro Level)

## 2.1 Vault Base Data

The Subgraph stores for each vault:

- VaultID  
- owner address  
- current collateral  
- current debt  
- current CR (`CR = collateral * OraclePrice / debt`)  
- status (active, liquidated, redeemed, empty)  
- creation block, last update block  

---

## 2.2 Vault History (Time Series)

The Subgraph maintains full historical data:

- collateral history  
- debt history  
- CR history  
- liquidation events  
- redemption events  
- all status changes  

**Purpose:**  
Full transparency for auditors and developers.

---

## 2.3 Vault Risk Indicators

- CR decline rate  
- liquidation proximity (`CR / LiquidationCR`)  
- share of system debt  
- share of system collateral  

---

# 3. Liquidation KPIs

## 3.1 Liquidation Metrics

- number of liquidations per block/day  
- absorbed debt per liquidation  
- collateral distributed  
- liquidation impact on CR distribution  
- liquidation efficiency (`eff = collateral / debt`)  

---

## 3.2 Liquidation Timing

- time-to-liquidate (block difference)  
- liquidation queue depth  
- liquidation clustering (event bursts)  

---

## 3.3 Liquidation Risk Indicators

- percentage of risky vaults (`CR < 1.5 * LiquidationCR`)  
- liquidation pressure indicator  
- CR distribution trend  

---

# 4. Redemption KPIs

## 4.1 Redemption Volume

- redemption volume per block/day  
- number of affected vaults  
- average CR loss per redemption  
- systemic redemption pressure (`R-pressure`)  

---

## 4.2 Redemption Dynamics

- redemption frequency  
- redemption chain length  
- redemption spikes (volume > X * baseline)  

---

## 4.3 Redemption Risk Indicators

- load on top-CR vaults  
- vault structure redistribution  
- liquidation-to-redemption ratio  

---

# 5. StabilityPool KPIs

## 5.1 Pool Balance & History

- current PLS balance  
- historical pool balance  
- deposit/withdrawal events  
- reward distribution timeline  

---

## 5.2 Absorption Metrics

- debt absorbed per liquidation  
- total absorbed debt  
- pool health (`poolBalance / totalDebt`)  

---

## 5.3 StabilityPool Risk Indicators

- proximity to zero  
- liquidation capacity estimate  
- depositor reward rate  

---

# 6. Oracle KPIs

## 6.1 Price Feeds

- current median price  
- individual feed prices  
- feed deviation matrix  
- median price history  

---

## 6.2 Oracle Stability

- update frequency  
- update delays (`blockDelay`)  
- outlier detection (`abs(feed - median) > maxDeviation`)  
- medianizer stability  

---

## 6.3 Oracle Risk Indicators

- number of failed feeds  
- deviation from DEX TWAP (diagnostic only)  
- `oracleStale` warning flag  

---

# 7. Controller KPIs (Equilibrium Price R)

## 7.1 R History

- current value of `R`  
- historical R timeline  
- rate of change (`ΔR`)  
- epoch update intervals  

---

## 7.2 R Volatility

- R standard deviation  
- R stability index  
- R convergence rate  

---

## 7.3 R Risk Indicators

- divergence between OraclePrice and `R`  
- redemption pressure on `R`  
- temporary upward/downward deviations  

---

# 8. System-Wide KPIs (Macro Level)

## 8.1 System Health

- `totalDebt`  
- total collateral value  
- system equity (`equity = collateralValue - totalDebt`)  
- debt ratio (`totalDebt / collateralValue`)  
- health factor distribution (aggregated CR histogram)  

---

## 8.2 System Events

- number of active vaults  
- new vaults per day  
- liquidations per day  
- redemptions per day  
- volatility index  

---

## 8.3 Stress Indicators

- percentage of near-liquidation vaults  
- percentage of vaults with rapid CR decline  
- system-wide CR trend  

---

# 9. Incident KPIs (Runbook Integration)

These KPIs integrate directly with the Incident Runbook.

## 9.1 Oracle Incidents

- `oracleStaleCount`  
- `oracleDeviationSpike`  
- feed outlier rate  

---

## 9.2 Liquidation Incidents

- liquidation queue depth  
- number of undercollateralized vaults  
- liquidation anomaly detection  

---

## 9.3 Redemption Incidents

- redemption spike indicator  
- CR loss rate  
- redemption pressure index  

---

## 9.4 Network / Chain Incidents

- block delay  
- gas spikes  
- reorg indicator  

---

# 10. Data Models (Subgraph Entities)

## 10.1 Entities (Excerpt)

```text
Vault {
  id: ID!
  owner: Bytes!
  collateral: BigInt!
  debt: BigInt!
  cr: BigDecimal!
  status: String!
  createdAt: BigInt!
  updatedAt: BigInt!
}
```

```text
Liquidation {
  id: ID!
  vault: Vault!
  debtRepaid: BigInt!
  collateralDistributed: BigInt!
  timestamp: BigInt!
  blockNumber: BigInt!
}
```

```text
Redemption {
  id: ID!
  vaultsInvolved: [Vault!]!
  amountUSD: BigInt!
  collateralReturned: BigInt!
  timestamp: BigInt!
}
```

(Additional entities will be included in the final Subgraph implementation.)

---

## 11. Tests & Validation

### 11.1 UnitTests

correct indexing of events

correctness of CR, R, and price calculations

proper aggregation over vault groups

correct generation of time series

---

### 11.2 Property-Based Tests

bulk liquidations

redemption spikes

CR collapses

feed outages

---

### 11.3 Consistency Checks

collateral and debt sum checks

comparison of aggregated vault values vs on-chain state

verification of all invariants

---

## 12. License & References

© 2025 Aqua75 / ProjectUSD
License: MIT for code, CC BY-NC-SA 4.0 for documentation
References: ProjectUSD Whitepaper V2.1 (Ch. 6–9, Glossary pp. 24–28)
