# ProjectUSD  
### Autonomes Geldsystem für PulseChain

**Sprache:** 🇩🇪 Deutsch | [🇬🇧 Englisch](./README.md)

> *„Wenn der Code nicht lügen kann, muss es der Mensch auch nicht mehr.“*

---

## 🌐 Was ist ProjectUSD?

ProjectUSD ist ein **vollständig On-Chain basiertes, algorithmisches Geldsystem** für PulseChain.  
Es erreicht wirtschaftliche Stabilität **ohne Banken, ohne Governance, ohne Orakel und ohne jegliche zentrale Eingriffe.**

Es repräsentiert die nächste Evolutionsstufe dezentraler Finanzsysteme:  
ein **selbstregulierender ökonomischer Motor**, der ausschließlich durch transparente und unveränderliche Logik funktioniert.

---

## 📘 Whitepaper V2.1 (Mehrsprachig)

**Verfügbare Editionen:**

- 🇩🇪 [Deutsche Version (PDF)](https://github.com/Aqua75/ProjectUSD/releases/download/v2.1-DE/ProjectUSD.Whitepaper.V2.1.German.pdf)  
- 🇺🇸 [Englische Version (PDF)](https://github.com/Aqua75/ProjectUSD/releases/download/v2.1-EN/ProjectUSD.Whitepaper.V2.1.EN.Englisch.pdf)  
- 🇪🇸 [Spanisch (PDF)](https://github.com/Aqua75/ProjectUSD/releases/download/v2.1-es/ProjectUSD_Whitepaper_V2.1_ES_Espanol.pdf)  
- 🇫🇷 [Französisch (PDF)](https://github.com/Aqua75/ProjectUSD/releases/download/v2.1-FR/ProjectUSD_Whitepaper_V2.1_FR_Francais.pdf)  
- 🇧🇷 [Portugiesisch (PDF)](https://github.com/Aqua75/ProjectUSD/releases/download/v2.1-PT-BR/ProjectUSD_Whitepaper_V2.1_pt-BR_Portugues.pdf)  
- 🇮🇹 [Italienisch (PDF)](https://github.com/Aqua75/ProjectUSD/releases/download/v2.1-IT/ProjectUSD_Whitepaper_V2.1_IT_Italiano.pdf)  
- 🇵🇱 [Polnisch (PDF)](https://github.com/Aqua75/ProjectUSD/releases/download/v2.1-PL/ProjectUSD_Whitepaper_V2.1_PL_Polski.pdf)  
- 🇳🇱 [Niederländisch (PDF)](https://github.com/Aqua75/ProjectUSD/releases/download/v2.1-NL/ProjectUSD_Whitepaper_V2.1_NL_Nederlands.pdf)  
- 🇨🇳 [Chinesisch (PDF)](https://github.com/Aqua75/ProjectUSD/releases/download/v2.1-CN/ProjectUSD_Whitepaper_V2.1_CN_Chinese.pdf)  
- 🇯🇵 [Japanisch (PDF)](https://github.com/Aqua75/ProjectUSD/releases/download/v2.1-JA/ProjectUSD_Whitepaper_V2.1_JA_Japanese.pdf)  
- 🇷🇺 [Russisch (PDF)](https://github.com/Aqua75/ProjectUSD/releases/download/v2.1-RU/ProjectUSD_Whitepaper_V2.1_RU_Russian.pdf)  
- 🇮🇳 [Hindi (PDF)](https://github.com/Aqua75/ProjectUSD/releases/download/v2.1-HI/ProjectUSD_Whitepaper_V2.1_HI_Hindi.pdf)  
- 🇹🇷 [Türkisch (PDF)](https://github.com/Aqua75/ProjectUSD/releases/download/v2.1-TR/ProjectUSD_Whitepaper_V2.1_TR_Turkish.pdf)  
- 🇻🇳 [Vietnamesisch (PDF)](https://github.com/Aqua75/ProjectUSD/releases/download/v2.1-VI/ProjectUSD_Whitepaper_V2.1_VI_Vietnamese.pdf)  
- 🇮🇩 [Indonesisch (PDF)](https://github.com/Aqua75/ProjectUSD/releases/download/v2.1-ID/ProjectUSD_Whitepaper_V2.1_ID_Indonesian.pdf)  
- 🇰🇷 [Koreanisch (PDF)](https://github.com/Aqua75/ProjectUSD/releases/download/v2.1-KR/ProjectUSD_Whitepaper_V2.1_KR_Korean.pdf)  
- 🇸🇦 [Arabisch (PDF)](https://github.com/Aqua75/ProjectUSD/releases/download/v2.1-AR/ProjectUSD_Whitepaper_V2.1_AR_Arabic.pdf)  
- 🕉 [Sanskrit (Experimentell)](https://github.com/Aqua75/ProjectUSD/releases/download/v2.1-SA/ProjectUSD_Whitepaper_V2.1_SA_Sanskrit.pdf)

---

## 🧩 Technische Architektur

ProjectUSD besteht aus fünf unveränderlichen Kernmodulen:

- **VaultEngine** – Collateral-, Schulden- und CR-Logik  
- **Controller** – Autonomes Gleichgewichtssystem (R & r-Epochen)  
- **Oracle** – Median-basierte, sichere Preisaggregation  
- **Liquidation & Redemption Engine** – Stabilitätsdurchsetzung  
- **StabilityPool** – Kollektiver Risikopuffer  

---

> ### 🔍 Klarstellung: Internes TWAP-Oracle  
> Das „Oracle“-Modul in ProjectUSD ist **kein** externes Preis-Oracle.  
> Es verwendet **weder** Chainlink, Pyth, DIA, APIs **noch** sonstige Off-Chain-Datenquellen.  
>  
> Stattdessen handelt es sich um einen **rein on-chain berechneten TWAP-Reader**,  
> der seine Informationen ausschließlich aus dem ProjectUSD/PLS-AMM-Pool  
> auf PulseChain ableitet.  
>  
> - keine externen Abhängigkeiten  
> - keine Governance-Updates  
> - keine Admin-Eingriffe  
> - vollständig deterministisch und on-chain  
>  
> Damit bleibt ProjectUSD ein **autonomes, oracle-freies Währungssystem**,  
> während der Controller dennoch das Verhalten seines eigenen AMM-Marktes beobachten kann.

---

Detaillierte Erklärung:

➡ `/Architecture/README.de.md`

---

## 🚀 Schnellstart für Entwickler

Für Entwickler, Auditoren und Forscher, die direkt in die technische Struktur einsteigen möchten, sind die zentralen Einstiegspunkte:

### **1. Architekturüberblick**
➡ [`/Architecture/README.de.md`](./Architecture/README.de.md)  
Hohe Ebene der Systemarchitektur, Modulübersicht, Datenflüsse.

### **2. Vollständige SPECS**
➡ [`/Architecture/specs/README.de.md`](./Architecture/specs/README.de.md)  
Formale Spezifikationen aller Kernmodule:

- VaultEngine  
- Controller  
- Oracle  
- Liquidation und Redemption  
- StabilityPool  
- Security  
- Governance und Freeze  
- KPI-Subgraph  
- Incident-Runbook  

### **3. Entwickler-Playbook**
➡ [`/Developer_Playbook/README.de.md`](./Developer_Playbook/README.de.md)  
Praktischer Leitfaden für Entwickler, Standards, Empfehlungen und Workflow.

### **4. Glossar**
➡ [`/Glossary.de.md`](./Glossary.de.md)  
Definierte Fachbegriffe für Mechanismen, Variablen und Formeln.

---

Diese vier Einstiegspunkte bilden die Grundlage für jede Implementierung von ProjectUSD und ermöglichen Entwicklern eine schnelle und vollständige Orientierung im Systemdesign.

---

## 📂 Vollständige technische Spezifikationen (SPECS)

ProjectUSD enthält eine der vollständigsten SPECS-Bibliotheken in ganz DeFi:

➡ `/Architecture/specs/README.de.md`  
➡ `/Architecture/specs/README.md`

Dieser Abschnitt bildet das **vollständige audit-bereite Blueprint** des Systems und umfasst:

- VaultEngine SPEC  
- Controller SPEC  
- Oracle SPEC  
- Liquidation & Redemption SPEC  
- StabilityPool SPEC  
- Security SPEC  
- Governance & Freeze SPEC  
- Freeze Checklist  
- KPI-Subgraph SPEC  
- Incident-Runbook  
- DEX-LP SPEC (optional)

Alle Spezifikationen sind **modular**, **konsistent** und in **Deutsch und Englisch** verfügbar.

---

## 📚 Forschungsbibliothek

ProjectUSD stellt zwei kuratierte Dokumentensammlungen bereit, die über die technischen Spezifikationen hinausgehen und das ökonomische Fundament des Systems vertiefen.

### 📝 Artikel

➡ [`/Articles`](./Articles)  
Grundlegende Analysen und Essays zu zentralen Konzepten wie:
- interne Werteinheit und Kaufkraft
- Bedeutung des Namens ProjectUSD
- das P R r Modell
- ökonomische Prinzipien autonomer Geldsysteme

Diese Texte bilden das theoretische Fundament des Designs und erläutern die Konzepte hinter den SPECS.

### 📑 Studien

➡ [`/Studies`](./Studies)  
Wissenschaftliche Studienreihen zu Themen wie:
- Stabilitätsmechanismen und Anti Reflexivität
- Spieltheorie des Systems
- Collateral Modelle und Stresstests
- Liquiditäts und Arbitrageverhalten
- langfristiger Surplus Aufbau
- Gas und Effizienzmodelle

Die Studien liefern quantitative Modelle, konzeptionelle Rahmenwerke und vertiefende Analysen zum strukturellen Verhalten des ProjectUSD-Systems.

---

## 📌 Status  
🧩 *Architektur & vollständiger SPEC-Bauplan abgeschlossen – offen für Entwickler, Auditoren und Investoren.*

---

## 🔗 Diskussion & Entwicklung

Offizielle Diskussionsgruppe:

➡ https://t.me/ProjectUSD_Discussion

---

## ⚠️ Hinweis zur Implementierung

Dieses Repository enthält ausschließlich die offiziellen Spezifikationen von ProjectUSD.

Smart-Contract-Implementierungen können von unabhängigen Entwicklerteams erstellt werden.
Ob eine konkrete Implementation sicher ist, lässt sich ausschließlich durch:

- **öffentliche Audits**,  
- **Peer-Review**,  
- **Open-Source-Transparenz**,  
- **formale Verifikation**  

beurteilen – nicht durch dieses Dokument.

ProjectUSD veröffentlicht selbst **keine** Smart-Contracts und gibt **keine** Implementierung als offiziell aus.

Nutzer sollten ausschließlich Implementationen verwenden,
die von **anerkannten Auditoren** überprüft wurden und deren Code **öffentlich einsehbar** ist.

---

## 🏷️ ProjectUSD – Namens- und Attributionsrichtlinie

ProjectUSD ist ein originäres Open-Source-Konzept, veröffentlicht von  
**Aqua75 / PulseChain Community Initiative**  
unter der Lizenz **Creative Commons BY-NC-SA 4.0**.

Diese Lizenz gilt für alle Dokumentationen, Spezifikationen, Whitepaper, Studien und Medien in diesem Repository.

Der **Name „ProjectUSD“ sowie das ProjectUSD-Logo** sind jedoch geschützte Bezeichner des ursprünglichen, PulseChain-basierten Designs.

### Verwendung des Namens „ProjectUSD“

Implementierungen, die auf **PulseChain** bereitgestellt werden, müssen:

1. vollständig der offiziellen ProjectUSD-Spezifikation entsprechen, und  
2. den Konsolidierungsprozess durchlaufen  

um den Namen **„ProjectUSD“** verwenden zu dürfen.

### Unabhängige Forks

Alle anderen Implementierungen – auf PulseChain oder anderen Chains – müssen klar als **unabhängige Forks** gekennzeichnet sein und die folgende Attribution enthalten:

> Basierend auf dem „ProjectUSD“-Konzept von Aqua75 / PulseChain Community Initiative  
> https://github.com/Aqua75/ProjectUSD

Die unautorisierte Nutzung des Namens oder Logos außerhalb des definierten PulseChain-Kontexts  
stellt einen Verstoß gegen die Lizenzbedingungen dar.

© 2026 Aqua75 — Alle Rechte vorbehalten für den Namen und das Logo **„ProjectUSD“**.

---

## 🪙 Lizenz

Creative Commons **BY-NC-SA 4.0**  
© 2026 Aqua75 – PulseChain Community Initiative
