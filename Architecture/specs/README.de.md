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

- vaultengine-spec.de.md / .en.md  
  Logik der Vaults, Schulden, Collateral, CR-Berechnung und atomare Zustandsänderungen.

- R-spec.de.md / .en.md  
  Definition des internen Referenzpreises R des Systems, der von Controller und Redemption verwendet wird.

- controller-spec.de.md / .en.md  
  Kontrollalgorithmus für die Systemrate r basierend auf der Abweichung zwischen Marktpreis P und internem Referenzpreis R.

- oracle-spec.de.md / .en.md  
  Marktpreisfeed P, Medianizer-Logik, Redundanz und Sicherheitslimits.

- liquidation-redemption-spec.de.md / .en.md  
  Liquidations- und Redemption-Abläufe, Vault-Auswahlregeln und Sicherheitsinvarianten.

- stabilitypool-spec.de.md / .en.md  
  Mechanik des StabilityPools, Absorption von Schulden und Verteilung von Collateral.

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
2. **R-spec**
3. **controller-spec**  
4. **oracle-spec**  
5. **liquidation-redemption-spec**  
6. **stabilitypool-spec**  
7. **security-spec**  
8. **governance-freeze-spec** → dann **freeze-checklist**  
9. **incident-runbook**  
10. **kpi-subgraph-spec**

Diese Reihenfolge erläutert zuerst die ökonomische Basis (Vaults),  
dann das Steuerungssystem (Controller, Oracle),  
danach die Sicherheitsmechanismen (Liquidation, Pool, Security),  
und abschließend Monitoring & Diagnostik.

---

## 🔒 Core vs. Periphery

Die SPECS unterscheiden zwischen:

### **Core (nach Freeze unveränderlich)**
- VaultEngine
- R
- Controller  
- Oracle
- Liquidation & Redemption  
- StabilityPool  

### **Periphery (änderbar via Governance)**
- Analytics (Subgraph)  
- DEX-LP Module  
- Frontend / Monitoring-Tools  

---

## 📘 Whitepaper-Bezug

Alle SPECS entsprechen den Konzepten aus dem  
**ProjectUSD Whitepaper V2.2**  
(Architektur, Invarianten, Freeze-Modell, Systemgleichgewichtspreis R).

---

## 🪙 Lizenz
CC BY-NC-SA 4.0  
© 2026 Aqua75 / ProjectUSD
