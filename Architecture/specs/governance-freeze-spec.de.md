---
title: "ProjectUSD – Governance & Freeze SPEC v1"
status: "Draft"
last_updated: "2025-11-16"
author: "Aqua75"
language: "de"
related_whitepaper_sections: ["Kap. 8 – Governance & Freeze", "Glossar S. 24–26"]
---

# ProjectUSD – Governance & Freeze SPEC v1

## Zweck

Diese SPEC definiert das Governance-Modell von ProjectUSD **vor** dem Freeze  
und die Systemlogik **nach** der Freeze-Aktivierung.

Der Freeze ist:

- **absolut irreversibel**,  
- **dauerhaft**,  
- **ohne Backdoors**,  
- **ohne Notfallschlüssel**,  
- **ohne Upgrade-Mechanismen**.

Nach der Aktivierung des Freeze wird ProjectUSD zu einem vollständig  
autonomen, unveränderlichen Protokoll – vergleichbar mit einem  
algorithmisch festgelegten, mathematisch definierten Asset.

Die Governance existiert ausschließlich bis zum **einmaligen**  
Governance-Freeze-Event.

---

## 1. Prinzipien der ProjectUSD-Governance (vor Freeze)

### 1.1 Minimalistische Governance

Die Governance existiert nur, um:

- Parameter vor dem Freeze festzulegen,  
- Systemmodule zu aktivieren oder zu deaktivieren,  
- Risiko- und Sicherheitsanalysen abzuschließen,  
- den Freeze vorzubereiten.

Sie **darf nicht**:

- Preise setzen,  
- Marktinterventionen durchführen,  
- Algorithmik beeinflussen,  
- den Controller oder Oracle manipulieren.

### 1.2 Governance-Rechte sind temporär

Governance ist ein **temporäres Hilfsmodul**.

Sobald der Freeze aktiviert wird:

- endet jede Governance-Berechtigung,  
- alle Governance-Funktionen werden deaktiviert,  
- alle Parameter werden schreibgeschützt.

### 1.3 Kein Delegationsmodell

Es gibt:

- keine Stimmrechte,  
- keine Token-basierten Abstimmungen,  
- keine Governance-Tokens.

Governance ist ein rein technisches Setup-Modul.

---

## 2. Governance-Berechtigungen (vor Freeze)

| Bereich               | Berechtigung | Beschreibung |
|----------------------|--------------|--------------|
| Parameter-Setup      | erlaubt      | Anpassung von Systemparametern bis Freeze |
| Modul-Aktivierung    | erlaubt      | Aktivieren/Deaktivieren einzelner Komponenten |
| DEX-LP-Management    | erlaubt      | nur vor Freeze |
| Sicherheits-Parameter| erlaubt      | Rate-Limits, Slippage-Limits |
| Freeze-Aktivierung   | erlaubt      | einmalige Auslösung |

**Nicht erlaubt:**

- Kontrolle über Preise  
- Kontrolle über Liquidationen  
- Kontrolle über Controller oder Oracle  
- Eingriffe in VaultEngine-Logik  
- Änderungen nach Freeze

---

## 3. Freeze-Mechanismus (zentrale Architektur)

### 3.1 Typ: Vollständig irreversibler Freeze (Variante 1)

Der Freeze ist:

- **nicht wieder aufhebbar**,  
- **nicht verhandelbar**,  
- **nicht überschreibbar**,  
- **nicht durch Notfall-Keys auflösbar**,  
- **nicht durch MultiSig rückgängig machbar**.

Es gibt **keinen Mechanismus**, der den Freeze brechen kann.

### 3.2 Aktivierung durch Governance

Governance ruft einmalig auf:

- `activateFreeze()`  

Dies führt zu:

- Setzen des globalen Flags: `isFrozen = true`  
- vollständige Deaktivierung aller Governance-Module  
- permanente Deaktivierung aller Setter-Funktionen in allen Kernmodulen  
- Entfernen aller Admin-Rollen  
- Unzugänglichkeit aller nachträglichen Vertragsänderungen  
- Entfernen aller externen Kontrolleingänge

### 3.3 Wirkungen auf das System

Nach `isFrozen = true`:

- System-Parameter sind absolut schreibgeschützt  
- Contracts sind für immer unveränderlich  
- DEX-LP-System wird deaktiviert  
- Governance-Funktionalität existiert nicht mehr  
- alle Sicherheits-Kontrollpfade funktionieren nur noch automatisch  
- jede mutierende Admin-Funktion wird dauerhaft deaktiviert

---

## 4. Governance-Funktionen (vor Freeze)

### 4.1 Parameter-Setup

- `setMCR()`  
- `setLiquidationCR()`  
- `setDebtFloor()`  
- `setSystemDebtCap()`  
- `setRateLimits()`  
- `setMaxLPExposure()`  
- `setMaxSlippage()`  

Diese Funktionen existieren **nur vor Freeze** und sind nach Aktivierung  
desselben permanent deaktiviert.

### 4.2 Modulsteuerung

- `enableLP()` / `disableLP()`  
- Aktivieren/Deaktivieren einzelner Pools  
- Aktivieren/Deaktivieren analytischer Module  
- Freigeben oder Sperren experimenteller Funktionen (nur bis Freeze)

### 4.3 Sicherheit & Risk-Controls

- Setzen von Sicherheitsgrenzen  
- Aktualisierung von MEV-Schutzparametern  
- Einstellen von Caps & Rate-Limits

Diese Parameter definieren NUR Sicherheitsgrenzen, NICHT Ökonomie oder Preislogik.

---

## 5. Technische Architektur des Freeze

### 5.1 Globale Variable

```solidity
bool public isFrozen;
```

### 5.2 Freeze-Auslösung

```solidity
function activateFreeze() external onlyGovernance {
    require(!isFrozen, "ALREADY_FROZEN");
    isFrozen = true;
    _disableGovernance();
    _lockAllParameters();
    _disableAdminFunctions();
}
```

### 5.3 Parameter-Lockdown

```solidity
function _lockAllParameters() internal {
    // alle Setter dauerhaft deaktivieren
}
```

### 5.4 Governance-Deaktivierung

```solidity
function _disableGovernance() internal {
    // entfernt alle Rollen
    // löscht Governance-Privilegien
}
```

### 5.5 Admin-Funktionen deaktivieren

```solidity
function _disableAdminFunctions() internal {
    // deaktiviert alle Admin-Pfade
    // keine Updates, keine Parameteränderungen
}
```

Nach Freeze existiert kein Contract-Code, der
Mutationen oder Upgrades erlaubt.

---

## 6. Invarianten

| ID | Invariante                                  | Bedeutung                           |
| -- | ------------------------------------------- | ----------------------------------- |
| G1 | `isFrozen` ist nach Aktivierung immer TRUE  | Freeze ist irreversibel             |
| G2 | Alle Governance-Funktionen sind deaktiviert | keine Änderungen mehr möglich       |
| G3 | Alle Parameter-Setter sind deaktiviert      | System bleibt unverändert           |
| G4 | Keine Admin-Rolle existiert                 | keine zentrale Kontrolle            |
| G5 | Controller/Oracle bleiben algorithmisch     | Governance kann sie nicht verändern |

---

## 7. Telemetrie & Überwachung

Nach dem Freeze:

Monitoring kann nur noch lesend erfolgen

kein Parameter ist veränderbar

nur noch On-Chain-Metriken werden angezeigt

Telemetrie enthält:

isFrozenFlag

Systemdebt

Collateral-Verteilungen

Liquidationsdaten

Vault-Status

Surplus-Daten

---

## 8. Offene Designparameter (nur vor Freeze)

Vor dem Freeze müssen festgelegt werden:

| Parameter       | Status | Beschreibung         |
| --------------- | ------ | -------------------- |
| `MCR`           | offen  | Mindestbesicherung   |
| `LiquidationCR` | offen  | Liquidationsschwelle |
| `DebtFloor`     | offen  | minimale Schuld      |
| `maxLPExposure` | offen  | System-LP-Grenze     |
| `maxSlippage`   | offen  | LP-Slippage-Limit    |
| `RateLimits`    | offen  | Anti-MEV-Grenzen     |

Nach Freeze sind alle Parameter final.

---

## 9. Verification (Prüf- & Validierungsleitfaden)

Ziel:
Nachweis, dass:

der Freeze sicher aktiviert wird,

danach keine Parameteränderung mehr möglich ist,

alle Mutationspfade deaktiviert sind,

keine Governance- oder Admin-Rolle existiert.

Methoden:

UnitTests:
– Aktivierung von activateFreeze()
– sicherstellen, dass alle Setter revertieren
– sicherstellen, dass Governance zurückgesetzt ist

Static Analysis:
– Prüfung, dass es keinen Upgrade-Pfad gibt
– Prüfung, dass keine ungeschützten Mutationsfunktionen existieren

Property-Based Tests:
– zufällige Angriffsversuche (Parameter-Mutationen)

Akzeptanzkriterien:

alle Invarianten G1–G5 bleiben in 100 % aller Tests bestehen

Freeze ist nach Aktivierung nicht auflösbar

keine einzige Funktion erlaubt Änderungen am Systemzustand

System verhält sich strikt deterministisch

---

## 10. Interaktion mit anderen SPECS

VaultEngine-SPEC:
– bleibt unveränderlich nach Freeze

Controller-SPEC:
– algorithmisch, nicht governance-gesteuert

Oracle-SPEC:
– governance-unabhängiger Medianizer

StabilityPool-SPEC:
– keine Parameter änderbar nach Freeze

DEX-LP-SPEC:
– System-LP wird vollständig deaktiviert

Security-SPEC:
– alle Sicherheitsgrenzen nur vor Freeze einstellbar

---

## 11. Lizenz & Referenzen

© 2025 Aqua75 / ProjectUSD
Lizenz: MIT für Code, CC BY-NC-SA 4.0 für Dokumentation
Verweis: ProjectUSD Whitepaper V2.1 (Kap. 8, Glossar S. 24–26)
