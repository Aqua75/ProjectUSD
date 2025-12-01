# Study 07 – Die Atmungsdynamik von ProjectUSD: Wie r-Anpassung Marktvolatilität absorbiert
*Analyse der dynamischen Preisstabilität durch Controller-Logik, Arbitrage und Angebots-/Nachfrageeffekte*  
*(Level-3 Research Format)*

---

## Abstract

ProjectUSD ist ein vollständig on-chain operierendes, autonom reguliertes Geldsystem auf PulseChain.  
Im Gegensatz zu fiatgedeckten Stablecoins beruht seine Stabilität nicht auf externen Sicherheiten, sondern auf einer **dynamischen Regelung**, die Preisabweichungen misst und über die Systemrate **r** wirtschaftliche Gegenkräfte aktiviert.

Diese Studie untersucht die sogenannte **Atmungsdynamik** des Systems:  
Wie Preisabweichungen (ε = P − R), Controller-Reaktionen (Δr), Arbitrage über Redemption und Angebot/Nachfrage-Effekte gemeinsam Volatilität absorbieren.  
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
- ε = P − R  
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

Wir verwenden die definitorischen Größen aus Whitepaper und ControllerSPEC:

- **R** – Gleichgewichtspreis (Redemption-Preis)  
- **P** – Marktpreis (Median-TWAP)  
- **ε = P − R** – Preisabweichung  
- **r** – Systemrate je Epoche  
- **t** – Zeit in Epochen  

Der Controller berechnet aus εₜ die neue Systemrate rₜ₊₁.

---

## 2.2 Oracle-Modell: Glättung vor der Regelung

Das Oracle besteht aus:

- mehreren DEX-Pools  
- Liquiditätsgewichtung  
- TWAP-Berechnung pro Pool  
- Medianbildung  
- Outlier-Filter  
- STALE-Mechanismen

Der endgültige Marktpreis:

$$
P = \text{median}(P_{\text{twap},1}, \dots, P_{\text{twap},n})
$$

Das Oracle liefert ein **gefiltertes, langsam reagierendes** Preissignal, damit der Controller nicht auf Rauschen reagiert.

---

## 2.3 Controller-Logik: ε → r

Preisabweichung:

$$
\varepsilon_t = P_t - R
$$

Wenn die relative Abweichung innerhalb des Deadbands liegt, bleibt r konstant.

Sonst:

$$
\Delta r_t = K_p \cdot \frac{\varepsilon_t}{R}
$$

mit Begrenzung:

$$
\Delta r_t = \text{clamp}(\Delta r_t,\ -\delta r_{\max},\ +\delta r_{\max})
$$

und Aktualisierung:

$$
r_{t+1} = r_t + \Delta r_t
$$

Interpretation:

- **P > R → r steigt** → Schulden werden teurer → Emission sinkt → P fällt  
- **P < R → r sinkt** → Schulden werden billiger → Nachfrage steigt → P steigt  

---

## 2.4 Angebot und Nachfrage als Funktionen von r

Linearisierte qualitative Beziehungen:

**Emission:**

$$
E(r) \approx E_0 - \alpha_r (r - r_0)
$$

**Nachfrage:**

$$
D(r) \approx D_0 - \beta_r (r - r_0)
$$

**Marktpreisreaktion:**

$$
P(Q) \approx P^* - \gamma (Q - Q^*)
$$

Damit wirkt r indirekt über Angebots- und Nachfrageverschiebungen auf den Preis zurück.

---

## 2.5 Lokale Stabilitätsanalyse

Für kleine Kₚ und moderate Preisempfindlichkeit c gilt:

$$
r_{t+1} = r_t + K_p'(P_t - R)
$$

$$
P_{t+1} = P^* - c(r_t - r^*) + u_t
$$

Eigenwertanalyse zeigt:

- System ist lokal stabil  
- zeigt gedämpfte Oszillationen  
- nähert sich monoton dem Gleichgewicht an  

Stabilität ist abhängig von:  
Kₚ, Deadband, δr_max, Arbitrageintensität und Oracle-Glättung.

---

# 3. Dynamik in volatilen Märkten

## 3.1 Arbitrage & Redemption als schneller Preisanker

**Unterbewertung (P < R):**

- Arbitrageure kaufen ProjectUSD  
- Redemption löst ihn zu R ein  
- Supply sinkt  
- P steigt

**Überbewertung (P > R):**

- Neue Prägung (sofern r dies zulässt)  
- Verkauf zu hoher Bewertung  
- Angebot steigt  
- P fällt  

Arbitrage wirkt als **schneller** Mechanismus.  
Der Controller ist der **langsame**, systemische Mechanismus.

---

## 3.2 Rolle des Orakels bei hoher DEX-Volatilität

TWAP und Median:

- glätten Flash-Spikes  
- filtern manipulierte Pools  
- reduzieren kurzfristige Preisexzesse  

Der Controller reagiert nur auf Trends, nicht auf Rauschen.

---

## 3.3 r als Schockabsorber bei PLS-Volatilität

Da R den Preis ProjectUSD/PLS beschreibt, bleibt die interne Stabilität erhalten – selbst wenn PLS gegenüber externen Assets stark schwankt.

Bei starkem PLS-Preisverfall:

- Vault-Collateral fällt → Liquidationen  
- Stability Pool erhält PLS → ProjectUSD-Supply sinkt  
- P sinkt kurzfristig  
- Controller erkennt P < R → r sinkt  
- Nachfrage steigt → P stabilisiert  

---

# 4. Szenarien: niedriger vs. hoher Stress

## 4.1 Niedriger Stress

- geringe P-Abweichungen  
- arbitragefreundliche Marktverhältnisse  
- Controller reagiert moderat  
- Peg-Deviation bleibt klein  
- r bleibt meist im Deadband oder nahe daran  

---

## 4.2 Hoher Stress (z. B. 50 % PLS-Crash)

Ablauf:

1. Liquidationswelle  
2. ProjectUSD-Supply sinkt  
3. kurzfristiger Verkaufsdruck auf P  
4. Arbitrage kauft unterbewertete Coins  
5. Controller senkt r über mehrere Epochen  
6. Stabilisierung des Pegs innerhalb des R-Korridors  

Während externe Preise kollabieren, bleibt die interne Einheit ProjectUSD in PLS relativ stabil.

---

# 5. Analyse der Atmungsmechanik

## 5.1 Expansion (Einatmen)

(P < R) → r sinkt  
→ Emission/Halten wird attraktiver  
→ Nachfrage steigt  
→ Supply kontrahiert durch Redemption  
→ P nähert sich wieder R  

## 5.2 Kontraktion (Ausatmen)

(P > R) → r steigt  
→ Emission wird teurer  
→ Nachfrage fällt  
→ Angebot wächst langsamer  
→ P sinkt  

## 5.3 Deadband & RateLimiter

- Deadband verhindert Überreaktion auf Mikrovolatilität  
- Limiter verhindert extreme r-Sprünge  
- gemeinsam sorgen beide für **glatte Atmung statt Hyperventilation**

## 5.4 Surplus-Puffer als langfristige Stabilisierung

Der Surplus-Puffer:

- sammelt Gebühren  
- kann langfristige Sparraten finanzieren  
- stabilisiert r im Zeitverlauf  
- wirkt wie eine „Lunge mit Reservetank“

---

# 6. Grenzen & Risiken

## 6.1 Technische Risiken

- Smart-Contract-Risiko  
- Oracle-STALE führt zu eingefrorenem r  
- erforderliche Audits vor Freeze-Event

## 6.2 Ökonomische Risiken

- geringe DEX-Liquidität → träge Arbitrage  
- Panikverhalten kann rationale Mechanismen temporär überlagern  
- Parameterwahl kritisch: Kₚ, Deadband, δr_max

## 6.3 Offene Designfragen

- negative r-Phasen sicher umsetzbar?  
- Langzeit-Sparraten und ihre Wechselwirkung mit r  
- Interaktion mit PSM/AMO in späteren Phasen  

---

# 7. Schlussfolgerung

ProjectUSD stabilisiert sich nicht durch starre Fixierung, sondern durch **kontrollierte, atmende Anpassung** des monetären Gleichgewichts.

Kernmechanismen:

- **Median-TWAP-Oracle**  
- **Proportional-Controller (ε → r)**  
- **Arbitrage & Redemption**  
- **Surplus-Puffer & Stability Pool**  

Gemeinsam erzeugen sie eine robuste, autonome Form dynamischer Stabilität:  
Preisabweichungen werden gedämpft, Schocks absorbiert, Gleichgewichtszustände wiederhergestellt.

Die Atmungsmechanik macht ProjectUSD zu einem **adaptiven, selbststabilisierenden Geldsystem**, dessen Verhalten formal analysierbar, simulierbar und überprüfbar ist.

---

# 8. Verification

> ## 📘 Prüfkriterien für Reviewer
- Ist die Controller-Logik korrekt beschrieben?  
- Ist der Zusammenhang zwischen ε, r und P konsistent?  
- Wurde die Arbitragewirkung korrekt modelliert?  
- Sind die Stabilitätsannahmen realistisch?  
- Ist der Übergang zwischen Mikro- und Makrovolatilität sauber dargestellt?  

Diese Studie bildet die Basis für weiterführende Forschung zur dynamischen Modellierung, zur Parameteroptimierung und zu systemweiten Stresssimulationen.
