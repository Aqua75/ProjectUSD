# Das Herz von ProjectUSD – Eine einfache Erklärung von P, R und r

## Einleitung

Die drei Variablen **P**, **R** und **r** bilden das Fundament der Preisstabilität von ProjectUSD.  
Sie sind einfach zu verstehen, aber ökonomisch tief – und genau diese Kombination macht das System einzigartig.  

Dieser Artikel erklärt die drei Größen so klar wie möglich, ohne mathematische Überladung.  
Denn im Gegensatz zu klassischen Stablecoins benötigt ProjectUSD weder:

- einen externen USD-Peg  
- Orakel  
- Banken  
- Governance-Entscheidungen  

Die Stabilität entsteht **rein durch interne Rückkopplung**.  
Diese Rückkopplung wird durch das Zusammenspiel von **P**, **R** und **r** erzeugt.

---

## 1. P – der Marktpreis

**P** ist der tatsächliche Handelspreis von ProjectUSD auf PulseX.

- Er entsteht ausschließlich durch Angebot und Nachfrage.  
- Er kann über oder unter dem Gleichgewichtspreis **R** liegen.  
- Er verhält sich wie der Preis jedes anderen Tokens: volatil, schnell, dynamisch.

**Kurz:**  
**P = das, was der Markt gerade tut.**

Das System bewertet P nicht.  
Es misst lediglich die Abweichung zu R – und darauf reagiert der Controller.

---

## 2. R – der interne Gleichgewichtspreis

**R** ist der Wert, den das System als „fairen“ inneren Referenzpreis definiert.

Wichtig ist, was R **nicht** ist:

- R kommt nicht aus einem USD-Oracle.  
- R kommt nicht aus externen Preisen wie PLS oder PLSX.  
- R wird nicht von Teams, Governance oder Menschen festgelegt.  
- R ist nicht an den Dollar gekoppelt.  

Stattdessen ist R ein **rein interner, mathematisch abgeleiteter Wert**, der aus der Struktur des Systems entsteht.

R ist der Preis, zu dem ProjectUSD jederzeit **intern in PLS eingelöst** werden kann.  
Diese Einlösbarkeit erzeugt einen natürlichen Wertanker und sorgt dafür, dass der Marktpreis P nicht langfristig vom Systemwert abweichen kann.

---

## 3. Die Preisabweichung ε

Zwischen P und R besteht fast immer eine kleine Differenz.

Diese **relative** Abweichung nennen wir:

**ε = (P − R) / R**

- ε > 0 → P liegt relativ über R (Überbewertung)  
- ε < 0 → P liegt relativ unter R (Unterbewertung)  

Die Größe von ε bestimmt, wie stark der Controller r angepasst wird.

---

## 4. r – die Systemrate (Regelkraft)

**r** ist die wichtigste Variable im ganzen System.  
Sie ist **kein Zins**, **keine Belohnung**, **keine Inflation** und **keine Governance-Variable**.

r ist die **Regelkraft**, die P immer wieder zum Gleichgewichtspreis R zurückzieht.

### Wenn P > R  
- r steigt  
- Minting wird teurer  
- Halten wird weniger attraktiv  
- Arbitrage und Angebot kühlen den Preis ab  
→ **P bewegt sich nach unten Richtung R**

### Wenn P < R  
- r sinkt  
- Halten wird attraktiver  
- Arbitrage wird profitabel  
- die Nachfrage steigt  
→ **P bewegt sich nach oben Richtung R**

**Kurz:**  
**r ist die automatische Gegenkraft, die jede Abweichung korrigiert.**

---

## 5. Warum R nicht völlig fix ist – aber extrem stabil

R ist kein absolut fixer Wert.  
Er kann sich verändern – aber:

- nur langsam  
- nie sprunghaft  
- nie abhängig vom externen Markt  
- ausschließlich intern begründet  

Der Grund: Schulden, Sicherheiten und Redemptions sind dynamisch.  
Damit das System langfristig im Gleichgewicht bleibt, darf sich auch R sanft anpassen.

Man kann sich R vorstellen wie einen **langsam wandernden Referenzpunkt**, während P der schnelle Marktpreis ist.

---

## 6. Wie R tatsächlich gebildet wird

R entsteht aus den **inneren Zuständen des Systems**, insbesondere:

- der Einlösungslogik (Redemption-Engine)  
- den Sicherheiten und Schulden aller Vaults  
- Liquidationsdynamik  
- systeminterner Drift  
- Schuldenabbau und Surplus-Puffer-Struktur  

Das macht R zu einem **buchhalterisch korrekten, internen Fair Value**, der nichts mit externen Preisen zu tun hat.

R ist der Wert, zu dem das System ProjectUSD immer ausgeben kann – garantiert durch Mathematik, nicht durch Versprechen.

---

## 7. R und interne Kaufkraft

R stabilisiert nicht nur den inneren Wert von ProjectUSD –  
er stabilisiert auch die **Kaufkraft des Tokens innerhalb der PulseChain-Ökonomie**.

1 ProjectUSD entspricht immer einer **konstanten Einheit wirtschaftlicher Aktivität** innerhalb des Systems.  
Externe Preisänderungen spielen dabei keine Rolle.

Eine ausführliche Analyse der internen Kaufkraft findest du im eigenen Artikel  
[„ProjectUSD – und das Geheimnis der Kaufkraft“](https://github.com/Aqua75/ProjectUSD/blob/main/Articles/projectusd-and-purchasing-power/projectusd-and-purchasing-power.de.md).

---

## 8. Zusammenfassung

- **P** ist volatil und bildet den Markt ab.  
- **R** ist der interne Gleichgewichtspreis – stabil, träge und systemisch.  
- **r** ist die automatische Regelkraft, die P immer wieder zu R zurückführt.  

Deshalb funktioniert ProjectUSD:

- ohne Peg  
- ohne Orakel  
- ohne Governance  
- ohne USD  
- rein algorithmisch  
- vollständig on-chain  

**ProjectUSD stabilisiert sich selbst, weil r kontinuierlich P zurück in Richtung R führt.**  
So entsteht ein autonomes Geldsystem, das auf PulseChain eine stabile interne Ökonomie ermöglicht.

