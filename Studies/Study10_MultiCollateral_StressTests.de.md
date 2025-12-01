# Study 10 – Multi-Collateral-Stresstests für ProjectUSD
*Analyse systemischer Risiken, Korrelationseffekte und Ausfallmechanismen bei verschiedenen Besicherungsmodellen*  
*(Level-3 Research Format)*

---

## Abstract

ProjectUSD ist als reines PLS-basiertes System konzipiert, kann jedoch in späteren Entwicklungsphasen theoretisch um zusätzliche Collateral-Typen erweitert werden.  
Die Frage, ob und unter welchen Bedingungen ein Multi-Collateral-System stabil betrieben werden kann, ist zentral für die langfristige Evolutionsfähigkeit des Protokolls.

Diese Studie untersucht:

- systemische Risiken von Multi-Collateral-Designs,  
- Korrelationseffekte zwischen Collateral-Assets,  
- Liquidationsdynamiken in Cross-Collateral-Architekturen,  
- Stress-Propagation (Ausbreitung von Schocks),  
- Worst-Case-Szenarien,  
- und ob ProjectUSD unter Multi-Collateral-Bedingungen strukturell stabil bleibt.

Das Ergebnis zeigt:  
Ein Multi-Collateral-Modell ist **nur unter strengen Bedingungen** kompatibel mit dem Sicherheitsprofil von ProjectUSD.  
Insbesondere muss gewährleistet sein, dass **keine Death-Spiral-Mechanismen**, **keine Oracle-Angriffsflächen** und **keine Korrelationseffekte** entstehen, die das Kernsystem gefährden.

---

# 1. Einleitung – Warum Multi-Collateral ein Risiko darstellt

Viele Stablecoins erlauben multiple Collateral-Typen, um die Flexibilität zu erhöhen (z. B. DAI).  
Doch dies erzeugt zusätzliche Risiken:

- unterschiedliche Volatilität,  
- unterschiedliche Liquiditätsprofile,  
- Abhängigkeit von mehreren Orakeln,  
- potenzielle Cross-Asset-Kaskaden,  
- unklare Stressreaktionen.

ProjectUSD wurde ursprünglich **bewusst als Single-Collateral-System (PLS)** entworfen,  
weil dadurch zentrale Risiken eliminiert werden:

- keine Cross-Asset-Korrelationen,  
- kein Oracle-Mix,  
- konsistente Liquidationsmechanik,  
- homogener Risikoparameter,  
- hohe Vorhersagbarkeit bei Stress.

Diese Studie untersucht, ob und unter welchen Bedingungen eine Multi-Collateral-Architektur technisch, ökonomisch und sicher realisierbar wäre.

---

# 2. Definitionen und Systemkomponenten

## 2.1 Basissystem (Single Collateral: PLS)
ProjectUSD basiert auf:

- PLS-Vaults,  
- Stability-Pool-Liquidationen,  
- Redemption gegen PLS,  
- r-gesteuerte Dynamik,  
- Surplus-Puffer zur Langzeitstabilität.

Im Single-Collateral-Modell ist die Risikoanalyse eindeutig und monodimensional.

---

## 2.2 Multi-Collateral-Erweiterung (hypothetisch)

Zusätzliche Collateral-Typen könnten sein:

- wPLS-Derivate,  
- Liquid-Staking-Tokens (LSTs),  
- PulseX-LP-Token,  
- externe Assets via Bridge (weniger wahrscheinlich),  
- andere PulseChain-Native Assets.

Jedes Asset bringt einen eigenen Risikoprozess mit:

- eigene Volatilität  
- eigene Liquidität  
- eigene Orakelquellen  
- eigene Korrelationen  

Diese Heterogenität erhöht die Komplexität nicht linear, sondern **exponentiell**.

---

# 3. Risikotypen bei Multi-Collateral-Designs

## 3.1 Volatilitätsrisiko
Jedes Asset besitzt:

- unterschiedliche Schwankungsbreiten,  
- unterschiedliche Tail-Risiken,  
- unterschiedliche Mean-Reversion-Profile.

Ein Multi-Collateral-System lässt Stresstransfers zwischen Volatilitätsclustern zu.

---

## 3.2 Korrelationsstruktur

Hauptproblem:  
**Korrelation ≠ Stabilität.**  
Collateral-Typen können in Krisen plötzlich stark korrelieren.

Beispiel:

- Asset A und B sind in normalen Zeiten unkorreliert,  
- in Stressphasen aber beide von Marktpanik betroffen,  
- gleichzeitig fallen → Liquidationswellen verstärken sich.

Das führt zu **Kaskaden**, die das Single-System nicht kennt.

---

## 3.3 Oracle-Risiken

Jeder zusätzliche Collateral-Typ benötigt:

- eigenes Preisfeed-Design  
- eigene TWAP-Fenster  
- eigene Median-Struktur  
- eigene Outlier-Filter  

Mehr Orakel = mehr Angriffsfläche.

---

## 3.4 Liquiditätsrisiko

Ein Collateral-Asset kann in hoher Volatilität:

- illiquide werden,  
- Spread-Verluste erzeugen,  
- zu verzögerten Liquidationen führen.

Dies führt zu **Alpha-Verlust**, den der Stability Pool absorbieren muss.

---

## 3.5 Komplexitätsrisiko

Mehr Assets →  
mehr Parameter →  
mehr Fehlermodi →  
mehr mögliche Black-Swan-Szenarien.

---

# 4. Liquidationsdynamik bei Multi-Collateral

## 4.1 Single-Collateral-Vorteil

Im Single-Collateral-Modell gilt:

- Liquidationen sind homogen  
- Stability Pool kennt das Risiko  
- Surplus-Puffer kann vorhersehbar wachsen  
- Redemption-Mechanik bleibt konsistent

---

## 4.2 Multi-Collateral-Herausforderung

Mit mehreren Assets entstehen:

- Cross-Collateral-Liquidationen  
- Value-Mismatch-Risiken  
- Collateral-Bias im Stability Pool  
- unbalancierte Exposure-Strukturen

Worst-Case:  
Ein volatiles Asset wird liquidiert und destabilisiert den Stability Pool.

---

## 4.3 Gewichtete Liquidationen

Eine theoretisch mögliche Lösung:

- Stability Pool erhält Collateral proportional zur Risikoqualität  
- risikoreiche Assets werden höher rabattiert  
- der Puffer schützt vor Fehlbewertungen

Doch jede Gewichtungsmethode erzeugt systemische Angriffsflächen.

---

# 5. Stresstests: Szenarien für Multi-Collateral-Risiken

## 5.1 Szenario A – Korrelationsschock
Zwei bisher unkorrelierte Assets fallen gleichzeitig stark.

Ergebnis:

- doppelte Liquidationswelle  
- Stability Pool erhält gemischtes Collateral  
- Puffer muss unerwartete Verluste absorbieren  
- Systemzyklen werden instabiler

---

## 5.2 Szenario B – Oracle-Manipulation eines Collaterals
Ein Manipulationsangriff auf Asset B führt zu:

- Fehlbewertung  
- falscher Liquidationsauslösung  
- systemischen Verlusten  
- Vertrauensschwund  
- potenziellen r-Fehlimpulsen

---

## 5.3 Szenario C – Illiquides Collateral
Ein Asset bricht ein und verliert Liquidität.

Konsequenzen:

- Liquidationen werden unprofitabel  
- Stability Pool sammelt toxisches Collateral  
- Surplus-Puffer wird besser belastet  
- Redemption wird komplexer

---

## 5.4 Szenario D – Bridge-Ausfall bei externen Assets
Wenn Collateral von externen Chains stammt:

- Bridge-Risiko  
- potenzieller Totalverlust  
- Oracle-Desync  
- unklare Einlösbarkeit

Solche Risiken sind **inkompatibel** mit ProjectUSD-Philosophie.

---

# 6. Systemische Bewertung: Kann Multi-Collateral sicher sein?

## 6.1 Vorteile einer Multi-Collateral-Struktur
- breitere Risikostreuung  
- theoretisch höhere Kapitalbasis  
- mehr Vault-Nutzer  
- robustere Auslastung bei Einzelasset-Shock

---

## 6.2 Nachteile (überwiegen derzeit)
- exponentiell höhere Komplexität  
- neue Failure Modes  
- höhere Oracle-Abhängigkeit  
- schlechter vorhersagbare Liquidationsmechanik  
- instabile Redemption-Rückkopplung  
- Belastung für Stability Pool und Surplus Buffer

---

## 6.3 Kernergebnis
Ein Multi-Collateral-System kann **funktionieren**,  
aber nur unter extrem strengen Bedingungen:

- identische Sicherheitsprofile der Assets  
- robuste On-Chain-Oracle-Struktur  
- garantierte Liquidität  
- starke Isolation problematischer Assets  
- harte Caps pro Collateral-Typ  
- algorithmische Gewichtung  
- hohe Pufferkapazität  

Ohne diese Sicherheitsmechanismen steigt das systemische Risiko enorm.

---

# 7. Empfehlung: Phasenbasierter Ansatz für Multi-Collateral-Erweiterung

ProjectUSD sollte Multi-Collateral **nicht** früh einführen.  
Stattdessen:

## Phase 1 – Reines PLS-System (maximal stabil)
- höchste Vorhersehbarkeit  
- minimale Risikofläche  
- ideale Lernbasis für Controller, Oracle, Redemption

## Phase 2 – Erweiterung um sehr ähnliche Assets
Beispiele:

- wPLS  
- Staking-Derivate (wenn sicher)

Diese Assets sind *nahezu identisch* zu PLS.

## Phase 3 – Algorithmisch streng limitierte weitere Assets
Nur mit:

- Hard Caps  
- dynamischer Risikobewertung  
- separaten Liquidationspools  
- isolierten Orakelstrukturen  

---

# 8. Schlussfolgerung

Multi-Collateral-Designs sind mächtig, aber gefährlich.  
Sie erhöhen:

- Komplexität  
- Korrelation  
- Angriffsflächen  
- Liquidationsrisiken  
- Orakelabhängigkeit  
- systemische Fragilität  

Für ProjectUSD gilt:

> **Ein Single-Collateral-Modell ist strukturell am sichersten.  
> Multi-Collateral ist nur unter strengen Risikobedingungen tragfähig.**

Eine spätere Erweiterung ist möglich, aber nur mit:

- isolierten Risiken,  
- gesicherten Orakeln,  
- starken Puffern,  
- algorithmischer Kontrolle,  
- minimaler Komplexität.

---

# 9. Verification

> ## 📘 Prüfkriterien für Reviewer
- Sind alle Risikotypen korrekt identifiziert?  
- Sind Multi-Collateral-Failure Modes vollständig beschrieben?  
- Ist die Liquidationsdynamik korrekt dargestellt?  
- Ist die Empfehlung logisch begründet?  
- Sind Stresstests realistisch modelliert?  

Diese Studie bildet die Grundlage für fortgeschrittene Sicherheitsdesigns und zukünftige Multi-Asset-Forschung innerhalb von ProjectUSD.
