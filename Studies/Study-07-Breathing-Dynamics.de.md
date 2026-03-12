# Study 07 – Die Atmungsdynamik von ProjectUSD: Wie r-Anpassung Marktvolatilität absorbiert
*Analyse der dynamischen Preisstabilität durch Controller-Logik, Arbitrage und Angebots-/Nachfrageeffekte*  
*(Level-3 Research Format)*

---

## Abstract

ProjectUSD ist ein vollständig on-chain operierendes, autonom reguliertes Geldsystem auf PulseChain.  
Im Gegensatz zu fiatgedeckten Stablecoins beruht seine Stabilität nicht auf externen Sicherheiten, sondern auf einer **dynamischen Regelung**, die Preisabweichungen misst und über die Systemrate **r** wirtschaftliche Gegenkräfte aktiviert.

Diese Studie untersucht die sogenannte **Atmungsdynamik** des Systems:  
Wie Preisabweichungen (ε = (P − R) / R), Controller-Reaktionen (Δr), Arbitrage über Redemption und Angebots-/Nachfrageeffekte gemeinsam Volatilität absorbieren.  
Wir modellieren die Regelkreise, analysieren stressabhängiges Verhalten und identifizieren Grenzen sowie Bedingungen für Systemstabilität.

---

# 1. Einleitung – Bedeutung dynamischer Stabilität

## 1.1 Motivation

Klassische Stablecoins stabilisieren ihren Marktpreis über externe Sicherheiten, Banken oder institutionelle Garantien.  
Ihre Stabilität ist „geliehen“ – abhängig von Fiat, Regulierung und zentraler Infrastruktur.

ProjectUSD verfolgt einen anderen Ansatz:

- keine Bindung an USD  
- keine Banken  
- keine Off-Chain-Orakel  
- keine Governance über den Kern  

Stattdessen entsteht Stabilität durch **Rückkopplung**: Das System misst Preisabweichungen und steuert ökonomische Anreize, die den Markt zum Gleichgewicht zurückführen.

---

## 1.2 Dynamische vs. statische Stabilität

**Statische Stabilität**  
– Preis bleibt nahezu fix um einen Zielwert.  
– Erfordert harte Pegs oder zentrale Garantien.

**Dynamische Stabilität**  
– Preis darf schwanken, aber das System erzeugt kontrollierende Gegenkräfte.  
– Verhalten ähnelt einem gedämpften Oszillator.

ProjectUSD stellt bewusst auf dynamische Stabilität ab:

- R = interner Gleichgewichtspreis  
- P = Median-TWAP-Marktpreis  
- ε = relative Preisabweichung  
- r = Systemrate, die Angebot und Nachfrage beeinflusst

---

## 1.3 Forschungsfrage

> Wie absorbiert ProjectUSD Marktvolatilität durch r-Anpassungen, Arbitrage und Redemption – und unter welchen Bedingungen versagt diese Atmungsmechanik?

Die Studie untersucht:

- Modellierung des Regelkreises  
- Verhalten bei niedriger und hoher Marktvolatilität  
- Interaktion zwischen Controller, Supply und Arbitrage  
- Systemische Grenzen und Failure Modes  

---

# 2. Modell: Preisabweichungen & r-Reaktionskurven

## 2.1 Grundvariablen

- **R** – Gleichgewichtspreis (Redemption-Preis)  
- **P** – Marktpreis (Median-TWAP)  
- **ε** – relative Preisabweichung:  
  $$\varepsilon_t = \frac{P_t - R}{R}$$  
- **r** – Systemrate je Epoche  
- **t** – Zeit in Epochen  

---

## 2.2 Oracle-Modell: Glättung vor der Regelung

Das Oracle nutzt:

- mehrere DEX-Pools  
- Liquiditätsgewichtung  
- TWAP-Berechnungen  
- Medianfilter  
- Outlier-Filter  
- STALE-Schutzmechanismen

Finaler Marktpreis:

$$
P = \text{median}(P_{\text{twap},1}, \dots, P_{\text{twap},n})
$$

Das Oracle liefert ein **geglättetes, manipulationsresistentes** Signal.

---

## 2.3 Controller-Logik: ε → r

Die relative Abweichung:

$$
\varepsilon_t = \frac{P_t - R}{R}
$$

Wenn |ε| innerhalb des Deadbands liegt → r bleibt unverändert.

Außerhalb:

$$
\Delta r_t = K_p \cdot \varepsilon_t
$$

mit Begrenzung:

$$
\Delta r_t = \text{clamp}(\Delta r_t,\ -\delta r_{\max},\ +\delta r_{\max})
$$

Neue Systemrate:

$$
r_{t+1} = clamp(r_t + Δr_t, 0, r_{cap})
$$

Interpretation:

- **ε > 0 (P > R)** → r steigt → Emission sinkt → P fällt  
- **ε < 0 (P < R)** → r sinkt → Nachfrage steigt → P steigt  

---

## 2.4 Angebots- und Nachfragefunktionen

Qualitative Näherungen:

**Emission:**

$$
E(r) \approx E_0 - \alpha_r (r - r_0)
$$

**Nachfrage:**

$$
D(r) \approx D_0 + \beta_r (-r)
$$

**Preiswirkung durch Gesamtmenge Q:**

$$
P(Q) \approx P^* - \gamma (Q - Q^*)
$$

Damit wirkt r indirekt über Angebots- und Nachfrageverschiebungen auf den Preis zurück.

---

## 2.5 Lokale Stabilitätsanalyse

Für kleine Kₚ und moderate Preisänderungskoeffizienten gilt:

$$
r_{t+1} = clamp(r_t + K_p · ε_t, 0, r_{cap})
$$

$$
P_{t+1} = P^* - c(r_t - r^*) + u_t
$$

Die Eigenwertanalyse ergibt:

- gedämpfte Oszillationen möglich  
- Monotone Konvergenz bei geeigneten Parametern  
- Stabilität abhängig von: Kₚ, Deadband, δr_max, Arbitrage, Oracle-Glättung  

---

# 3. Dynamik in volatilen Märkten

## 3.1 Arbitrage & Redemption als schnelle Korrekturkraft

**P < R:**

- Arbitrageure kaufen ProjectUSD  
- Redeem zu R  
- Supply sinkt  
- P steigt in Richtung R  

**P > R:**

- Prägung (sofern r dies zulässt)  
- Verkauf über Markt  
- Angebot wächst → P fällt  

Arbitrage ist der **schnelle Mechanismus**,  
der Controller die **langsame, systemische Komponente**.

---

## 3.2 Oracle als Volatilitätsfilter

TWAP + Median:

- dämpfen Preisrauschen  
- verhindern Überreaktion  
- filtern Manipulation  
- erzeugen ein stabiles Eingangssignal für den Controller

---

## 3.3 r als Schockabsorber bei PLS-Volatilität

Da ProjectUSD **in PLS** bewertet wird, wirken externe USD-Preisbewegungen nicht direkt destabiliserend.

Bei starkem PLS-Preisverfall:

1. Liquidationen → Stability Pool erhält Collateral  
2. ProjectUSD-Supply sinkt  
3. kurzfristiger Abwärtsdruck auf P  
4. ε < 0 → r wird gesenkt  
5. Nachfrage steigt → P stabilisiert sich

---

# 4. Szenarien: Niedriger, mittlerer und hoher Stress

## 4.1 Niedriger Stress

- kleine Preisabweichungen  
- schnelle Arbitrage  
- r bleibt stabil oder bewegt sich nur leicht  
- P verbleibt eng um R  

---

## 4.2 Mittlerer Stress (z. B. Intraday-Volatilität)

- ε schwankt moderat  
- r passt sich über mehrere Epochen an  
- leichte Oszillationen möglich  
- Redemption glättet Abweichungen nach unten  

---

## 4.3 Hoher Stress (PLS-Crash, Marktpanik)

Ablauf:

1. Liquidationswellen  
2. Supply sinkt  
3. P fällt kurzfristig  
4. Arbitrage setzt ein  
5. r wird massiv gesenkt  
6. P nähert sich wieder R an  

So entsteht ein **endogener Dämpfungsmechanismus**, der Schocks absorbiert.

---

# 5. Analyse der Atmungsmechanik

## 5.1 Expansion (Einatmen)

Wenn P < R → ε < 0:

- r sinkt  
- Schuldenaufnahme wird attraktiver  
- Nachfrage steigt  
- Redemption reduziert Supply  
- P bewegt sich nach oben Richtung R

---

## 5.2 Kontraktion (Ausatmen)

Wenn P > R → ε > 0:

- r steigt  
- Emission wird teurer  
- Nachfrage sinkt  
- Angebot wächst langsamer  
- P bewegt sich nach unten Richtung R

---

## 5.3 Rolle von Deadband & RateLimiter

Deadband:

- verhindert Überreaktion auf Mikrovolatilität  

RateLimiter:

- begrenzt maximale r-Änderungen  
- schützt vor reflexiver Instabilität  
- erzeugt „sanftes Atmen“ statt abruptem Verhalten

---

## 5.4 Surplus-Puffer als langfristige Stabilisierung

Der Surplus-Puffer:

- speichert Gebühren  
- stärkt langfristig die Protokollsolvenz
- erhöht die Widerstandsfähigkeit des Systems in längeren Stressphasen
- wirkt als langfristiger Energiespeicher des Systems  

---

# 6. Grenzen & Risiken

## 6.1 Technische Risiken
- Smart-Contract-Risiken  
- STALE-Oracle → r friert temporär ein  
- Verlässlichkeit der PulseChain-Infrastruktur  

## 6.2 Ökonomische Risiken
- geringe DEX-Liquidität → träge Arbitrage  
- Marktpanik kann Controller-Signale überlagern  
- Parameterwahl (Kₚ, δr_max) entscheidend

## 6.3 Offene Designfragen
- optimale r-Spannbreite  
- langfristige r-Niveaus  
- Interaktion mit späteren PSM/AMO-Modulen  

---

# 7. Schlussfolgerung

ProjectUSD stabilisiert sich nicht durch starre Fixierung, sondern durch ein **atmendes**, dynamisches Gleichgewicht.  
Die Preisabweichung ε, die Controller-Reaktion Δr, Arbitrage und Redemption bilden einen geschlossenen Regelkreis, der:

- Schocks absorbiert  
- Gleichgewicht wiederherstellt  
- systemische Stabilität erzeugt  

Diese Atmungsdynamik macht ProjectUSD zu einem **adaptiven, selbststabilisierenden Geldsystem**, das ohne externe Orakel, Banken oder Governance funktioniert.

---

# 8. Verification

> ## 📘 Prüfkriterien für Reviewer
- Wird die korrekte Formel für ε verwendet?  
- Ist die Controller-Kopplung ε → r korrekt dargestellt?  
- Sind Supply- und Nachfrageeffekte konsistent modelliert?  
- Sind Stabilitätsannahmen realistisch?  
- Ist die Atmungsmechanik vollständig und logisch beschrieben?  

Dieses Dokument bildet die Grundlage für weitere Forschung zur Systemdynamik, Parameteroptimierung und Simulation von Stressszenarien.
