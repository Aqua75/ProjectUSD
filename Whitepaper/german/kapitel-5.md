# Kapitel 5 - Sicherheit und Transparenz: Wenn Code das Vertrauen ersetzt

In einer Welt, in der Geldsysteme auf Versprechen gebaut sind, wählt ProjectUSD einen anderen Weg:
Sicherheit durch Mathematik, Vertrauen durch Sichtbarkeit.
Das System wurde so gestaltet, dass kein einzelner Akteur - weder Mensch, noch Behörde, noch Miner -
es kontrollieren oder korrumpieren kann.
Sicherheit bedeutet hier nicht, Risiken zu vermeiden, sondern sie so zu gestalten, dass sie vorhersehbar 
und begrenzt sind.

---

## 5.1 Das Prinzip der Autarkie

Wahre Sicherheit in DeFi beginnt dort, wo menschlicher Einfluss endet.
ProjectUSD folgt dem Grundsatz:

„Was sich nicht verändern lässt, kann auch nicht missbraucht werden.“

Der Kern des Systems - Vaults, Liquidationen, Redemption, Controller, Orakel - wird nach der 
Einführungsphase eingefroren.
Niemand kann ihn mehr stoppen, umschreiben oder anpassen.
Selbst die Governance hat nur Zugriff auf die äußere Schicht, niemals auf den inneren Code.

Dadurch entsteht ein autarkes Geldsystem, das nicht auf Vertrauen in Entwickler, Teams oder 
Institutionen angewiesen ist.
Es existiert, weil es läuft - nicht, weil jemand es erlaubt.

---

## 5.2 On-Chain-Transparenz

Jede Zahl, jeder Prozess, jede Metrik von ProjectUSD ist on-chain einsehbar:

- die aktuelle Verteilung der Vault-Besicherungen,
- der momentane Gleichgewichtspreis R und die Systemrate r,
- die Größe des Stability Pools,
- die Liquidationshistorie,
- der Zustand des Surplus-Puffers.

Nichts ist verborgen, nichts ist proprietär.
Wer wissen will, wie gesund das System ist, muss keinen Bericht lesen - er ruft einfach den Smart 
Contract ab.
Das ist buchhalterische Wahrheit in Reinform.

---

## 5.3 Schutz vor Marktmanipulation

DeFi ist kein Labor, sondern ein Schlachtfeld.
Preisfeeds, Orakel und Pools sind Angriffspunkte für Miner Extractable Value (MEV), Front-Running 
und Sandwiching.
ProjectUSD begegnet diesen Risiken mit mehrschichtiger Logik:

- Median-TWAP-Orakel:
Der Preis speist sich aus mehreren PulseChain-Paaren (z. B. ProjectUSD/PLS, 
ProjectUSD/PLSX) und bildet daraus einen Medianwert über Zeit. Kurzzeitige Pump-and
Dump-Manöver verlieren so ihren Einfluss.
- Outlier-Filter:
Paare mit zu geringer Liquidität oder statistischen Ausreißern werden automatisch 
ausgeschlossen.
- Rate-Limiter:
Die Veränderung der Systemrate r ist pro Epoche begrenzt, etwa auf 50 Basispunkte. Das 
verhindert abrupte Zinssprünge durch Marktstress.
- Reentrancy- und Governance-Capture-Schutz:
Kritische Funktionen sind voneinander isoliert, Rückrufe ausgeschlossen, Governance
Änderungen timelocked und vollständig transparent.

So entsteht ein Sicherheitsmodell, das technische wie ökonomische Angriffe abwehrt, ohne die 
Autonomie zu gefährden.

---

## 5.4 Der Surplus-Puffer - das kollektive Sicherheitsnetz

Jede Transaktion innerhalb von ProjectUSD erzeugt minimale Gebühren, die in einen Surplus-Puffer
fließen.
Dieser Puffer fungiert als kollektive Reserve, die eingesetzt werden kann, um:

- vorübergehende Verluste aus AMO-Operationen auszugleichen,
- extreme Zinsschwankungen (r) zu glätten,
- oder langfristige Sparraten zu finanzieren.

Je mehr ProjectUSD im Umlauf ist, desto größer wird der Puffer -
ein selbstverstärkender Schutzmechanismus, gespeist aus der Aktivität der Nutzer.

---

## 5.5 Governance als Wächter, nicht als Herrscher

ProjectUSD definiert Governance neu:
Sie darf koordinieren, aber nicht kontrollieren.

Nach dem Parameter-Freeze ist ihre Aufgabe auf die Pflege der Peripherie beschränkt:
neue Collateral-Typen, AMO-Parameter, oder optionale PSM-Module.
Jede Änderung erfolgt über On-Chain-Abstimmungen, mit Vorlauf und voller Transparenz.

Governance ist damit kein Machtzentrum, sondern ein Wächter des Rahmens.
Sie sorgt dafür, dass sich das System weiterentwickeln kann,
ohne jemals das zu gefährden, was es stark macht - seine Unbestechlichkeit.

## 5.6 Sicherheit als Form von Freiheit

ProjectUSD beweist, dass Sicherheit und Freiheit kein Widerspruch sind.
Ein System, das sich selbst beschränkt, befreit sich von der Willkür seiner Schöpfer.
Was einmal läuft, läuft für immer - so lange, wie PulseChain selbst existiert.

Hier liegt das wahre Versprechen:
Nicht „Code is Law“ - sondern Code ist Vertrag.
Ein Vertrag, der nicht gebrochen werden kann,
weil niemand mehr die Macht hat, ihn zu brechen.
