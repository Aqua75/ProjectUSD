---
title: "ProjectUSD – StabilityPool SPEC v1"
status: "Draft"
last_updated: "2025-11-15"
author: "Aqua75"
language: "de"
related_whitepaper_sections: ["Kap. 6 – Liquidation & Redemption", "Kap. 7 – Stability Layer", "Glossar S. 22–24"]
---

# ProjectUSD – StabilityPool SPEC v1

## Zweck

Der **StabilityPool** ist ein zentraler Sicherheitsmechanismus im ProjectUSD-System.  
Er dient dazu:

- systemweite Schulden (*ProjectUSD Coin*) im Liquidationsfall zu absorbieren,  
- im Gegenzug PLS-Collateral aus liquidierten Vaults zu erhalten,  
- Überschüsse und Gebühren aus der VaultEngine aufzunehmen,  
- BadDebt zu verhindern oder stark zu begrenzen.

Der StabilityPool ermöglicht ein **verlustarmes, sofortiges Liquidationsmodell**,  
das ohne Auktionen oder externe Bieter auskommt und damit:

- schnell,  
- manipulationsresistent,  
- gas-effizient  
arbeitet.

---

## 1. Kernkonzept

Der StabilityPool folgt einem einfachen Prinzip:

> **Liquidity Providers (LPs) hinterlegen ProjectUSD Coins im StabilityPool.  
> Wenn ein Vault liquidiert wird, übernimmt der Pool dessen Schulden –  
> und erhält dafür das Collateral dieses Vaults.**

Damit ermöglicht der Pool:

- **sofortige Liquidation**, ohne komplizierte Auktionsmechaniken,  
- **BadDebt-Vermeidung**, weil Schulden durch bereitstehendes ProjectUSD gedeckt werden,  
- **Collateral-Gewinn für LPs**, weil sie PLS unter Marktwert erhalten.

Das System bleibt dadurch extrem stabil, selbst bei starken Preisstürzen.

---

## 2. Rollen & Akteure

| Rolle                 | Beschreibung |
|-----------------------|--------------|
| **Depositor (LP)**   | Hinterlegt ProjectUSD im Pool & erhält anteilig PLS aus Liquidationen |
| **StabilityPool**     | Aggregiert Schuldenabsorptionskapital |
| **VaultEngine**       | Liefert Schulden- & Collateral-Werte, erhöht `surplusBuffer` |
| **Liquidation-Modul** | Führt Liquidationen aus und ruft Pool-Funktionen auf |
| **Controller**        | Indirekt beteiligt über `r_epoch` und Systemdebt-Entwicklung |

---

## 3. Datenstrukturen

### 3.1 StabilityPool

```solidity
struct StabilityPool {
    uint256 totalDeposits;      // Summe aller eingezahlten ProjectUSD Coins
    uint256 totalPLSClaimable;  // Gesamtmenge an PLS, die den LPs zusteht (nicht ausgezahlt)
    
}
```
### 3.2 Individuelle Depositoren

```solidity
mapping (address => uint256) deposits;      // ProjectUSD Coin
mapping (address => uint256) PLS_credits;   // zugewiesene PLS aus Liquidationen
```

---

## 4. Kernfunktionen (High Level API)

### 4.1 Einzahlung & Entnahme

deposit(uint256 amountProjectUSD)
– erhöht deposits[msg.sender],
– erhöht totalDeposits.

withdraw(uint256 amountProjectUSD)
– reduziert den Deposit (soweit vorhanden),
– reduziert totalDeposits,
– LP erhält zusätzlich seine bisher angesammelten PLS_credits.

### 4.2 Liquidation-Integration

Wenn liquidation(VaultID) in der VaultEngine ausgelöst wird:

Das Liquidation-Modul ruft
absorbDebt(VaultID id, uint256 debt, uint256 collateralPLS)
auf.

Der StabilityPool übernimmt die Schuld:
totalDeposits -= debt

Das Collateral fließt vollständig an die LPs:
totalPLSClaimable += collateralPLS

Anteilige Verteilung erfolgt proportional nach LP-Anteil:

LP_share = deposits[LP] / totalDeposits_before

PLS_credits[LP] += LP_share * collateralPLS

### 4.3 Überschüsse aus VaultEngine

Wenn die VaultEngine Systemgebühren erzeugt:

surplusBuffer wächst ← diese Gebühren können dem StabilityPool zugeführt werden
(Mechanismus wird in StabilityPool v2 spezifiziert).

---

## 5. Liquidationslogik (Interaktion mit VaultEngine)

Ein Vault wird liquidierbar, wenn:

CR ≤ LiquidationCR

Das Liquidation-Modul:

liest debt und collateral aus der VaultEngine,

ruft absorbDebt() im StabilityPool auf,

setzt den Vault in der VaultEngine auf debt = 0, collateral = 0,

aktualisiert totalDebt und totalCollateral.

Der StabilityPool ist niemals für:

Preisberechnungen,

Liquidations-Trigger,

Penalty-Definitionen
verantwortlich.

Diese Logik liegt in der Liquidation-SPEC.

---

## 6. Invarianten

| ID | Invariante                                      | Bedeutung                               |
| -- | ----------------------------------------------- | --------------------------------------- |
| S1 | `totalDeposits ≥ 0`                             | Pool kann nie negativ werden            |
| S2 | `deposits[LP] ≥ 0`                              | keine negativen LP-Balances             |
| S3 | `totalPLSClaimable ≥ Σ PLS_credits[LP]`         | Buchhaltungskonsistenz                  |
| S4 | `absorbDebt()` darf nur durch Liquidation-Modul | kein direkter Angriff über LP-Interface |
| S5 | Liquidation führt nie zu BadDebt                | Pool absorbiert immer vollständig       |

---

## 7. Telemetrie & KPIs

| KPI                  | Beschreibung                            |
| -------------------- | --------------------------------------- |
| `PoolCoverageRatio`  | `totalDeposits / totalDebt`             |
| `LiquidityAvailable` | projectUSD im Pool zur Schulden-Deckung |
| `PLSRewards`         | noch nicht ausgezahlte PLS-Credits      |
| `LiquidationVolume`  | kumulierte absorbierte Schulden         |
| `AvgRewardPerLP`     | durchschnittliche PLS-Rendite           |

---

## 8. Offene Designparameter

| Parameter          | Status | Nächster Schritt                |
| ------------------ | ------ | ------------------------------- |
| `MinDeposit`       | offen  | Gas-Kostenanalyse               |
| `RewardDelay`      | offen  | Anti-Flash-Arbitrage            |
| `PoolFeeShare`     | offen  | in Verbindung mit SurplusBuffer |
| `DistributionMode` | offen  | linear vs. pro-epoch            |

Alle Parameter befinden sich im Design-in-Progress-Status
und werden durch Simulationen und Backtests festgelegt.

---

## 9. Verification (Prüf- & Validierungsleitfaden)

Ziel:
Sicherstellen, dass:

Liquidationen ohne BadDebt funktionieren,

LPs proportional korrekt PLS erhalten,

Pool-Buchhaltung immer stabil und konsistent bleibt.

Methoden:

UnitTests (Foundry):
– Ein-/Auszahlung,
– multiple simultane LPs,
– Debt-Absorption in verschiedenen Szenarien.

Property-Based Tests:
– Zufällige LP-Bewegungen während Serien von Liquidationen.

SimKit Szenarien:
– starke Preisstürze → viele Vaults liquidieren gleichzeitig,
– langfristige Stressphasen mit hoher Volatilität.

Akzeptanzkriterien:

alle Invarianten (S1–S5) bleiben in jeder Simulation gültig,

keine Schuldenreste im System (BadDebt = 0),

alle LPs erhalten exakt proportional berechnete PLS-Credits.

---

## 10. Interaktion mit anderen SPECS

VaultEngine-SPEC: liefert Collateral und Debt-Daten.

Controller-SPEC: beeinflusst Systemdebt-Entwicklung über r_epoch.

Oracle-SPEC: indirekt relevant als Preisbasis für Liquidationen.

Liquidation-SPEC: definiert Trigger und Liquidationsmechanik.

Security-SPEC: validiert Ein-/Auszahlungslogik, Caps & Safety-Checks.

---

## 11. Lizenz & Referenzen

© 2025 Aqua75 / ProjectUSD
Lizenz: MIT für Code, CC BY-NC-SA 4.0 für Dokumentation
Verweis: ProjectUSD Whitepaper V2.1 (Kap. 6, 7, Glossar S. 22–24)
