---
title: "ProjectUSD – Liquidation & Redemption SPEC v1"
status: "Draft"
last_updated: "2025-11-18"
author: "Aqua75"
language: "de"
related_whitepaper_sections: ["Kap. 6 – Liquidation & Rücktausch", "Kap. 9 – Sicherheit", "Glossar S. 18–22"]
---

# ProjectUSD – Liquidation & Redemption SPEC v1

## Zweck

Diese SPEC definiert die vollständige Logik für:

1. **Liquidation** (Zwangsauflösung eines unterbesicherten Vaults)  
2. **Redemption** (Rücktausch von ProjectUSD Coin gegen Collateral zum Systempreis)

Beide Mechanismen sind zentrale Sicherheitskomponenten von ProjectUSD  
und garantieren langfristige Systemstabilität ohne zentrale Eingriffe.

---

# 1. Liquidation (Zwangsauflösung)

## 1.1 Prinzip

Ein Vault wird liquidiert, wenn:

`CR` < `LiquidationCR`

Das heißt, der Marktpreis von PLS (Collateral) ist relativ zum Systemwert der Schuld zu stark gefallen.

Ziel der Liquidation:

- verhindern, dass das System ungedeckte Schulden hält  
- sicherstellen, dass jede ProjectUSD-Schuld immer durch Collateral gedeckt bleibt  
- automatische Stabilisierung ohne Governance

---

## 1.2 Trigger-Bedingung

Die Liquidation wird ausgelöst, sobald:

```solidity
CR < LiquidationCR
```

Berechnung:

```solidity
CR = (collateral * OraclePrice) / debt
```

OraclePrice = Median aus mehreren Preisfeeds.

---

## 1.3 Ablauf der Liquidation (atomar)

Eine Liquidation erfolgt in einem atomaren Ablauf, ohne Zwischenzustände:

- Oracle liefert aktuellen Preis  
- Vault wird als unterbesichert erkannt  
- StabilityPool absorbiert die Schulden  
- PLS (Collateral) wird an StabilityPool-Teilnehmer verteilt  
- Vault wird auf `collateral = 0` / `debt = 0` gesetzt  
- Event wird ausgelöst (`Liquidation(...)`)  

Kein Teil dieses Vorgangs kann durch MEV manipuliert werden.

---

## 1.4 Interaktion mit dem StabilityPool

Der StabilityPool erfüllt zwei Aufgaben:

- Schulden absorbieren  
- PLS aus der Liquidation an Einzahler verteilen  

Der Liquidationsalgorithmus:

```solidity
absorbDebt(vaultID, debtAmount);
distributeCollateral(proRata);
resetVault(vaultID);
```

Keine Aktion ruft externe Verträge auf → kein Reentrancy-Risiko.

---

## 1.5 Sicherheit & MEV-Schutz

Schutzmechanismen:

- keine externen Calls  
- atomische Ausführung  
- keine Slippage  
- kein Preisvergleich mit DEX (reiner Medianizer)  
- keine Flashloan-Abhängigkeiten  
- Preisschwelle nur über Oracle manipulierbar (durch Median fast unmöglich)  
- Liquidation und LP-Operationen dürfen nie im selben Block stattfinden  

---

## 1.6 Liquidationskosten

Es existieren keine Liquidationsgebühren.
Die „Belohnung“ für Liquidatoren ergibt sich ausschließlich aus:

- das PLS, das sie aus dem StabilityPool erhalten  

---

## 1.7 Invarianten der Liquidation

| ID | Invariante                             | Bedeutung                          |
| -- | -------------------------------------- | ---------------------------------- |
| L1 | Liquidation erzeugt nie BadDebt        | System verliert nie gedeckten Wert |
| L2 | Liquidation ist atomar                 | keine Zwischenzustände             |
| L3 | CR < LiquidationCR immer Voraussetzung | keine Fehltrigger                  |
| L4 | StabilityPool bleibt nie negativ       | Sicherheit der Puffer              |
| L5 | Oracle bestimmt Preis, nicht DEX       | Manipulationsschutz                |

---

## 1.8 Telemetrie & Monitoring

Telemetriepunkte:

- Anzahl aktiver Vaults  
- Liquidationsereignisse  
- absorbierte Schulden  
- verteiltes Collateral  
- durchschnittliche CR aller Vaults  
- Oracle-Preisabweichungen  

---

## 1.9 Tests (Liquidation)

### UnitTests

- Liquidation bei `CR < LiquidationCR`  
- keine Liquidation bei `CR >= LiquidationCR`  
- Debt-Absorption durch StabilityPool  
- CR-Berechnung korrekt  
- atomarer Ablauf garantiert  

### Property-Based Tests

- Preis-Chaos-Simulation  
- Liquidationsstürme  
- Oracle-Ausreißer  

### Static Analysis

- Reentrancy unmöglich  
- keine externen Calls  
- keine Loops mit unbounded iteration  

---

## 2. Redemption (Rücktausch)

### 2.1 Prinzip

Redemption ermöglicht es, ProjectUSD Coin jederzeit gegen PLS einzutauschen
– zum Systemwert, nicht zum DEX-Preis.

Dies schafft einen absoluten Mindestwert für ProjectUSD und stabilisiert den Peg.

1 ProjectUSD Coin → (1 / R) PLS

R = Systemgleichgewichtspreis aus Controller-SPEC.

---

### 2.2 Warum Redemption notwendig ist

- erzeugt garantierten Mindestwert  
- verhindert langfristige Unterdeckung  
- eliminiert PLS/ProjectUSD Arbitrage-Zonen  
- hält den Marktpreis nahe R  
- ermöglicht automatische Preiskorrekturen  
- schützt Nutzer langfristig  

---

### 2.3 Ablauf der Redemption

- Nutzer sendet ProjectUSD Coin an VaultEngine  
- System wählt den am stärksten überbesicherten Vault  
- Collateral dieses Vaults wird reduziert  
- Schulden dieses Vaults werden reduziert  
- Nutzer erhält entsprechend PLS  

Redemption ist **nicht**:

- ein Liquidationsmechanismus  
- ein Notfallmechanismus  
- ein Preisfixing durch Governance  

Es ist ein reiner, algorithmischer Prozess.

---

### 2.4 Auswahl der Vaults (FIFO nach Überbesicherung)

Vaults werden in folgender Reihenfolge reduziert:

- höchstes CR zuerst  
- nächstes höchstes CR  
- usw.  

Dies stellt sicher:

- fairen Ausgleich  
- keine Überbelastung einzelner Nutzer  
- natürliche Harmonisierung der Collateralstruktur  

---

### 2.5 Sicherheit & MEV-Schutz

- keine externen Calls  
- keine DEX-Interaktionen  
- Oracle-Preis + R sind die einzigen Faktoren  
- Redemption-Volumen per Block begrenzbar (`RedeemLimit`)  
- kein Flashloan-Arbitrage (Systempreis ≠ DEX-Preis)  
- atomare Ausführung  

---

### 2.6 Invarianten der Redemption

| ID | Invariante                                 | Bedeutung             |
| -- | ------------------------------------------ | --------------------- |
| R1 | Redemption erzeugt nie BadDebt             | System bleibt gedeckt |
| R2 | Vault bleibt nie negativ                   | Collateral >= 0       |
| R3 | nur überbesicherte Vaults werden reduziert | Fairness              |
| R4 | Systemwert bleibt erhalten                 | Konsistenz            |
| R5 | keine DEX-Preiskomponente                  | Manipulationsschutz   |

---

### 2.7 Telemetrie & Monitoring

- Gesamt-Redemption-Volumen  
- Anzahl betroffener Vaults  
- durchschnittliche CR-Veränderung  
- Collateral-Abfluss durch Redemption  
- Oracle-Preisbewegungen  
- `R` (Systemgleichgewichtspreis)  

---

### 2.8 Tests (Redemption)

### UnitTests

- Redemption reduziert ausschließlich überbesicherte Vaults  
- CR-Reihenfolge korrekt  
- atomare Abläufe  
- Preisberechnung korrekt  

### Property-Based Tests

- Extrempreisbewegungen  
- Multi-Redemption-Szenarien  
- Stress-Redemption  

### Static Analysis

- keine externen Calls  
- keine manipulationsanfälligen Loops  

---

## 3. Interaktion mit anderen SPECS

- **VaultEngine-SPEC:**  
  – Liquidationen und Redemptions verändern Vaults atomar  

- **StabilityPool-SPEC:**  
  – absorbiert Schulden aus Liquidationen  

- **Oracle-SPEC:**  
  – Preisquelle für CR  

- **Controller-SPEC:**  
  – R bestimmt Redemption-Raten  

- **Security-SPEC:**  
  – garantiert atomare, manipulationsfreie Abläufe  

- **Freeze-SPEC:**  
  – Liquidation & Redemption bleiben nach Freeze unverändert  

---

## Lizenz

© 2025 Aqua75 / ProjectUSD  
Lizenz: MIT für Code, CC BY-NC-SA 4.0 für Dokumentation  
Verweis: ProjectUSD Whitepaper V2.1 (Kap. 6, 9, Glossar S. 18–22)  
