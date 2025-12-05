# Nikolai Mushegians RICO Konzept und seine Weiterführung in ProjectUSD  
Wie die Vision eines autonomen Geldes weiterlebt

## Einleitung

Die Geschichte der algorithmischen Stablecoins lässt sich in zwei große Entwicklungswege einteilen.  
Der erste Weg beginnt mit MakerDAO und den frühen DeFi Systemen. Sie bewiesen, dass Kreditmärkte direkt auf der Chain funktionieren können, verloren jedoch im Laufe der Zeit ihre Unabhängigkeit durch stark wachsende Abhängigkeit von Fiat Sicherheiten.

Der zweite Weg ist die kaum veröffentlichte, aber einflussreiche Idee von Nikolai Mushegian. Sein Konzept RICO sollte ein vollkommen eigenständiges Geldsystem sein, das sich aus sich selbst heraus stabilisiert und keinerlei Bezug zum Dollar benötigt. Es war seiner Zeit voraus und blieb unvollständig, doch es enthielt die entscheidenden Gedanken eines autarken Wertmaßes.

Heute taucht genau diese Idee wieder auf, jedoch in strukturierter und vollständig definierter Form: ProjectUSD.

---

# 1 RICO in Kürze  
Die unvollendete Idee eines autonomen Wertmaßes

RICO war nicht als Produkt gedacht, sondern als Vision eines Geldsystems, das ganz ohne externe Bezugspunkte funktioniert.

Mushegians Kerngedanke:

**Wenn ein Geldsystem intern Rückkopplung erzeugt, kann es sich selbst stabilisieren.**

Wesentliche Ziele von RICO waren:

* kein Fiat Peg  
* keine Banken  
* keine zentralen Reserven  
* keine Orakel  
* vollständige Autonomie durch algorithmische Dynamik

RICO stellte damit die radikalste Form eines On Chain Wertmaßes dar. Doch RICO blieb fragmentarisch. Es gab keine vollständige Architektur, keine klare Mechanik und keine Definition der zentralen Variablen.

---

# 2 ProjectUSD  
Die technische und konzeptionelle Vollendung der ursprünglichen RICO Idee

ProjectUSD entwickelt exakt diese Idee weiter und verwandelt sie in ein vollständiges System.  
Das Whitepaper V2.1 beschreibt ProjectUSD als ein autonomes rückgekoppeltes Geldsystem, das vollständig ohne Orakel Banken oder zentrale Steuerung auskommt.

> ProjectUSD ist ein vollständig on chain operierendes algorithmisches Geldsystem das Preisstabilität ohne Orakel Banken oder zentrale Eingriffe erreicht.

Damit erfüllt ProjectUSD exakt das Ziel, das Mushegian mit RICO anstrebte, allerdings erstmals in geschlossener klarer und überprüfbarer Form.

---

# 3 Die zentrale Mechanik  
P, R und r als Rückkopplungssystem

Die entscheidende Gemeinsamkeit zwischen RICO und ProjectUSD ist der Gedanke, dass ein Wertmaß nicht fixiert werden muss, sondern sich durch Abweichungen selbst reguliert.

ProjectUSD formuliert diese Rückkopplung in drei Variablen:

### P  
Der freie Marktpreis auf der DEX.  
Er zeigt lediglich, wie der Markt aktuell reagiert.

### R  
Der interne Gleichgewichtspreis.  
Er dient als mathematischer Referenzpunkt und wird nicht durch Orakel bestimmt.  
Er ist der Wert, zu dem ProjectUSD jederzeit intern eingelöst werden kann.

### r  
Die Systemrate, die auf Preisabweichungen reagiert.  
Sie ist die Regelkraft des Systems.

> r ist die automatische Gegenkraft, die jede Abweichung korrigiert.

Diese kompakte Regelmechanik war bereits in RICO angelegt, wird jedoch erst in ProjectUSD vollständig operationalisiert.

---

# 4 Die Architektur von ProjectUSD  
Der fehlende technische Rahmen, den RICO nie erreichte

ProjectUSD ist nicht nur ein Konzept, sondern eine vollständige Infrastruktur.  
Die wichtigsten Komponenten werden im Whitepaper präzise beschrieben.

### Vaults  
PLS dient als Sicherheit. Neue ProjectUSD Einheiten entstehen durch Besicherung.

### Stability Pool  
Der Pool stabilisiert das System durch automatische Übernahme unterbesicherter Positionen.

### Redemption Engine  
Sie garantiert, dass der Preis niemals dauerhaft vom internen Wert abweicht.  
Sie dient als fundamentaler Wertanker ohne Orakel.

### Immutable Core  
Ein eingefrorener Kern ohne Eingriffsmöglichkeiten.  
Nach dem Freeze Event kann niemand das System verändern.

> Was sich nicht verändern lässt kann auch nicht missbraucht werden.

Damit ist ProjectUSD das erste System, das diese Philosophie technisch realisiert.

---

# 5 Die Weiterentwicklung der RICO Idee

ProjectUSD geht über RICO in mehreren entscheidenden Punkten hinaus:

### 1 Ein klar definierter Gleichgewichtspreis R  
RICO hatte keine vollständige Definition.  
ProjectUSD nutzt R als mathematisch abgeleiteten Systemwert, der unabhängig von externen Märkten existiert.

### 2 Eine vollständige Rückkopplungsfunktion r  
Die Systemrate r wird strikt durch die Größe der Preisabweichung bestimmt.  
Sie ist begrenzt, transparent und algorithmisch.

### 3 Ein funktionierender Geldschöpfungsprozess  
Vaults erzeugen ProjectUSD durch Collateral in PLS.  
Dies war bei RICO nur angedeutet.

### 4 Ein ausgereiftes Sicherheitsmodell  
Median TWAP, Outlier Filter, Rate Limits und Anti MEV Schutz sind vollständig integriert.

### 5 Ein echtes Autonomiesystem durch das Freeze Event  
Damit wird ProjectUSD zum Organismus ohne menschliche Eingriffe.

ProjectUSD ist damit nicht nur eine Fortsetzung der Idee, sondern deren Realisierung.

---

# 6 Die gemeinsame Philosophie  
Warum RICO und ProjectUSD denselben Ursprung teilen

Beide Systeme folgen derselben Leitidee:

**Ein Wertmaß soll nicht zentral bestimmt werden, sondern aus dem Verhalten der Teilnehmer entstehen.**

Aus dem Whitepaper:

> Statt Vertrauen gibt es Transparenz  
> Statt Versprechen gibt es Code

Mushegian hätte sich genau ein solches System gewünscht.  
Nicht ein Produkt, sondern ein autonomes ökonomisches Gleichgewicht.

---

# 7 Bedeutung für die PulseChain Ökonomie

ProjectUSD gibt PulseChain etwas, das bisher fehlte:

* eine interne Recheneinheit  
* eine autonome Preisstabilität  
* ein System, das Kaufkraft auf der Chain hält  
* ein Fundament für Lending Derivate und Liquidität  
* eine echte Alternative zu zentralen Stablecoins

> Kaufkraft bleibt dort wo sie nützlich ist  
> ProjectUSD hält sie im System

Damit wird PulseChain erstmals zur geschlossenen Ökonomie.

---

# Fazit  
ProjectUSD ist nicht wie RICO  
ProjectUSD ist die Vollendung von RICO

RICO war der erste Versuch, Geld völlig neu zu denken.  
ProjectUSD ist die technische und konzeptionelle Ausarbeitung dieser Idee in moderner Form.

Die Vision bleibt dieselbe:

**Ein Geldsystem ist dann frei, wenn es sich selbst stabilisiert.**

RICO sprach diesen Gedanken aus.  
ProjectUSD schreibt ihn in Code.
