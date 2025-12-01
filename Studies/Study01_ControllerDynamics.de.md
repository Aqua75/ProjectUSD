# Study 01 – Controller-Dynamik & Preisrückkopplung in ProjectUSD
Wissenschaftliche Analyse der algorithmischen Geldpolitik eines autonomen On-Chain-Systems

---

## Abstract

ProjectUSD ist ein vollständig on-chain operierendes, algorithmisches Geldsystem auf PulseChain. Die Stabilität des Stablecoins entsteht nicht durch externe Orakel, Banking-Backups oder Governance-Eingriffe, sondern durch die interne Rückkopplungsmechanik zwischen dem Marktpreis \(P\), dem Gleichgewichtspreis \(R\) und der Systemrate \(r\).

Diese Studie analysiert die mathematische Struktur und Stabilitätsdynamik des Controllers, der Preisabweichungen misst und über die Variable \(r\) Anreize für Schuldner und Sparer setzt. Ein formales Modell für die Abweichung  

$$
\varepsilon = \frac{P - R}{R}
$$  

bildet die Grundlage für eine proportionale Regelfunktion mit Deadband, Rate-Limiter und Obergrenzen.  

Theoretische Simulationsszenarien untersuchen Über- und Unterbewertung, starke Volatilität und niedrige Liquidität. Die Ergebnisse zeigen, dass ProjectUSD durch die Kombination aus Controller, Redemption-Engine und Stability Pool eine robuste Rückführung von \(P \rightarrow R\) ermöglichen kann, jedoch Verzögerungen, Orakel-Bias und Stressphasen berücksichtigt werden müssen.

---

# 1. Einleitung – Algorithmische Rückkopplung als Kernprinzip

ProjectUSD verfolgt das Ziel, eine autonome, selbstregulierende Recheneinheit für die PulseChain-Ökonomie bereitzustellen. Anstelle eines extern fixierten 1:1-Peg zu Fiat basiert das System auf:

- einem **internen Gleichgewichtspreis \(R\)**  
- einem **gehandelten Marktpreis \(P\)**  
- einer **algorithmenbasierten Systemrate \(r\)**  

Der Controller bildet das Herzstück dieser geldpolitischen Architektur. Er misst Preisabweichungen zwischen \(P\) und \(R\) und passt die Systemrate \(r\) an, wodurch sich Anreize für Verschuldung, Sparen, Arbitrage und Haltebereitschaft verschieben.

Der Rückkopplungspfad lautet:

1. DEX-Märkte bestimmen einen Spotpreis \(P\).  
2. Das on-chain Oracle ermittelt über Median-TWAP einen robusten Wert.  
3. Der Controller berechnet aus der Abweichung \(\varepsilon = (P-R)/R\) eine Anpassung \(\Delta r\).  
4. Die Veränderung der Systemrate beeinflusst Angebot, Nachfrage und Arbitrageströme.  
5. Diese ökonomischen Effekte wirken zurück auf den Marktpreis \(P\).  

Damit ersetzt ProjectUSD klassische, institutionelle Geldpolitik durch **deterministische, unveränderliche Logik**, die nach dem Freeze-Event nicht mehr modifiziert werden kann.

---

# 2. Systembeschreibung – Variablen und relevante Module

## 2.1 Relevante Komponenten

### Vaults  
Nutzer hinterlegen PLS als Sicherheit und prägen ProjectUSD. Sinkt die Besicherung unter die Mindestschwelle, erfolgt eine automatische Liquidation.

### Stability Pool  
Nutzer hinterlegen ProjectUSD, um Liquidationen abzufedern und PLS-Gewinne zu erhalten. Liquidierte Schulden werden aus dem Pool beglichen und der entsprechende ProjectUSD-Supply vernichtet.

### Redemption-Engine  
ProjectUSD kann jederzeit zum Gleichgewichtspreis \(R\) gegen PLS eingelöst werden. Arbitrageure nutzen Abweichungen zwischen \(P\) und \(R\), wodurch natürliche Reversionseffekte entstehen.

---

## 2.2 Zentrale Variablen

- \(R_t\): Gleichgewichtspreis in Periode \(t\)
- \(P_t\): Marktpreis laut Oracle (Median-TWAP)
- \(r_t\): Systemrate (Zins / Sparrate)
- \(\varepsilon_t\): Preisabweichung  

```math
\varepsilon_t = \frac{P_t - R_t}{R_t}
```

- \(\text{EpochLength}\): Anzahl Blöcke pro Regelschritt

---

## 2.3 Funktionsweise des Controllers

Die vorläufige Controller-Spezifikation folgt einer proportionalen Regelung:

### 1. Abweichung berechnen
```math
\varepsilon_t = \frac{P_t - R_t}{R_t}
```

### 2. Deadband prüfen
```math
|\varepsilon_t| < \varepsilon_{\text{db}} \Rightarrow \Delta r_t = 0
```

### 3. Proportionale Anpassung
```math
\Delta r_t = K_p \cdot \varepsilon_t
```

### 4. Rate-Limiter
```math
\Delta r_t^{\text{clamped}} =
\max\left(-\delta r_{\max}, \min(\delta r_{\max}, \Delta r_t)\right)
```

### 5. Neue Rate
```math
r_{t+1} = \text{clip}\big(r_t + \Delta r_t^{\text{clamped}}, 0, r_{\text{cap}}\big)
```

---

# 3. Mathematische Analyse

## 3.1 Preisabweichung

$$
\varepsilon_t = \frac{P_t - R_t}{R_t}
$$

Eine dimensionslose Größe, interpretierbar als prozentuale Über- oder Unterbewertung.

---

## 3.2 Dynamik des Reglers

$$
\Delta r_t =
\begin{cases}
0, & |\varepsilon_t| < \varepsilon_{\text{db}} \\
K_p \varepsilon_t, & \text{sonst}
\end{cases}
$$

$$
r_{t+1} = \text{clip}\big(r_t + \Delta r_t^{\text{clamped}}, 0, r_{\text{cap}}\big)
$$

---

## 3.3 Vereinfachtes lineares Modell

$$
\varepsilon_t \approx \alpha \cdot \frac{S_t - D_t}{D_t}
$$

$$
\Delta S_{t+1} \approx -\beta_s \Delta r_t,
\quad
\Delta D_{t+1} \approx +\beta_d \Delta r_t
$$

$$
\varepsilon_{t+1} \approx (1 - \kappa K_p)\varepsilon_t
$$

Stabilitätsbedingung:

$$
0 < \kappa K_p < 2
$$

---

# 4. Theoretische Simulationsszenarien

## 4.1 Moderate Überbewertung  
`[Diagramm 1: Pfad P → R bei ε = +1%]`

## 4.2 Moderate Unterbewertung  
`[Diagramm 2: Pfad P → R bei ε = -1%]`

## 4.3 Extreme Volatilität  
`[Diagramm 3: Verzögerung durch Oracle-TWAP bei hohen Schwankungen]`

## 4.4 Niedrige Liquidität  
`[Diagramm 4: Verhalten des Controllers bei STALE-Pools]`

---

# 5. Diskussion – Arbitrage, Psychologie & Reaktionszeit

## 5.1 Arbitrageure  

Operativer Transmissionsmechanismus des Pegrückwegs:

- \(P < R\): Kaufen, redeem, Gewinn in PLS  
- \(P > R\): Prägen, verkaufen, später tilgen  

## 5.2 Marktpsychologie  

- Vertrauen → stabilisierend  
- Zweifel → reflexiv und destabilisierend  

## 5.3 Zeitskalen  

- Sekunden–Minuten: Noise  
- Epochen: Controller  
- Wochen: strukturelle Reallokation

---

# 6. Risiken & Grenzen

- Verzögerungen durch Oracle und Epoch-Lag  
- Liquiditätsbias  
- Stressphasen und Liquidationskaskaden  
- Modellrisiken  
- psychologische Reflexivität  

---

# 7. Schlussfolgerung

Der Controller ist ein zentraler Baustein des autonomen Geldsystems von ProjectUSD. Seine Wirksamkeit ist hoch, jedoch abhängig von Liquidität, Arbitrageeffizienz und Oracle-Qualität. Die Kombination aus Controller, Redemption-Engine und Stability Pool bildet einen robusten, aber komplexen Rückkopplungskreis, dessen Parameter sorgfältig kalibriert und kontinuierlich überwacht werden müssen.

---

# 8. Next Steps

- SimKit-Framework aufbauen  
- Parameterraum für \(K_p\), \(\varepsilon_{\text{db}}\), \(\delta r_{\max}\) kalibrieren  
- Liquiditäts- und Schockmodelle testen  
- Messmetriken (PegDeviation, HalfLife, LimiterHit-Rate) definieren  
- nichtlineare AMM-Dynamiken ergänzen  

---

## 9. Verification

- Parameter-Validierung gegen Spezifikation  
- Formel-Konsistenzprüfung  
- Reproduktion der Szenarien in Simulation  
- Logik-Kohärenztest zwischen Controller, Oracle, Redemption, Stability Pool  
- Stabilitätsanalyse gemäß:

```math
0 < \kappa K_p < 2
```
