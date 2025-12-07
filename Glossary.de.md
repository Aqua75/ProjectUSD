# ProjectUSD – Glossar (Deutsch)
### Vollständige Definitionen aller zentralen Konzepte, Variablen, Module und Mechaniken

Dieses Glossar umfasst sämtliche relevanten Begriffe aus:
- der ProjectUSD-Architektur  
- den offiziellen SPECS  
- dem Whitepaper  
- den Studien (1–14)  
- allen Artikeln und Modellen (inkl. P R r Modell)  
- der Controller-, Vault- und Liquidationslogik

Es ersetzt frühere Versionen vollständig.

---

# 🧩 Grundbegriffe

**ProjectUSD**  
Autonomes, algorithmisches Geldsystem für PulseChain ohne Orakel, Governance oder zentrale administrierbare Eingriffe.

**Interne Werteinheit**  
Algorithmisch definierter Referenzwert, der zur Stabilitätsmessung genutzt wird (über R, r und TWAP).

**Autonome Geldpolitik**  
Gesamtheit aller Regeln, durch die ProjectUSD Preisstabilität ohne menschliche Eingriffe aufrechterhält.

---

# 🏛 Architekturbegriffe

**Unveränderlicher Core (Immutable Core)**  
Die permanent unveränderlichen Module: VaultEngine, Controller, Oracle, Liquidation/Redemption, StabilityPool.

**Freeze-Event**  
Ein einmaliger Prozess, der den Core dauerhaft einfriert und alle Upgrades unmöglich macht.

**Deterministische Ausführung**  
Alle Systemabläufe sind eindeutig, vorhersehbar und mathematisch festgelegt.

**Kein Admin-Key / Keine Upgrades**  
Es existieren keinerlei privaten Schlüssel oder Upgrade-Mechanismen im Core.

---

# 🔢 Controller, Epochen & Preislogik

**Controller**  
Autonomes Gleichgewichtssystem, das Angebot, Nachfrage und Preisabweichungen reguliert.

**R-Epoche (Restore-Epoche)**  
Phase, in der der Controller Marktpreisabweichungen durch Redemptions und Parameteranpassungen korrigiert und den Gleichgewichtspreis R stabilisiert.

**r-Epoche (Rebalance-Epoche)**  
Phase mit regulärem Betrieb, in der der Controller Parameter feinjustiert, solange keine starken Stressoren bestehen.

**Epoche (Epoch)**  
Zustandsperiode, die entweder als R- oder r-Phase klassifiziert ist.

**Epoch-Transition**  
Automatischer Wechsel zwischen R- und r-Epoche, ausgelöst durch interne Systemmetriken.

**Feedback-Schleife**  
Regelfluss zwischen Nachfrage, Angebot, Preisabweichungen und Controller-Reaktionen.

**Gleichgewichtspreis (R)**  
Systeminterner Preisanker, zu dem Redemptions ausgeführt werden.

**Preisabweichung (ΔP)**  
Differenz zwischen Marktpreis und Gleichgewichtspreis R.

---

# 🧮 Ökonomische Modelle

**P R r Modell**  
Ökonomisches Modell, das die Beziehung zwischen Nachfrage (P), Gleichgewichtspreis (R) und Rebalance-Phasen (r) beschreibt.

**Elastic Supply Mechanism**  
Dynamische Anpassung der Geldmenge abhängig von Marktverhalten.

**System Surplus (Überschusspuffer)**  
Langfristig aufgebauter ökonomischer Sicherheits- und Absorptionspuffer.

**System Exposure**  
Gesamte Risikoposition des Systems gegenüber Marktveränderungen.

---

# 🏦 VaultEngine & Collateral

**Vault**  
Benutzerposition mit hinterlegtem Collateral und erzeugter Systemschuld.

**Collateral Ratio (CR)**  
Collateral-Wert geteilt durch Schuld.

**Minimum Collateral Ratio (MCR)**  
Unterer Grenzwert für sichere Besicherung; bei Unterschreitung erfolgt Liquidation.

**Systemschuld**  
Gesamte umlaufende Menge ProjectUSD.

**Debt Ceiling**  
Maximal erlaubte Systemschuld (gesamt oder pro Collateralgruppe).

**Debt Expansion / Debt Contraction**  
Automatische Ausweitung oder Verringerung der Systemschuld durch Controller-Mechanismen.

**Collateral Bucket**  
Untergruppe oder Kategorie von Collateralarten.

---

# 💥 Liquidation & Redemption

**Liquidation**  
Erzwungene Abwicklung eines Vaults, wenn CR < MCR fällt.

**Pro-Rata Liquidation**  
Stückweise Aufteilung des unterbesicherten Vaults auf StabilityPool-Teilnehmer.

**Liquidation Penalty (Strafgebühr)**  
Wird während Liquidationen erhoben und fließt in den StabilityPool.

**Soft Liquidation**  
Schonendere Liquidationsform, falls im SPECS definiert (z. B. bei moderatem Stress).

**Hard Liquidation**  
Vollständige Liquidation unter hohem Stresslevel.

**Redemption**  
Eintausch von ProjectUSD gegen PLS zum Gleichgewichtspreis R.

**Targeted Redemption**  
Redemption, die Vaults nach CR-Priorität ansteuert.

**Redemption Queue**  
Ablaufreihenfolge der abzuarbeitenden Vaults bei Redemptions.

---

# 📊 Preisermittlung, Oracle & TWAP

**Oracleless Design**  
ProjectUSD verwendet ausschließlich On-Chain-Daten (TWAP), keine externen Orakel.

**TWAP (Time-Weighted Average Price)**  
Zeitgewichteter Durchschnittspreis aus dem PLS/ProjectUSD-AMM-Pool.

**TWAP Window**  
Zeitraum, aus dem der Durchschnitt berechnet wird.

**Deviation Limit**  
Zulässige maximale Abweichung zwischen TWAP-Preis und Systemparametern.

---

# 🛡 Sicherheit & Invarianten

**Atomarität**  
Jede Operation ist vollständig oder gar nicht gültig.

**Invarianten**  
Ökonomische und logische Regeln, die zu jedem Zeitpunkt erfüllt sein müssen.

**Fail-Safe Mode**  
Systemzustand, der bei extremen Abweichungen eingenommen wird.

**State Transition Function**  
Formale Funktion, die gültige Zustandsänderungen beschreibt.

**Censorship Resistance**  
Unmöglichkeit, Transaktionen durch zentrale Akteure zu blockieren.

---

# 📈 Monitoring & Analyse

**Epoch Tracker**  
Messsystem zur Beobachtung von R- und r-Epochen.

**Collateral Health Index**  
Indikator für Systembesicherung und durchschnittliche CR.

**Redemption Pressure Index**  
Messwert für Redemptions-Stress im System.

**Stability Pool Utilization**  
Nutzungsauslastung des StabilityPools.

**System Stress Level**  
Makroindikator für Markt- und Systemstress.

---

# 👥 Community- & Organisationsbegriffe

**Independent Implementation**  
Wunschgemäß getrennte Dritt-Implementierung außerhalb dieses Repositories.

**Spezifikation (SPEC)**  
Formaler technischer Bauplan, der vollständig beschreibt, wie ein Modul funktionieren muss.

**Open-Source-Blueprint**  
Gesamtheit der öffentlich bereitgestellten SPECS, Artikel und Studien.

**Self-Starter**  
Mitwirkender, der eigenständig Research oder Tools erstellt.

---

# 🧾 Meta-Begriffe

**Incident-Runbook**  
Ablaufplan zur Analyse unerwarteter Ereignisse in unabhängigen Implementationen.

**Invariant Enforcement Layer**  
Sicherungsebene, die erzwingt, dass definierte Invarianten niemals verletzt werden.

**Deterministic Path**  
Pfad im System, der bei gleichen Eingangswerten stets exakt dieselben Ergebnisse erzeugt.

---

### 📌 Schlussbemerkung

Dieses Glossar bildet die vollständige definitorische Grundlage des ProjectUSD-Systems und ist ein zentraler Bestandteil der Dokumentation.
