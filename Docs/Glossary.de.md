# Glossary – Wichtigste Begriffe der ProjectUSD-Spezifikation

Dieses Glossar definiert die zentralen Begriffe der ProjectUSD-Spezifikation.  
Die beschriebenen Module zeigen, wie die Komponenten in einer späteren Implementierung funktionieren,  
sofern ein externes Team die Spezifikation in Code übersetzt.

---

# 🔹 Grundlegende Systemgrößen

## **R – Redemption Price (Gleichgewichtspreis)**  
Der interne Referenzwert des Systems.  
R fungiert als mathematischer Gleichgewichtspreis und definiert den Wert, um den sich das gesamte System stabilisiert.  
R basiert ausschließlich auf on-chain messbaren Größen und benötigt keine externen Orakel oder Fiat-Referenzen.

---

## **P – Market Price (Marktpreis)**  
Der Preis, zu dem ProjectUSD an dezentralen Börsen gehandelt wird.  
P ist die exogene Größe, gegen die das System Stabilität herstellt.

---

## **r – System Rate**  
Der variable Steuerparameter der Spezifikation.  
r reguliert Anreize, Nachfrage, Schuldverhalten und Preisreaktionen, indem es Abweichungen zwischen Marktpreis P und Gleichgewichtspreis R ausgleicht.  
Ein positives r macht Geldschöpfung teurer (bremsend), ein negatives r macht Halten und Prägen attraktiver (stimulierend).

---

# 🔹 Kernmodule des Systems

## **Vault (Collateral-Modul)**  
Ein Modulsystem zur Hinterlegung von Sicherheiten und Erzeugung neuer Einheiten.  
Ein Vault definiert Besicherung, Schuldenproduktion, Liquidationsregeln und die Beziehung zwischen Collateral und Systemverbindlichkeiten.  
Es ist ein zentrales Element der Wertschöpfung und Risikosteuerung.

---

## **Stability Pool**  
Ein kollektiver Risikopuffer für unterbesicherte Positionen.  
Der Stability Pool absorbiert die Schulden liquidierter Vaults und verteilt deren Collateral an die Poolteilnehmer entsprechend den definierten Regeln der Spezifikation.  
Er sorgt für eine kontinuierliche Bereinigung schwacher Positionen.

---

## **Redemption Engine**  
Der spezifizierte Preisanker-Mechanismus.  
Die Redemption Engine erzeugt Arbitragesignale, die Marktpreise langfristig auf den Gleichgewichtswert R zurückführen.  
Sie definiert, wie ProjectUSD gegen Collateral eingetauscht werden kann, um Marktungleichgewichte zu korrigieren.

---

## **Liquidation Mechanism**  
Der Mechanismus, der unterbesicherte Vaults entfernt und ihr Collateral gemäß den Regeln der Spezifikation verteilt.  
Er sorgt dafür, dass die Systemintegrität stets gewahrt bleibt und keine unbesicherten Schulden im System verbleiben.

---

## **Controller**  
Das mathematische Regelsystem, das die Beziehung zwischen P, R und r analysiert und daraus die notwendigen Anpassungen der Systemrate ableitet.  
Der Controller stellt die dynamische Rückführung des Systems in Richtung Gleichgewicht sicher.

---

# 🔹 Erweiterungsmodule

## **AMO – Algorithmic Market Operations**  
Optionale algorithmische Module, die innerhalb definierter Parameter Liquidität bereitstellen, Arbitragespreads verkleinern oder interne Überschüsse optimieren.  
AMOs agieren streng regelbasiert und beeinflussen externe Märkte nicht willkürlich, sondern ausschließlich innerhalb enger ökonomischer Grenzen.

---

## **PSM – Peg Stability Module**  
Ein optionaler Mechanismus zur Modellierung kurzfristiger Marktfriktion.  
Der PSM verwendet limitierte Mengen externer Stablecoins als Puffer, ohne Abhängigkeit von deren Preislogik.  
Er ist rein ergänzend und nicht notwendig für die Funktion der Kernarchitektur.

---

## **Surplus Buffer**  
Ein interner ökonomischer Puffer, der Überschüsse speichert und Spannungen im System ausgleicht.  
Der Surplus Buffer stabilisiert r, ermöglicht langfristige Sparmodelle und dient als Risikoabsorber für Fluktuationen.

---

# 🔹 Strukturelle und Sicherheitskonzepte

## **Immutable Core**  
Der definierte, unveränderliche Kern aller kritischen Mechanismen.  
Nach einem Freeze-Konzept bleibt der Immutable Core dauerhaft fixiert und schützt das System vor Manipulation, Governance-Angriffen und zentraler Kontrolle.

---

## **Freeze Event**  
Der definierte Zeitpunkt, an dem der Kern der Spezifikation dauerhaft eingefroren wird.  
Der Freeze garantiert dauerhafte Autonomie, Sicherheit und Unveränderlichkeit der fundamentalen Regeln.

---

## **Periphery Layer**  
Ein äußerer Funktionsbereich, in dem nicht-kritische Module wie AMOs, Analysewerkzeuge oder zusätzliche Collateral-Modelle existieren.  
Die Periphery ist flexibel, kann erweitert werden und unterliegt transparenten, restriktiven Änderungsmechanismen.

---

## **TWAP (Time-Weighted Average Price)**  
Ein aus on-chain Preisdaten berechneter Durchschnittswert, der kurzfristige Manipulationen herausfiltert.  
TWAP-Werte dienen als Grundlage für interne Preisreferenzen ohne externe Orakel.

---

## **MEV-Resilience**  
Ein Sammlung von Mechanismen, die sicherstellen, dass das System robuste Ergebnisse liefert, selbst wenn Miner/Validatoren versuchen, Transaktionen zu reorderen oder auszunutzen.  
Dazu zählen Preisschutzlogik, Liquidationsdesign, und kontrollierte Übergänge zwischen P und R.

---

# 🔹 Ökonomische Mechanismen

## **Debt Position (Schuldposition)**  
Die Verpflichtung, die beim Prägen neuer Einheiten entsteht.  
Jede Debt Position ist vollständig Collateral-gebunden und folgt den Liquidationsregeln des Systems.

---

## **Collateral Ratio (Besicherungsgrad)**  
Das Verhältnis zwischen Collateralwert und Schuldwert innerhalb eines Vaults.  
Die Spezifikation definiert Mindestwerte und Sicherheitsgrenzen, die die Stabilität der Schuldpositionen sicherstellen.

---

## **Redemption Spread**  
Der Unterschied zwischen dem Marktpreis P und dem Redemption Price R.  
Dieser Spread bestimmt die Richtung der Arbitrage und die Stärke der Preisrückführung.

---

## **Savings Dynamics / Interest Dynamics**  
Die Art und Weise, wie r Sparanreize schafft oder Schulden verteuert.  
Diese Dynamik ist der zentrale Regler der monetären Mechanik.

---

# 🔹 Systemweite Eigenschaften

## **Autonomous Monetary Policy**  
Eine vollständig regelbasierte, algorithmisch definierte Geldpolitik ohne Governance, ohne Orakel und ohne zentrale Entscheidungsträger.

---

## **On-Chain Transparency**  
Alle Parameter, Mechanismen und Übergänge sind offen einsehbar, geprüft und reproduzierbar.  
Die Spezifikation basiert vollständig auf nachvollziehbarer Mathematik.

---

## **Decentralized Stability**  
Die Stabilität entsteht nicht durch externe Stützungen, sondern durch interne Regelkreise, Arbitrage und mathematisch definierte Reaktionen.

---
