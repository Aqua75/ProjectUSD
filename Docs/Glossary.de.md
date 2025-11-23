# Glossary – Key Terms of the ProjectUSD Specification

Dieses Glossar definiert die zentralen Begriffe der ProjectUSD-Spezifikation.  
Die beschriebenen Module zeigen, wie die Komponenten in einer späteren Implementierung  
funktionieren würden, sofern ein externes Team die Spezifikation in Code übersetzt.

---

## **R – Redemption Price (Gleichgewichtspreis)**  
Der interne Referenzwert, um den sich ein implementiertes System stabilisieren würde.  
R dient als mathematischer Gleichgewichtspreis und entsteht ausschließlich aus  
on-chain messbaren Größen – ohne Orakel oder Fiat-Bezug.

---

## **r – System Rate**  
Ein variabler Steuerparameter in der Spezifikation.  
Bei einer Umsetzung würde r als Regler für Nachfrage, Anreize und Marktreaktionen dienen  
und auf Abweichungen zwischen Marktpreis P und Gleichgewichtspreis R reagieren.

---

## **Vault (Collateral-Modul)**  
Ein in der Spezifikation definiertes Modul, das beschreibt, wie Sicherheiten hinterlegt,  
wie Schulden erzeugt und wie Risiken abgefedert werden könnten.  
Falls implementiert, würde ein Vault-Modul die Regeln für Besicherung,  
Liquidation und Schuldenmanagement vorgeben.

---

## **Stability Pool (kollektiver Risikopuffer)**  
Ein konzeptionelles Modell zur Behandlung unterbesicherter Positionen.  
Bei einer Implementierung würde dieses Modul als gemeinsamer Liquiditätspool wirken,  
der theoretisch Schulden absorbieren und Collateral umverteilen könnte.

---

## **Redemption Engine**  
Ein im Design definiertes Preisanker-Modul.  
Würde die Spezifikation umgesetzt, könnte dieser Mechanismus Arbitragekräfte aktivieren,  
sodass Marktpreise langfristig zu R konvergieren.

---

## **AMO – Algorithmic Market Operations**  
Optionale Module der Spezifikation, die erklären, wie ein System durch begrenzte,  
algorithmische Mechanismen Liquidität beeinflussen *könnte*.  
AMOs sind konzeptionelle Erweiterungen – nicht notwendig für die Kernfunktion.

---

## **PSM – Peg Stability Module**  
Ein in der Spezifikation beschriebener optionaler Mechanismus zur Modellierung  
kurzfristiger Liquiditätsreibung.  
Falls implementiert, würde der PSM externe Stablecoins in engem Rahmen nutzen,  
ohne die Autonomie des Systems zu beeinträchtigen.

---

## **Surplus Buffer**  
Ein definierter ökonomischer Puffer innerhalb der Architektur.  
In einer möglichen Umsetzung würde dieser Überschüsse speichern  
und theoretisch dazu dienen, r-Schwankungen oder langfristige Sparmodelle zu glätten.

---

## **Immutable Core**  
Der in der Spezifikation festgelegte Bereich aller kritischen Funktionen,  
der bei einer Implementierung nach einem Freeze-Konzept unveränderlich wäre.  
Der Immutable Core definiert, welche Mechanismen dauerhaft fix sein müssen,  
damit ein autonomes System stabil und fälschungssicher bleibt.

---

## **Freeze Event**  
Ein theoretisch definierter Zeitpunkt in einer möglichen Implementierung,  
an dem der Kerncode eingefroren und dauerhaft unveränderlich würde.  
Der Begriff beschreibt ein Architekturprinzip – kein tatsächliches Ereignis  
in diesem Repository.

---

## **Controller**  
Ein mathematisches Regelsystem, das die Beziehung zwischen P (Marktpreis),  
R (Gleichgewichtspreis) und r (Systemrate) modelliert.  
Bei einer Implementierung würde der Controller die zentrale Rolle der  
selbststabilisierenden Rückkopplung übernehmen.
