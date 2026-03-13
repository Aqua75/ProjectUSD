# Kapitel 4 - Die Architektur: Aufbau eines unbestechlichen 
Systems

Ein System kann nur so stark sein wie seine Architektur.

Bei ProjectUSD wurde jede Komponente so entworfen, dass sie nicht korrumpierbar ist - weder durch 
Menschen, noch durch externe Daten, noch durch Governance-Mehrheiten.

Alles, was das System am Leben hält, existiert auf-Chain, öffentlich überprüfbar und ohne 
Eingriffsrechte.

## 4.1 Vaults - das Fundament der Geldschöpfung

Vaults sind persönliche Tresore, in denen Nutzer native PulseChain-Assets - vor allem PLS - als 
Sicherheit hinterlegen.

Auf Basis dieser Sicherheiten prägen sie neue ProjectUSD-Token.

Der maximal mögliche Betrag hängt vom festgelegten Collateral-Ratio (CR) ab; typischerweise 170 % 
oder mehr.

Fällt der Wert der Sicherheiten unter die Mindestgrenze, wird der Vault automatisch liquidiert.

Kein Mensch, kein Team und keine Behörde kann diesen Prozess stoppen oder bevorzugen - alles 
geschieht nach derselben Regel.

Vaults sind damit die Geburtsorte des Geldes im System.

Jeder kann sie öffnen, jeder kann sie schließen, und jede Handlung ist durch Code bestimmt.

## 4.2 Der Stability Pool - Sicherheit durch Schwarmverhalten

Der Stability Pool ist das kollektive Sicherheitsnetz von ProjectUSD.

Hier hinterlegen Nutzer freiwillig ProjectUSD-Token, um Zinsen und Liquidationsboni zu verdienen.

Wenn ein Vault unter die Sicherheitsgrenze fällt, werden dessen Schulden automatisch mit Mitteln aus 
dem Stability Pool beglichen.

Im Gegenzug erhalten die Pool-Teilnehmer die PLS-Sicherheiten - mit einem kleinen Bonus - und der 
überschüssige ProjectUSD-Supply wird vernichtet.

Das Ergebnis:

• schwache Positionen verschwinden,

• starke Hände erhalten zusätzliche Sicherheiten,

• und das gesamte System wird stabiler.

So entsteht ein selbstheilender Kreislauf, der Marktstress absorbiert, statt ihn zu verstärken.

## 4.3 Die Redemption-Engine - der innere Preisanker

Der wichtigste Stabilitätsmechanismus ist die Redemption-Engine.

Sie erlaubt es jedem Nutzer, ProjectUSD zum aktuellen Gleichgewichtspreis R gegen PLS einzulösen.

Dabei werden die am schwächsten besicherten Vaults zuerst reduziert - jene, die der Liquidationsgrenze 
am nächsten sind.

Dieses Prinzip schafft eine natürliche Marktordnung:

Überdehnte Schulden werden automatisch abgebaut,

Arbitrageure gleichen Preisabweichungen aus,

und das Vertrauen in die Einlösbarkeit verankert den Preis dauerhaft an R.

Kein externer Orakel-Feed, kein manuelles Eingreifen, keine Blackbox - nur offene, deterministische 
Logik.

## 4.4 Der Kern - unveränderlich (Immutable Core)

Im Zentrum von ProjectUSD steht der unveränderliche Kern.

Hier liegen alle lebenswichtigen Funktionen:

• Vault-Logik und Liquidationsmechanismen

• Redemption-Engine

• Controller und r-Steuerung

• interne Parameter wie Collateral-Ratio und Liquidation-Threshold

• Median-Orakel-Aggregation für Preisstabilität

Nach dem sogenannten Freeze-Event wird dieser Kern eingefroren.

Von diesem Moment an kann niemand - nicht die Entwickler, nicht die DAO, nicht die Community -

ihn mehr verändern oder anhalten.

ProjectUSD wird zu einem autonomen Organismus: einmal gestartet, bleibt er bestehen.

## 4.5 Die Peripherie - kontrollierte Flexibilität

Um Innovation zu ermöglichen, besitzt ProjectUSD eine Peripherie-Schicht.

Hier können Module angehängt oder ersetzt werden, ohne das Herz des Systems zu gefährden:

• neue Collateral-Adapter

• Peg-Stability-Module (PSM) für optionale On-Chain-Swaps

• Algorithmic Market Operations (AMO) zur Liquiditätssteuerung

• Telemetrie- und Analytics-Schnittstellen

Alle Änderungen erfolgen über Timelocks und On-Chain-Abstimmungen, öffentlich nachvollziehbar 
und zeitverzögert.

So bleibt die Governance offen, aber nie gefährlich.

## 4.6 Ein System ohne Stecker

Es gibt keinen Admin-Key, keinen „Pause-Button“, keinen Notfallzugang.

ProjectUSD kann weder eingefroren noch gelöscht werden.

Das System ist damit nicht nur dezentral - es ist autark.

Sobald es einmal deployed ist, gehört es niemandem - und damit allen.

Diese Unbestechlichkeit ist kein Nebeneffekt, sondern das Ziel selbst:

Ein Geldsystem, das keiner Kontrolle mehr bedarf,

weil es im Innersten bereits perfekt ausbalanciert ist.
