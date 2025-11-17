---
title: "ProjectUSD – Freeze-Checklist v1"
status: "Draft"
last_updated: "2025-11-18"
author: "Aqua75"
language: "de"
related_whitepaper_sections: ["Kap. 8 – Governance & Freeze", "Kap. 9 – Sicherheit", "Glossar S. 24–28"]
---

# ProjectUSD – Freeze-Checklist v1

## Zweck

Diese Checkliste definiert alle technischen, organisatorischen und sicherheitsrelevanten Schritte,  
die **vor der Aktivierung des irreversiblen Freeze** abgeschlossen sein müssen.

Nach der Aktivierung von `activateFreeze()` wird ProjectUSD zu einem vollständig autonomen,  
unveränderlichen System ohne Governance, Admin-Rechte oder Upgrade-Pfade.

Ein Freeze ist endgültig – diese Liste dient dazu, sicherzustellen,  
dass **alle Voraussetzungen** erfüllt sind, bevor dieser Schritt erfolgt.

---

# 1. Technische Voraussetzungen (Core System)

## 1.1 Parameter-Finalisierung

Alle Systemparameter müssen final gesetzt und dokumentiert sein:

- [ ] `MCR` (Minimum Collateral Ratio)  
- [ ] `LiquidationCR`  
- [ ] `DebtFloor`  
- [ ] `SystemDebtCap`  
- [ ] `maxLPExposure`  
- [ ] `maxSlippage`  
- [ ] `RateLimits`  
- [ ] `blockDelay` (Oracle-Schutz)  
- [ ] `maxDeviation` (Preisabweichung)  
- [ ] `N_feeds` (Oracle-Redundanz)

**Ziel:** Nach Freeze können diese Werte nie wieder verändert werden.

---

## 1.2 Modulstatus

Alle Module müssen in ihrem vorgesehenen Endzustand sein:

- [ ] VaultEngine vollständig aktiviert  
- [ ] StabilityPool aktiv  
- [ ] Liquidation-Modul aktiv  
- [ ] Oracle stabil, Feeds synchron  
- [ ] DEX-LP-System im vorgesehenen Zustand:  
  - [ ] aktiviert ODER  
  - [ ] sauber deaktiviert (empfohlen)  
- [ ] Controller aktiv, `r_epoch` berechenbar  
- [ ] keine experimentellen Module aktiv  

---

## 1.3 Codefinalität

- [ ] Keine Proxy-Verträge  
- [ ] Keine Upgrade-Pfade (`delegatecall`, `UUPS`, `Transparent Proxy`)  
- [ ] Keine Admin-Setter  
- [ ] Keine externen Owner-Rollen  
- [ ] Code entspricht exakt dem finalen Audit-Bytecode  
- [ ] Deployment-Adresse dokumentiert  
- [ ] Code verifiziert auf Block-Explorer  

---

# 2. Sicherheits- & Invarianten-Checks

## 2.1 System-Invarianten (müssen erfüllt sein)

- [ ] S1: `isFrozen` = false (vor Freeze)  
- [ ] S2: kein Admin existiert  
- [ ] S3: alle Parameter stabil, keine dynamischen Abweichungen  
- [ ] S4: `totalDebt >= 0`  
- [ ] S5: Liquidationen erzeugen kein BadDebt  
- [ ] S6: Oracle manipuliert keine Werte außerhalb der definierten Grenzen  
- [ ] S7: kein Upgrade möglich

---

## 2.2 Sicherheitsmodule geprüft

- [ ] MEV-Schutz für DEX/LP aktiv  
- [ ] Slippage-Schutz aktiv  
- [ ] Oracle-Deviation-Checks aktiv  
- [ ] Anti-Sandwich-Mechanismen aktiv  
- [ ] Rate-Limit-Mechanismen korrekt  
- [ ] Reentrancy Guards in allen Modulen aktiv  
- [ ] Keine externen Calls in kritischen Pfaden  
- [ ] Liquidationspfad korrekt isoliert  

---

## 2.3 Gas- & Laufzeitverhalten

- [ ] Liquidationen funktionieren in realistischen Gas-Limits  
- [ ] StabilityPool absorbiert Debt ohne Probleme  
- [ ] VaultEngine-Operationen bleiben in festen Grenzen  
- [ ] Keine Endlosschleifen, keine dynamischen Loops  

---

# 3. Test- & Auditvoraussetzungen

## 3.1 Unit Tests

- [ ] 100 % Coverage aller Kernpfade  
- [ ] Tests für:  
  - [ ] Vault-Erstellung  
  - [ ] Mint  
  - [ ] Repay  
  - [ ] Liquidation  
  - [ ] StabilityPool-Interaktionen  
  - [ ] Oracle-Verhalten  
  - [ ] Controller (r_epoch-Berechnung)  

---

## 3.2 Property-Based Tests

- [ ] Zufallssimulationen bestehen  
- [ ] Hohe Volatilität besteht  
- [ ] Random Walk Szenarien bestanden  
- [ ] Liquidationsstürme bestanden  

---

## 3.3 Formale Prüfungen

- [ ] Reentrancy-Analyse bestanden  
- [ ] Static-Analysis bestanden  
- [ ] Overflow/Underflow-Prüfung  
- [ ] Prüfungen für Dead Code / Unreachable Code  
- [ ] Bytecode auf Upgradefreiheit geprüft  

---

## 3.4 Externe Sicherheits-Audits

- [ ] Interner Audit abgeschlossen  
- [ ] Externer Audit abgeschlossen  
- [ ] Alle Findings behoben  
- [ ] Finaler Audit-Report im GitHub veröffentlicht  

---

# 4. Orakel- & Preisfeed-Check

- [ ] Mindestanzahl aktiver Feeds erfüllt  
- [ ] Medianizer arbeitet stabil  
- [ ] Keine Feed-Ausreißer > `maxDeviation`  
- [ ] Blockverzögerungen stabil  
- [ ] Notfallfeedprüfung erfolgreich  
- [ ] DEX-Absicherung funktioniert  

---

# 5. DEX-/LP-Zustand (falls aktiviert)

- [ ] LP-Positionen innerhalb `maxLPExposure`  
- [ ] Slippage-Grenzen strikt eingehalten  
- [ ] PLS- und ProjectUSD-Balancen korrekt  
- [ ] Keine LP-Transaktionen im selben Block wie Liquidationen  
- [ ] LP-System konsistent deaktivierbar  

---

# 6. Dokumentation & Projektstatus

## 6.1 Whitepaper & SPECS

- [ ] Whitepaper final  
- [ ] Alle SPECS final  
- [ ] Architekturdiagramme final  
- [ ] Freeze-SPEC final  
- [ ] Security-SPEC final  
- [ ] DEX-LP-SPEC final  
- [ ] Liquidation-/Redemption-SPECs final  

---

## 6.2 GitHub & Deployment-Dokumentation

- [ ] GitHub-Struktur vollständig  
- [ ] Readme final  
- [ ] Developer-Dokumentation final  
- [ ] Freeze-Checklist im Repo verlinkt  
- [ ] RPC-Hinweise und Sicherheitsinfos dokumentiert  
- [ ] Versionsnummern fixiert  

---

# 7. Organisatorische Schritte (vor Freeze)

- [ ] Freeze-Ankündigung vorbereitet  
- [ ] Community über Unveränderlichkeit informiert  
- [ ] Letzte technische Review-Session  
- [ ] Freeze-Zeitpunkt definiert  
- [ ] Monitoring-System aktiviert  
- [ ] Offchain-Tools aktualisiert  
- [ ] DEX-/LP-Bots deaktiviert (falls nicht benötigt)  
- [ ] Notfallkommunikation (nur informativ, nicht technisch)  

---

# 8. Durchführung der Freeze-Transaktion

- [ ] Wallet geprüft  
- [ ] Contract-Adresse geprüft  
- [ ] Transaktion klar dokumentiert  
- [ ] Gas-Limits ausreichend  
- [ ] `activateFreeze()` ausgelöst  
- [ ] Transaction Hash archiviert  
- [ ] `isFrozen = true` bestätigt  
- [ ] Monitoring zeigt Freeze-Zustand  

---

# 9. Nach-Freeze-Prüfung

- [ ] Keine Governance-Funktion mehr verfügbar  
- [ ] Keine Setter-Funktion durchführbar  
- [ ] Keine Admin-Funktion existent  
- [ ] System verhält sich deterministisch  
- [ ] Alle Invarianten weiterhin gültig  

---

# 10. Lizenz & Referenzen

© 2025 Aqua75 / ProjectUSD  
Lizenz: MIT für Code, CC BY-NC-SA 4.0 für Dokumentation  
Verweis: ProjectUSD Whitepaper V2.1 (Kap. 8–9, Glossar S. 24–28)  

