```markdown
# Studie 15: Extremstresstests und Worst Case Szenarien

**Ziel:** Simulation und Analyse von 90 Prozent PLS Crash, Liquidity Exodus, Chain Reorgs, MEV Extremphasen, inklusive Kombinations und Kaskadenszenarien.  
**Umfang:** Konzeptionelle 8 bis 12 Seiten als Textreport, als Blaupause für Implementierung und formale Tests.  
**Quelle:** PDF Upload :contentReference[oaicite:0]{index=0}

---

## Kapitel 1: Einleitung

### 1.1 Warum Black Swan Tests bei ProjectUSD zentral sind

ProjectUSD folgt laut Whitepaper einer Autarkie Philosophie. Die Kernlogik wird nach einem Freeze Event unveränderlich, Immutable Core, Governance wirkt nur noch auf eine Peripherie Schicht. Zudem gibt es keinen Admin Key und keinen Pause Button.

Das macht klassische Notbremsen im Stressfall bewusst unmöglich. Stabilität muss daher aus Mechanik, Parametrisierung und Marktanreizen entstehen, nicht aus Eingriffen.

### 1.2 Systemkomponenten, die im Stresstest relevant sind

Für Worst Case Szenarien sind vier Mechanikblöcke besonders kritisch:

1. **Vaults und Liquidationen**  
   Nutzer hinterlegen vor allem PLS als Sicherheit. Typische Collateral Ratio wird im Whitepaper bei ungefähr 170 Prozent oder mehr verortet. Bei Unterschreiten erfolgt automatische Liquidation.

2. **Stability Pool, SP**  
   Der SP begleicht in Liquidationen Vault Schulden. Im Gegenzug erhalten Einzahler die Sicherheiten, PLS, mit Bonus, und überschüssiger Supply wird vernichtet. Ziel ist Stress zu absorbieren statt zu verstärken.

3. **Redemption Engine als innerer Preisanker**  
   Redemption erlaubt ProjectUSD zum Gleichgewichtspreis R gegen PLS einzulösen. Dabei werden schwächste Vaults zuerst reduziert. Das soll Preisabweichungen per Arbitrage glätten.

4. **Controller und Rate r, Feedback Regelkreis**  
   Wenn Marktpreis P über oder unter R liegt, wird r angepasst, um Minting und Holding Incentives zu drehen. Die Reaktion ist begrenzt, um Überreaktionen zu vermeiden.

### 1.3 Black Swan Fokus dieser Studie

Diese Studie behandelt Stress, der gleichzeitig

- ökonomisch wirkt, PLS Kollaps, Liquidationen  
- liquiditätsseitig wirkt, DEX Volumen und Liquidität verschwinden  
- netzwerktechnisch wirkt, Reorgs  
- adversarial wirkt, MEV, Front Running, Sandwiching

und das System an mehreren Fronten gleichzeitig bricht.

---

## Kapitel 2: Szenarien

### 2.1 Szenario Matrix, Einzel und Kombinationsschocks

Wir definieren vier Basisszenarien plus ein Kaskadenszenario:

**S1: PLS 90, Preis Schock**  
- Exogener Schock: PLS minus 90 Prozent in kurzer Zeit, Minuten bis wenige Epochen  
- Erwartete Folge: massive Unterschreitungen der Collateral Ratio, Liquidationswelle

**S2: Liquidity Exodus, Marktstruktur Schock**  
- DEX Liquidität und Volumen fallen abrupt, LP Abzug, risk off  
- Whitepaper Risiko: Bei sinkendem DEX Volumen verlangsamt sich Arbitrage, Preisabweichungen können länger bestehen

**S3: Reorg Storm, Netzwerk Schock**  
- Serie von Chain Reorgs, zum Beispiel tiefe Reorgs über mehrere Blöcke, instabile Finalität  
- Wirkung: Liquidationen und Redemptions können verzögert, neu geordnet oder revertiert werden

**S4: MEV Supercycle, Adversarial Schock**  
- Extrem erhöhte MEV Aktivität, Sandwiching, Oracle Micro Manipulation, Backrunning von Liquidationen  
- Whitepaper erkennt MEV und Netzwerkstress explizit als Risiko an  
- Gegenmaßnahmen: Median TWAP, Rate Limiter, aber keine vollständige Immunität

**S5: Four Horsemen, Kaskade**  
- PLS 90 löst Panik aus, dann Liquidity Exodus, dann Oracle Lags und Preisrauschen, dann eskaliert MEV, dann verschärft Reorg Storm das Execution Risk  
- Ziel: Worst credible case inklusive Feedback Loops

### 2.2 Stressvariablen je Szenario, Test Inputs

Für reproduzierbare Tests werden die Schocks als Parametervektoren modelliert:

- **Preisprozess PLS:** Sprung minus 90 Prozent, optional Nachbeben, weiter minus 20 Prozent oder plus 30 Prozent intraday  
- **DEX Liquidität L:** minus 70 Prozent bis minus 95 Prozent in Kernpairs, Swap Spreads steigen nichtlinear  
- **Oracle Qualität:** TWAP Fenster, Staleness, Outlier Filter Schwellen  
- **Reorg Parameter:** Reorg Tiefe d, zum Beispiel 2 bis 20 Blöcke, Häufigkeit, Time to Finality  
- **MEV Intensität:** Anteil adversarialer Blöcke, Sandwich Rate, Front Run Wahrscheinlichkeit

### 2.3 Erfolgskriterien, was heißt System überlebt

Ein Black Swan Test gilt als bestanden, wenn

1. **Solvenz:** Kein systemischer Bad Debt Overhang, der dauerhaft unbacked Supply erzeugt, oder ein definierter Mechanismus zur Defizit Sozialisierung existiert  
2. **Peg Resilienz:** P bleibt in einem tolerierten Band um R oder kehrt dorthin zurück, Abweichung ist temporär, nicht permanent  
3. **Funktionalität:** Redemption und Liquidation funktionieren trotz Lags und Reorgs innerhalb definierter Grenzen  
4. **Manipulationsresistenz:** Oracle und Controller werden nicht dauerhaft gefangen, zum Beispiel durch illiquide Preise oder MEV

---

## Kapitel 3: Simulation

**Hinweis:** Das Whitepaper liefert Architektur und Risikohinweise, aber keine vollständige Parametertabelle, zum Beispiel konkrete Liquidation Thresholds, Gebühren, Epochenlänge. Diese Simulation ist daher konzeptionell und muss beim Engineering mit echten Parametern und Testnet Daten kalibriert werden.

### 3.1 Baseline Modellelemente, State Variables

Wir simulieren ein diskretes Zeitschrittmodell, block oder epochebasiert, mit Zuständen:

- **Vault Menge V = {vᵢ}:**  
  - Collateral Cᵢ in PLS  
  - Debt Dᵢ in ProjectUSD  
  - Collateral Ratio CRᵢ = (Cᵢ · PLS Preis) / Dᵢ

- **Stability Pool SP:** Einlage S in ProjectUSD  
- **Supply:** Total Supply T in ProjectUSD, zirkulierend versus gebunden  
- **DEX Pools:** Liquidität Lₖ, Price Impact Funktion  
- **Oracle:** Median TWAP aus mehreren Paaren plus Outlier Filter  
- **Controller:** r(t), reagiert auf ε(t) = P(t) minus R(t), Änderung begrenzt durch Rate Limiter  
- **Surplus Puffer:** Reserve, gespeist aus Gebühren, zur Glättung extremer r Schwankungen und AMO Verluste

### 3.2 Liquidationslogik, Engine

Whitepaper Kern: Wenn ein Vault unter die Sicherheitsgrenze fällt, wird Schuld aus dem SP beglichen. Einzahler erhalten PLS, überschüssiger Supply wird geburnt.

Simulation Implementierung, abstrakt:

1. Identifiziere unterbesicherte Vaults: CRᵢ kleiner als LT, Liquidation Threshold  
2. Sortiere nach CRᵢ, schwächste zuerst, oder pro Block begrenzte Menge  
3. Für jeden liquidierten Vault:  
   - SP zahlt min(S, Dᵢ) Schuld  
   - Debt wird reduziert oder geburnt  
   - Collateral wird an SP Allokation transferiert

**Offene Designfrage für echte Tests:**  
Was passiert, wenn SP kleiner ist als Summe der liquidationsfähigen Dᵢ. Im Whitepaper nicht detailliert.

Für Stresstests muss eine definierte Fallback Regel angenommen werden, zum Beispiel:

- Option A: Externe Liquidatoren kaufen Collateral gegen Debt, Auktion  
- Option B: Debt wird teilweise redistributed auf verbleibende Vaults, Sozialisierung  
- Option C: Defizit wird aus Surplus Puffer gedeckt, sonst Haircut

**Empfehlung:** Diese Fallback Mechanik muss explizit spezifiziert werden, sonst ist Worst Case Solvenz nicht prüfbar.

### 3.3 Redemption Logik, Arbitrage Kanal

Redemption: ProjectUSD kann zum Gleichgewichtspreis R gegen PLS eingelöst werden, schwächste Vaults werden zuerst reduziert.

Simulation Mechanik:

- Redemption Demand steigt, wenn P kleiner als R ist, Arbitrage, billig kaufen und zu R einlösen  
- Redemption reduziert Debt in den schwächsten Vaults und zieht Collateral ab  
- Effekt: Supply sinkt, Peg Stütze, aber Collateral Base wird verbraucht

### 3.4 Oracle und Price Feed Modell, on chain

Whitepaper Schutz gegen Manipulation:

- Median TWAP Oracle aus mehreren Paaren  
- Outlier Filter, low liquidity und excessive outliers werden ausgeschlossen  
- Rate Limiter für Änderungen von r

Zusatz für Black Swan: Whitepaper nennt explizit Oracle Bias. In extrem illiquiden Phasen kann Median TWAP träge reagieren und temporäre Abweichungen verursachen.

Daher modellieren wir:

- sinkende Liquidität führt zu höherem Oracle Noise und größerer Verzögerung  
- Outlier Filter kann im Extremfall zu viel herausfiltern, Median basiert dann auf wenigen Daten, Single Source Risk

### 3.5 Network und MEV Layer

- **MEV Strategien:** Sandwiching, kurzfristige Preisverzerrung in dünner Liquidität, Backrunning von Liquidations Orders. Whitepaper erkennt MEV, Front Running und Sandwiching als Angriffsflächen.  
- **Reorgs:** Probabilistische Reorg Events, die einen Teil der letzten Transaktionen rückgängig machen und neu ordnen.

### 3.6 Output Metriken, KPIs

- Peg Deviation: |P minus R| / R, Peak, Dauer, AUC über Zeit  
- Liquidationsdruck: Anzahl und Volumen pro Epoche, Backlog  
- SP Depletion: S(t) / S(0), Anteil nicht gedeckter Liquidationen  
- Oracle Error: |Oracle Price minus true pool price| und Staleness  
- Controller Stability: r Volatilität inklusive Rate Limiter Wirkung  
- MEV Extraction Estimate: value leaked durch Sandwich und Backrun  
- User Harm: Gas Spikes, Slippage, Forced Liquidation Rate

---

## Kapitel 4: Auswirkungen, Ergebnisse und Erwartungsbilder

### 4.1 S1: PLS 90, 90 Prozent PLS Crash

Primärer Mechanismus: PLS ist Kern Collateral, Vaults hinterlegen vor allem PLS.

#### 4.1.1 Mathematische Konsequenz für CR

Ein minus 90 Prozent Schock skaliert CRᵢ effektiv mit Faktor 0,1.

- Ein Vault mit 300 Prozent CR wird zu ungefähr 30 Prozent CR  
- Um nach minus 90 Prozent noch mindestens 170 Prozent zu sein, bräuchte man vorab ungefähr 1700 Prozent CR

Interpretation: Ein 90 Prozent Crash ist nicht nur eine Liquidationswelle. Er ist bei Single Collateral Heavy Design ein systemischer Stresstest, der fast alle normal gehebelten Vaults unter Wasser drückt.

#### 4.1.2 Liquidationswelle und SP Absorption

Der SP ist konzipiert, Liquidationen aufzufangen und Supply zu burnen, selbstheilender Kreislauf.

Worst Case Effekt:

- SP wird schnell geleert, falls S nicht groß genug ist  
- Wenn die Fallback Mechanik nicht robust ist, droht Bad Debt Akkumulation

Sekundär Effekt:

SP Einzahler erhalten sehr viel PLS Collateral, aber zu einem Zeitpunkt maximaler Panik und minimaler Liquidität. Das ist ökonomisch korrekt als Risikotransfer, kann aber psychologisch zu einem SP Run führen, Einzahler ziehen vorher ab, wenn möglich.

#### 4.1.3 Redemption in der Crash Phase

Redemption verankert P an R über Einlösbarkeit. Im PLS 90 Umfeld ist Redemption ambivalent:

- positiv: Supply Contraction stützt den Peg  
- negativ: Redemption entnimmt Collateral aus den schwächsten Vaults, beschleunigt deren Stress

Black Swan Spitze: Wenn PLS gleichzeitig illiquide wird, Szenario S2, und Oracle laggt, kann Redemption Collateral zu billig oder zu teuer bewerten. Genau dann wird Oracle Bias relevant.

#### 4.1.4 Erwartetes Peg Verhalten

Whitepaper betont: Bei sinkendem DEX Volumen verlangsamt sich Arbitrage. Preisabweichungen können länger bestehen.

Im PLS 90 allein, ohne Liquidity Exodus, wäre kurzfristig zu erwarten:

- Flight to safety in ProjectUSD, P größer als R  
- oder Vertrauensschock, P kleiner als R, durch Solvenzangst, wenn Nutzer Defizite fürchten

Welche Richtung dominiert, hängt stark von Transparenz und on chain Metriken ab, zum Beispiel sichtbare SP Größe und Vault Verteilung. Whitepaper betont, dass zentrale Metriken on chain einsehbar sind, unter anderem Größe des Stability Pools und Surplus Puffer.

### 4.2 S2: Liquidity Exodus, DEX Liquidität bricht weg

#### 4.2.1 Hauptrisiko: Preisfindung und langsame Arbitrage

Wenn DEX Volumen sinkt, verlangsamt sich Arbitrage. Preisabweichungen bleiben länger. Das ist besonders kritisch, weil ProjectUSD Stabilität über Marktmechanik plus Rückkopplung erzeugt, Controller r.

#### 4.2.2 Oracle Qualität unter Illiquidität

Gegen Manipulation setzt ProjectUSD auf Median TWAP aus mehreren Paaren plus Outlier Filter. Unter Liquidity Exodus treten zwei gegensätzliche Effekte auf:

- Filter schützt gegen Pump and Dump Spikes, gut  
- Filter kann Datenbasis ausdünnen, TWAP wird träge und unsicher, schlecht

Whitepaper erwähnt explizit, dass Median TWAP in extrem illiquiden Phasen träge reagieren kann.

#### 4.2.3 Systemische Folge

- Liquidationen können hinterherlaufen, Preis fällt, aber Oracle passt verzögert an  
- r Anpassungen können zu spät kommen, Rate Limiter verhindert Sprünge, kann aber auch Reaktionsgeschwindigkeit begrenzen, Trade off

### 4.3 S3: Reorg Storm, Chain Reorgs

#### 4.3.1 Was Reorgs im Protokoll praktisch bedeuten

Da ProjectUSD vollständig on chain operiert, sind Liquidationen, Redemptions und Oracle Samples transaktions und blockabhängig. Reorgs können:

- Liquidation Transaktionen reverteren, Backlog steigt  
- Reihenfolgen ändern, wer zuerst liquidiert oder redeemed wird  
- TWAP Datenfenster umschreiben, kurzfristige Oracle Instabilität

#### 4.3.2 Kritischer Punkt: No Pause

Da es keinen Pause Button gibt, muss das System Reorg Resilienz von vornherein haben, zum Beispiel Mindestbestätigungen, reorg sichere Oracles, konservative Windows.

### 4.4 S4: MEV Supercycle, extremes Front Running und Sandwiching

#### 4.4.1 Angriffsflächen

Whitepaper nennt MEV, Front Running und Sandwiching explizit als Angriffsflächen für Preisfeeds, Oracles und Pools. In Extremsituationen sind typische Vektoren:

- Oracle Micro Manipulation: dünne Pools kurz pumpen, TWAP beeinflussen  
- Liquidation Backrun: Liquidationsbots konkurrieren, treiben Gas, extrahieren Boni  
- Redemption Front Run: bei großer Redemption versuchen Bots den Preis vorher zu bewegen

#### 4.4.2 Eingebaute Gegenmaßnahmen

ProjectUSD begegnet MEV und Manipulation mit:

- Median TWAP Oracle aus mehreren Paaren  
- Outlier Filter  
- Rate Limiter für r, zum Beispiel ungefähr 50 Basispunkte pro Epoche

Aber: keine vollständige Immunität.

Black Swan Erkenntnis: In einem MEV Supercycle wird nicht unbedingt der Peg zerstört, aber es kann zu erheblichem Value Leakage kommen. Nutzer zahlen Slippage und Gas, Bots extrahieren Renten. Das verstärkt Liquidity Exodus, Szenario S2, und erhöht Kaskadenrisiko.

### 4.5 S5: Four Horsemen, Kaskade

Dieses Szenario ist der eigentliche Worst Case, weil Schutzmechanismen gegeneinander arbeiten können:

- PLS 90 führt zu Liquidationen und SP Stress  
- Liquidity Exodus führt zu Oracle Lag und langsamer Arbitrage  
- MEV erzeugt zusätzliche Friktion und Leakage  
- Reorg erzeugt Execution Risk und Backlogs  
- Ergebnis: Peg Recovery Time steigt stark, Vertrauen kann kippen, obwohl Mechanik formal weiterläuft

---

## Kapitel 5: Maßnahmen, Design und Betriebsmaßnahmen

### 5.1 Leitprinzip: Conservative by Design, weil immutable

Der Kern wird nach Freeze unveränderlich und es gibt keine Notabschaltung. Wichtigste Maßnahme ist daher konservative Parameterwahl vorab und phasenweises Hochfahren.

Whitepaper schlägt dafür eine Guarded Launch Phase vor: kleine maximale Schuldensumme, keine aktiven PSM oder AMO Module, intensive on chain Beobachtung.

Empfehlung, konkret für Black Swan Readiness:

- Debt Cap pro Collateral und global, TVL und Supply Deckel, im Guarded Launch  
- Stress Ready Parameter erst nach empirischer Stabilität, danach Freeze, Whitepaper: Kernparameter werden dauerhaft fixiert

### 5.2 Maßnahmen gegen PLS 90, S1

**A: Overcollateralization und Nutzer Leitplanken**  
- Da minus 90 Prozent faktisch alles unter Wasser drückt, müssen Nutzer zu höheren CRs motiviert werden, zum Beispiel über UI und Docs, empfohlenes CR Band  
- Optional: progressive Fees für riskante CRs, niedrige CR zahlen mehr

**B: Fallback Liquidationsmechanik spezifizieren**  
- Wie in Kapitel 3.2: SP kann leer laufen. Dann braucht es ein definiertes, auditierbares Verfahren, sonst ist Solvenz nicht beweisbar

**C: Collateral Diversifikation**  
- Whitepaper erwähnt Erweiterung um zusätzliche native Collaterals als langfristige Evolution  
- Für Black Swan Resilienz ist das nicht nice to have, sondern die strukturelle Antwort auf Single Asset Crash Risiko

### 5.3 Maßnahmen gegen Liquidity Exodus, S2

**A: Mehrere tiefe Referenzpaare**  
- Da Oracle auf mehreren Paaren basiert, muss Governance und Peripherie, DEX und Integrationen, dafür sorgen, dass diese Paare wirklich tief sind

**B: PSM als Friktionsdämpfer, nicht als Krücke**  
- Whitepaper: PSM optional nach Freeze, strikt limitiert, zum Beispiel Tageslimit und Haircuts, und darf ausfallen ohne Systemfunktion zu brechen  
- In Black Swan Logik: PSM nicht zur Rettung, sondern als kurzfristiger Stoßdämpfer, wenn DEX Liquidität reißt

**C: AMO nur mit Budget und Audit Trails**  
- AMOs, falls aktiviert, sollen innerhalb enger Preisbereiche agieren, budgetiert und auditierbar  
- Black Swan Regel: AMO Budgets im Normalbetrieb klein halten, erst nach Stabilität erhöhen

### 5.4 Maßnahmen gegen Reorg Storm, S3

Reorgs lassen sich nicht weg governen. Es braucht technische Robustheit:

- Reorg sichere Oracle Windows: TWAP so wählen, dass einzelne Reorg Blöcke keinen massiven Effekt haben, größeres Fenster, Mindestbestätigungen  
- Idempotente Liquidation und Redemption: Wiederholte Ausführung nach Reorg darf keine Doppelzählung erzeugen  
- Backlog Management: Wenn Liquidations Backlog entsteht, muss klar sein, wie Fairness umgesetzt wird, First seen versus worst CR first

### 5.5 Maßnahmen gegen MEV Supercycle, S4

Whitepaper setzt auf Median TWAP, Outlier Filter, Rate Limiter. Ergänzend, ohne Pause:

- Batching und Queues: Redemptions und Liquidationen in Batches, um einzelne Transaktionen schwerer sandwichbar zu machen  
- Commit Reveal für große Redemptions: reduziert Front Run, kostet aber UX  
- MEV aware Routing, Peripherie: AMO und PSM sollten MEV resistente Ausführung nutzen, begrenzte Slippage, Preisband Checks  
- Transparenz als Abschreckung: on chain Telemetrie in der Peripherie ist vorgesehen, in Stressphasen MEV Heatmaps veröffentlichen

### 5.6 Surplus Puffer als Stabilisator

Surplus Puffer ist im Whitepaper als kollektive Reserve beschrieben, die unter anderem extreme r Schwankungen glätten kann.

Für Black Swan Design:

- klare Policy, wann der Puffer eingesetzt werden darf, zum Beispiel r Glättung, SP Anreize  
- harte Obergrenzen, um Moral Hazard zu verhindern

### 5.7 Governance Risiko, sekundärer Black Swan

Whitepaper warnt: Peripherie könnte durch Mehrheiten beeinflusst werden, Governance Capture. Timelocks reduzieren Risiko, schließen es nicht aus.

Black Swan Maßnahme:

- Timelocks lang genug, damit Märkte reagieren können  
- Emergency Governance ist schwierig ohne Pause. Daher vordefinierte Parameterkorridore, die auch im Stress nicht überschritten werden dürfen

---

## Kapitel 6: Fazit

ProjectUSD ist als autarkes, on chain rückgekoppeltes Geldsystem entworfen, das Stabilität über Vaults und Liquidationen, Stability Pool, Redemption Engine und einen Controller mit Rate r um einen internen Gleichgewichtspreis R erzeugt.

Gerade weil der Kern nach dem Freeze Event unveränderlich ist und es keinen Pause Button gibt, müssen Black Swan Resilienzen vor Deployment in Parametern und Mechaniken verankert werden.

Wesentliche Erkenntnisse der Black Swan Analyse:

1. PLS 90 ist ein Extrem, das Single Collateral Systeme grundsätzlich bedroht. Überleben hängt an Overcollateralization, SP Tiefe und einer sauber spezifizierten Fallback Liquidation, wenn der SP leer ist.  
2. Liquidity Exodus verlängert Peg Abweichungen, weil Arbitrage langsamer wird und Oracle Lags zunehmen können.  
3. MEV kann in Extremphasen erhebliche Reibungsverluste erzeugen, auch wenn Median TWAP, Outlier Filter und Rate Limiter Schutz bieten. Vollständige Immunität ist nicht garantiert.  
4. Reorgs sind ein Execution Black Swan. Ohne Pause Option zwingend durch reorg sichere Oracles und idempotente Ausführung abzufedern.

Strategischer Schluss: Der sicherste Weg ist der im Whitepaper angelegte. Guarded Launch, kleine Schuldensumme, keine PSM oder AMO, intensive Beobachtung. Danach Freeze erst bei nachgewiesener Stabilität. Damit werden Black Swan Risiken nicht entfernt, aber so weit eingedämmt, dass das System auch unter Extremstress weiterläuft, ohne auf menschliche Eingriffe angewiesen zu sein.

---

## Offene Parameter und Engineering Aufgaben

Die folgenden Punkte sind in der PDF Vorlage ausdrücklich als offene Designfragen oder Kalibrierungsbedarf erkennbar und müssen vor formalen Tests spezifiziert werden:

1. Konkrete Parameter: Liquidation Thresholds, Gebühren, Epochenlänge, Rate Limiter Grenzen  
2. Fallback Mechanik, wenn der Stability Pool nicht ausreicht: Option A, B oder C, oder eine neue definierte Regel  
3. Definition von Fairness Regeln bei Backlogs: Reihenfolge Logik und Kapazitätsgrenzen pro Block oder Epoche  
4. Oracle Fenster und Reorg Resilienz: Mindestbestätigungen, Window Längen, Filter Schwellen  
5. Messbare Definition des tolerierten Peg Bandes und der maximalen Recovery Time im Worst Case

---

## Verification

Diese Studie ist als konzeptionelle Blaupause formuliert. Verifikation bedeutet hier, die beschriebenen Szenarien und Metriken als reproduzierbare Testfälle in einem Simulationsframework und anschließend auf Testnet umzusetzen.

**Vorschlag für überprüfbare Schritte:**

1. **Parameter Freeze Liste erstellen**  
   Definiere alle Kernparameter, die vor Freeze unveränderlich sind, und dokumentiere sie in einer Parametertabelle.

2. **Simulationsmodell implementieren**  
   Diskretes Modell mit Vault Verteilung, SP Größe, DEX Liquidität und Oracle Verzögerung. Erzeuge deterministische Seeds für Preisprozesse, Reorg Events, MEV Intensität.

3. **Szenario Runner bauen**  
   Implementiere S1 bis S5 als Parametervektoren. Jeder Run speichert KPIs, insbesondere Peg Deviation, SP Depletion, Bad Debt Indikatoren, Oracle Error, r Volatilität.

4. **Bestehens Kriterien operationalisieren**  
   Setze Grenzwerte, zum Beispiel maximaler Bad Debt Anteil, maximale Peg Abweichung, maximale Recovery Time, und bewerte Runs automatisiert als bestanden oder nicht bestanden.

5. **Testnet Validierung**  
   Führe die gleichen Szenarien mit realen on chain Daten und echten Oracles auf einem Testnet nach. Vergleiche Simulation und Testnet Outputs, kalibriere Parameter.

**Ergebnis der Verifikation:**  
Eine reproduzierbare Test Suite, die Worst Case Robustheit messbar macht, bevor ein Freeze Event den Immutable Core fixiert.
```
