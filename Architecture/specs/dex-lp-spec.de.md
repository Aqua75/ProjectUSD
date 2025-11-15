---
title: "ProjectUSD – DEX-LP SPEC v1"
status: "Draft"
last_updated: "2025-11-15"
author: "Aqua75"
language: "de"
related_whitepaper_sections: ["Kap. 4 – Marktmechanik", "Kap. 7 – Liquidity Layer", "Glossar S. 20–24"]
---

# ProjectUSD – DEX-LP SPEC v1

## Zweck

Die **DEX-LP-Schnittstelle** beschreibt, ob und wie ProjectUSD mit  
dezentralen Börsen (DEX) interagiert, um Liquidität bereitzustellen.

Das Ziel ist *nicht*, ProjectUSD zu einem AMM-System zu machen, sondern:

- Preisstabilität durch ausreichende Liquidität sicherzustellen,  
- Spread zwischen Kauf/Verkauf minimal zu halten,  
- Liquiditätsengpässe in Extremsituationen zu vermeiden,  
- optional System-LP-Positionen auf PulseChain zu ermöglichen  
  (ProjectUSD/PLS).

Die DEX-LP-SPEC wird nur aktiv, wenn Governance entscheidet,  
dass das System **eigene LP-Positionen** halten darf.  
Im „Freeze“-Status sind alle LP-Funktionen deaktiviert.

---

## 1. DEX-Grundlagen im ProjectUSD-Kontext

ProjectUSD interagiert ausschließlich mit:

- **AMM-Pools auf PulseChain** (z. B. PulseX, 1inch Aggregationen)  
- Paaren der Form:  
  - ProjectUSD / PLS  
  - ProjectUSD / stable-oraclesichere Assets (z. B. PLSX)  
  - ProjectUSD / wETH (optional für Routing)

Es gibt **keine Off-Chain-Liquidity** und keine CEX-Integration.

---

## 2. Rollen & Akteure

| Rolle            | Beschreibung |
|------------------|--------------|
| **SystemLP**     | Contract-Modul, das LP-Positionen im Namen des Systems hält |
| **Governance**   | aktiviert/deaktiviert System-LP-Funktionen, definiert Parameter |
| **DEX-Pool**     | AMM-Pool auf PulseChain |
| **LP-Provider**  | Externe Benutzer, die Liquidität hinzufügen (nicht Teil der SPEC) |

---

## 3. Designziele

3.1 **Spread-Reduktion**  
Große Preisabweichungen werden durch tiefe Liquidität reduziert.

3.2 **Zielkorridor um R (interner Gleichgewichtspreis)**  
System-LP ergänzt externe LP, um ProjectUSD/PLS in einem Preiskorridor zu halten.

3.3 **Maximaler Schutz vor MEV**  
Durch spezifische Regeln (siehe Security-SPEC):

- Schutz vor Sandwich-Angriffen  
- Kein Front-Running bei System-LP-Transaktionen  
- Einsatz von privaten RPCs und verzögerten Ausführungen  

3.4 **Keine direkte Preisbeeinflussung**  
System-LP **darf nicht aktiv traden**.  
Es stellt nur passiv Liquidität bereit.

---

## 4. Datenstrukturen

### 4.1 LPStatus

```solidity
struct LPStatus {
    bool enabled;              // ob System-LP aktiv ist
    uint256 usdAmount;         // Menge an ProjectUSD Coin im LP
    uint256 plsAmount;         // Menge an PLS im LP
    uint256 lpTokens;          // erhaltene LP-Token des DEX-Pools
}
```

### 4.2 Globale Zustände

```solidity
LPStatus systemLP;
address dexPoolAddress;        // Ziel-Pool (z. B. ProjectUSD/PLS)
uint256 maxLPExposure;         // maximale System-LP-Position in ProjectUSD Coin
```

---

## 5. Kernfunktionen

### 5.1 Aktivierung & Parameter

- `enableLP(uint256 maxExposure)`  
  – aktiviert System-LP  
  – setzt maximale Projekt-Exposure  

- `disableLP()`  
  – deaktiviert System-LP  
  – ermöglicht kein weiteres Bereitstellen von Liquidität  
  – Entzug vorhandener LP-Positionen bleibt möglich  

### 5.2 Bereitstellen von Liquidität

- `provideLiquidity(uint256 amountProjectUSD, uint256 amountPLS)`  
  – fügt im DEX-Pool Liquidität hinzu  
  – erhält DEX-spezifische LP-Token  
  – aktualisiert `systemLP.lpTokens`, `usdAmount`, `plsAmount` 

### 5.3 Abziehen von Liquidität

- `withdrawLiquidity(uint256 lpTokenAmount)`  
  – löst LP-Token im DEX ein  
  – erhält PLS & ProjectUSD Coin zurück  
  – bucht zurück in System-LP-Cache  

### 5.4 Parameter Constraints

- LP darf niemals mehr als `maxLPExposure` bereitstellen  
- keine täglichen LP-Deltas > definierter Rate-Limiter  
- LP-Funktion immer nur durch Governance oder MultiSig  

---

## 6. AMM-Interaktion

### 6.1 Gültige DEX-Typen

Unterstützte AMM-Modelle:

- Constant-Product-AMM (`x*y=k`)  
- Concentrated Liquidity (CLAMM, PulseX v2)  
- Weighted Balancer Pools (optional)  

### 6.2 Simulation & Schutz

Jede LP-Transaktion muss:

- Slippage-Parameter respektieren (`maxSlippage`)  
- private RPCs/Relays nutzen  
- Fehlermeldungen auslösen, wenn:  
  - Liquidität im Pool zu tief ist  
  - pathologische AMM-Zustände erkannt werden  
  - Preisabweichung zu stark ist (Oracle Deviation Check)  

### 6.3 Interner Benchmark

System prüft bei jeder LP-Aktion:

`PLS_per_USD_LP ≤ P * (1 + Δ)`

wobei:

P = Oracle-Preis (PLS per ProjectUSD Coin)

Δ = erlaubte Abweichung, z. B. 2 %

---

## 7. Invarianten

| ID | Invariante                                    | Bedeutung                        |
| -- | --------------------------------------------- | -------------------------------- |
| L1 | `systemLP.enabled` muss explizit gesetzt sein | kein versehentliches LP          |
| L2 | `usdAmount + plsAmount` ≤ `maxLPExposure`     | System darf nicht überexponieren |
| L3 | `lpTokens ≥ 0`                                | keine negativen LP-Bestände      |
| L4 | LP-Operationen nur durch Governance           | kein unautorisierter Zugriff     |
| L5 | jede LP-Aktion löst Slippage-Prüfung aus      | Schutz vor MEV-Attacken          |

---

## 8. Telemetrie & KPIs

| KPI               | Beschreibung                                         |
| ----------------- | ---------------------------------------------------- |
| `LPDepth`         | bereitgestellte Gesamtliquidität                     |
| `LPShareSystem`   | Anteil des Systems an der gesamten DEX-Liquidität    |
| `ImpermanentLoss` | IL-Schätzung durch AMM-Simulation                    |
| `LPYield`         | Rendite aus PLS/ProjectUSD im Verhältnis zu lpTokens |
| `LPExposure`      | Anteil des Systems relativ zu maxLPExposure          |

---

## 9. Offene Parameter

| Parameter          | Status | Nächster Schritt             |
| ------------------ | ------ | ---------------------------- |
| `maxLPExposure`    | offen  | Simulation Liquiditätsrisiko |
| `maxSlippage`      | offen  | PulseX-Optimierung           |
| `LPActivationMode` | offen  | Governance-Entscheidung      |
| `LPExitMode`       | offen  | geplanter Freeze-Workflow    |

**Alle Parameter sind Design-in-Progress**,  
bis Modeling & Backtests vollständig sind.

---

## 10. Verification (Prüf- & Testleitfaden)

**Ziel:**  
Nachweis, dass System-LP:

- sicher aktiviert/deaktiviert wird,  
- nicht unautorisiert handeln kann,  
- nie überexponiert ist,  
- korrekte LP-Token- und PLS/ProjectUSD-Balancen führt.  

**Methoden:**

- **UnitTests:**  
  – Aktivieren/Deaktivieren  
  – Slippage-Verletzungsversuche  
  – Provide/Withdraw Liquidität  

- **Property-Based Tests:**  
  – zufällige LP-Bewegungen unter starker Volatilität  

- **AMM-Simulation:**  
  – IL-Szenarien  
  – Preisverzerrungen  
  – manipulierte Blöcke  

**Akzeptanzkriterien:**

- Invarianten L1–L5 bleiben in allen Tests gültig,  
- keine LP-Transaktion riskiert Exposure über Cap,  
- LP-Positionswerte stimmen exakt mit DEX-Poolwerten überein.  

---

## 11. Interaktion mit anderen SPECS

- **VaultEngine-SPEC:** kann Collateral/Schulden an System-LP weiterreichen (optional).  
- **Controller-SPEC:** beeinflusst `r_epoch` → System-Deleveraging kann LP-Verhalten verändern.  
- **Oracle-SPEC:** liefert den Preis für LP-Slippage-Checks.  
- **Security-SPEC:** definiert MEV-Schutz & Rate-Limits.  
- **Governance-Freeze-SPEC:** legt fest, wann LP deaktiviert wird.  

---

## 12. Lizenz & Referenzen

© 2025 Aqua75 / ProjectUSD  
Lizenz: MIT für Code, CC BY-NC-SA 4.0 für Dokumentation  
Verweis: ProjectUSD Whitepaper V2.1 (Kap. 7, Glossar S. 20–24)  
