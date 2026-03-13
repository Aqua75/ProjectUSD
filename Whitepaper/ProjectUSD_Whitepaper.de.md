# ProjectUSD
## Ein autonomes Geldsystem für PulseChain

### Whitepaper V2.1 – Vision und Architektur einer selbstregulierenden Blockchain-Ökonomie

---

## Zusammenfassung

ProjectUSD ist ein vollständig on-chain operierendes, algorithmisches Geldsystem, das Preisstabilität ohne Orakel, Banken oder zentrale Eingriffe erreicht.

Es verbindet ökonomische Rückkopplung, unveränderlichen Code und ein duales System aus Vaults, Stability Pool und Redemption-Mechanik, um auf PulseChain eine echte, autarke DeFi-Ökonomie zu schaffen.

Dieses Dokument ist kein Produkt-Launch, sondern eine Vision: ein Staffelstab – von der Idee zum Code, von der Theorie zur Umsetzung, vom Vertrauen zur Transparenz.

**Projektstatus**

Konzeptionelle Blaupause  
(offen für Entwickler, Forscher und Kapitalgeber)

**Autoren**

Aqua75  
PulseChain Community Initiative

**Version**

Whitepaper V2.1 – November 2025

**Lizenz**

CC BY-NC-SA 4.0 – Creative Commons Attribution-NonCommercial-ShareAlike

---

# Kapitel 1 – Das Versprechen eines autonomen Geldes

Es gibt Momente in der Geschichte, in denen eine Idee größer ist als ihre Urheber.

ProjectUSD ist genau das: kein fertiges Produkt, kein Startup, keine Firma – sondern eine Vision, geboren aus dem Wunsch, Geld wieder auf seinen Ursprung zurückzuführen: mathematische Ordnung, nicht menschliche Willkür.

Die heutige DeFi-Welt ruht auf einem Fundament, das längst Risse zeigt.

Stablecoins – einst Sinnbild für Stabilität – sind zu Stellvertretern zentraler Macht geworden. Sie hängen an Banken, an Firmen, an rechtlichen Zusicherungen, die im Zweifel widerrufen werden können.

Ihre Stabilität ist geliehen, nicht verdient. Und sobald die Institution, die sie stützt, wankt, wankt das ganze System.

Doch PulseChain zeigt: Es geht auch anders.

Sie beweist, dass eine neue Kette entstehen kann, ohne zentrale Kontrolle, ohne Erlaubnis.

Was aber fehlt, ist das Geld, das dieser Philosophie entspricht – ein Wertanker, der ebenso autonom funktioniert wie die Chain selbst.

Hier beginnt ProjectUSD.

Ein Konzept, das beweisen will, dass Stabilität kein Vertrauen braucht. Dass Preisgleichgewicht entstehen kann, wenn ökonomische Rückkopplung die Rolle menschlicher Kontrolle ersetzt.

Und dass ein Stablecoin nicht auf Dollarreserven, sondern auf Code beruhen kann.

ProjectUSD ist ein Vorschlag – eine Blaupause.

Sein Ziel ist nicht, ein fertiges Protokoll vorzustellen, sondern eine Idee so klar zu formulieren, dass andere sie aufgreifen, erweitern und verwirklichen können.

Dieses Whitepaper ist deshalb ein Staffelstab:

von der Vision zur Umsetzung  
von Theorie zu Code  
von Gedanke zu Realität

Es richtet sich an jene, die in PulseChain mehr sehen als nur einen neuen Markt:

an Entwickler, die an das Prinzip der Unveränderlichkeit glauben,  
und an Geldgeber, die verstehen, dass echte Stabilität ein seltenes Gut ist – eines, das man nicht kaufen, sondern nur bauen kann.

Wenn dieses Dokument eines beweisen soll, dann dies:

Ein autonomes, selbstregulierendes Geldsystem ist möglich.  
Und es kann hier, auf PulseChain, entstehen.

---

# Kapitel 2 – Was ist ProjectUSD?

ProjectUSD ist kein weiterer Stablecoin im endlosen Strom neuer Token.

Es ist der Versuch, Geld neu zu definieren – ohne Orakel, ohne Banken, ohne Vertrauen in Menschen oder Institutionen.

Ein System, das seine eigene Balance findet, weil es seine eigenen Regeln kennt.

Der zentrale Gedanke ist einfach:

Stabilität kann entstehen, wenn ein System auf sich selbst reagiert.

Wenn Angebot und Nachfrage, Schulden und Sparen, Expansion und Kontraktion in einem geschlossenen Kreislauf miteinander kommunizieren – rein mathematisch, ohne externe Datenquelle.

Im Herzen dieses Systems steht der interne Gleichgewichtspreis **R**.

Er ist der innere Kompass, an dem sich der Marktpreis **P** orientiert.

Weicht der tatsächliche Marktpreis auf den dezentralen Börsen ab, reagiert das System automatisch über eine variable Größe **r** – die kombinierte Schuld- und Sparerate.

Sie fungiert als Puls der Ökonomie:

Steigt **r**, wird das Prägen neuer Token unattraktiver.  
Sinkt **r**, lohnt es sich, ProjectUSD zu halten oder zu erzeugen.

So kehrt der Preis immer wieder zum inneren Anker **R** zurück.

Dieses Gleichgewicht entsteht ohne Orakel, ohne dass jemand von außen sagt, was „ein Dollar“ wert sein soll.

Der Wert ergibt sich aus der Interaktion der Teilnehmer:

Vaults hinterlegen Sicherheiten.  
Stability Pools absorbieren schwache Positionen.  
Die Redemption Engine ermöglicht jederzeitige Einlösung.

Drei einfache Komponenten, ein geschlossener Kreislauf:

Prägung → Umlauf → Einlösung → Tilgung → neue Prägung

Alles geschieht on-chain, überprüfbar und autonom.

ProjectUSD ist damit nicht bloß ein technisches Design, sondern ein ökonomisches Ökosystem.

Es verhält sich wie eine Mini-Zentralbank – nur ohne Menschen, ohne Politik und ohne Machtstrukturen.

Statt Versprechen gibt es Code.  
Statt Vertrauen gibt es Transparenz.

Und statt Zwangsbindung an den US-Dollar gibt es einen inneren, algorithmisch definierten Maßstab.

Das Ergebnis ist ein autarkes Gleichgewichtssystem, das seine Stabilität aus Dynamik gewinnt – wie ein Planet, der nicht stabil bleibt, weil er stillsteht, sondern weil er im perfekten Umlauf bleibt.

---

# Kapitel 3 – Das ökonomische Herz: Wie ProjectUSD Stabilität erzeugt

Jede Ökonomie braucht ein Herz – etwas, das schlägt, reagiert und die Balance hält.

Bei ProjectUSD ist dieses Herz der **Controller**.

Er ist kein Mensch, kein Governance-Gremium und kein externer Algorithmus, der auf Preisfeeds reagiert.  
Er ist ein mathematisches Regelwerk, das die Dynamik des Systems steuert.

Seine Aufgabe ist einfach zu beschreiben, aber tief in ihrer Wirkung:

Er sorgt dafür, dass der Marktpreis **P** des Stablecoins um den inneren Gleichgewichtspreis **R** pendelt – nicht durch starre Bindung, sondern durch Rückkopplung.

## Die Rückkopplung zwischen Preis und Rate

Wenn der Marktpreis über **R** steigt, signalisiert das ein Überangebot an Nachfrage.

ProjectUSD ist zu teuer geworden – das System muss abkühlen.

Der Controller erhöht die variable Rate **r**, die als kombinierte Zinsgröße sowohl für Schuldner als auch für Sparer gilt.

Für Schuldner:  
Das Prägen neuer ProjectUSD-Token wird teurer.

Für Sparer:  
Das Halten von ProjectUSD wird weniger attraktiv.

Die Folge:

Das Angebot wächst langsamer.  
Die Nachfrage sinkt.  
Der Preis kehrt allmählich zu **R** zurück.

Wenn der Marktpreis unter **R** fällt, geschieht das Gegenteil:

ProjectUSD ist zu billig – das System ist unterkühlt.

Der Controller senkt **r**, manchmal bis in den negativen Bereich.

Dann lohnt es sich, ProjectUSD zu halten oder zu erzeugen.

Arbitrageure kaufen unterbewertete Tokens auf.  
Der Preis steigt.  
Das Gleichgewicht kehrt zurück.

So entsteht ein digitaler Zinsmechanismus.

Vergleichbar mit geldpolitischer Steuerung – nur vollständig automatisch.

## Mathematische Einfachheit, ökonomische Tiefe

Die Logik dahinter lässt sich als Regel formulieren:

Die Preisabweichung **ε** misst, wie stark der Marktpreis vom internen Gleichgewicht abweicht.

Der Controller übersetzt diese Abweichung in eine Anpassung der Rate **r**.

Je größer die Abweichung, desto stärker reagiert das System – jedoch innerhalb klarer Grenzen, um Überreaktionen zu vermeiden.

Stabilität entsteht nicht durch Fixierung.

Sondern durch Bewegung.

Nicht durch Kontrolle.

Sondern durch Resonanz.

## Der Selbstregulierungseffekt

Das System „atmet“.

Jede Preisabweichung löst eine Gegenkraft aus.

Je größer der Ausschlag, desto stärker die Rückstellung.

So pendelt sich das System in einem dynamischen Gleichgewicht ein.

Nie vollkommen starr.  
Nie vollkommen chaotisch.

Ein Geldsystem, das sich selbst stabilisiert.

## Warum das Vertrauen ersetzt

In traditionellen Stablecoins garantiert eine Firma:

„1 Token = 1 USD“.

Dieses Versprechen hängt an Bankkonten, Jurisdiktionen und Vertrauen.

Bei ProjectUSD gibt es kein solches Versprechen.

Nur Code.

Code, der das Verhalten der Marktteilnehmer aufeinander abstimmt.

Vertrauen wird durch Verlässlichkeit ersetzt.

Jeder kann die Mechanik prüfen.

Jede Variable beobachten.

Jede Anpassung nachvollziehen.

Das ist Stabilität durch Transparenz.

---

# Kapitel 4 – Die Architektur: Aufbau eines unbestechlichen Systems

Ein System kann nur so stark sein wie seine Architektur.

Bei ProjectUSD wurde jede Komponente so entworfen, dass sie nicht korrumpierbar ist – weder durch Menschen, noch durch externe Daten, noch durch Governance-Mehrheiten.

Alles existiert **on-chain**, öffentlich überprüfbar und ohne Eingriffsrechte.

## Vaults – das Fundament der Geldschöpfung

Vaults sind persönliche Smart-Contract-Tresore.

Nutzer hinterlegen dort PulseChain-Assets – hauptsächlich **PLS** – als Sicherheit.

Auf Basis dieser Sicherheiten prägen sie neue ProjectUSD-Token.

Der maximal mögliche Betrag hängt vom **Collateral Ratio (CR)** ab.

Typischerweise etwa **170 % oder höher**.

Fällt der Wert der Sicherheiten unter die Mindestgrenze, wird der Vault automatisch liquidiert.

Dieser Prozess geschieht vollständig automatisch.

Vaults sind die Geburtsorte des Geldes im System.

Jeder kann sie öffnen.  
Jeder kann sie schließen.

Alles geschieht durch Code.

## Der Stability Pool – Sicherheit durch Schwarmverhalten

Der Stability Pool ist das kollektive Sicherheitsnetz des Systems.

Nutzer hinterlegen freiwillig ProjectUSD, um Zinsen und Liquidationsboni zu verdienen.

Wenn ein Vault unterbesichert ist, wird seine Schuld automatisch mit Mitteln aus dem Stability Pool beglichen.

Im Gegenzug erhalten die Teilnehmer die Sicherheiten.

So verschwinden schwache Positionen.

Und das System stabilisiert sich selbst.

## Die Redemption Engine – der innere Preisanker

Die Redemption Engine erlaubt es jedem Nutzer, ProjectUSD zum internen Gleichgewichtspreis **R** gegen **PLS** einzulösen.

Dabei werden zuerst die am schwächsten besicherten Vaults reduziert.

Das schafft eine natürliche Marktordnung.

Überdehnte Schulden werden automatisch abgebaut.

Arbitrageure gleichen Preisabweichungen aus.

Der Preis bleibt dauerhaft an **R** verankert.

## Immutable Core

Im Zentrum von ProjectUSD steht der **Immutable Core**.

Er enthält:

Vault-Logik  
Liquidationen  
Redemption Engine  
Controller  
Preislogik  
Systemparameter

Nach dem **Freeze Event** wird dieser Kern dauerhaft eingefroren.

Von diesem Moment an kann niemand ihn mehr verändern.

Nicht Entwickler.  
Nicht Governance.  
Nicht die Community.

ProjectUSD wird zu einem autonomen System.

## Peripherie – kontrollierte Flexibilität

Um Innovation zu ermöglichen, besitzt ProjectUSD eine Peripherieschicht.

Hier können Module erweitert werden:

neue Collateral-Adapter  
PSM-Module  
AMO-Module  
Analytics-Schnittstellen

Alle Änderungen erfolgen über Timelocks und On-Chain-Abstimmungen.

Der Kern bleibt unverändert.

## Ein System ohne Stecker

Es gibt keinen Admin-Key.

Keinen Pause-Button.

Keinen Notfallzugang.

ProjectUSD kann nicht gestoppt werden.

Es gehört niemandem.

Und genau deshalb allen.

---

# Kapitel 5 – Sicherheit und Transparenz

ProjectUSD ersetzt Vertrauen durch Mathematik.

Das System wurde so entworfen, dass kein einzelner Akteur es kontrollieren kann.

## Autarkie

Der Kern des Systems wird nach der Einführungsphase eingefroren.

Niemand kann ihn mehr verändern.

Das System existiert, weil es läuft.

Nicht, weil jemand es erlaubt.

## On-Chain Transparenz

Alle Daten sind öffentlich einsehbar:

Vault-Verteilungen  
Preis R  
Rate r  
Stability Pool Größe  
Liquidationen  
Surplus-Puffer

Jeder kann den Zustand des Systems prüfen.

## Schutz vor Manipulation

ProjectUSD verwendet:

Median-TWAP-Orakel  
Outlier-Filter  
Rate-Limiter  
Reentrancy-Schutz

Diese Mechanismen schützen vor:

MEV  
Front-Running  
Preis-Manipulation

## Surplus-Puffer

Alle Transaktionen erzeugen Gebühren.

Diese fließen in einen Surplus-Puffer.

Der Puffer kann genutzt werden, um:

Verluste auszugleichen  
Zinsbewegungen zu glätten  
Sparraten zu finanzieren

## Governance

Governance darf koordinieren – aber nicht kontrollieren.

Sie verwaltet nur die Peripherie.

Der Kern bleibt unangreifbar.

---

# Kapitel 6 – Roadmap

ProjectUSD wird schrittweise eingeführt.

## Phase 1 – Guarded Launch

kleine Schuldensummen  
keine AMO  
keine PSM  
intensive Beobachtung

## Phase 2 – Parameter Freeze

Sobald Stabilität nachgewiesen ist:

Controller fixieren  
Collateral Ratio fixieren  
Redemption fixieren  
Core einfrieren

## Phase 3 – PSM light

Optionaler Stabilitätskorb.

Strenge Limits.

## Phase 4 – AMO

Algorithmic Market Operations zur Liquiditätssteuerung.

## Phase 5 – Ökosystem Integration

DEX Paare  
Lending  
Derivate  
Payments

## Phase 6 – Langfristige Evolution

Neue Collaterals  
DSR aus Surplus  
AMO Governance

---

# Kapitel 7 – Anwendung und Nutzen

ProjectUSD ermöglicht PulseChain eine eigene Währung.

Nutzen:

DEX Liquidität  
Lending  
Derivate  
Zahlungen  
Yield Strategien

Es ersetzt Vertrauen durch Transparenz.

---

# Kapitel 8 – Risiken

ProjectUSD kann Stabilität erzeugen.

Aber keine Wunder.

Risiken:

Smart Contract Bugs  
MEV Manipulation  
Collateral Volatilität  
Liquiditätsverschiebungen  
psychologische Marktreaktionen

Das System macht Risiken sichtbar.

---

# Kapitel 9 – Philosophie

ProjectUSD ist mehr als ein Stablecoin.

Es ist eine Idee.

Stabilität aus Logik.

Vertrauen aus Transparenz.

Ein Geldsystem ohne Kontrolle.

---

# Glossar

**R – Gleichgewichtspreis**

Interner Referenzwert des Systems.

**r – Systemrate**

Zinsmechanismus des Controllers.

**Vault**

Smart Contract Tresor zur Geldschöpfung.

**Stability Pool**

Liquidationspool.

**Redemption Engine**

Preisanker.

**AMO**

Algorithmic Market Operations.

**PSM**

Peg Stability Module.

**Surplus Puffer**

Reservepool des Systems.

**Immutable Core**

Unveränderlicher Systemkern.

**Freeze Event**

Moment des endgültigen Einfrierens des Codes.

**Controller**

Steuert das Gleichgewicht zwischen Marktpreis P und internem Preis R.
