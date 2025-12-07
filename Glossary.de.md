# ProjectUSD – Glossar (Deutsch)
### Vollständige Definitionen aller zentralen Systembegriffe, Variablen, Mechaniken und Modelle

Dieses Glossar umfasst sämtliche relevanten Begriffe aus:
- der ProjectUSD-Architektur  
- den SPECS  
- dem Whitepaper  
- dem P-R-r Modell  
- der Controller-Logik  
- VaultEngine  
- Liquidation & Redemption  
- den Studien und Research-Artikeln  

Diese Version ersetzt alle früheren Glossare vollständig.

---

# 🧩 Grundbegriffe

**ProjectUSD**  
Autonomes, algorithmisches Geldsystem auf PulseChain ohne Orakel, Governance oder zentrale Eingriffe. Das System folgt ausschließlich deterministischen Regeln.

**Autonome Geldpolitik**  
Regelsystem, durch das ProjectUSD langfristig Kaufkraft erhält. Vollständig algorithmisch, nicht menschlich steuerbar.

---

# 🧠 Zentrale Variablen: P, R, r

## **R – Interne Werteinheit (Kaufkraftanker)**  
Die interne Referenzgröße, gegen die der Wert von ProjectUSD stabilisiert wird.  
R bestimmt:  
- den Redemption-Preis  
- den Stabilitätsmaßstab des Controllers  
- das interne Gleichgewicht des Systems  

R ist unveränderlich und bildet die Grundlage der Kaufkraftstabilität.

---

## **r – Kombinierte Schuld- und Sparerate**  
Interner Parameter, der die strukturelle Dynamik des Systems steuert.  
r beeinflusst:  
- die Wachstumsrate der Systemschuld  
- die implizite Sparrate  
- die langfristige Angebotselastizität  

r wird durch den Controller dynamisch angepasst, um strukturelle Spannungen abzubauen.

---

## **P – Marktpreis / Nachfrageimpuls**  
P ist der vom Markt erzeugte Preisimpuls, basierend auf dem tatsächlich beobachteten TWAP-Preis des ProjectUSD-PLS-AMM-Pairs.

P repräsentiert:  
- Marktpreisbewegungen  
- Nachfrage- oder Angebotsschocks  
- externe Preisrealitäten  

P ist der **einzige externe Faktor** im P-R-r-Modell.

---

# 🔢 P-R-r Modell

Das zentrale ökonomische Modell von ProjectUSD.  
Es beschreibt die Interaktion von:

- **P** – Marktpreisimpuls  
- **R** – interne Werteinheit (Preisanker)  
- **r** – kombinierte Schuld- und Sparerate  

Das Modell erklärt:  
- Preisstabilität  
- Nachfrageabsorption  
- Epochenwechsel  
- Angebots- und Sparverhalten  
- langfristige Wertkonsistenz  

---

# 🕒 Epochen & Controllerphasen

## **R-Epoche (Restore)**  
Phase, in der das System aktiv Preisabweichungen korrigiert und den Wertanker R durchsetzt.  
Typische Merkmale:  
- erhöhte Redemption-Aktivität  
- starke Controllerintervention  
- Rückführung des Preises auf R  

---

## **r-Epoche (Rebalance)**  
Phase struktureller Feinjustierung.  
Der Controller passt r an, um zukünftige Spannungen zu vermeiden und Balance herzustellen.

---

## **Epoch Transition**  
Automatischer Wechsel zwischen R-Epoche und r-Epoche, ausgelöst durch:

- Marktpreisbewegungen (P)  
- Abweichungen von R  
- strukturellen Stress  
- Controller-Metriken  

---

# 🏛 Architekturbegriffe

**Unveränderlicher Core (Immutable Core)**  
Dauerhaft unveränderliche Module: VaultEngine, Controller, StabilityPool, Redemption, Liquidation, TWAP-Modul.

**Freeze-Event**  
Der Moment, in dem der Core eingefroren wird. Danach sind Upgrades unmöglich.

**Deterministische Ausführung**  
Alle Abläufe führen bei gleichen Eingaben zu genau gleichen Ergebnissen.

**No-Admin-Key**  
Es existiert kein Schlüssel, der Eingriffe oder Parameteränderungen erlauben würde.

---

# 🏦 VaultEngine & Collateral

**Vault**  
Benutzerposition bestehend aus Collateral und erzeugter Schuld.

**Collateral Ratio (CR)**  
Collateral-Wert geteilt durch Schuld.

**Minimum Collateral Ratio (MCR)**  
Untergrenze; bei Unterschreitung erfolgt Liquidation.

**Debt Ceiling**  
Maximal erlaubte Systemschuld (gesamt oder pro Collateralgruppe).

**Systemschuld**  
Alle ausgegebenen ProjectUSD-Einheiten.

**Debt Expansion / Debt Contraction**  
Erhöhung bzw. Verringerung der Systemschuld durch Controller-Mechanismen.

**Collateral Bucket**  
Gruppe von Collateralarten mit gemeinsamen Parametern.

**Debt Floor (Mindestschuldmenge)**  
Die minimal erforderliche Schuld, die ein Vault erzeugen muss, um gültig zu sein.

---

# 💥 Liquidation & Redemption

**Liquidation**  
Erzwungene Abwicklung eines Vaults bei CR < MCR.

**Pro-Rata-Liquidation**  
Verteilung der unterbesicherten Position auf StabilityPool-Teilnehmer proportional zu deren Anteil.

**Liquidation Penalty**  
Strafaufschlag, der an den StabilityPool ausgezahlt wird.

**Liquidation Discount**  
Abschlag, zu dem StabilityProvider Collateral in einer Liquidation erhalten.

**Soft Liquidation / Hard Liquidation**  
Unterschiedliche Liquidationsformen je nach Systemstress.

---

## **Redemption**  
Eintausch von ProjectUSD gegen PLS zum festen Wertanker R.

**Redemption Queue**  
Reihenfolge der abzuarbeitenden Vaults.

**Redemption Spread**  
Optionaler systemischer Korrekturfaktor, der Redemptions leicht modifiziert.

**Redemption Density**  
Intensität der Redemption-Aktivität über mehrere Blöcke hinweg.

---

# 🏦 StabilityPool

**StabilityPool**  
Liquiditätspool, der Liquidationen übernimmt und dafür Collateral erhält.

**Stability Provider (SP)**  
Teilnehmer, die ProjectUSD im StabilityPool hinterlegen und Liquidationsgewinne erhalten.

**Stability Pool Utilization**  
Grad, zu dem der Pool durch Liquidationen beansprucht wird.

---

# 📊 Oracle, Preisermittlung & TWAP

**Oracleless Design**  
Keine externen Oracle; Preisermittlung ausschließlich On-Chain.

**TWAP (Time-Weighted Average Price)**  
Zeitgewichteter Durchschnittspreis aus dem AMM.

**TWAP-Window**  
Zeitraum, aus dem der Durchschnitt berechnet wird.

**Oracle Window Shift (TWAP-Rollperiode)**  
Weiterbewegen des TWAP-Fensters, um neue Daten einzubeziehen.

**Deviation Limit**  
Maximal tolerierte Abweichung zwischen TWAP und Systemparametern.

**Deviation Trigger**  
Auslöser, bei dem die R-Epoche aktiviert wird.

---

# 🛡 Sicherheit & Invarianten

**Atomarität**  
Operationen sind entweder vollständig gültig oder werden vollständig rückgängig gemacht.

**Invarianten**  
Systemregeln, die niemals verletzt werden dürfen (z. B. CR ≥ MCR).

**State Transition Function**  
Formale Definition aller gültigen Zustandswechsel.

**Fail-Safe Mode**  
Zustand, der bei extremen Abweichungen aktiviert wird.

**Invariant Enforcement Layer**  
Schicht, die sicherstellt, dass Invarianten konsequent eingehalten werden.

**Deterministic Path**  
Pfad, der bei gleichen Eingaben identische Ergebnisse produziert.

---

# 📈 Analysemetriken & Monitoring

**Epoch Tracker**  
Überwachung der Epochen (R und r).

**Collateral Health Index**  
Zustandsmaß für die durchschnittliche Besicherung des Systems.

**Redemption Pressure Index**  
Messgröße für Redemption-Stress.

**System Stress Level**  
Makroindikator für Markt- und Systembelastung.

**Controller Saturation**  
Zustand, bei dem der Controller r nicht weiter anpassen kann.

**Supply Elasticity Envelope**  
Der erlaubte dynamische Rahmen, innerhalb dessen das System die Geldmenge elastisch regulieren darf.

---

# 👥 Organisationsbegriffe

**SPEC (Spezifikation)**  
Formale technische Beschreibung eines Systemmoduls.

**Independent Implementation**  
Unabhängige Implementierung außerhalb des offiziellen Repositories.

**Open-Source-Blueprint**  
Gesamtheit aller SPECS, Artikel und Studien.

**Incident-Runbook**  
Dokumentation zur Behandlung unerwarteter Ereignisse in Dritt-Implementierungen.

---

# 📌 Schlussbemerkung

Dieses Glossar bildet die vollständige definitorische Grundlage von ProjectUSD  
und stellt sicher, dass alle Module, SPECS, Artikel und Studien konsistent verstanden werden.
