# Kapitel 5 - Sicherheit und Transparenz: Wenn Code das Vertrauen ersetzt

In einer Welt, in der Geldsysteme auf Versprechen gebaut sind, wählt ProjectUSD einen anderen Weg:<br>
Sicherheit durch Mathematik, Vertrauen durch Sichtbarkeit.

Das System wurde so gestaltet, dass kein einzelner Akteur - weder Mensch, noch Behörde, noch Miner -<br>
es kontrollieren oder korrumpieren kann.<br>
Sicherheit bedeutet hier nicht, Risiken zu vermeiden, sondern sie so zu gestalten, dass sie vorhersehbar<br> 
und begrenzt sind.

---

## 5.1 Das Prinzip der Autarkie

Wahre Sicherheit in DeFi beginnt dort, wo menschlicher Einfluss endet.<br>
ProjectUSD folgt dem Grundsatz:

„Was sich nicht verändern lässt, kann auch nicht missbraucht werden.“

Der Kern des Systems - Vaults, Liquidationen, Redemption, Controller, Orakel - wird nach der <br>
Einführungsphase eingefroren.<br>
Niemand kann ihn mehr stoppen, umschreiben oder anpassen.<br>
Selbst die Governance hat nur Zugriff auf die äußere Schicht, niemals auf den inneren Code.

Dadurch entsteht ein autarkes Geldsystem, das nicht auf Vertrauen in Entwickler, Teams oder <br>
Institutionen angewiesen ist.<br>
Es existiert, weil es läuft - nicht, weil jemand es erlaubt.

---

## 5.2 On-Chain-Transparenz

Jede Zahl, jeder Prozess, jede Metrik von ProjectUSD ist on-chain einsehbar:

- die aktuelle Verteilung der Vault-Besicherungen,<br>
- der momentane Gleichgewichtspreis R und die Systemrate r,<br>
- die Größe des Stability Pools,<br>
- die Liquidationshistorie,<br>
- der Zustand des Surplus-Puffers.

Nichts ist verborgen, nichts ist proprietär.<br>
Wer wissen will, wie gesund das System ist, muss keinen Bericht lesen - er ruft einfach den Smart <br>
Contract ab.<br>
Das ist buchhalterische Wahrheit in Reinform.

---

## 5.3 Schutz vor Marktmanipulation

DeFi ist kein Labor, sondern ein Schlachtfeld.<br>
Preisfeeds, Orakel und Pools sind Angriffspunkte für Miner Extractable Value (MEV), Front-Running<br> 
und Sandwiching.<br>
ProjectUSD begegnet diesen Risiken mit mehrschichtiger Logik:

- Median-TWAP-Orakel:<br>
Der Preis speist sich aus mehreren PulseChain-Paaren (z. B. ProjectUSD/PLS, <br>
ProjectUSD/PLSX) und bildet daraus einen Medianwert über Zeit. Kurzzeitige Pump-and<br>
Dump-Manöver verlieren so ihren Einfluss.<br>
- Outlier-Filter:<br>
Paare mit zu geringer Liquidität oder statistischen Ausreißern werden automatisch<br> 
ausgeschlossen.<br>
- Rate-Limiter:<br>
Die Veränderung der Systemrate r ist pro Epoche begrenzt, etwa auf 50 Basispunkte. Das <br>
verhindert abrupte Zinssprünge durch Marktstress.<br>
- Reentrancy- und Governance-Capture-Schutz:<br>
Kritische Funktionen sind voneinander isoliert, Rückrufe ausgeschlossen, Governance<br>
Änderungen timelocked und vollständig transparent.<br>

So entsteht ein Sicherheitsmodell, das technische wie ökonomische Angriffe abwehrt, ohne die <br>
Autonomie zu gefährden.

---

## 5.4 Der Surplus-Puffer - das kollektive Sicherheitsnetz

Jede Transaktion innerhalb von ProjectUSD erzeugt minimale Gebühren, die in einen Surplus-Puffer<br>
fließen.<br>
Dieser Puffer fungiert als kollektive Reserve, die eingesetzt werden kann, um:

- vorübergehende Verluste aus AMO-Operationen auszugleichen,<br>
- extreme Zinsschwankungen (r) zu glätten,<br>
- oder langfristige Sparraten zu finanzieren.

Je mehr ProjectUSD im Umlauf ist, desto größer wird der Puffer -<br>
ein selbstverstärkender Schutzmechanismus, gespeist aus der Aktivität der Nutzer.

---

## 5.5 Governance als Wächter, nicht als Herrscher

ProjectUSD definiert Governance neu:<br>
Sie darf koordinieren, aber nicht kontrollieren.

Nach dem Parameter-Freeze ist ihre Aufgabe auf die Pflege der Peripherie beschränkt:<br>
neue Collateral-Typen, AMO-Parameter, oder optionale PSM-Module.<br>
Jede Änderung erfolgt über On-Chain-Abstimmungen, mit Vorlauf und voller Transparenz.

Governance ist damit kein Machtzentrum, sondern ein Wächter des Rahmens.<br>
Sie sorgt dafür, dass sich das System weiterentwickeln kann,<br>
ohne jemals das zu gefährden, was es stark macht - seine Unbestechlichkeit.

## 5.6 Sicherheit als Form von Freiheit

ProjectUSD beweist, dass Sicherheit und Freiheit kein Widerspruch sind.<br>
Ein System, das sich selbst beschränkt, befreit sich von der Willkür seiner Schöpfer.<br>
Was einmal läuft, läuft für immer - so lange, wie PulseChain selbst existiert.

Hier liegt das wahre Versprechen:<br>
Nicht „Code is Law“ - sondern Code ist Vertrag.<br>
Ein Vertrag, der nicht gebrochen werden kann,<br>
weil niemand mehr die Macht hat, ihn zu brechen.
