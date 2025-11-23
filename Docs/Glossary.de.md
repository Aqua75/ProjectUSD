# Glossary – Key Terms of the ProjectUSD Specification

Dieses Glossar definiert die zentralen Begriffe der ProjectUSD-Spezifikation.  
Die beschriebenen Module zeigen, wie die Komponenten in einer späteren Implementierung funktionieren,  
sofern ein externes Team die Spezifikation in Code übersetzt.

---

## **R – Redemption Price (Gleichgewichtspreis)**  
Der interne Referenzwert, auf den sich das System ausrichtet.  
R definiert das mathematische Gleichgewicht und basiert ausschließlich auf  
on-chain messbaren Größen – ohne Orakel oder Fiat-Bezug.

---

## **r – System Rate**  
Ein variabler Steuerparameter der Spezifikation.  
r steuert Anreize, Nachfrage und Preisreaktionen, indem es Abweichungen  
zwischen Marktpreis P und Gleichgewichtspreis R ausgleicht.

---

## **Vault (Collateral-Modul)**  
Ein Modul, das festlegt, wie Sicherheiten hinterlegt werden,  
wie Schulden entstehen und wie Risiken verarbeitet werden.  
Das Vault-Modell definiert Besicherung, Liquidation und die Ausgabe neuer Einheiten.

---

## **Stability Pool (kollektiver Risikopuffer)**  
Ein Modell zur Behandlung unterbesicherter Positionen.  
Der Stability Pool absorbiert Schulden und verteilt Collateral  
entsprechend der definierten Regeln der Spezifikation.

---

## **Redemption Engine**  
Der spezifizierte Preisanker-Mechanismus.  
Die Redemption Engine erzeugt Arbitragesignale, die den Marktpreis  
auf den Gleichgewichtswert R zurückführen.

---

## **AMO – Algorithmic Market Operations**  
Optionale algorithmische Module.  
AMOs steuern Liquidität innerhalb definierter Grenzen  
und beeinflussen interne Überschüsse oder Puffermechanismen.

---

## **PSM – Peg Stability Module**  
Ein optionaler Mechanismus für kurzfristige Marktfriktion.  
Der PSM nutzt externe Stablecoins innerhalb enger Parameter,  
ohne die Autonomie des Systems zu beeinträchtigen.

---

## **Surplus Buffer**  
Ein ökonomischer Puffer, der interne Überschüsse speichert  
und r-Schwankungen sowie langfristige Sparmodelle stabilisiert.

---

## **Immutable Core**  
Der definierte Kern aller kritischen Mechanismen.  
Der Immutable Core bleibt nach dem Freeze-Konzept dauerhaft unveränderlich  
und schützt die Systemintegrität.

---

## **Freeze Event**  
Der definierte Zeitpunkt, ab dem der Kern dauerhaft eingefroren wird  
und keine Änderungen mehr zulässt.  
Das Freeze Event sichert Stabilität, Unbestechlichkeit und dauerhafte Autonomie.

---

## **Controller**  
Das mathematische Regelsystem der Spezifikation.  
Der Controller analysiert die Beziehung zwischen P, R und r  
und stellt die dynamische Stabilisierung des Systems her.
