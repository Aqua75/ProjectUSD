# Study 03 – Die Redemption-Engine als innerer Preisanker von ProjectUSD
*Wissenschaftliche Analyse der internen Wertreferenz, der Arbitrage-Dynamik und der Rolle von Redemption im Gleichgewichtssystem*  
*(Level-3 Research Format)*

---

## Abstract

Die Redemption-Engine ist das zentrale Element, das dem ProjectUSD-System eine interne Wertreferenz verleiht. Während der Marktpreis P durch Angebot und Nachfrage bestimmt wird, definiert die Redemption-Engine den Gleichgewichtspreis R und stellt sicher, dass:

- ProjectUSD immer einen eindeutig definierten internen Wert besitzt,  
- Arbitrage das System jederzeit in Richtung R zurückzieht,  
- P langfristig nicht von R abweichen kann, ohne dass ökonomische Kräfte aktiv werden.

Diese Studie erläutert die Mechanik der Redemption, ihr Zusammenspiel mit dem Oracle, die arbitragegetriebene Rückführung von P → R und ihre Rolle in Stressszenarien. Die Analyse zeigt, dass Redemption nicht lediglich eine Funktion ist, sondern das ökonomische Fundament, das ProjectUSD von externen Geldsystemen und Fiat-abhängigen Stablecoins unterscheidet.

---

# 1. Einleitung – Warum Redemption der innere Preisanker ist

In ProjectUSD gibt es **keine Bindung an Fiat**, **keine Orakel zu externen Währungen** und **keine Governance**, die den Wert festlegt.  

Stattdessen entsteht der Wert von ProjectUSD durch:

- den Gleichgewichtspreis **R**,  
- die Redemption-Engine,  
- die Arbitrage,  
- die marktbasierte Umsetzung dieser Mechanik.

Redemption stellt die Frage:

> *„Wie viel PLS entspricht 1 ProjectUSD im System selbst?“*

Damit fungiert R als interner Maßstab, unabhängig von externen Märkten.

---

# 2. Technische Grundlagen der Redemption-Engine

## 2.1 Definition des Gleichgewichtspreises R

> ## 📘 Definition – Redemption-Preis \(R\)
> Der Gleichgewichtspreis R beschreibt den internen Wert, zu dem 1 ProjectUSD durch Redemption gegen PLS eingetauscht werden kann.

R ist nicht von Fiat, nicht von USD-Orakeln und nicht von Governance abhängig.

---

## 2.2 Grundprinzip der Redemption

Wenn ein Nutzer ProjectUSD einlöst:

1. Das System wählt die **schwächsten Vaults** (niedrigste CR).  
2. Die dort hinterlegte Menge PLS wird an den Redeemer ausgezahlt.  
3. Die Schuld des Vaults wird reduziert bzw. gelöscht.  
4. Der Vault wird dadurch sicherer oder geschlossen.  
5. Der ProjectUSD-Supply sinkt.

Wichtig:

- Es findet **kein Verkauf auf der DEX** statt.  
- Redemption erzeugt **keinen Price Impact** auf PLS.  
- Redemption ist rein systemintern.

---

## 2.3 Auswirkungen auf das System

Redemption führt zu:

- höherer Gesamtsicherheit  
- Zerstörung von ProjectUSD-Supply  
- Bereinigung schwacher Vaults  
- systeminterner Reallokation von Collateral  
- einem **klar definierten Wertmaßstab**

---

# 3. Arbitrage-Mechanik zwischen Marktpreis P und Gleichgewichtspreis R

Redemption schafft ein ökonomisches Gefälle, das Arbitrageure ausnutzen.  
Die Dynamik ist einfach und deterministisch:

---

## 3.1 Fall 1 – P < R (Unterbewertung)

Wenn ProjectUSD an der DEX unterhalb des internen Wertes gehandelt wird:

- Arbitrageure kaufen ProjectUSD günstig ein  
- lösen ihn durch Redemption ein  
- erhalten PLS im Wert von R  
- realisieren einen Gewinn  
- P steigt wieder in Richtung R  
- der Supply sinkt

Unterbewertung kann deshalb **nicht dauerhaft bestehen**, solange Redemption aktiv ist.

---

## 3.2 Fall 2 – P > R (Überbewertung)

Wenn ProjectUSD teurer gehandelt wird als R:

- Nutzer prägen neue ProjectUSD  
- verkaufen ihn über dem Gleichgewicht  
- arbitragebedingter Verkaufsdruck senkt P  
- nach dem Verkauf wird die Schuld später getilgt  
- P fällt in Richtung R

Auch Überbewertung wird durch Arbitrage abgebaut.

---

## 3.3 Ergebnis: R wirkt wie ein Magnet

Der Gleichgewichtspreis R:

- ist der interne Wertanker  
- zieht P durch Arbitrage konstant an  
- definiert die langfristige Wertstabilität  
- wirkt unabhängig von externen Marktbedingungen

R ist kein Vorschlag – R ist der *ökonomische Pflichtpunkt*, an dem der Markt sich ausrichtet.

---

# 4. Rolle des Oracles

## 4.1 Oracle-Input für Redemption

Das Oracle liefert:

- Median-TWAP-Preise für PLS  
- geglättete Daten  
- Schutz gegen Manipulation  
- STALE-Modus bei Illiquidität

Redemption selbst verwendet die Oracle-Daten **nicht**, aber:

- der relative Wert zwischen Collateral und Schuld  
- die CR-Bewertung  
- die Auswahl der Vaults  

hängen vom Oracle ab.

---

## 4.2 Oracle-Filterung schützt vor Manipulation

Wenn ein Pool illiquide oder manipuliert ist:

- der Oracle-Filter ignoriert ihn  
- STALE-Preise werden blockiert  
- Redemption bleibt korrekt  
- das Gleichgewicht R bleibt sauber definiert

Redemption ist deshalb immun gegen kurzfristige Preismanipulation.

---

# 5. Rückführung des Marktpreises – mathematische Grundlage

Die zentrale Frage lautet:

> *Wie führt Redemption dazu, dass P langfristig immer gegen R konvergiert?*

---

## 5.1 Relative Abweichung εₜ

> ## 📘 Definition – Relative Preisabweichung
> $$
> \varepsilon_t = \frac{P_t - R_t}{R_t}
> $$

Eine positive Abweichung bedeutet Überbewertung, eine negative Unterbewertung.

---

## 5.2 Arbitrage-induzierte Mean Reversion

Redemption erzeugt:

- Nachfrage bei P < R  
- Angebotsdruck bei P > R  
- Rückführung in Richtung R  

Die Rückführung erfolgt monoton, da Arbitrage niemals gegen R arbeiten kann.

---

## 5.3 Stabilität durch Supply-Reduktion

Redemption reduziert den ProjectUSD-Supply.  
Dadurch steigt die durchschnittliche Collateral-Deckung im System:

- stabileres Risiko­profil  
- bessere Absicherung  
- stärkere Reversion

---

# 6. Redemption in Stressszenarien

## 6.1 Starke Preisabfälle

Bei Crashs:

- viele Vaults verlieren CR  
- Redemption reduziert Schuld bei schwachen Vaults  
- Systemdeckung steigt trotz Stress  
- Arbitrage bleibt aktiv  
- P wird stabilisiert

---

## 6.2 Oracle-Ausfälle

Wenn Oracle-Preise ausfallen:

- Redemption wählt die schwächsten Vaults nach letzter gültiger Information  
- STALE-Modus schützt vor Manipulation  
- keine falsche Collateralbewertung  
- Arbitrage setzt ein, sobald Oracle wieder aktiv ist

---

## 6.3 Gas-Spitzen

Redemption-Transaktionen bleiben durch:

- priorisierte Logik  
- begrenzte Komplexität  
- fehlende externe Abhängigkeiten  

auch bei Gas-Spitzen funktionsfähig.

---

# 7. Redemption als spieltheoretischer Mechanismus

Redemption erzeugt ein Spiel:

- Arbitrage gewinnt, wenn P ≠ R  
- Vault-Nutzer verlieren, wenn sie zu stark hebeln  
- Stability-Pool-Teilnehmer profitieren von Systemschwäche  
- das System gewinnt an Stabilität

Der Gleichgewichtspunkt:

> *Arbitrage verhindert dauerhafte Abweichungen von R.*

---

# 8. Schlussfolgerung

Die Redemption-Engine ist das monetäre Fundament von ProjectUSD.  
Sie erzeugt:

- einen internen Wertmaßstab  
- Arbitrage-getriebene Rückführung  
- Supply-Reduktion  
- robuste Systemstabilität  
- Stressresilienz  
- ein selbstregulierendes Gleichgewicht

Ohne Redemption gäbe es keinen internen Preisanker – mit ihr entsteht der Kern der ökonomischen Stabilität von ProjectUSD.

---

# 9. Verification

> ## 📘 Prüfkriterien für Reviewer
- Ist der Gleichgewichtspreis R korrekt definiert und verwendet?  
- Sind Arbitragepfade konsistent beschrieben?  
- Wird an keiner Stelle externe Fiat-Referenz benötigt?  
- Bleibt der Mechanismus auch in Stressfällen korrekt?  
- Ist die Rückführung P → R logisch und vollständig dargestellt?  

Dieses Dokument bildet die Grundlage für weitere Studien zu Arbitrage, Marktmechanik und Interaktion zwischen Redemption, Controller und Stability Pool.
