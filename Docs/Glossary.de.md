# Glossary – Terminology of the ProjectUSD Specification  

Dieses Glossar definiert zentrale Begriffe, die in der wirtschaftlichen, mathematischen  
und architektonischen Spezifikation von ProjectUSD verwendet werden.  
Es beschreibt **keine Implementierung**, sondern ausschließlich theoretische Module  
und Konzepte des Designs.

---

## **R – Redemption Price (Gleichgewichtspreis)**  
Der interne, theoretische Referenzwert in der ProjectUSD-Architektur.  
R fungiert als ökonomischer Gleichgewichtspunkt, um den sich ein  
selbststabilisierendes Wertesystem ausrichten kann.  
Der Begriff ist rein konzeptionell und wird ausschließlich durch  
on-chain messbare Mechanismen definiert.

---

## **r – System Rate**  
Ein variabler Steuerparameter innerhalb der theoretischen Kontrolllogik.  
Die Systemrate r repräsentiert den mathematischen Regler, der in der  
Spezifikation zur Modellierung von Nachfrageverhalten, Anreizen  
und Gleichgewichtsrückführung eingesetzt wird.

---

## **Vault (Konzeptionelles Collateral-Modul)**  
Ein Vault ist ein **theoretischer Baustein** der Architektur, der die Regeln für  
Kollateralisierung und Ausgabe der Einheit „ProjectUSD“ beschreibt.  
Das Vault-Modul definiert Konzepte wie Besicherungsgrad, Liquidationsbedingungen  
und die Interaktion zwischen Collateral und Systemverpflichtungen –  
rein auf Spezifikationsebene, ohne Bezug zu einer konkreten Implementierung.

---

## **Stability Pool (Konzeptionelles Stabilitätsmodul)**  
Ein in der Spezifikation definiertes Modell für kollektive Risikopuffer.  
Es beschreibt, wie ein System theoretisch mit unterbesicherten Positionen  
umgehen kann und welche Mechanismen eine selbstkorrigierende Struktur  
begünstigen würden.  
Der Stability Pool existiert ausschließlich als konzeptionelles Element  
innerhalb der Architektur.

---

## **Redemption Engine**  
Ein theoretischer Mechanismus, der erklärt, wie ein internes Gleichgewicht  
zwischen R (Redemption Price) und dem Marktpreis modelliert werden kann.  
Er beschreibt, wie Arbitragestrukturen in einem autonomen System  
zu Preiskonvergenz führen könnten.  
Es handelt sich um ein **Definitionsmodul**, nicht um eine Implementierung.

---

## **AMO – Algorithmic Market Operations**  
In der Spezifikation definierte optionale, algorithmische Steuerungsmechanismen.  
AMOs beschreiben abstrakt, wie ein System in bestimmten Modellen  
Liquidität oder Reserven anpassen könnte, sofern es innerhalb klarer  
mathematischer Grenzen operiert.  
AMOs sind **rein theoretische Komponenten** des Designs.

---

## **PSM – Peg Stability Module**  
Ein optionales, rein spezifikatives Konzept zur Modellierung von  
Kurstreibung und Liquiditätspuffern.  
In der Architektur wird der PSM als theoretische Ergänzung beschrieben,  
die externe stabile Einheiten nutzen *könnte*, ohne dass dies für die  
Funktionsweise der Kernlogik notwendig wäre.

---

## **Surplus Buffer**  
Ein konzeptioneller ökonomischer Puffer innerhalb der Architektur.  
Er dient dazu, modelltheoretisch zu erklären, wie interne Überschüsse  
in einem autonomen System aufgefangen, gespeichert oder verteilt  
werden könnten.

---

## **Immutable Core**  
Der in der Spezifikation definierte Kernbereich aller kritischen Regeln  
und mathematischen Mechanismen.  
Der Immutable Core beschreibt, **welche Teile eines autonomen Systems  
nach einem Freeze-Konzept unveränderlich sein müssten**, um  
dauerhafte Stabilität und Manipulationsfreiheit zu ermöglichen.

---

## **Freeze Event**  
Ein theoretischer Begriff, der beschreibt, wann ein Systemkern nach  
vollständigem Audit und Stabilitätsnachweis dauerhaft eingefroren wird  
und ab diesem Zeitpunkt nicht mehr änderbar ist.  
Das Freeze Event ist ein **architektonisches Prinzip**, kein  
umzusetzender realer Vorgang.

---

## **Controller**  
Ein mathematisches Regelsystem, das in der Spezifikation definiert,  
wie r (System Rate) in Abhängigkeit von Abweichungen zwischen  
Marktpreis P und Gleichgewichtspreis R angepasst werden könnte.  
Der Controller ist ein **rein theoretisches Modell** zur Beschreibung  
selbststabilisierender, algorithmischer Geldpolitik.
