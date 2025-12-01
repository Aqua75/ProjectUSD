# Study 01 – Controller-Dynamik & Preisrückkopplung in ProjectUSD
*Wissenschaftliche Analyse der algorithmischen Geldpolitik eines autonomen On-Chain-Systems*  
*(Level-3 Research Format)*

---

## Abstract

ProjectUSD ist ein vollständig on-chain operierendes, algorithmisches Geldsystem auf PulseChain. Die Preisstabilität entsteht nicht durch externe Orakel, Banken oder Governance-Eingriffe, sondern durch einen **internen Rückkopplungskreis** zwischen:

- dem Marktpreis P  
- dem Gleichgewichtspreis R  
- der Systemrate r  

Diese Studie analysiert die mathematische Struktur dieses Controllers, der Abweichungen zwischen Markt- und Gleichgewichtspreis misst und über r die ökonomischen Anreize von Schuldnern, Haltern und Arbitrageuren beeinflusst.

Wir entwickeln ein formales Modell für die Preisabweichung, leiten Konvergenzbedingungen ab und diskutieren vier Szenarien: Überbewertung, Unterbewertung, extreme Volatilität und niedrige Liquidität.

---

# 1. Einleitung – Algorithmische Rückkopplung statt zentraler Steuerung

ProjectUSD ersetzt klassische Zentralbankmechanismen durch **deterministische, unveränderliche Logik**.

Der Regelkreis:

1. DEX-Märkte bilden den Spotpreis P.  
2. Das Oracle ermittelt via Median-TWAP einen geglätteten Wert.  
3. Der Controller berechnet die Abweichung zwischen P und R.  
4. Die Systemrate r wird angepasst.  
5. Die Änderung von r beeinflusst Angebot, Nachfrage und Arbitrage.  
6. Diese Kräfte bewegen P wieder in Richtung R.

---

# 2. Systembeschreibung

## 2.1 Kernelemente von ProjectUSD

### Vaults
- Nutzer hinterlegen PLS als Sicherheit  
- prägen ProjectUSD  
- Unterbesicherung führt zu Liquidation

### Stability Pool
- fängt Liquidationen ab  
- vernichtet ProjectUSD-Supply  
- verteilt PLS-Gewinne

### Redemption Engine
- Einlösung von ProjectUSD zu R  
- arbitragebasierter Preisanker  
- reduziert die schwächsten Vaults

---

## 2.2 Definition zentraler Variablen

- **Rₜ** – Gleichgewichtspreis  
- **Pₜ** – Marktpreis laut Oracle  
- **rₜ** – Systemrate  
- **εₜ** – relative Preisabweichung  

$$
\varepsilon_t = \frac{P_t - R_t}{R_t}
$$

- **EpochLength** – Anzahl Blöcke pro Regelschritt

---

## 2.3 Der Controller als Regler

> ## 📘 Definition – Reglerlogik  
> Der Controller übersetzt Preisabweichungen in Anpassungen von r, um P wieder an R anzunähern.

### 1. Preisabweichung

$$
\varepsilon_t = \frac{P_t - R_t}{R_t}
$$

### 2. Deadband

$$
|\varepsilon_t| < \varepsilon_{\text{db}} \Rightarrow \Delta r_t = 0
$$

### 3. Proportionale Anpassung

$$
\Delta r_t = K_p \cdot \varepsilon_t
$$

### 4. Rate-Limiter

$$
\Delta r_t^{\text{clamped}} =
\max\left(-\delta r_{\max}, \min(\delta r_{\max}, \Delta r_t)\right)
$$

### 5. Neue Systemrate

$$
r_{t+1} = \text{clip}\big(r_t + \Delta r_t^{\text{clamped}}, 0, r_{\text{cap}}\big)
$$

---

# 3. Mathematische Herleitung

## 3.1 Preisabweichung

> 📘 **Definition – Relative Peg-Abweichung**

$$
\varepsilon_t = \frac{P_t - R_t}{R_t}
$$

---

## 3.2 Proportionale Regelfunktion

$$
\Delta r_t =
\begin{cases}
0, & |\varepsilon_t| < \varepsilon_{\text{db}} \\
K_p \varepsilon_t, & \text{sonst}
\end{cases}
$$

---

## 3.3 Einfaches dynamisches Modell

> 📘 **Modell – Lineare Preisapproximation**

Preisabweichung in Abhängigkeit von Angebot Sₜ und Nachfrage Dₜ:

$$
\varepsilon_t \approx \alpha \cdot \frac{S_t - D_t}{D_t}
$$

Einfluss der Rate auf Angebot und Nachfrage:

$$
\Delta S_{t+1} \approx -\beta_s \Delta r_t
$$

$$
\Delta D_{t+1} \approx +\beta_d \Delta r_t
$$

Lineare Rekursion der Abweichung:

$$
\varepsilon_{t+1} \approx (1 - \kappa K_p)\varepsilon_t
$$

> 📘 **Theorem – Konvergenzbedingung**  
> Der Controller stabilisiert das System genau dann, wenn gilt:
>
> $$
> 0 < \kappa K_p < 2
> $$

---

# 4. Simulationsszenarien

## 📊 Szenario 1 – Überbewertung (P > R)

Wenn der Marktpreis oberhalb des Gleichgewichtspreises liegt:

- r steigt  
- Neuverschuldung wird unattraktiver  
- Prägung und Verkauf von ProjectUSD nimmt zu  
- P fällt graduell zurück in Richtung R  

Dieses Szenario beschreibt eine kontrollierte Abwärtskonvergenz des Marktpreises hin zum internen Gleichgewichtswert.

---

## 📊 Szenario 2 – Unterbewertung (P < R)

Wenn der Marktpreis unter dem Gleichgewichtspreis liegt:

- r sinkt  
- Redemption-Arbitrage erzeugt zusätzliche Nachfrage  
- P steigt in Richtung R  

Dieses Szenario beschreibt eine Aufwärtsbewegung, getrieben durch arbitragebasierte Nachfrage und reduzierten ökonomischen Druck auf Schuldner.

---

## 📊 Szenario 3 – Extreme Volatilität

Bei kurzfristigen Marktverwerfungen oder starken Preisschwankungen:

- das Oracle (Median-TWAP) glättet Schocks  
- der Controller reagiert bewusst verzögert, um Übersteuerung zu vermeiden  
- Arbitrage korrigiert schnelle, nicht nachhaltige Ausschläge  

Dieses Szenario beleuchtet das Zusammenspiel zwischen geglätteten Daten, verzögerter Regellogik und schneller Marktreaktion.

---

## 📊 Szenario 4 – Niedrige Liquidität

In illiquiden oder manipulierten Marktphasen:

- illiquide oder auffällige Pools werden gefiltert  
- der Controller kann seine Aktivität temporär einschränken  
- Redemption fungiert als robuste Hauptstabilisierungsquelle  

Dieses Szenario zeigt, wie das System in Phasen geringer Marktverlässlichkeit auf die internen Mechanismen der Wertdefinition zurückgreift.

---

# 5. Diskussion

## 5.1 Arbitrage als Transmissionsmechanismus

Arbitrageure sind die ökonomischen Akteure, die die Logik des Controllers in Markttransaktionen übersetzen:

- **P < R:**  
  Kaufen von ProjectUSD an der DEX, Redemption zu R, Realisierung eines Profits in PLS → P steigt.

- **P > R:**  
  Prägung neuer ProjectUSD gegen Collateral, Verkauf über dem Gleichgewichtspreis, späteres Tilgen → P fällt.

---

## 5.2 Marktpsychologie

> 📘 **Beobachtung – Erwartungen als Verstärker**

- Vertrauen in die Mechanik → stabilisierend  
- Zweifel an Reaktionsgeschwindigkeit oder Robustheit → reflexiv, destabilisierend  

Kommunizierte Kennzahlen wie durchschnittliche Peg-Abweichung und Halbwertszeit der Rückführung können Vertrauen messbar machen.

---

## 5.3 Reaktionszeiten

- **Sekunden–Minuten:** DEX-Noise, kurzfristige Volatilität  
- **Epochen-Skala:** Anpassung der Systemrate r  
- **Tage–Wochen:** strukturelle Reallokation von Schulden, Collateral und Stability-Pool-Positionen  

---

# 6. Grenzen & Risiken

## 6.1 Verzögerungen

- Oracle-Lag (TWAP-Fenster)  
- Regel-Lag (Epochenlänge)  
- Behavioral-Lag (Reaktionszeit der Nutzer)

## 6.2 Orakel-Bias

- Liquiditätsbias (Preis dominiert von einem Pool)  
- STALE-Daten bei illiquiden Paaren  
- Notwendigkeit von Filter- und Sicherungslogiken

## 6.3 Stressphasen

- Liquidationswellen bei starken PLS-Crashs  
- temporäre Dominanz von Liquidationen über normale Marktaktivität  
- r-Limiter, die die Anpassungsgeschwindigkeit deckeln

## 6.4 Parameterrisiko

- Kₚ zu hoch → Oszillationen  
- Kₚ zu niedrig → träge Rückführung  
- schlechte Kombination mit EpochLength → unerwartete Dynamik

## 6.5 Psychologische Risiken

- Übervertrauen („System fängt alles ab“)  
- Panik („System kollabiert bei Stress“)  

Beides kann Marktreaktionen verstärken, die über die mathematische Logik hinausgehen.

---

# 7. Schlussfolgerung

Der Controller ist ein zentraler Baustein im autonomen Stabilitätsmechanismus von ProjectUSD. Er misst Preisabweichungen zwischen P und R und übersetzt sie in Anpassungen der Systemrate r, die wiederum das Verhalten von Schuldnern, Sparern und Arbitrageuren beeinflusst.

In Kombination mit:

- der Redemption Engine  
- dem Stability Pool  
- der Oracle-Architektur  

entsteht ein geschlossener Rückkopplungspfad, der darauf ausgelegt ist, P immer wieder in die Nähe von R zurückzuführen. Die Stabilität hängt jedoch maßgeblich von sorgfältig gewählten Parametern, ausreichender Liquidität und der Effizienz der Arbitrage ab.

---

# 8. Next Steps

- Aufbau eines dedizierten Simulationsframeworks (SimKit)  
- systematische Schocksimulationen (Preiscrash, Liquiditätsschocks, Orakel-Fehler)  
- Kalibrierung der Parameter Kₚ, ε_db, δr_max und EpochLength  
- Definition und Messung von Kennzahlen wie PegDeviation, HalfLife(P → R) und LimiterHit-Rate  
- Erweiterung der Modelle um nichtlineare AMM-Dynamiken und realistische Orderflow-Profile  

---

# 9. Verification

> 📘 **Prüfkriterien für Reviewer**

- Konsistenz von Symbolen und Parametern gegenüber der offiziellen Spezifikation  
- formale Überprüfung der Herleitung der Konvergenzbedingung  
- Reproduktion der beschriebenen Szenarien im Simulationsframework  
- Prüfung der Kohärenz des Regelkreises (Controller ↔ Oracle ↔ Redemption ↔ Stability Pool)  
- Validierung, dass für praxisnahe Parameterbereiche tatsächlich gilt:

$$
0 < \kappa K_p < 2
$$
