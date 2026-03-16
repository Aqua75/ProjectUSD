# ProjectUSD Architektur

Die **ProjectUSD-Architektur** definiert das strukturelle und funktionale Fundament des Systems.  
Sie beschreibt, wie die On-Chain-Komponenten interagieren, um Gleichgewicht, Autonomie  
und Transparenz sicherzustellen.

---

## 🧩 Kernkomponenten

- **Vaults** – Das Fundament der Geldschöpfung.  
  Nutzer hinterlegen native PulseChain-Assets (z. B. PLS) als Collateral, um ProjectUSD zu prägen.

- **Stability Pool** – Kollektiver Sicherheitsmechanismus, der unterbesicherte Positionen absorbiert  
  und deren Collateral an die Einzahler verteilt.

- **Redemption Engine** – Hält den internen Gleichgewichtspreis (R) stabil,  
  indem ProjectUSD jederzeit 1:1 gegen PLS zum internen Referenzwert eingelöst werden kann.

- **Controller** – Der autonome Feedback-Algorithmus, der die Systemrate (r) reguliert  
  und Angebot sowie Nachfrage dynamisch ausgleicht.

---

## 🧱 Architekturebenen

| Ebene | Beschreibung |
|-------|--------------|
| **Unveränderlicher Kern** | Enthält die unantastbare Logik: Vaults, Controller, Liquidationen und Redemption. Nach dem Freeze kann dieser Bereich nicht mehr verändert oder pausiert werden. |
| **Peripherie** | Optionale Erweiterungen: Collateral-Adapter, Analyse-Module und weitere nicht-kritische Komponenten. |
| **Governance-Ebene** | Beschränkt auf Koordination und Upgrades der Peripherie. Kein Einfluss auf den unveränderlichen Kern. |

---

## 🧭 Designprinzipien

- **On-Chain-Autonomie:** Keine externen Oracles, keine menschliche Intervention.  
- **Mathematisches Feedback:** Stabilität entsteht durch algorithmische Reaktion, nicht durch einen festen Peg.  
- **Transparenz durch Code:** Jede Variable und jeder Prozess ist On-Chain verifizierbar.  
- **Freeze-Event (nur Kern):** Nach Aktivierung wird ausschließlich der **unveränderliche Kern** eingefroren;  
  periphere Module bleiben über Timelocked Governance anpassbar.

---

## 📂 Technische Spezifikationen (SPECS)

Der vollständige Satz technischer Spezifikationen – inklusive aller Kernmodule,  
Sicherheitskonzepte, Freeze-Mechanik, Stabilitätslogik, Liquidations-Engine,  
Subgraph-KPIs und Diagnoseprozesse – befindet sich unter:

**➡ `/Architecture/specs/`**

Es stehen zwei Einstiegspunkte zur Verfügung:

- 🇩🇪 **SPECS Übersicht (Deutsch)**  
  `/Architecture/specs/README.de.md`

- 🇬🇧 **SPECS Overview (English)**  
  `/Architecture/specs/README.md`

Diese Dateien bieten:

- eine vollständige Modulübersicht  
- direkte Links zu allen Spezifikationen  
- empfohlene Lesereihenfolgen  
- Trennung zwischen Core und Peripherie  
- Verweise auf das ProjectUSD-Whitepaper  

Der SPECS-Ordner bildet die **komplette technische Grundlage** für Entwickler,  
Auditoren und Forscher.

---

## 📐 Normative Quellen

Die ProjectUSD-Dokumentation existiert in mehreren Formaten, darunter Spezifikationen,  
Whitepaper, Artikel und Studien. Wenn Unterschiede zwischen Dokumenten auftreten,  
gilt folgende Prioritätsreihenfolge als **normative Quelle der Wahrheit**.

1. **Architektur-Spezifikationen (`/Architecture/specs/`)**  
   Die Spezifikationen definieren das formale Verhalten des Protokolls und sind  
   die normative Referenz für Implementierungen.

2. **Controller- und Core-Modul-Spezifikationen**  
   Diese Dokumente definieren die operativen Parameter und Invarianten des  
   unveränderlichen Kerns.

3. **Whitepaper**  
   Das Whitepaper erläutert Architektur und ökonomisches Design, kann jedoch  
   vereinfachte Darstellungen enthalten.

4. **Artikel und Studien**  
   Diese Texte liefern konzeptionelle Erklärungen und Forschungsperspektiven,  
   sind jedoch nicht normativ.

Bei widersprüchlichen Beschreibungen haben **die Spezifikationen immer Vorrang**.

---

## 📘 Referenz

Alle Architekturkonzepte basieren auf dem  
[ProjectUSD Whitepaper – Vision & Architektur einer selbstregulierenden Blockchain-Ökonomie](https://github.com/Aqua75/ProjectUSD/tree/main/Whitepaper)

---

## 🪙 Lizenz
Creative Commons **BY-NC-SA 4.0**  
© 2026 Aqua75 – PulseChain Community Initiative
