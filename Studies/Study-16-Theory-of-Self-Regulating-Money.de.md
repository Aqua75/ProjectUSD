# Study 16 - Die Theorie des selbstregulierenden Geldes  
*Philosophie des autonomen Geldes, Geldtheorie, Dezentralität und Systemautonomie im Spiegel von ProjectUSD auf PulseChain*  
*(Level-3 Research Format)*

---

## Abstract

Diese Studie entwickelt eine akademisch philosophische Theorie des selbstregulierenden Geldes und untersucht, unter welchen Bedingungen ein Geldsystem ohne institutionelles Zentrum als stabil, legitim und funktionsfähig gelten kann. Ausgehend von klassischen und modernen Geldtheorien wird Stabilität nicht als bloße Preisfixierung verstanden, sondern als performatives Ergebnis von Erwartungen, Rückkopplungen und institutionellen Garantien.

Anschließend werden Konzepte der Systemtheorie und Kybernetik auf monetäre Ordnungen übertragen: Autonomie erscheint nicht als Isolation, sondern als Fähigkeit, Störungen durch interne Regelkreise zu verarbeiten, ohne auf willkürliche Eingriffe angewiesen zu sein.

Im vierten Kapitel wird ProjectUSD als Fallstudie gelesen: ein vollständig on chain entworfenes, algorithmisches Geldsystem für PulseChain, das Stabilität über einen internen Gleichgewichtspreis R, eine variable Systemrate r, Vault basiertes Collateral, Stability Pool und Redemption Mechanik herstellen will, ergänzt durch einen Immutable Core nach einem Freeze Event, Unveränderlichkeit als monetäre Verfassung.

Das Fazit formuliert Kriterien, unter denen ProjectUSD als paradigmatischer Entwurf autonomen Geldes gelten kann, und benennt philosophische Spannungsfelder: Autonomie versus Anpassungsfähigkeit, Transparenz versus Komplexität, sowie die Frage, ob Stabilität ohne externen Nominalanker mehr ist als interne Kohärenz.

---

# 1. Einleitung

## 1.1 Problemstellung - Geld zwischen Vertrauen, Macht und Technik

Geld ist nie nur ein neutrales Tauschmittel. Es ist zugleich Institution, Infrastruktur und politische Technologie. Wer Geld emittiert, definiert implizit Spielregeln: welche Sicherheiten zählen, welche Schuldverhältnisse akzeptiert werden, wer im Krisenfall gerettet wird und wer nicht. Die historische Normalform dieser Macht war der Staat, Steuerhoheit und gesetzliches Zahlungsmittel, oder das Bankensystem, Kreditgeldschöpfung und lender of last resort.

Dezentrale Finanzsysteme treten an, diese Machtarchitektur zu umgehen. Doch gerade bei Stablecoins zeigt sich ein Paradox: Stabilität wird häufig mit Zentralität erkauft, Verwahrer, Bankkonten, Blacklists, regulatorische Zugriffspunkte. Das ProjectUSD Whitepaper setzt hier an und formuliert eine Gegenposition: ein vollständig on chain operierendes, algorithmisches Geldsystem, das Preisstabilität ohne Banken und ohne zentrale Eingriffe erreichen will, zugleich aber ausdrücklich keine Produktankündigung, sondern eine konzeptionelle Blaupause ist.

Philosophisch verschiebt sich damit die Frage von Ist das schon real zu Welche Art von Geld wäre denkbar, wenn wir das Steuer vollständig an Regeln übergeben.

## 1.2 Leitfragen

Diese Studie untersucht fünf Leitfragen:

1. Was ist Geld in theoretischer Hinsicht, Funktion, Ursprung, Legitimität  
2. Was heißt Stabilität, Fixierung an einen externen Maßstab oder interne dynamische Balance  
3. Was bedeutet Autonomie in Systemen und ist ein Geldsystem überhaupt autonom möglich  
4. Wie übersetzt ProjectUSD die Idee der Autonomie in Mechanismen, R, r, Vaults, Stability Pool, Redemption, Immutable Core  
5. Welche normativen Konsequenzen hat Code als Geldordnung, Verantwortung, Freiheit, Gerechtigkeit, Fehlertoleranz

## 1.3 Methode und Abgrenzung

Methodisch handelt es sich um eine philosophische Analyse mit systemtheoretischem Zugriff und einer interpretativen Lektüre der Primärquelle, ProjectUSD Whitepaper V2.1. Der Text wird nicht als technische Spezifikation im engen Sinne behandelt, sondern als Entwurf einer monetären Verfassung und als Programm einer bestimmten Geldphilosophie: statt Versprechen gibt es Code, statt Vertrauen gibt es Transparenz.

Abgrenzung: Diese Studie ist keine Investmentanalyse und keine formale Sicherheitsprüfung. Sie fragt nach Begriffen, Voraussetzungen und Widersprüchen, nicht nach kurzfristigen Marktchancen.

---

# 2. Geldtheorie

## 2.1 Geldfunktionen - Tauschmittel, Recheneinheit, Wertaufbewahrung

In der klassischen Ökonomie wird Geld über drei Kernfunktionen definiert:

1. Medium of Exchange, Tauschmittel  
2. Unit of Account, Recheneinheit  
3. Store of Value, Wertaufbewahrung

Philosophisch ist entscheidend: Diese Funktionen sind nicht naturgegeben, sondern beruhen auf kollektiven Erwartungen und institutionellen Garantien. Geld funktioniert, weil hinreichend viele Akteure erwarten, dass es auch morgen als Geld akzeptiert wird.

Damit wird Geld zu einem sozialen Vertrag, nicht notwendig im rechtlichen Sinn. In Krypto Systemen kann dieser Vertrag technisch codiert sein: Regeln werden zu Ausführungsbedingungen. ProjectUSD formuliert diese Perspektive als Substitution von Vertrauen durch Sichtbarkeit und deterministische Logik.

## 2.2 Ursprungstheorien - Ware, Staat, Kredit

Geldtheorie ist historisch in drei große Erzählungen gespalten:

- Warengeld und Tauschtheorie: Geld entsteht aus Marktprozessen, um Tausch zu erleichtern  
- Chartalismus und Staatstheorie: Geld ist primär staatliches Zeichen, Akzeptanz wird über Steuern und Rechtsordnung gestiftet  
- Kredittheorien: Geld ist zuerst ein Schuld und Kreditverhältnis, Banken erzeugen Geld durch Bilanzierung, Vertrauen durch Institutionen

ProjectUSD steht quer zu diesen Linien. Es ist nicht staatlich gestiftet, nicht an Bankbilanzen gebunden, nicht zwingend Warengeld, und nutzt zugleich collateral basierte Logik, Vaults, die an Sicherungsintuitionen erinnert: Geldschöpfung wird an Sicherheiten gekoppelt. Das System erzeugt Token über überbesicherte Positionen, Collateral Ratio typischerweise 170 Prozent oder mehr.

Philosophisch lässt sich das als Versuch verstehen, Kreditgeld ohne Bank zu realisieren: Schulden werden durch Smart Contracts formalisiert, Sicherheit durch Liquidationsmechanik und kollektive Puffer, Stability Pool, organisiert.

## 2.3 Stabilität als normative Kategorie

Stabilität ist nicht nur ein Preisbegriff, sondern ein Wohlfahrts und Gerechtigkeitsargument. Unstabile Recheneinheiten erzeugen Umverteilung, weil sie Kalkulation und Vertragsbeziehungen verzerren. Klassisch wird Stabilität daher an einen externen Nominalanker gebunden, Gold, staatliche Zielinflation, Währungskorb.

ProjectUSD schlägt eine andere Definition vor: Stabilität als Pendeln um einen internen Gleichgewichtspreis R, wobei Abweichungen über eine endogene Rate r gedämpft werden. Diese Stabilität ist nicht identisch mit einer externen Parität. Das Whitepaper betont ausdrücklich, ProjectUSD wolle keine Fiat Kopie sein, sondern eine eigenständige digitale Recheneinheit.

Damit verschiebt sich der Begriff: Stable heißt hier weniger externe Parität, sondern interne Kohärenz und Einlösbarkeit.

## 2.4 Regelbindung versus Diskretion - die alte Debatte in neuer Form

Geldordnungen schwanken historisch zwischen Diskretion, situatives Eingreifen, und Regelbindung, feste Regeln. ProjectUSD radikalisiert Regelbindung: kein Admin Key, kein Pause Button, keine Eingriffsrechte. Nach dem Freeze Event soll der Kern unveränderlich werden.

Philosophisch entspricht dies der These: Willkür ist das Grundproblem des Geldes, die Lösung ist nicht bessere Herrschaft, sondern deren Ausschluss durch Unveränderlichkeit. Doch Regelbindung bleibt ambivalent. Sie schützt vor Machtmissbrauch, kann aber die Fähigkeit nehmen, auf echte Systemfehler zu reagieren.

Der Konflikt ist nicht technisch, sondern politisch philosophisch: Wollen wir ein Geld, das im Zweifel nicht gerettet werden kann, selbst wenn es sollte.

---

# 3. Autonome Systeme

## 3.1 Autonomie - nicht Isolation, sondern Selbststeuerung

In Systemtheorie und Kybernetik bezeichnet Autonomie nicht primär Abgeschlossenheit, sondern die Fähigkeit, wesentliche Zustände durch interne Prozesse zu reproduzieren. Ein autonomes System verarbeitet Störungen über Rückkopplung, nicht über Befehl von außen.

ProjectUSD beschreibt genau dieses Motiv: Abweichungen zwischen Marktpreis P und internem Preis R führen zu Anpassungen der Systemrate r, wodurch Verhalten von Schuldnern und Sparern beeinflusst wird. Der Controller wirkt wie ein Regelkreis: messen, vergleichen, korrigieren.

## 3.2 Rückkopplung und Homeostase

Viele biologische und technische Systeme stabilisieren sich nicht durch Starrheit, sondern durch Dynamik, Homeostase. Das Whitepaper nutzt diese Metapher: Stabilität entstehe nicht durch Fixierung, sondern durch Bewegung, das System atmet über Gegenkräfte bei Preisabweichungen.

Philosophisch ist das bemerkenswert: Stabilität wird als Prozess verstanden, nicht als Zustand. Geld wird weniger Ding, sondern Regelbetrieb.

## 3.3 Autopoiesis und strukturelle Kopplung

Autopoiesis Theorien betonen: Autonome Systeme sind operational geschlossen, aber strukturell gekoppelt an ihre Umwelt. Sie sehen die Umwelt nur durch eigene Sensorik und reagieren nur über eigene Operationen.

Übertragen auf ProjectUSD heißt das: Oracleless bedeutet nicht ohne Umweltkontakt, sondern ohne fremde Autorität. Das System nutzt on chain Preisbezüge, Median und TWAP über DEX Paare, als interne Wahrnehmung. Es gibt keinen externen Schiedsrichter, sondern einen selbst definierten Messprozess.

Autonomie ist damit eine Frage der epistemischen Schnittstelle: nicht keine Daten, sondern keine fremde Autorität.

## 3.4 Komplexität, Reflexivität und Grenzen der Steuerung

Autonome Systeme in Märkten sind reflexiv: Erwartungen beeinflussen Ergebnisse, Ergebnisse beeinflussen Erwartungen. Ein Regelkreis kann stabilisieren oder Oszillationen erzeugen, Überreaktion, Trägheit, Panik.

ProjectUSD adressiert dieses Risiko über Rate Limiter, begrenzte Veränderung von r pro Epoche, und Filtermechanismen gegen Manipulation, Median TWAP und Outlier Filter. Gleichzeitig bleibt: Kein Regelwerk kann den sozialen Anteil des Marktes vollständig eliminieren. Psychologische Faktoren, Panik, irrationales Handeln, markieren Grenzen algorithmischer Perfektion.

Autonomie ist daher graduell, nicht absolut.

## 3.5 Governance - Wächter oder Souverän

Wer darf Regeln ändern. ProjectUSD entwirft eine zweischichtige Ordnung:

- Immutable Core, Kernfunktionen wie Vaults, Liquidationen, Redemption, Controller, wird nach dem Freeze unveränderlich  
- Peripherie bleibt über Timelocks und Abstimmungen anpassbar, Module wie AMO und PSM, Adapter

Governance ist Wächter, nicht Herrscher. Philosophisch entspricht dies einem konstitutionellen Modell: Es gibt eine Verfassung, die politische Prozesse begrenzt.

Dezentralität bedeutet damit nicht nur Verteilung von Macht, sondern Einschränkung von Macht durch Architektur.

---

# 4. ProjectUSD im Kontext

## 4.1 Systemidee - autonomes Geld für eine autonome Chain

Das Whitepaper positioniert ProjectUSD als fehlenden Baustein einer autarken DeFi Ökonomie auf PulseChain: ein Wertanker, der ebenso autonom funktioniert wie die Chain selbst. Die Grundthese lautet: Stabilität braucht kein Vertrauen, wenn Rückkopplung menschliche Kontrolle ersetzt.

Geld erscheint hier nicht als Produkt, sondern als Systemorgan. ProjectUSD spricht vom Herz der Ökonomie und beschreibt sich als Mini Zentralbank, nur ohne Menschen.

Philosophisch ist das eine Umdeutung von Zentralbankfunktionen in Code:

- Steuerung der Geldschöpfung, Vaults und r  
- Krisenmechanismen, Stability Pool und Liquidation  
- Einlösbarkeit und Anker, Redemption zu R

## 4.2 R und r - endogener Maßstab statt externer Peg

Im Zentrum steht der interne Gleichgewichtspreis R als Referenz, um den der Marktpreis P pendeln soll. Die Steuergröße r kann positiv oder negativ sein und beeinflusst Minting und Holding von ProjectUSD.

Die Mechanik impliziert eine kybernetische These: Stabilität entsteht, wenn Anreize so gesetzt sind, dass Abweichungen unattraktiv werden. Nicht Befehl, sondern Feld, ein Anreizfeld, in dem Akteure durch Eigeninteresse zur Rückkehr in die Nähe des Gleichgewichts beitragen.

Kritische Frage: Was ist dann Wert. Wenn R nicht an einen externen Maßstab gebunden ist, wird Wert zu einem inneren Bezugspunkt des Systems. ProjectUSD betont diese Eigenständigkeit ausdrücklich. Philosophisch lässt sich das als Versuch lesen, eine monetäre Sphäre zu schaffen, in der Recheneinheit und Stabilität aus der Systemlogik entstehen.

Damit wird Stablecoin als Label potenziell irreführend: Es ist eher eine algorithmische Recheneinheit mit Stabilitätsziel, nicht notwendigerweise eine Fiat Abbildung.

## 4.3 Vaults, Stability Pool, Redemption - Institutionen ohne Institution

ProjectUSD organisiert Geldschöpfung und Stabilität über drei Kerninstitutionen in Codeform:

1. Vaults: Nutzer hinterlegen Sicherheiten, vor allem PLS, und prägen ProjectUSD bei Mindestbesicherung. Unterhalb der Schwelle erfolgen automatische Liquidationen  
2. Stability Pool: Nutzer hinterlegen ProjectUSD, um Liquidationen zu absorbieren und dafür Sicherheiten und Bonifikationen zu erhalten. Dabei wird Supply reduziert, Burn, Stress wird geschluckt  
3. Redemption Engine: Jeder kann ProjectUSD zum Gleichgewichtspreis R gegen PLS einlösen, die schwächsten Vaults werden zuerst reduziert

Philosophisch übersetzt das klassische Institutionen:

- der Vault ist eine individualisierte Bilanz  
- der Stability Pool ist kollektive Versicherungslogik  
- die Redemption ist Einlösbarkeit als Legitimationskern

In traditioneller Geldtheorie ist Einlösbarkeit politisch, Steuern, oder institutionell, Bankreserven. Hier wird sie prozedural: Einlösbarkeit ist Funktion des Protokolls, nicht Versprechen einer Instanz.

## 4.4 Immutable Core und Freeze Event - monetärer Konstitutionalismus

Der Immutable Core ist Herzstück: Nach einem Freeze Event kann niemand mehr Kernlogik oder Kernparameter verändern. Es gibt keinen Admin Key und keinen Stecker.

Philosophisch ist das der stärkste normative Anspruch: Autonomie durch Unveränderlichkeit. Geld wird zur dauerhaften Regel, nicht zur laufenden politischen Entscheidung.

Ambivalenz:

- positiv: Minimierung von Willkür, Verringerung von Capture Risiken, maximale Vorhersehbarkeit  
- negativ: Unveränderlichkeit macht auch Fehler dauerhaft. Smart Contract Fehler sind irreversibel, Qualität vor dem Freeze muss kompromisslos sein

Damit entsteht ein klassisches Dilemma politischer Philosophie in technischer Form: lieber fehlbare Anpassungsfähigkeit, mit Machtmissbrauchsrisiko, oder Starrheit, mit irreversiblen Fehlerkosten.

ProjectUSD beantwortet das tendenziell zugunsten der Starrheit und verlagert Verantwortung in die Vorphase: Audit, Verifikation, Tests.

## 4.5 Oracleless und dennoch Messung - epistemische Unterscheidung

Das Whitepaper betont ohne Orakel und beschreibt zugleich Median TWAP, Outlier Filter und Preisaggregation über mehrere DEX Paare. Das ist weniger Widerspruch als epistemische Unterscheidung:

- ohne Orakel meint ohne off chain Autorität und ohne bankgestützten Fiat Referenzfeed  
- mit Orakel im technischen Sinn meint interne on chain Messung des Systemumfelds, DEX Preise, um Manipulationen zu glätten

Philosophisch: Das Protokoll kann die Welt nicht nicht beobachten. Es kann nur entscheiden, wie es beobachtet und welche Beobachtungsform als legitim gilt. ProjectUSD wählt Beobachtung aus dem eigenen System heraus und setzt Filter gegen Manipulation.

## 4.6 Sicherheit und Transparenz - buchhalterische Wahrheit als Norm

ProjectUSD versteht Transparenz als Ersatz für Vertrauen: Metriken wie R, r, Vault Verteilung, Pool Größe und Historien sollen on chain einsehbar sein.

Normative Verschiebung:

- traditionelle Systeme verlangen Vertrauen in Berichte, Institutionen, Prüfer  
- on chain Systeme setzen auf unmittelbare Verifizierbarkeit, wer wissen will, ruft den Smart Contract ab

Doch Transparenz ist nicht identisch mit Verständlichkeit. Ein komplexes Protokoll kann faktisch transparent sein und dennoch epistemisch exklusiv. Daraus folgt die Frage: Ersetzt Transparenz wirklich Vertrauen oder ersetzt sie nur blindes Vertrauen durch technische Autorität.

Ob Transparenz Vertrauen ersetzt, hängt weniger von Daten ab als von ihrer sozial geteilten Interpretierbarkeit.

## 4.7 PulseChain Kontext - Souveränität durch eigene Recheneinheit

Das Whitepaper argumentiert, PulseChain brauche eine eigene stabile Währung, um unabhängig von zentralisierten Stablecoins zu werden, die durch Blacklisting, Regulierung oder Ausfälle das Ökosystem gefährden könnten.

Philosophisch ist das ein Souveränitätsargument: Ein System ist nur so autonom wie seine Recheneinheit. Ohne eigenes Geld bleibt eine Chain abhängig, ökonomisch und politisch. ProjectUSD wird damit als Versuch gelesen, monetäre Unabhängigkeit zu schaffen, nicht nur technische Dezentralität.

## 4.8 Risiken und Grenzen - Ehrlichkeit als Teil der Geldphilosophie

Bemerkenswert ist die explizite Risikobenennung: Smart Contract Fehler, MEV, Oracle Bias in illiquiden Phasen, Volatilität der Sicherheiten, psychologische Marktreaktionen, Governance Capture in der Peripherie sowie rechtliche Unsicherheiten.

Die Pointe lautet: Perfekte Sicherheit existiert nicht. Der Unterschied liegt darin, wo Risiken liegen und ob sie sichtbar sind. ProjectUSD verlagert Risiko vom Menschen in den Code, um es sichtbar, messbar und fair zu machen.

Das ist eine Ethik expliziter Regeln: Nicht Abwesenheit von Risiko ist das Ziel, sondern Abwesenheit verdeckter, willkürlicher Entscheidungen.

---

# 5. Fazit

## 5.1 Ergebnisse in Thesenform

1. Selbstregulierendes Geld ist philosophisch plausibel, wenn Stabilität als dynamische Rückkopplung verstanden wird, nicht als starre Parität. ProjectUSD entwirft Stabilität als Regelkreis um R mit Anpassung über r  
2. Autonomie bedeutet nicht Umweltfreiheit, sondern die Fähigkeit, Umweltstörungen über interne Operationen zu verarbeiten. ProjectUSD operationalisiert dies über on chain Messung, Regelanpassung und Einlösbarkeit, Redemption  
3. Unveränderlichkeit, Immutable Core und Freeze Event, ist monetärer Konstitutionalismus: Sie begrenzt Macht, erhöht aber Kosten irreversibler Fehler  
4. Transparenz ersetzt Vertrauen nur teilweise: Sie macht Prozesse prüfbar, aber nicht automatisch sozial verständlich. Expertise, Kultur und Erwartungskoordination bleiben relevant  
5. ProjectUSD ist dem eigenen Anspruch nach keine Fiat Kopie, sondern eigenständige Recheneinheit für eine geschlossene Ökonomie. Damit verschiebt sich die Debatte von Peg halten zu Systemkohärenz aufrechterhalten

## 5.2 Offene Fragen, philosophisch systemisch

- Nominalanker Frage: Wenn R endogen ist, woran misst man Stabilität außerhalb des Systems. Reicht interne Einlösbarkeit als Legitimationskern  
- Gerechtigkeitsfrage: Wer trägt Lasten in Stressphasen, Vault Owner, Pool Teilnehmer, Arbitrageure. Ist Verteilung normativ fair oder nur regelkonform  
- Governance Frage: Kann Peripherie Governance langfristig sicher bleiben, wenn sie ökonomisch attraktiv wird, Capture Risiko  
- Epistemische Frage: Wie verhindert man, dass Transparenz in der Praxis zur Herrschaft derjenigen wird, die Daten interpretieren können

## 5.3 Schlussgedanke

ProjectUSD formuliert eine radikale These: Geld kann als autonomes System existieren, wenn es als unbestechlicher Regelbetrieb konstruiert wird, ein Vertrag, der nicht gebrochen werden kann.

Philosophisch ist das mehr als DeFi Engineering. Es ist der Versuch, die politische Frage des Geldes durch eine architektonische Antwort zu ersetzen: nicht bessere Herrschaft, sondern weniger Herrschaft.

Ob diese Verschiebung gelingt, hängt nicht nur vom Code ab, sondern von der sozialen Realität, die ihn umgibt: Märkte, Erwartungen, Liquidität, Krisen und der menschlichen Neigung, selbst im transparentesten System wieder Autoritäten zu suchen. Autonomes Geld ist deshalb nicht die Abschaffung des Politischen, sondern seine Neuformulierung: von Souveränität als Person oder Institution zu Souveränität als Protokoll.

---

# 6. Literaturhinweise

## Primärquelle

- ProjectUSD - Ein autonomes Geldsystem für PulseChain. Whitepaper V2.1 DE, Vision und Architektur einer selbstregulierenden Blockchain Ökonomie, Nov. 2025. Konzeptionelle Blaupause, Kapitel zu Versprechen autonomen Geldes, Mechanik R und r, Architektur, Sicherheit, Roadmap, Risiken, Philosophie

## Klassische und moderne Referenzlinien zur Einordnung

- Aristoteles: Nikomachische Ethik, Tausch, Maß, Geld als Konvention  
- Georg Simmel: Philosophie des Geldes, Geld als Form sozialer Vermittlung  
- Carl Menger: Grundsätze der Volkswirtschaftslehre, Geldentstehung  
- John M. Keynes: A Treatise on Money, General Theory, Geld, Unsicherheit, Erwartungen  
- Friedrich A. Hayek: Denationalisation of Money, Privates Geld, Wettbewerb der Währungen  
- Niklas Luhmann: Die Wirtschaft der Gesellschaft, Geld als Kommunikationsmedium  
- Norbert Wiener: Cybernetics, Rückkopplung, Steuerung  
- Humberto Maturana, Francisco Varela: Autopoiesis and Cognition, operative Geschlossenheit, strukturelle Kopplung

---

# 7. Verification

> ## 📘 Prüfkriterien für Reviewer

- Sind die Leitfragen klar beantwortet und logisch miteinander verknüpft  
- Ist die Unterscheidung Stabilität als Parität versus Stabilität als Rückkopplung sauber herausgearbeitet  
- Sind die systemtheoretischen Begriffe korrekt übertragen, Autonomie, Rückkopplung, Homeostase, Autopoiesis  
- Ist ProjectUSD als Fallstudie präzise und konsistent zum Whitepaper beschrieben, insbesondere R, r, Vaults, Stability Pool, Redemption, Immutable Core  
- Sind die Spannungsfelder und offenen Fragen sauber benannt, ohne sie vorschnell zu glätten  
- Ist die Argumentation insgesamt im Einklang mit dem ProjectUSD Design und dessen Grenzen

Diese Studie bildet die Grundlage für eine philosophisch systematische Einordnung von ProjectUSD als Entwurf autonomen Geldes und für die Ableitung von Kriterien, an denen sich spätere technische und ökonomische Tests normativ orientieren können.
