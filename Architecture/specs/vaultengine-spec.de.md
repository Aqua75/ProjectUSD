---
title: "ProjectUSD – VaultEngine SPEC v1"
status: "Draft"
last_updated: "2025-11-14"
author: "Aqua75"
language: "de"
related_whitepaper_sections: ["Kap. 2 – Systemübersicht", "Kap. 5.1 – Collateral & Vaults", "Kap. 6 – Liquidation & Redemption", "Glossar S. 18–24"]
---

# ProjectUSD – VaultEngine SPEC v1

## Zweck

Die **VaultEngine** ist das zentrale Buchhaltungssystem von ProjectUSD.  
Sie verwaltet:

- alle besicherten Positionen (Vaults),
- das Verhältnis zwischen gebundenem PLS und ausgegebenen ProjectUSD Coins,
- die Schnittstelle zu Liquidation, Redemption und Controller.

Die VaultEngine selbst hält **kein externes Preiswissen** und trifft **keine** Liquidationsentscheidungen.  
Sie stellt ausschließlich konsistente, manipulationsresistente Zustände bereit:

- Collateral-Salden pro Vault  
- Schulden (in ProjectUSD Coin) pro Vault  
- Systemweite Summen und Puffer  

Liquidationslogik, Auktionen und Redemptions werden in der  
`liquidation-redemption-spec` definiert und greifen über wohldefinierte Funktionen auf die VaultEngine zu.

---

## 1. Kernbegriffe & Parameter

| Begriff           | Beschreibung                                                | Beispielwert       | Einheit                          |
|-------------------|-------------------------------------------------------------|--------------------|----------------------------------|
| `VaultID`         | Eindeutiger Index pro Vault                                 | 1, 2, 3, ...       | –                                |
| `owner`           | Adresse, die den Vault kontrolliert                         | `0xABC…`           | Adresse                          |
| `collateral`      | gebundenes PLS im Vault                                     | 10.0               | PLS                              |
| `debt`            | offene Schuld in ProjectUSD Coin                            | 5.0                | ProjectUSD Coin                  |
| `MCR`             | Mindestbesicherungsquote pro Vault                          | 160 %              | % (Wert in PLS / Schuld)        |
| `LiquidationCR`   | Schwelle, ab der ein Vault liquidierbar ist                 | 150 %              | %                                |
| `DebtFloor`       | minimale Schuld pro Vault                                   | 100                | ProjectUSD Coin                  |
| `SystemDebtCap`   | maximale gesamte ProjectUSD Coin-Schuld im System          | noch offen         | ProjectUSD Coin                  |
| `SurplusBuffer`   | Systempuffer für Gebühren und Überschüsse                   | dynamisch          | ProjectUSD Coin                  |
| `BadDebt`         | uneinbringliche Schuld nach Liquidationsereignissen         | 0                  | ProjectUSD Coin                  |
| `r_epoch`         | vom Controller gelieferte Zins-/Gebührquote pro Epoche      | 0.0 – 0.05         | 1/Epoche                         |

**Legende:**  
„noch offen“ kennzeichnet Parameter ohne festen Beispielwert.  
Diese Werte sind Design- oder Governance-Entscheidungen und werden  
über Simulationen und Sicherheitsanalysen festgelegt.

---

## 2. Rollen & Verantwortlichkeiten

### 2.1 VaultEngine

Die VaultEngine garantiert:

- korrekte Buchhaltung von PLS-Collateral und ProjectUSD Coin-Schulden,  
- Einhaltung der Mindestbesicherung (`MCR`),  
- saubere Übergabe an Liquidations- und Redemption-Module,  
- deterministische Anwendung des vom Controller gelieferten Zinssatzes `r_epoch`.

### 2.2 Externe Module

- **Controller:** liefert `r_epoch` und beeinflusst damit Schuldenentwicklung.  
- **Oracle:** liefert den Preis `P` (PLS pro ProjectUSD Coin) an Liquidationslogik.  
- **Liquidation & Redemption:** führen Aktionen aus, die über definierte Schnittstellen  
  Collateral und Schulden in der VaultEngine anpassen.  
- **StabilityPool / SurplusBuffer:** nehmen Gebühren und Überschüsse auf und  
  gleichen Defizite aus (eigene SPEC).

---

## 3. Datenstrukturen

### 3.1 Vault

```solidity
struct Vault {
    address owner;        // Besitzer
    uint256 collateral;   // PLS in Wei
    uint256 debt;         // ProjectUSD Coin (interne Units)
}
```

### 3.2 Globale Zustände

```solidity
mapping (uint256 => Vault) vaults;
uint256 totalCollateral;   // Summe aller PLS in Vaults
uint256 totalDebt;         // Summe aller Schulden in ProjectUSD Coin
uint256 surplusBuffer;     // Systempuffer (Fees, Überschüsse)
uint256 badDebt;           // uneinbringliche Restschulden
```

---

## 4. Kernfunktionen (High Level API)

> Die genaue Signatur wird in einer späteren Contract-SPEC präzisiert.  
> Hier werden nur Verhalten und Invarianten beschrieben.

### 4.1 Vault-Lifecycle

- `openVault()`  
  – erzeugt einen neuen `VaultID` mit `owner = msg.sender`,  
  – initial `collateral = 0`, `debt = 0`.

- `deposit(VaultID id, uint256 amountPLS)`  
  – erhöht `collateral` des Vaults,  
  – erhöht `totalCollateral`.

- `withdraw(VaultID id, uint256 amountPLS)`  
  – reduziert `collateral` des Vaults,  
  – prüft anschließend `CollateralRatio ≥ MCR`,  
  – reduziert `totalCollateral`.

### 4.2 Schuldaufnahme & Rückzahlung

- `mint(VaultID id, uint256 amountProjectUSD)`  
  – erhöht `debt` des Vaults,  
  – erhöht `totalDebt`,  
  – prüft `CollateralRatio ≥ MCR` und `debt ≥ DebtFloor`,  
  – übergibt die geminteten ProjectUSD Coins an den `owner`.

- `repay(VaultID id, uint256 amountProjectUSD)`  
  – reduziert `debt` des Vaults (nicht unter 0),  
  – reduziert `totalDebt`,  
  – ggf. werden anteilige Zinsen zuerst bedient, Principal danach.

### 4.3 Rate-Anwendung (Controller-Integration)

- `applyEpochRate(uint256 r_epoch)`  
  – wird einmal pro Epoche aufgerufen (nur durch den Controller oder ein autorisiertes Modul),  
  – aktualisiert `debt` aller Vaults entsprechend der Formel:  
    `debt_next = debt_prev * (1 + r_epoch)`  
  – akkumuliert die Differenz `debt_next − debt_prev` systemweit im `surplusBuffer`,  
  – aktualisiert `totalDebt`.

Zur Effizienz kann die Implementation mit „globalen Multiplikatoren“ arbeiten,  
statt jede Position einzeln zu aktualisieren. Die Invariante bleibt jedoch identisch.

### 4.4 Liquidations- und Redemption-Hooks

- `liquidate(VaultID id, LiquidationContext ctx)`  
  – nur aufrufbar durch das Liquidation-Modul,  
  – prüft, ob `CollateralRatio < LiquidationCR`,  
  – passt `collateral`, `debt`, `totalCollateral`, `totalDebt`, `surplusBuffer` und `badDebt`  
    entsprechend dem in `liquidation-redemption-spec` definierten Verfahren an.

- `redeem(uint256 amountProjectUSD, RedemptionContext ctx)`  
  – nur aufrufbar durch das Redemption-Modul,  
  – reduziert systemweite `totalDebt`,  
  – bewegt Collateral aus übersicherten Vaults an den Redeemer,  
  – Details siehe `liquidation-redemption-spec`.

---

## 5. Besicherungsquote & Liquidationskriterien

### 5.1 Collateral Ratio (CR)

Für jeden Vault gilt:

`CR = (collateral * P) / debt`

- `collateral` in PLS  
- `P` in PLS pro ProjectUSD Coin  
- `debt` in ProjectUSD Coin  

### 5.2 Mindestanforderungen

**Mindestbesicherung:**  
`CR ≥ MCR` nach jeder Benutzeraktion (`mint`, `withdraw`).

**Liquidierbarkeit:**  
Ein Vault ist potentiell liquidierbar, wenn:  
`CR ≤ LiquidationCR`

Die konkrete Auslösung (wann, durch wen, mit welcher Belohnung)  
wird in der Liquidations-SPEC geregelt.

---

## 6. Invarianten

| ID | Invariante                                  | Bedeutung                                         |
| -- | ------------------------------------------- | ------------------------------------------------- |
| V1 | `totalCollateral ≥ Σ vault.collateral`      | Es gehen keine PLS „verloren“ in der Buchhaltung. |
| V2 | `totalDebt ≥ Σ vault.debt`                  | Systemdebt entspricht Summe der Vault-Schulden.   |
| V3 | `CR ≥ MCR` für alle aktiven Vaults          | Alle aktiven Vaults bleiben überbesichert.        |
| V4 | `DebtFloor == 0` ⇒ `debt == 0` oder ≥ Min   | keine Staub-Schulden unterhalb `DebtFloor`.       |
| V5 | `badDebt` wird nur durch Liquidation erhöht | uneinbringliche Schuld entsteht nicht „heimlich“. |
| V6 | `surplusBuffer ≥ 0`                         | Puffer kann nie negativ werden.                   |

**Hinweis:**  
`Σ` bezeichnet die Summe über alle existierenden Vaults.

---

## 7. Telemetrie & Messgrößen

| KPI                | Beschreibung                               | Quelle                |
| ------------------ | ------------------------------------------ | --------------------- |
| `SystemCR`         | systemweite Collateral Ratio               | Subgraph (Vaults + P) |
| `AvgVaultCR`       | durchschnittliche CR aller Vaults          | Subgraph-Auswertung   |
| `DebtDistribution` | Verteilung der Schulden nach Größenklassen | Analytics / Subgraph  |
| `BadDebt`          | Höhe uneinbringlicher Schulden             | VaultEngine-Events    |
| `SurplusLevel`     | Höhe des Systempuffers                     | VaultEngine-Events    |

Empfehlung: 
- wöchentliche „State of the System“-Berichte analog zum „State of the Peg“ aus der Controller-SPEC.

---

## 8. Offene Designparameter

| Parameter                     | Status                  | Nächster Schritt                           |
| ----------------------------- | ----------------------- | ------------------------------------------ |
| `MCR`                         | 150–180 %               | Simulation verschiedener Marktphasen       |
| `LiquidationCR`               | 140–160 %               | Abstimmung mit Liquidationsmechanismus     |
| `DebtFloor`                   | noch offen              | Analyse Gas-Kosten vs. Fragmentierung      |
| `SystemDebtCap`               | noch offen              | hängt von PulseChain-Liquidität ab         |
| `r_epoch`-Granularität        | definiert im Controller | gemeinsame Simulationsbasis mit Controller |
| `FeeSplit` (Surplus vs. Pool) | noch offen              | Definition in StabilityPool-SPEC           |

**Alle Parameter sind ausdrücklich als Design in Progress zu verstehen,**
bis Simulationen und Backtests vorliegen.

---

## 9. Verification (Prüf- & Validierungsleitfaden)

**Ziel:**  
Nachweis, dass die VaultEngine:

- alle Invarianten aus Abschnitt 6 einhält,  
- korrekt mit dem Controller zusammenarbeitet,  
- unter Stressbedingungen (Preisstürze, Massenliquidationen) konsistent bleibt.

**Methoden:**

- **UnitTests (Foundry)**  
  – Erstellung, Befüllung und Schließung von Vaults  
  – Tests für `mint`, `repay`, `deposit`, `withdraw`  
  – gezielte Verletzungsversuche der Invarianten (sollten revertieren)

- **Property-Based Tests**  
  – zufällige Sequenzen von Benutzeraktionen über viele Epochen  
  – Sicherstellung, dass `totalCollateral` und `totalDebt` konsistent bleiben

- **SimKit-Szenarien**  
  – Kopplung an Controller- und Oracle-Simulation  
  – Preisstürze, Überlastung, lange Seitwärtsphasen  
  – Auswertung von `SystemCR`, `BadDebt`, `SurplusBuffer`

**Akzeptanzkriterien:**

- keine Invariante aus Abschnitt 6 wird in Tests verletzt,  
- unter extremen Preisschocks bleibt `BadDebt` innerhalb vorher definierter Risikoschwellen,  
- die Anwendung von `r_epoch` führt zu nachvollziehbaren, reproduzierbaren Schuldenpfaden.

---

## 10. Interaktion mit anderen SPECS

- **Controller-SPEC:** definiert, wie `r_epoch` berechnet wird.  
  Die VaultEngine wendet den Wert nur deterministisch an.

- **Oracle-SPEC:** liefert `P` für CR-Berechnungen und Liquidations-Trigger  
  (über das Liquidationsmodul, nicht direkt in der VaultEngine).

- **Liquidation-Redemption-SPEC:** beschreibt detailliert, wie  
  `liquidate()` und `redeem()` auf die VaultEngine zugreifen.

- **StabilityPool-SPEC:** definiert, wie Gebühren und Überschüsse aus  
  `surplusBuffer` in Pools fließen oder für Systemstabilisierung genutzt werden.

- **Security-SPEC:** listet alle Schutzmechanismen (Reentrancy, Caps, RateLimits)  
  und verweist auf konkrete Checks in der VaultEngine-Implementierung.

---

## 11. Lizenz & Referenzen

© 2025 Aqua75 / ProjectUSD  
Lizenz: MIT für Code, CC BY-NC-SA 4.0 für Dokumentation  
Verweis: ProjectUSD Whitepaper V2.1 (Kap. 2, 5.1, 6, Glossar S. 18–24)
