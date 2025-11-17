---
title: "ProjectUSD – KPI Subgraph SPEC v1"
status: "Draft"
last_updated: "2025-11-19"
author: "Aqua75"
language: "de"
related_whitepaper_sections: ["Kap. 6 – Liquidation & Redemption", "Kap. 7 – Systemarchitektur", "Kap. 9 – Sicherheit", "Incident-Runbook"]
---

# ProjectUSD – KPI Subgraph SPEC v1

## Zweck

Diese SPEC definiert alle Key Performance Indicators (KPIs),  
die durch einen Subgraphen überwacht, aggregiert und für Dashboards bereitgestellt werden.

Der KPI-Subgraph dient:

- der Systemüberwachung  
- der Analyse wirtschaftlicher Stabilität  
- der Bewertung von Liquidation/Redemption-Verhalten  
- der Überwachung von Oracle-Integrität  
- der Analyse der Vault-Gesamtstruktur  
- der Vorbereitung und Interpretation von Incidents  
- dem Post-Mortem-Prozess  

Da ProjectUSD nach dem Freeze unveränderlich ist,  
ist der KPI-Subgraph die **zentrale Informationsquelle**, um das System langfristig zu verstehen.

---

# 1. Architektur & Datenfluss

## 1.1 Datenquellen

Der Subgraph bezieht Daten ausschließlich aus:

- VaultEngine  
- StabilityPool  
- Liquidation-Modul  
- Redemption-Modul  
- Oracle (Medianizer)  
- Controller (Systemgleichgewichtspreis R)  
- Events aller Module  
- On-Chain-Blockdaten  

Keine externen APIs.  
Keine DEX-Daten.

---

## 1.2 Indexierungsebenen

Der Subgraph arbeitet auf drei Ebenen:

- **Vault-Ebene** (Mikro-KPIs)  
- **System-Ebene** (Makro-KPIs)  
- **Incident-Ebene** (Diagnose-KPIs)  

---

# 2. Vault-KPIs (Micro-Level)

### 2.1 Vault-Basisdaten

Der Subgraph speichert für jeden Vault:

- VaultID  
- Owner-Adresse  
- aktuelles Collateral  
- aktuelle Schuld  
- aktuelles CR (`CR = collateral * OraclePrice / debt`)  
- Status (aktiv, liquidiert, redeemed, leer)  
- Erstellungsblock, letzter Updateblock  

---

### 2.2 Vault-Historie

Für jeden Vault wird eine vollständige Historie geführt:

- Collateral-Verlauf  
- Debt-Verlauf  
- CR-Verlauf  
- Liquidationsereignisse  
- Redemption-Ereignisse  
- Zeitreihen aller Statusänderungen  

**Zweck:**  
Transparente Nachvollziehbarkeit aller Vault-Entwicklungen.

---

### 2.3 Vault-Risikoindikatoren

- CR-Abfallgeschwindigkeit  
- Liquidationsnähe (`CR / LiquidationCR`)  
- Anteil am SystemDebt  
- Anteil am SystemCollateral  

---

# 3. Liquidation-KPIs

### 3.1 Liquidationsmetriken

- Anzahl Liquidationen pro Block / pro Tag  
- absorbiertes Debt pro Liquidation  
- verteiltes Collateral  
- Liquidation-Impact auf CR-Struktur  
- durchschnittliche Liquidationseffizienz (`eff = collateral/debt`)  

---

### 3.2 Liquidationszeiten

- Time-to-Liquidate (Blockdifferenz)  
- LiquidationQueueDepth  
- Liquidationshäufung (Clustergrößen)  

---

### 3.3 Liquidationsrisiko

- Anteil riskanter Vaults (`CR < 1.5 * LiquidationCR`)  
- Liquidationsdruckindikator (Anzahl gefährdeter Vaults)  
- Liquidationsvorhersage (Trend der CR-Struktur)  

---

# 4. Redemption-KPIs

### 4.1 Redemption-Mengen

- Redemption-Volumen pro Block / Tag  
- Anzahl beteiligter Vaults  
- durchschnittlicher CR-Verlust pro Redemption  
- Systemischer Redemption-Druck (`R-Pressure`)  

---

### 4.2 Redemption-Dynamik

- Redemption-Frequenz  
- Redemption-Chain-Length (Anzahl Vaults pro Redemption)  
- Redemption-Spikes (Heuristik: Volumen > X * Durchschnitt)  

---

### 4.3 Redemption-Risikoindikatoren

- Belastung der Top-CR-Vaults  
- Veränderung der Collateral-Struktur  
- Verhältnis: Liquidation vs. Redemption  

---

# 5. StabilityPool-KPIs

### 5.1 Pool-Balance & Verlauf

- aktuelle PLS-Menge im Pool  
- historischer PLS-Verlauf  
- Einzahlungs- und Auszahlungsereignisse  
- Zeitreihen der Belohnungsverteilung  

---

### 5.2 Absorptionsmetriken

- Debt-Absorption pro Liquidation  
- Gesamtmenge absorbierter Schulden  
- Poolgesundheit (`poolBalance / totalDebt`)  

---

### 5.3 Poolrisiko

- Annäherung an Nullsaldo  
- Kapazität für zukünftige Liquidationen  
- Belohnungsrate für Einzahler  

---

# 6. Oracle-KPIs

### 6.1 Preisfeeds

- aktueller Medianpreis  
- Einzel-Feed-Werte  
- Feed-Abweichungsmatrix  
- historischer Medianverlauf  

---

### 6.2 Oracle-Stabilität

- Updatefrequenz  
- Verzögerungen (`blockDelay`)  
- Ausreißererkennung (`abs(feed - median) > maxDeviation`)  
- Medianizer-Stabilität  

---

### 6.3 Oracle-Risikoindikatoren

- Anzahl ausgefallener Feeds  
- Divergenz zum DEX-TWAP (diagnostisch, nicht systemrelevant)  
- Warnflag `oracleStale`  

---

# 7. Controller-KPIs (Systemgleichgewichtspreis R)

### 7.1 R-Verlauf

- aktueller R-Wert  
- historischer R-Verlauf  
- Änderungsrate (`ΔR`)  
- Epoch-Update-Zeiten  

---

### 7.2 R-Volatilität

- Standardabweichung von R  
- R-Stabilitätsindex  
- R-Konvergenzrate  

---

### 7.3 R-Risikoindikatoren

- Divergenz zwischen Oracle-Preis und R  
- Belastung durch Redemption-Spikes  
- temporäre Aufwärts-/Abwärtsabweichungen  

---

# 8. Systemweite KPIs (Macro-Level)

### 8.1 Systemgesundheit

- `totalDebt`  
- Gesamt-Collateralwert  
- Systemequity (`Equity = CollateralValue - totalDebt`)  
- DebtRatio (`totalDebt / CollateralValue`)  
- HealthFactorDistribution (aggregierte CR-Verteilung)  

---

### 8.2 System-Ereignisse

- Anzahl aktiver Vaults  
- neue Vaults pro Tag  
- liquidierte Vaults pro Tag  
- redemptions pro Tag  
- Volatilitätsindex  

---

### 8.3 Stressindikatoren

- Anteil von Vaults nahe Liquidation  
- Anteil von Vaults mit stark fallendem CR  
- CR-Veränderungsrate über alle Vaults  

---

# 9. Incident-KPIs (für das Incident-Runbook)

Diese KPIs dienen der automatischen Unterstützung des Incident-Prozesses.

### 9.1 Orakel-Incidents

- `oracleStaleCount`  
- `oracleDeviationSpike`  
- `feedOutlierRate`  

### 9.2 Liquidations-Incidents

- LiquidationQueueDepth  
- Anzahl gleichzeitig unterbesicherter Vaults  
- Abweichung Liquidationen/Block  

### 9.3 Redemption-Incidents

- Redemption-Spike-Indikator  
- CR-Loss-Rate  
- RedemptionPressureIndex  

### 9.4 Netzwerk-/Chain-Incidents

- BlockDelay  
- GasSpikes  
- ReorgIndicator  

---

# 10. Datenmodelle (Subgraph Entities)

## 10.1 Entities (Auszug)

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

(Weitere Entities folgen im tatsächlichen Graph-Code.)

---

## 11. Tests & Validierung

### 11.1 UnitTests

- korrekte Indexierung aller Events  
- Korrektheit von CR-, R- und Preisberechnungen  
- Aggregation über Vault-Gruppen  
- Zeitreihen richtig erzeugt  

---

### 11.2 Property-Based Tests

- Bulk-Liquidationen  
- Redemption-Spikes  
- CR-Stürze  
- Feed-Ausfälle  

---

### 11.3 Konsistenzprüfungen

- Summenprüfungen für Collateral und Debt
- Vergleich von Vault-Gesamtwerten mit On-Chain-Zustand
- Prüfen aller Invarianten

---

## 12. Lizenz & Referenzen

© 2025 Aqua75 / ProjectUSD  
Lizenz: MIT für Code, CC BY-NC-SA 4.0 für Dokumentation  
Referenzen: ProjectUSD Whitepaper V2.1 (Kap. 6–9, Glossar S. 24–28)  
