# ProjectUSD Forschungsstudien  
*Eine strukturierte Sammlung technischer, ökonomischer und systemischer Analysen der ProjectUSD-Architektur*

---

## Überblick

Dieses Verzeichnis enthält die vollständige Sammlung der **ProjectUSD Forschungsstudien** – eine fortlaufend wachsende Reihe wissenschaftlich strukturierter Dokumente, die die Architektur, Mechanismen und ökonomischen Eigenschaften von ProjectUSD analysieren und formal darstellen.

ProjectUSD ist ein autonomes, oracle-unabhängiges und selbstregulierendes Geldsystem für PulseChain.

Alle Studien folgen einem gemeinsamen **Level-3-Research-Format**, das gewährleistet:

- klare formale Struktur  
- logische Konsistenz  
- überprüfbare Aussagen  
- saubere Trennung von Theorie, Mechanismus-Design und empirischen Annahmen  
- professionelle Lesbarkeit für Entwickler, Forscher und Auditoren  

Jede Studie ist verfügbar auf **Deutsch (.de.md)** und **Englisch (.en.md)**.

---

## Zweck der Forschungsreihe

Die ProjectUSD Forschungsstudien dienen drei übergeordneten Zielen:

### **1. Technische Dokumentation**

Bereitstellung präziser, implementierungsrelevanter Spezifikationen der Kernmechanismen:

- Controller-Logik (r-Anpassung)  
- Redemption-Abläufe  
- Liquidationen und Stability-Pool-Mechanik  
- Oracle-Design (Median/TWAP)

### **2. Ökonomische und spieltheoretische Analyse**

Untersuchung des Verhaltens aller Akteure im System und der Anreize, die negative Rückkopplungen, Stabilität und Manipulationsresistenz erzeugen.

### **3. Vergleichs- und Stresstestreihen**

Analyse der Systemstabilität unter extremen Marktbedingungen  
sowie Vergleiche mit anderen dezentralen und zentralen Stablecoins.

---

## Inhalt

Nachfolgend die chronologische Liste aller Forschungsstudien:

### **01 – Controller-Dynamik**  
Mechanik der Preisabweichung ε und der r-Regelung.

### **02 – Liquidationskaskaden**  
Stabilitätsverhalten von Vault-Liquidationen und Stability-Pool-Dynamik.

### **03 – Die Redemption-Engine**  
Interner Preisanker und Gleichgewichtsherstellung.

### **04 – MEV-Resistenz & Median-TWAP-Stabilität**  
Oracle-Glättung, Manipulationsschutz und MEV-Robustheit.

### **05 – Vergleich: ProjectUSD vs DAI, LUSD, GHO, USDe, USDC**  
Dezentralität, Risiko, Architektur und ökonomische Vergleiche.

### **06 – PulseChain als geschlossene Ökonomie**  
Einfluss interner Wertdefinitionen ohne Fiat-Abhängigkeit.

### **07 – Atmungsdynamik von r**  
Wie r-Anpassung Volatilität absorbiert.

### **08 – Surplus-Puffer & langfristige Systemgesundheit**  
Warum autonome Puffer langfristige Stabilität verstärken.

### **09 – Warum ProjectUSD keine Death Spirals entwickeln kann**  
Strukturelle Analyse negativer Feedback-Schleifen.

### **10 – Multi-Collateral-Stresstests**  
Systemverhalten bei korrelierten Collateral-Schocks und Tail-Risiken.

### **11 – Liquiditätsanalyse der ProjectUSD-Handelspaare**  
Marktmikrostruktur, Arbitrage und Liquiditätsverhalten.

### **12 – Spieltheorie der ProjectUSD-Ökonomie**  
Strategische Anreize aller Akteursgruppen und Nash-Gleichgewichte.

### **13 – Dezentralitätsvergleich**  
Strukturelle Dezentralität vs. Governance-basierte Systeme.

### **14 – Effizienz von ProjectUSD auf PulseChain**  
Gas-Kosten, Skalierung und Performance-Vergleich zu Ethereum.

---

## Dateibenennung

Alle Dokumente folgen dem Schema:

- Study-XX-Kurztitel.de.md
- Study-XX-Kurztitel.md


Dies gewährleistet:

- klare Struktur  
- einfache Navigation  
- alphabetische Sortierung  
- SEO-optimierte URLs  
- hohe Lesbarkeit für Entwickler und Forscher

---

## Lizenz & Namensnutzung

**ProjectUSD** ist ein originäres Open-Source-Konzept, veröffentlicht von  
**Aqua75 / PulseChain Community Initiative**  
unter der Lizenz **Creative Commons BY-NC-SA 4.0**.

Diese Lizenz gilt für:

- Whitepaper  
- Forschungsstudien  
- Übersetzungen  
- Spezifikationen  
- Medieninhalte  
- Diagramme und begleitende Materialien  

in diesem Repository und seinen offiziellen Releases.

### **Verwendung des Namens „ProjectUSD“**

Implementierungen auf **PulseChain** müssen:

1. vollständig der offiziellen ProjectUSD-Spezifikation entsprechen, und  
2. den Konsolidierungsprozess durchlaufen  

um den Namen **„ProjectUSD“** verwenden zu dürfen.

Alle anderen Implementierungen – auf PulseChain oder anderswo – müssen klar als **unabhängige Forks** gekennzeichnet sein und eine sichtbare Attribution enthalten:

> Basierend auf dem „ProjectUSD“-Konzept von Aqua75 / PulseChain Community Initiative  
> https://github.com/Aqua75/ProjectUSD

Die unautorisierte Nutzung des Namens oder Logos außerhalb des PulseChain-Kontexts  
stellt einen Verstoß gegen die Lizenzbedingungen dar.

© 2025 Aqua75 – Alle Rechte vorbehalten für den Namen und das Logo **„ProjectUSD“**.

---

## Beitrag, Kontakt & weitere Ressourcen

Dieses Repository wird in kuratierter Form gepflegt.  
Externe Issues, Pull Requests oder Code-Beiträge sind nicht Teil des Workflows.

Für Feedback, Fragen, Diskussionen oder Anmerkungen  
nutze bitte die offizielle Community-Gruppe:

**Telegram (ProjectUSD Discussion Group)**  
https://t.me/ProjectUSD_Discussion

Dieser Kanal dient als zentrale Anlaufstelle für:

- Forschungsfragen  
- technische Klärungen  
- architektonische Diskussionen  
- Feedback zu Dokumenten oder Studien  

### Wichtige Dokumentation

- **Whitepaper (Englisch)**  
  `ProjectUSD.Whitepaper.V2.1.EN.Englisch.pdf`

- **Architektur & Modulspezifikationen**  
  `/Architecture/`

- **Developer Playbook**  
  `/Developer_Playbook/`

- **Forschungsstudien (Deutsch & Englisch)**  
  `/Studies/`

- **Artikel & Konzeptpapiere**  
  `/Articles/`
