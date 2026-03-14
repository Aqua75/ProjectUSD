[← Kapitel 3](03-kapitel-3.md) | [Inhaltsverzeichnis](README.md) | [Kapitel 5 →](05-kapitel-5.md)

---

# Kapitel 4 - Die Architektur: Aufbau eines unbestechlichen Systems

Ein System kann nur so stark sein wie seine Architektur.<br>
Bei ProjectUSD wurde jede Komponente so entworfen, dass sie **nicht korrumpierbar** ist - weder durch<br> 
Menschen, noch durch externe Daten, noch durch Governance-Mehrheiten.<br>
Alles, was das System am Leben hält, existiert **auf-Chain**, öffentlich überprüfbar und ohne
Eingriffsrechte.

---

## 4.1 Vaults - das Fundament der Geldschöpfung

Vaults sind persönliche Tresore, in denen Nutzer native PulseChain-Assets - vor allem PLS - als<br>
Sicherheit hinterlegen.<br>
Auf Basis dieser Sicherheiten prägen sie neue ProjectUSD-Token.<br>
Der maximal mögliche Betrag hängt vom festgelegten **Collateral-Ratio** (CR) ab; typischerweise 170 %<br>
oder mehr.

Fällt der Wert der Sicherheiten unter die Mindestgrenze, wird der Vault automatisch liquidiert.<br>
Kein Mensch, kein Team und keine Behörde kann diesen Prozess stoppen oder bevorzugen - alles <br>
geschieht nach derselben Regel.

Vaults sind damit die **Geburtsorte** des Geldes im System.<br>
Jeder kann sie öffnen, jeder kann sie schließen, und jede Handlung ist durch Code bestimmt.

---

## 4.2 Der Stability Pool - Sicherheit durch Schwarmverhalten

Der Stability Pool ist das kollektive Sicherheitsnetz von ProjectUSD.<br>
Hier hinterlegen Nutzer freiwillig ProjectUSD-Token, um Zinsen und Liquidationsboni zu verdienen.

Wenn ein Vault unter die Sicherheitsgrenze fällt, werden dessen Schulden automatisch mit Mitteln aus<br>
dem Stability Pool beglichen.<br>
Im Gegenzug erhalten die Pool-Teilnehmer die PLS-Sicherheiten - mit einem kleinen Bonus - und der<br>
überschüssige ProjectUSD-Supply wird vernichtet.

Das Ergebnis:

- schwache Positionen verschwinden,<br>
- starke Hände erhalten zusätzliche Sicherheiten,<br>
- und das gesamte System wird stabiler.

So entsteht ein selbstheilender Kreislauf, der Marktstress absorbiert, statt ihn zu verstärken.

---

## 4.3 Die Redemption-Engine - der innere Preisanker

Der wichtigste Stabilitätsmechanismus ist die **Redemption-Engine**.<br>
Sie erlaubt es jedem Nutzer, ProjectUSD zum aktuellen Gleichgewichtspreis R gegen PLS einzulösen.<br>
Dabei werden die am schwächsten besicherten Vaults zuerst reduziert - jene, die der Liquidationsgrenze<br> 
am nächsten sind.

Dieses Prinzip schafft eine natürliche Marktordnung:<br>

- Überdehnte Schulden werden automatisch abgebaut,<br>
- Arbitrageure gleichen Preisabweichungen aus,<br>
- und das Vertrauen in die Einlösbarkeit verankert den Preis dauerhaft an R.

Kein externer Orakel-Feed, kein manuelles Eingreifen, keine Blackbox - nur offene, deterministische 
Logik.

---

## 4.4 Der Kern - unveränderlich (Immutable Core)

Im Zentrum von ProjectUSD steht der unveränderliche Kern.<br>
Hier liegen alle lebenswichtigen Funktionen:

- Vault-Logik und Liquidationsmechanismen<br>
- Redemption-Engine<br>
- Controller und r-Steuerung<br>
- interne Parameter wie Collateral-Ratio und Liquidation-Threshold<br>
- Median-Orakel-Aggregation für Preisstabilität

Nach dem sogenannten **Freeze-Event** wird dieser Kern eingefroren.<br>
Von diesem Moment an kann niemand - nicht die Entwickler, nicht die DAO, nicht die Community -<br>
ihn mehr verändern oder anhalten.<br>
ProjectUSD wird zu einem autonomen Organismus: einmal gestartet, bleibt er bestehen.

---

## 4.5 Die Peripherie - kontrollierte Flexibilität

Um Innovation zu ermöglichen, besitzt ProjectUSD eine Peripherie-Schicht.<br>
Hier können Module angehängt oder ersetzt werden, ohne das Herz des Systems zu gefährden:

- neue Collateral-Adapter<br>
- Peg-Stability-Module (PSM) für optionale On-Chain-Swaps<br>
- Algorithmic Market Operations (AMO) zur Liquiditätssteuerung<br>
- Telemetrie- und Analytics-Schnittstellen

Alle Änderungen erfolgen über **Timelocks** und **On-Chain-Abstimmungen**, öffentlich nachvollziehbar<br>
und zeitverzögert.<br>
So bleibt die Governance offen, aber nie gefährlich.

---

## 4.6 Ein System ohne Stecker

Es gibt keinen Admin-Key, keinen „Pause-Button“, keinen Notfallzugang.<br>
ProjectUSD kann weder eingefroren noch gelöscht werden.<br>
Das System ist damit nicht nur dezentral - es ist **autark**.<br>
Sobald es einmal deployed ist, gehört es niemandem - und damit allen.<br>
Diese Unbestechlichkeit ist kein Nebeneffekt, sondern das Ziel selbst:<br>
Ein Geldsystem, das keiner Kontrolle mehr bedarf,<br>
weil es im Innersten bereits perfekt ausbalanciert ist.

---

[← Kapitel 3](03-kapitel-3.md) | [Inhaltsverzeichnis](README.md) | [Kapitel 5 →](05-kapitel-5.md)
