# Study 12 – Spieltheorie der ProjectUSD-Ökonomie
*Analyse strategischer Interaktionen zwischen Marktteilnehmern, Arbitrageuren, Schuldnern, Haltern und dem autonomen Protokoll*  
*(Level-3 Research Format)*

---

## Abstract

ProjectUSD ist ein autonom reguliertes Währungssystem, dessen Stabilität nicht durch zentrale Akteure, sondern durch spieltheoretische Gleichgewichte entsteht.  
Die zentrale Frage lautet:  
**Wie verhalten sich Marktteilnehmer rational, wenn Arbitrage, Redemption, r-Anpassung und Liquidationen deterministische, transparente Spielregeln erzeugen?**

Diese Studie modelliert die wichtigsten Akteurstypen:

- **Arbitrageure**  
- **ProjectUSD-Halter**  
- **Vault-Besitzer (Schuldner)**  
- **Stability-Pool-Teilnehmer**  
- **Liquidatoren**  
- **Externe Spekulanten**

und zeigt, wie ihre strategischen Entscheidungen zu:

- hoher Preisstabilität,  
- geringer Manipulationsanfälligkeit,  
- robusten Gleichgewichtszuständen,  
- negativen Rückkopplungseffekten (statt instabiler Spiralen),  
- stabilen Erwartungen,

führen.

Das Ergebnis:  
ProjectUSD bildet ein **spieltheoretisch starkes Gleichgewicht**, in dem jeder rationale Akteur durch sein Eigeninteresse das System stabilisiert, statt es zu destabilisieren.

---

# 1. Einleitung – Warum Spieltheorie für ProjectUSD entscheidend ist

Die Ökonomie von ProjectUSD wird nicht zentral gesteuert.  
Stattdessen entsteht sie aus:

- automatisierten Mechanismen (Controller, Oracle, Redemption),  
- ökonomischen Anreizen,  
- rationalen Entscheidungen der Nutzer.

Spieltheorie untersucht, ob diese Anreize:

- stabil,  
- widerspruchsfrei,  
- manipulationsresistent,  
- und langfristig tragfähig sind.

ProjectUSD ist so gestaltet, dass die individuellen Strategien der Teilnehmer **automatisch** das Gesamtsystem stabilisieren.

---

# 2. Akteurstypen und ihre Nutzenfunktionen

## 2.1 Arbitrageure

Ziel: **Risikofreier Profit durch Preisabweichungen P ↔ R**.

Nutzenfunktion:

- bei P < R: Kauf → Redemption → Gewinn  
- bei P > R: Minting (abhängig von r) → Verkauf → Gewinn  

Arbitrageure sind die **natürlichen Stabilisatoren** des Systems.

---

## 2.2 Halter von ProjectUSD

Ziel: **Wertstabilität und geringe Volatilität**.

Nutzenfunktion:

- P stabil um R  
- geringer Slippage  
- geringes Liquidationsrisiko für Schuldner  
- Vertrauen in langfristige Stabilität

Halter profitieren von stabilen Gleichgewichten.

---

## 2.3 Vault-Besitzer (Schuldner)

Ziel: **PLS-Hebelwirkung durch besicherte Kreditaufnahme**.

Nutzenfunktion:

- niedrige Zinsen (r)  
- hoher Collateralwert  
- geringer Liquidationsdruck

Vault-Besitzer reagieren sensibel auf r-Anpassungen.

---

## 2.4 Stability-Pool-Teilnehmer

Ziel: **Ertrag durch Liquidationsgewinne**.

Nutzenfunktion:

- Collateral > Schuldwert  
- stabile Alphastruktur  
- Surplus-Puffer als Sicherheitsschicht

Sie stabilisieren das System, indem sie Liquidationen ermöglichen.

---

## 2.5 Liquidatoren (Arbitrage in Liquidationen)

Ziel: **Übernahme von Vaults zu Discount-Preisen**.

Nutzenfunktion:

- effizienter Liquidationsmechanismus  
- geringe Oracle-Manipulationsflächen  
- profitables PLS-Risiko

Liquidatoren verhindern faule Schulden.

---

## 2.6 Externe Spekulanten

Ziel: **Profit durch Preisbewegungen von ProjectUSD oder PLS**.

Sie können für Volatilität sorgen,  
aber das Systemdesign verhindert systemische Schäden.

---

# 3. Spieltheoretische Grundstruktur: Negative Rückkopplung

## 3.1 Warum stable Systeme negative Feedback-Loops benötigen

Instabile Systeme (z. B. UST/LUNA, IRON/TITAN) besitzen **positive Rückkopplung**:

Preis fällt → Supply steigt → Preis fällt stärker → System kollabiert.

ProjectUSD besitzt **ausschließlich negative Rückkopplung**:

Preis fällt → r sinkt → Nachfrage steigt → P steigt  
Preis steigt → r steigt → Nachfrage sinkt → P fällt  

Dies verhindert systemische Eskalation.

---

## 3.2 Nash-Gleichgewicht der Arbitrageure

Arbitrage ist ein **dominantes Verhalten**:

- bei P < R hat jeder Arbitrageur einen Anreiz zu kaufen  
- bei P > R hat jeder einen Anreiz zu verkaufen oder zu minten  
- niemand kann durch Abweichen eine bessere Auszahlung erzielen

Daher entsteht ein **stabiles Gleichgewicht um R**.

---

## 3.3 Gleichgewicht zwischen Schuldnern und Haltern

Schuldner wollen niedrige r-Werte, Halter wollen Preisstabilität.  
Beide Ziele werden durch:

- den Controller,  
- den Oracle-Median,  
- Redemption

gleichzeitig erfüllt.

Das System schafft ein **Spiel mit gemeinsamem Optimum**.

---

## 3.4 Stability Pool als spieltheoretischer „Sicherheitsanker“

Teilnehmer übernehmen Schulden und erhalten Collateral mit positivem Erwartungswert.  
Das Spiel führt zu:

- geringer Liquidationsangst,  
- stabiler Nachfrage nach ProjectUSD,  
- hohem Anreiz, stabil zu bleiben.

---

# 4. Strategische Interaktionen im Preisfindungsprozess

## 4.1 Unterbewertung (P < R)

Dominante Strategien:

- Arbitrageur: kaufen & redeem  
- Halter: kaufen, da sicherer Wertanker  
- Schuldner: r ist geringer → Nachfrage steigt  
- Liquidatoren: aktiv, wenn Liquidationen ausgelöst werden

Ergebnis: **P steigt wieder Richtung R**.

---

## 4.2 Überbewertung (P > R)

Dominante Strategien:

- Arbitrageur: minten & verkaufen  
- Halter: eher verkaufen  
- Schuldner: r steigt → Emission wird unattraktiv  
- Stability Pool: bleibt im Gleichgewicht

Ergebnis: **P fällt Richtung R**.

---

## 4.3 Neutralzone (P ≈ R)

Strategische Ruhe:

- keine starke Arbitrage  
- r bleibt stabil  
- Halter und Schuldner haben wenig Grund zu reagieren  

Das System stabilisiert sich in einem **Nash-Gleichgewicht**.

---

# 5. Strategische Stabilität in Stressszenarien

## 5.1 PLS-Crash

Strategische Reaktionen:

- Liquidatoren übernehmen Vaults  
- Stability Pool erhält wertvolle Collateral-Bestände  
- r sinkt → Nachfrage nach ProjectUSD steigt  
- Arbitrage hält P stabil

Ergebnis:  
Das System bleibt funktional.

---

## 5.2 Illiquide Märkte

Strategische Reaktionen:

- Oracle glättet extreme Ausschläge  
- Trader vermeiden große Swaps  
- Arbitrage passt sich an kleinere Mengen an  
- Stability Pool bleibt aktiv

Das System kann bei Liquiditätsstress „im Leerlauf“ bleiben, ohne zu kollabieren.

---

## 5.3 Panikphase in PulseChain

Durch:

- Redemption  
- Stability Pool  
- Surplus-Puffer  
- r-Anpassung

entstehen **sichere strategische Reaktionen**,  
die Paniklimitierung unterstützen.

---

# 6. Rolle des Surplus-Puffers in der Spieltheorie

Der Surplus-Puffer erweitert das strategische Gleichgewicht:

- bietet Sicherheit bei Stress  
- stabilisiert negative r-Phasen  
- erzeugt Vertrauen für Halter und Schuldner  
- ermöglicht systemische Resilienz

Der Puffer fungiert als **strategische Versicherung** für alle Akteure.

---

# 7. Manipulationsresistenz als spieltheoretisches Gleichgewicht

ProjectUSD ist resistent gegen:

- Oracle-Manipulation (Median + TWAP)  
- Low-Liquidity-Manipulation  
- Flashloan-basierte Preisangriffe  
- Death-Spiral-Operationen  
- Governance-Angriffe auf Kernlogik (nicht existent)

Kein rationaler Angreifer kann nachhaltigen Gewinn erzielen,  
da:

- Arbitrage ihn bestraft,  
- Oracle ihn neutralisiert,  
- r-Anpassung ihn langfristig entwertet.

---

# 8. Spieltheoretische Identität des Systems

ProjectUSD ist ein **selbststabilisierendes Spiel**:

- Negative Rückkopplung  
- Dominante Arbitrage-Strategien  
- Symmetrische Interessen der Akteure  
- Stabile Nash-Gleichgewichte  
- Keine reflexiven Risiko-Token  
- Keine externe Peg-Abhängigkeit  
- Kein Governance-Kontrollpunkt  

Jeder Teilnehmer hat Anreiz, rational zu handeln –  
und rationales Verhalten führt zur **Stabilität des Gesamtsystems**.

---

# 9. Schlussfolgerung

ProjectUSD ist nicht nur ein technisches, sondern ein spieltheoretisches Design:

Es schafft ein Gleichgewicht, in dem:

- Arbitrage stabilisiert,  
- Halter Sicherheit gewinnen,  
- Schuldner rational agieren,  
- Stability Pool robust bleibt,  
- Liquidationen effizient funktionieren,  
- r den systemischen Puls reguliert.

Das System ist so konstruiert, dass **Eigeninteresse und Systemstabilität übereinstimmen**.

Damit bildet ProjectUSD ein **selbstverstärkendes, spieltheoretisch stabiles Geldsystem**,  
das resistent gegen Manipulation, Panik, externe Schocks und reflexive Instabilität ist.

---

# 10. Verification

> ## 📘 Prüfkriterien für Reviewer
- Sind alle Akteurstypen korrekt definiert?  
- Ist die spieltheoretische Logik präzise und konsistent?  
- Sind dominante Strategien korrekt beschrieben?  
- Ist das Gleichgewicht P → R sauber hergeleitet?  
- Werden Stressszenarien und Reaktionen korrekt modelliert?  

Diese Studie bildet die Grundlage für weiterführende Forschung zu Mechanism Design, Incentive Theory und dynamischer Systemsteuerung in ProjectUSD.
