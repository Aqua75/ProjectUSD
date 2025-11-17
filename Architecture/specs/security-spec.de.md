---
title: "ProjectUSD – Security SPEC v1"
status: "Draft"
last_updated: "2025-11-17"
author: "Aqua75"
language: "de"
related_whitepaper_sections: ["Kap. 9 – Sicherheit & Invarianten", "Kap. 8 – Freeze", "Glossar S. 26–28"]
---

# ProjectUSD – Security SPEC v1

## Zweck

Diese SPEC definiert das vollständige Sicherheitsmodell von ProjectUSD.  
Es basiert auf **Hard-Security & Minimal Trust**, d. h.:

- keine Upgrades  
- keine Admin-Pfade  
- keine Proxy-Verträge  
- keine dynamischen Parameter nach Freeze  
- keine Backdoors  
- vollständige Unveränderlichkeit und Berechenbarkeit  
- Schutz vor MEV, Preismanipulation, Reentrancy, DoS und Front-Runs  
- maximale Prüfbarkeit durch statische Invarianten

Sicherheit wird **nicht** durch Governance erzielt, sondern durch:

- deterministische Regeln,  
- mathematische Invarianten,  
- formale Kontrolle der Datenflüsse,  
- strikte Zugangsbeschränkungen,  
- frühzeitige Parameterfixierung,  
- irreversiblen Freeze.

---

## 1. Sicherheitsgrundsätze

### 1.1 Kein Vertrauen in Personen oder Gremien  
Nach Freeze existiert **keine Governance** und kein Admin.  
Alle Sicherheitsgarantien sind permanent im Code verankert.

### 1.2 Keine Upgrades  
Es existieren:

- **keine Proxy-Verträge**,  
- keine Upgradable Patterns,  
- keine „delegatecall“-basierten Modularitäten.

Der gesamte Code bleibt unveränderlich.

### 1.3 Alle Parameter werden vor Freeze fixiert  
Nach dem Freeze sind alle Parameter vollständig schreibgeschützt:

- MCR  
- LiquidationCR  
- DebtFloor  
- SystemDebtCap  
- maxLPExposure  
- maxSlippage  
- Rate-Limits  

### 1.4 Nur deterministische Sicherheit  
Es gibt keine „Live-Intervention“ und keine Rettungsmechanismen.  
Sicherheit wird ausschließlich geboten durch:

- mathematische Invarianten,  
- Locked-Parameter,  
- Limits,  
- Checks,  
- Reverts.

### 1.5 Minimaler externer Angriffsraum  
Es existiert keine zentrale Macht, die kompromittiert werden könnte.  
Alle Systemaktionen sind 100% öffentlich, deterministisch und transparent.

---

## 2. Angriffsmodell (Threat Model)

ProjectUSD schützt sich vor:

- **Reentrancy-Angriffen**  
- **MEV-Sandwiching** (insbesondere bei LP/DEX-Funktionen)  
- **Oracle-Manipulation**  
- **Flash-Loan-Attacken**  
- **DoS auf Liquidationspfade**  
- **Front-Running bei Liquidationen**  
- **Preismanipulation an DEX-Paaren**  
- **wirtschaftlichen Manipulationsmustern** (BadDebt-Erzeugung)  
- **Überlastung von State-Änderungen** (Rate Limits)  

Nicht erforderlich sind Schutzmaßnahmen gegen:

- Governance-Kapern  
- Admin-Key-Compromise  
- Hintertüren  

(Ist durch den Freeze danach grundsätzlich ausgeschlossen).

---

## 3. Systemweite Sicherheitsarchitektur

### 3.1 Globale Zustände

```solidity
bool public isFrozen;
uint256 public lastExecutionTimestamp;
```

### 3.2 Keine Admin-Rollen

```solidity
address public constant ADMIN = address(0);
```

### 3.3 Parameter-Lockdown

```solidity
require(isFrozen == true);
```

### 3.4 Rate-Limits (Anti-MEV)

```solidity
mapping(address => uint256) lastAction;
uint256 public rateLimitDelay;
```

- verhindert Spam
- verhindert Flash-Loan-Kaskaden
- verhindert MEV-Cluster-Handlungen
- limitiert die pro-Block-Handlungsfrequenz

### 3.5 Deterministische Revert-Pfade

Jede sicherheitsrelevante Operation führt bei Verletzung zu:

```solidity
require(false, "SECURITY_VIOLATION");
```

Die Fehlertexte sind unveränderlich.

---

## 4. Schutzmechanismen pro Modul

### 4.1 VaultEngine

- keine Reentrancy  
- keine externen Aufrufe innerhalb von State-Änderungen  
- Validierung aller Vault-Eingaben  
- CR-Prüfung vor jeder Aktion  
- `totalDebt`-Konsistenz-Kontrolle  
- keine Flash-Mint-Mechaniken  

### 4.2 StabilityPool

- kein direkter Zugriff von externen Contracts  
- nur das Liquidation-Modul darf `absorbDebt()` auslösen  
- PLS-Verteilung proportional, nicht durch Loops (Gas-Sicherheit)  
- keine negativen Pool-Stände (Invariante SP3)  

### 4.3 Liquidation-Modul

- Nutzung von Snapshot-Daten, niemals Live-Preismanipulation  
- atomare Liquidationen:  
  – debt absorbieren  
  – collateral transferieren  
  – Vault zurücksetzen  
- keine externen Calls mit untrusted data  

### 4.4 Oracle-Modul

- Median-Mechanismus aus mehreren Feeds  
- starke Outlier-Filterung  
- Block-Delay-Cap zur Anti-Spoofing-Prävention  
- niemals weniger als `N_feeds`  
- Schutz vor DEX-Only-Manipulation  

### 4.5 Controller

- Berechnung von `r_epoch` ist deterministisch  
- keine Live-Parameteränderungen  
- keine Kontrollmechanismen durch Governance  
- uninterpretiert und unveränderlich  
- keine Stimulationspfade von außen  

### 4.6 DEX-LP-System

- nur vor Freeze aktivierbar  
- Anti-MEV-Slippage-Grenzen  
- Einsatz privater RPC durch Offchain-Bot (optional)  
- keine LP-Operation im selben Block wie Liquidation  
- Hard-Cap: `maxLPExposure`  

---

## 5. Sicherheitsinvarianten (Systemweite Regeln)

| ID | Invariante                                    | Bedeutung                   |
| -- | --------------------------------------------- | --------------------------- |
| S1 | `isFrozen` ändert sich nach Freeze nie wieder | absolut irreversibel        |
| S2 | keine Admin-Rolle existiert                   | kein privilegierter Zugriff |
| S3 | alle Parameter bleiben konstant nach Freeze   | vollständige Deterministik  |
| S4 | `totalDebt >= 0` immer wahr                   | Buchhaltungskonsistenz      |
| S5 | Liquidation erzeugt nie BadDebt               | Sicherheit des Systems      |
| S6 | Oracle verändert nur preisbezogene Daten      | keine externe Kontrolle     |
| S7 | keine Funktion erlaubt Upgrades               | keine Proxy-Pfade           |

---

## 6. Telemetrie & Monitoring

Nach dem Freeze:

- Monitoring ist rein lesend  
- alle Parameter sind statisch  

**Telemetrie liefert nur wesentliche Werte:**

- `isFrozen`  
- `totalDebt`  
- Vault-Kennzahlen  
- Liquidationsereignisse  
- StabilityPool-Daten  
- Gebührenentwicklungen  
- Systemrisiken (berechnet, nicht parametergesteuert)  

---

## 7. Offene Designparameter (nur vor Freeze relevant)

| Parameter            | Status | Beschreibung               |
| -------------------- | ------ | -------------------------- |
| `rateLimitDelay`     | offen  | Anti-MEV Frequenzkontrolle |
| `N_feeds`            | offen  | Oracle-Redundanz           |
| `maxDeviation`       | offen  | Preisabweichungsgrenze     |
| `slippageProtection` | offen  | LP/Liquidationsschutz      |
| `blockDelay`         | offen  | Anti-Spoofing-Puffer       |

Nach Freeze sind alle Parameter final gesperrt.

---

## 8. Verification (Prüf- & Validierungsleitfaden)

**Ziel:**  
Nachweis, dass das System nach Freeze:

- unveränderlich ist,  
- deterministisch funktioniert,  
- alle Invarianten einhält,  
- sicherheitskritische Angriffe zuverlässig verhindert.  

**Methoden:**

- **UnitTests:**  
  – Vault-Interaktionen  
  – Liquidationen  
  – Systemdebt-Änderungen  
  – Slippage-Verletzungsversuche  

- **Property-Based Tests:**  
  – zufällige State-Folgen  
  – extrem volatile Szenarien  
  – Oracle-Manipulationsversuche  

- **Static Analysis:**  
  – Verbot von Upgrades  
  – Reentrancy-Scan  
  – Unreachable Branch Checks  

**Akzeptanzkriterien:**

- S1–S7 (Sicherheitsinvarianten in Abschnitt 5) werden nie verletzt  
- kein Upgrade möglich (verifizierbar über Bytecode)  
- Reentrancy unmöglich  
- Liquidation immer sicher  
- Controller arbeitet deterministisch  

---

## 9. Interaktion mit anderen SPECS

- **VaultEngine-SPEC:**  
  – Sicherheit durch invariantenbasiertes Minting/Burning  

- **Controller-SPEC:**  
  – deterministische Rate-Berechnung, unveränderlich  

- **Oracle-SPEC:**  
  – manipulationsresistenter Medianizer  

- **StabilityPool-SPEC:**  
  – schützt Systemdebt durch sofortige Liquidationen  

- **DEX-LP-SPEC:**  
  – Anti-MEV-Schutz und LP-Caps  

- **Governance-Freeze-SPEC:**  
  – Security-Modell abgeschlossen nach Freeze  

---

## 10. Lizenz & Referenzen

© 2025 Aqua75 / ProjectUSD  
Lizenz: MIT für Code, CC BY-NC-SA 4.0 für Dokumentation  
Verweis: ProjectUSD Whitepaper V2.1 (Kap. 9, 8, Glossar S. 26–28)  
