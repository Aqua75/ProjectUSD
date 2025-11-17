---
title: "ProjectUSD – Incident-Runbook v1"
status: "Draft"
last_updated: "2025-11-19"
author: "Aqua75"
language: "de"
related_whitepaper_sections: ["Kap. 8 – Freeze", "Kap. 9 – Sicherheit", "Glossar S. 24–28"]
---

# ProjectUSD – Incident-Runbook v1

## Zweck

Dieses Incident-Runbook beschreibt alle möglichen Vorfallstypen (Incidents) für ProjectUSD  
und definiert die entsprechenden Diagnose- und Monitoring-Verfahren.

**Wichtig:**  
Nach Aktivierung des Freeze besitzt ProjectUSD:

- keine Admins  
- keine Notfallbefehle  
- keine Interventionsmechanismen  
- keine Upgrade-Pfade  

Dieses Runbook beschreibt daher **keine Eingriffe**,  
sondern ausschließlich:

- korrekte Diagnose  
- Mustererkennung  
- Überwachung des Systemzustands  
- Interpretation möglicher Szenarien  
- Dokumentation für Post-Mortems  

---

# 1. Klassifikation von Incidents

ProjectUSD unterscheidet fünf Kategorien von Incidents:

## 1.1 Technische Incidents (Smart Contracts / Blockchain)

- ungewöhnliche Gas-Spikes  
- extrem niedrige Blockproduktion  
- Reorgs / Forks im PulseChain-Netzwerk  
- RPC-Ausfälle  
- Subgraph-Verzögerungen  
- Zustand des Systems nicht abrufbar  

## 1.2 Ökonomische Incidents (Markt / Liquidation / Redemption)

- plötzliche PLS-Preiscrashes  
- Liquidationswellen  
- Redemption-Spikes (massive Rückwechsel)  
- Liquidationsverzögerungen  
- auffällige CR-Verteilungen  
- ungewöhnlich hoher SystemDebt-Wert  

## 1.3 Orakel-Incidents

- fehlende Preisupdates  
- starke Preisabweichungen  
- Median weicht abnorm von DEX-Preisen ab  
- einzelne Feeds liefern Ausreißer  

## 1.4 StabilityPool- und Vault-Health-Incidents

- StabilityPool nähert sich leerem Zustand  
- mehrmals negative CRs kurz hintereinander  
- übermäßige BadDebt-Risikoindikatoren  
- extreme Volatilität in CR-Struktur des Systems  

## 1.5 Offchain-/Infrastruktur-Incidents

- Monitoring-Frontends ausgefallen  
- Subgraph nicht erreichbar  
- API-Ratenlimits  
- Verzögerte Eventverarbeitung  

---

# 2. Schweregrad (Severity Levels)

ProjectUSD verwendet drei Incident-Schweregrade:

## SEV-0 (Kritisch)
- Gefahr potenzieller Systeminstabilität  
- Fehlender Orakelpreis > X Minuten  
- Massive Liquidationsstauungen  
- Extrem niedrige Blockproduktion  
- StabilityPool vollständig leer  
- Gesamtes System nicht einsehbar  

→ **Sofortige Diagnose**, globale Systembeobachtung, Dokumentation starten

## SEV-1 (Hoch)
- ungewöhnliche CR-Verteilungen  
- starker Rückstaus im Redemption-Prozess  
- einzelne Orakelfeeds ausgefallen  
- Subgraph verzögert  
- Netzwerküberlastung  

→ Diagnose & Monitoring intensivieren

## SEV-2 (Informativ)
- höhere Volatilität als üblich  
- einzelne Liquidationen verzögert  
- leichte RPC-Ausfälle  
- UI nicht erreichbar  

→ Beobachten und dokumentieren

---

# 3. Incident-Typen und Runbooks

## 3.1 Orakel-Ausfall (SEV-0 / SEV-1)

**Symptome:**

- `OraclePrice` wird länger als 60 Sekunden nicht aktualisiert  
- Medianizer zeigt alten Wert an  
- Datenpunkte einzelner Feeds fehlen  

**Diagnoseschritte:**

- Prüfe `priceUpdateTimestamp`  
- Prüfe Abweichung der einzelnen Feeds  
- Vergleiche Medianizer-Wert mit DEX-TWAP (nur diagnostisch)  
- Prüfe, ob `blockDelay` korrekt erhöht ist  

**Wichtig:**  
Das System bleibt stabil, da Liquidation/Redemption ohne frische Preise nicht ausgeführt werden können.

---

## 3.2 Liquidationsstau (SEV-0)

**Symptome:**

- viele Vaults mit `CR < LiquidationCR`  
- aber wenige Liquidationen  
- StabilityPool absorbiert Schulden verzögert  

**Diagnoseschritte:**

- Prüfe Transaktionsdaten: niedrige Gaspreise?  
- Prüfe Blockproduktion: Netzwerk langsam?  
- Prüfe LiquidationLogs (Verzögerung > X Blöcke?)  
- Prüfe StabilityPool-Kapazität  
- Prüfe `totalDebt` Entwicklung  

**Interpretation:**  
Kein Eingriff möglich.  
System bleibt korrekt: Liquidation wird ausgeführt, sobald Netzwerk es zulässt.

---

## 3.3 Redemption-Spike (SEV-1)

**Symptome:**

- viele Redemptions in kurzer Zeit  
- deutlicher CR-Abfall bei top-collateralized Vaults  
- `R` wird stark belastet  

**Diagnoseschritte:**

- Prüfe Anzahl Redemptions pro Block  
- Prüfe CR-Struktur (Top-CR-Vaults sinken schneller)  
- Prüfe `RedeemLimit`-Einfluss  
- Prüfe Gesamt-Redemption-Volumen  

**Interpretation:**  
System reagiert normal:  
Redemption stabilisiert Marktpreis automatisch.

---

## 3.4 StabilityPool fast leer (SEV-0)

**Symptome:**

- `SurplusBuffer` niedrig  
- StabilityPool-Kapazität nähert sich 0  
- Liquidationen verteilen kaum Collateral  

**Diagnoseschritte:**

- Prüfe aktuelle Höhe der im Pool hinterlegten PLS  
- Prüfe Liquidationslast der letzten Blöcke  
- Prüfe CR-Verteilung aller Vaults  

**Interpretation:**  
System bleibt funktionsfähig, Liquidationen laufen weiter – aber Rewards werden geringer.

---

## 3.5 Extremvolatilität (SEV-1)

**Symptome:**

- PLS-Preis bewegt sich > 20 % in < 1 Stunde  
- viele Vaults rutschen gleichzeitig in Liquidationsbereich  
- Redemption-Volumen steigt stark  

**Diagnoseschritte:**

- Prüfe Oracle-Geschwindigkeit  
- Prüfe Blockzeit  
- Prüfe LiquidationLogs  
- Prüfe CR-Strukturverlauf  

**Interpretation:**  
System bleibt vollautomatisch stabil – kein Eingriff möglich oder nötig.

---

## 3.6 Netzwerk-/Blockchain-Störungen (SEV-0)

**Symptome:**

- kaum neue Blöcke  
- Transaktionen hängen sehr lange  
- Reorgs / Forks  

**Diagnoseschritte:**

- Prüfe Blockexplorer  
- Prüfe `block.number`  
- Prüfe Verzögerungen im Subgraph  
- Prüfe Gaspreise  

**Interpretation:**  
System verhält sich deterministisch:  
Keine Liquidationen/Redemptions während Stillstand → keine Fehlzustände.

---

## 3.7 Monitoring-/Subgraph-Ausfall (SEV-2)

**Symptome:**

- Frontend zeigt keine Daten  
- Charts veraltet  
- Indexer blockiert  

**Diagnoseschritte:**

- Prüfe direkten RPC-Zugriff  
- Prüfe Contract-Events on-chain  
- Vergleiche Subgraph-Index mit aktuellem Block  

**Interpretation:**  
Nur Darstellungsfehler – System läuft normal.

---

# 4. Systemdiagnose-Protokoll

Für jeden Incident sollten folgende Daten erfasst werden:

- Incident-Zeitstempel  
- Blocknummer  
- Oracle-Werte  
- CR-Verteilung  
- StabilityPool-Zustand  
- Anzahl Liquidationen  
- Anzahl Redemptions  
- `totalDebt`  
- Gaspreise / Netzwerkstatus  
- Transaktionslogs  
- betroffene VaultIDs  

Diese Informationen ermöglichen spätere Post-Mortems.

---

# 5. Entscheidungsmatrix (Nur Diagnose, kein Eingriff)

ProjectUSD kann **nie** nachträglich geändert werden.  
Das Runbook definiert nur:

- Wie erkenne ich ein Problem?  
- Wie ermittle ich den Zustand?  
- Wie kommuniziere ich den Vorfall?  
- Wie dokumentiere ich ihn korrekt?  

---

# 6. Kommunikation

Bei relevanten Incidents wird in der Community Folgendes kommuniziert:

- Art des Incidents  
- aktuelle Auswirkungen  
- erwartetes Verhalten des Systems  
- was Nutzer beobachten können  
- bekannte externe Faktoren (Netzwerk, Oracle, Markt)  

Keine „Lösungen“ — nur transparente Information.

---

# 7. Post-Mortem-Prozess

Nach einem schweren Incident:

- Post-Mortem erstellen  
- Ursache dokumentieren  
- Blocknummern festhalten  
- Oracle-Feeds vergleichen  
- Liquidations- und Redemption-Logs prüfen  
- Learnings dokumentieren  

→ dient der Transparenz  
→ stärkt langfristiges Vertrauen  

---

# 8. Lizenz & Referenzen

© 2025 Aqua75 / ProjectUSD  
Lizenz: MIT für Code, CC BY-NC-SA 4.0 für Dokumentation  
Referenzen: ProjectUSD Whitepaper V2.1 (Kap. 8–9, Glossar S. 24–28)  
