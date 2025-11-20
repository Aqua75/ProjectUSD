# ProjectUSD Glossar  
### Definitionen aller zentralen Begriffe und Konzepte

Dieses Glossar liefert präzise Definitionen aller Begriffe aus der  
ProjectUSD-Architektur, den SPECS und dem Whitepaper.

---

## 🧩 Zentrale Konzepte

**ProjectUSD**  
Ein vollständig autonomes Geldsystem für PulseChain, basierend auf algorithmischem Gleichgewicht.

**Gleichgewichtspreis (R)**  
Interner Referenzwert, der Redemption und Systemstabilität steuert.

**r-Epoche**  
Periodisches Systemupdate, bei dem der Controller globale Parameter anpasst.

**Freeze-Event**  
Einmaliger Prozess, der den Core dauerhaft unveränderlich macht.

**Unveränderlicher Core**  
VaultEngine, Controller, Oracle, Liquidation/Redemption, StabilityPool.

---

## 🏦 Vault- & Collateral-Begriffe

**Vault**  
Nutzerposition mit Collateral und Schulden.

**Collateral Ratio (CR)**  
Collateral-Wert / Schuld, als Prozentwert.

**Minimum Collateral Ratio (MCR)**  
Schwellenwert, unter dem liquidiert wird.

**Systemschuld**  
Gesamte umlaufende Menge an ProjectUSD.

---

## 🔄 Stabilität & Liquidation

**Stability Pool**  
Kollektiver Puffer, der unterbesicherte Vaults absorbiert.

**Liquidation**  
Erzwungene Abwicklung bei Unterschreiten der MCR.

**Redemption**  
Eintausch von ProjectUSD gegen PLS zum Gleichgewichtspreis R.

---

## 🔒 Sicherheit & Invarianten

**Atomarität**  
Jede Statusänderung ist vollständig oder wird vollständig rückgängig gemacht.

**Invarianten**  
Ökonomische oder logische Regeln, die immer erfüllt sein müssen.

**Deviation Limit**  
Maximal zulässige Abweichung zwischen Orakelquellen.

---

## 📈 Analyse & Monitoring

**Subgraph-KPIs**  
Metriken für Vault-Gesundheit, Systemstabilität, Oracle-Verhalten und Incidents.

**Incident-Runbook**  
Ablauf zur Diagnose unerwarteter Ereignisse in unabhängigen Implementationen.

---

## 👥 Community- / Entwicklerbegriffe

**Self-Starter**  
Mitwirkender, der eigenständig handelt.

**Part-Time Steward**  
Community-Mitglied mit wiederkehrender Supportrolle.

**Spezifikation (SPEC)**  
Technischer Bauplan für notwendiges Systemverhalten.
