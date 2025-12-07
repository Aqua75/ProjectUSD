# ProjectUSD – Glossar (Deutsch)
### Vollständige Definitionen aller zentralen Systembegriffe, Variablen, Mechaniken und Modelle

Dieses Glossar enthält alle Begriffe aus:
- der ProjectUSD-Architektur  
- den vollständigen SPECS  
- dem Whitepaper  
- dem P-R-r Modell  
- dem Controller-System  
- der VaultEngine  
- Liquidation & Redemption  
- Studien und technischen Artikeln  

Es ersetzt frühere Glossarversionen vollständig.

---

# 🧩 Grundbegriffe

**ProjectUSD**  
Autonomes, algorithmisches Geldsystem für PulseChain. Es besitzt keinen Admin-Key, keine Governance, keine Upgrades und keine externen Orakel. Alle Prozesse folgen einer vollständig deterministischen Systemlogik.

**Autonome Geldpolitik**  
Die Gesamtheit der Regeln, über die ProjectUSD seine Kaufkraft erhält. Diese Geldpolitik ist vollständig algorithmisch und nicht menschlich steuerbar.

---

# 🧠 Zentrale Variablen: P, R, r

## **R – Interne Werteinheit (Kaufkraftanker)**
R ist die zentrale interne Referenzgröße des Systems.  
Es handelt sich um die algorithmisch definierte Werteinheit, gegen die das System stabilisiert wird.

- Redemptions werden zu R ausgeführt  
- Der Controller bewertet Preisabweichungen relativ zu R  
- R ist unveränderlich und dient als stabiler Wertanker  

R ist nicht der Marktpreis, sondern der **interne Maßstab**, anhand dessen ProjectUSD seine Kaufkraft bewahrt.

---

## **r – Kombinierte Schuld- und Sparerate**
r ist ein interner Systemparameter, der die strukturelle Dynamik von:

- Systemverschuldung  
- impliziter Sparrate  
- langfristiger Angebotselastizität  

steuert.

Der Controller passt r an, um:

- strukturelle Spannungen abzubauen  
- Nachfrageimpulse zu absorbieren  
- Stabilität in zukünftigen Epochen sicherzustellen  

r ist **keine Epoche**, kein Preis und kein Nutzerparameter —  
sondern eine algorithmisch gesteuerte **ökonomische Regulierungskraft**.

---

## **P – Nachfrageimpuls**
P ist der externe, marktseitige Nachfragefaktor.  
Er entsteht durch:

- Kaufdruck  
- Verkaufsdruck  
- Marktvolumen  
- Liquiditätsverschiebungen  

P beeinflusst, wie stark der Controller R und r anpassen bzw. durchsetzen muss.

---

# 🔢 P-R-r Modell

**P-R-r Modell**  
Das zentrale ökonomische Modell zur Stabilisierung von ProjectUSD.  
Es beschreibt die Interaktion von:

- **P** – Nachfrageimpuls  
- **R** – Interne Werteinheit (Preisanker / Kaufkraftmaßstab)  
- **r** – Kombinierte Schuld- und Sparerate  

Das Modell erklärt:

- wie Kaufkraft stabil bleibt  
- wie der Controller Nachfrage absorbiert  
- wie das Angebot elastisch wird  
- wie Epochen wechseln  
- wie Preisabweichungen geglättet werden  

Es ist der Kern der autonomen Stabilitätslogik.

---

# 🕒 Epochen & Controllerphasen

## **R-Epoche (Restore)**
Operative Phase, in der das System aktiv Preisabweichungen korrigiert  
und den Wertanker R durchsetzt.

Typische Merkmale:

- erhöhte Redemption-Aktivität  
- starke Controllerintervention  
- Rückführung des Preises in Richtung R  

---

## **r-Epoche (Rebalance)**
Phase struktureller Feinjustierung, in der der Controller:

- r dynamisch anpasst  
- zukünftigen Stress reduziert  
- Systemparametrik balanciert  

Dies geschieht in Zeiten geringerer Marktspannung.

---

## **Epoch Transition**
Der algorithmische Wechsel zwischen R-Epoche und r-Epoche.  
Er wird ausgelöst durch:

- Veränderungen in P (Nachfrageimpuls)  
- beobachtete Abweichungen von R  
- strukturelle Spannungen in r  
- Messgrößen des Controllers  

Dieser Prozess ist vollständig automatisiert und basiert ausschließlich auf P-R-r-Dynamik.

---

# 🏛 Architekturbegriffe

**Unveränderlicher Core (Immutable Core)**  
Der dauerhaft unveränderliche Systemkern: VaultEngine, Controller, Oracle/TWAP-Modul, Liquidation/Redemption, StabilityPool.

**Freeze-Event**  
Der Moment, in dem der Core für immer eingefroren wird. Danach existieren keine Upgrades oder Eingriffsmöglichkeiten.

**Deterministische Ausführung**  
Jede Systemaktion hat vorhersehbare, eindeutig definierte Ergebnisse.

**No-Admin-Key**  
Es existiert kein Schlüssel, der Änderungen am System erlauben könnte.

---

# 🏦 VaultEngine & Collateral

**Vault**  
Benutzerposition bestehend aus Collateral und erzeugter Schuld.

**Collateral Ratio (CR)**  
Collateral-Wert geteilt durch Schuld.

**Minimum Collateral Ratio (MCR)**  
Unterer Grenzwert; bei Unterschreitung kommt es zur Liquidation.

**Systemschuld**  
Alle ausgegebenen ProjectUSD-Einheiten.

**Debt Ceiling**  
Maximal zulässige Systemschuld (gesamt oder pro Collateralgruppe).

**Debt Expansion / Contraction**  
Veränderung des Systemangebots durch Controller-Modell oder Nachfrage.

**Collateral Bucket**  
Untergruppe von Collateralarten, die gemeinsame Parameter teilen.

---

# 💥 Liquidation & Redemption

**Liquidation**  
Erzwungene Schließung eines Vaults, wenn CR < MCR fällt.

**Pro-Rata-Liquidation**  
Aufteilung der unterbesicherten Position proportional auf StabilityPool-Teilnehmer.

**Liquidation Penalty**  
Strafaufschlag, der in den StabilityPool fließt.

**Hard Liquidation / Soft Liquidation**  
Abhängig vom Systemstress:  
– Soft = schonender  
– Hard = vollständige Abwicklung

---

## **Redemption**
Eintausch von ProjectUSD gegen PLS zum Wertanker **R**.  
Redemptions erzwingen Preiskorrektur Richtung R.

**Redemption Queue**  
Reihenfolge der abzuarbeitenden Vaults.

**Targeted Redemption**  
Bevorzugte Abwicklung basierend auf Collateral Ratio.

---

# 📊 Preisermittlung, Oracle & TWAP

**Oracleless Design**  
Keine externen Preisorakel; nur On-Chain-Daten.

**TWAP (Time-Weighted Average Price)**  
Zeitgewichteter Durchschnittspreis aus dem AMM-Pool.

**TWAP-Window**  
Betrachtungszeitraum für die Preisaggregation.

**Deviation Limit**  
Maximal tolerierte Abweichung zwischen TWAP-Preis und Systemparametern.

---

# 🛡 Sicherheit, Invarianten & Systemlogik

**Atomarität**  
Operationen sind vollständig oder gar nicht gültig.

**Invarianten**  
Regeln, die niemals verletzt werden dürfen (z. B. CR ≥ MCR).

**Fail-Safe Mode**  
Zustand, der bei extremen Anomalien aktiviert wird.

**State Transition Function**  
Mathematisch definierte Funktion aller gültigen Zustandswechsel.

**Deterministic Path**  
Ein Ablauf, der bei gleichen Eingaben immer identische Ergebnisse liefert.

---

# 📈 Monitoring & Analysemetriken

**Epoch Tracker**  
Überwachungssystem für R- und r-Epochen.

**Collateral Health Index**  
Zustandsmaß für Besicherungsstruktur.

**Redemption Pressure Index**  
Messgröße für Redemption-Stress.

**Stability Pool Utilization**  
Nutzungsauslastung des StabilityPools.

**System Stress Level**  
Makroindikator für Systembelastung.

---

# 🧾 Meta- und Organisationsbegriffe

**Spezifikation (SPEC)**  
Formaler technischer Bauplan eines Moduls.

**Open-Source-Blueprint**  
Gesamtheit der SPECS, Artikel und Studien.

**Independent Implementation**  
Unabhängige Implementierung außerhalb dieses Repositories.

**Invariant Enforcement Layer**  
Sicherungsebene, die Invarianten durchsetzt.

**Incident-Runbook**  
Prozessdokumentation für Anomalien in externen Implementationen.

---

# 📌 Schlussbemerkung

Dieses Glossar bildet die vollständige definitorische Grundlage von ProjectUSD und stellt sicher,  
dass alle Module, SPECS, Artikel und Studien konsistent verstanden werden.
