# ProjectUSD – SPECS Übersicht

Diese README-Datei bietet eine vollständige Orientierung über alle technischen
Spezifikationen (SPECS) von ProjectUSD.  
Sie dient als Einstieg für Entwickler, Auditoren, Forscher und Community-Mitglieder.

## 📚 Zweck der SPECS

Die SPECS definieren **jede Komponente des Systems** auf professionellem
Architektur- und Auditniveau.  
ProjectUSD ist ein vollständig autonomes, nach Freeze unveränderliches
Stablecoin-Protokoll — entsprechend wichtig ist eine vollständige, transparente
und modular dokumentierte Struktur.

## 🧩 Modulübersicht

Die SPECS gliedern sich in die folgenden Bereiche:

### **Core Module (unveränderlich nach Freeze)**

- **vaultengine-spec.de.md / .en.md**  
  Logik der Vaults, Schulden, Collateral, CR-Berechnung, atomare Zustandsänderungen.

- **controller-spec.de.md / .en.md**  
  Algorithmus für Systemgleichgewichtspreis R und r-Epoch Logik.

- **oracle-spec.de.md / .en.md**  
  Medianizer, Redundanz, Block-Delay, Deviation Limits.

- **liquidation-redemption-spec.de.md / .en.md**  
  Liquidation, Redemption, Invarianten, Sicherheit, atomare Abläufe.

- **stabilitypool-spec.de.md / .en.md**  
  Mechanismus des StabilityPools, Absorption von Systemschulden, Verteilung des Collaterals.

### **Security & Freeze**

- **security-spec.de.md / .en.md**  
  Sicherheitsgrundlagen: MEV-Schutz, atomare Abläufe, Reentrancy-Schutz.

- **governance-freeze-spec.de.md / .en.md**  
  Unveränderlichkeitsmodell, Freeze-Prozess, Governance-Ausschluss.

- **freeze-checklist.de.md / .en.md**  
  Schritt-für-Schritt Checkliste zur Vorbereitung des finalen Freeze.

### **Monitoring, Analytics & Incident Handling**

- **kpi-subgraph-spec.de.md / .en.md**  
  Datenmodell & KPIs für den Subgraph (Vaults, System KPIs, Oracle KPIs, Incident KPIs).

- **incident-runbook.de.md / .en.md**  
  Diagnoseleitfaden für verschiedene Incident-Typen (technisch, ökonomisch, Oracle, Netzwerk).

### **Peripherie (optional & flexibel)**

- **dex-lp-spec.de.md / .en.md**  
  Optionaler Mechanismus für LP-Integration über einen DEX.

---

## 🗂️ Lesereihenfolge (Empfehlung für neue Entwickler)

1. **vaultengine-spec**  
2. **controller-spec**  
3. **oracle-spec**  
4. **liquidation-redemption-spec**  
5. **stabilitypool-spec**  
6. **security-spec**  
7. **governance-freeze-spec** → dann **freeze-checklist**  
8. **incident-runbook**  
9. **kpi-subgraph-spec**

Diese Reihenfolge erläutert zuerst die ökonomische Basis (Vaults),  
dann das Steuerungssystem (Controller, Oracle),  
danach die Sicherheitsmechanismen (Liquidation, Pool, Security),  
und abschließend Monitoring & Diagnostik.

---

## 🔒 Core vs. Periphery

Die SPECS unterscheiden zwischen:

### **Core (nach Freeze unveränderlich)**
- VaultEngine  
- Liquidation & Redemption  
- Controller  
- Oracle  
- StabilityPool  

### **Periphery (änderbar via Governance)**
- Analytics (Subgraph)  
- DEX-LP Module  
- Frontend / Monitoring-Tools  

---

## 📘 Whitepaper-Bezug

Alle SPECS entsprechen den Konzepten aus dem  
**ProjectUSD Whitepaper V2.1**  
(Architektur, Invarianten, Freeze-Modell, Systemgleichgewichtspreis R).

---

## 🪙 Lizenz
CC BY-NC-SA 4.0  
© 2025 Aqua75 / ProjectUSD
