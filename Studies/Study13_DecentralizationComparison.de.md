# Study 13 – Dezentralitätsvergleich  
**ProjectUSD vs. MakerDAO, GHO, USDe & zentrale Stablecoins**  
*Systematische Analyse der Protokollstrukturen, Governance-Abhängigkeiten und Zentralisierungspfade*  
*(Level-3 Research Format)*

---

## Abstract

Dezentralität ist keine einfache Eigenschaft, sondern ein **mehrdimensionales Spektrum** technischer, ökonomischer und organisatorischer Faktoren.  
Während viele Stablecoins sich als „dezentral“ präsentieren, unterscheiden sich ihre tatsächlichen Abhängigkeiten erheblich.

Diese Studie untersucht systematisch:

- **MakerDAO/DAI**  
- **GHO (Aave)**  
- **USDe (Ethena)**  
- **zentrale Stablecoins (USDC, USDT)**  
- **ProjectUSD (PulseChain)**  

und bewertet sie anhand von sechs Dezentralitätsdimensionen:

1. **Governance-Abhängigkeit**  
2. **Oracle-Abhängigkeit**  
3. **Collateral-Zentralisierung**  
4. **Ausfallpunkte / Single Points of Failure**  
5. **Interne vs. externe Wertdefinition**  
6. **Manipulationsresistenz**

Die Analyse zeigt:  
ProjectUSD ist **das einzige System, das vollständige Protokollimmunität** besitzt:  
kein Governance-Einfluss, kein externer Peg, kein Oracle für Wertdefinition, keine zentralen Institutionen und keine menschliche Kontrolle des Kernmechanismus.

---

# 1. Einleitung – Warum Dezentralität ein mehrschichtiges Konzept ist

Stablecoins unterscheiden sich nicht primär durch Technologie, sondern durch:

- Kontrolle über Parameter,  
- Kontrolle über Collateral,  
- Kontrolle über Oracles,  
- Kontrolle über Emission,  
- rechtliche Abhängigkeiten,  
- Verwahrung externer Assets,  
- institutionelle Risiken.

„Dezentralität“ hat daher mehrere Dimensionen:

> Ein System kann technisch dezentral, aber ökonomisch zentralisiert sein – oder umgekehrt.

ProjectUSD ist das erste Modell, das **alle Dimensionen gleichzeitig** dezentralisiert.

---

# 2. Bewertungsrahmen: Die sechs Ebenen der Stablecoin-Dezentralität

Diese Studie verwendet die folgenden sechs Kriterien:

1. **Governance-Kontrolle**  
   – Kann ein Team, DAO oder Gremium Parameter ändern?

2. **Oracle-Abhängigkeit**  
   – Ist der Wert extern definiert (z. B. USD-Preis)?

3. **Collateral-Zentralisierung**  
   – Werden zentralisierte Assets gehalten (Treasuries, USDC, Banken-Cash)?

4. **Protokolländerbarkeit**  
   – Kann der Code geändert, pausiert oder abgeschaltet werden?

5. **Manipulationsangriffsflächen**  
   – TWAP-Manipulation, Governance-Angriffe, Bridge-Risiken.

6. **End-to-End-Dezentralität**  
   – Wie viele menschliche Eingriffe sind möglich?

Mit diesem Raster vergleichen wir die Systeme.

---

# 3. Systemanalyse: MakerDAO / DAI

## 3.1 Governance
- MakerDAO besitzt **umfangreiche Governance**
- Parameter (Fees, Collateral-Quoten, RWA-Exposition) sind **stark veränderbar**
- Einfluss großer MKR-Holder ist erheblich → **Oligopol-Risiko**

## 3.2 Oracle
- DAI ist direkt abhängig vom USD-Preis externer Assets  
→ Oracle = zentraler Wertanker

## 3.3 Collateral
- Großteil besteht heute aus:  
  - USDC  
  - USDP  
  - T-Bills über RWAs  
→ **stark zentralisiert**

## 3.4 Systemrisiko
- RWA-Exposure → staatliche Jurisdiktionen → Einfrierbarkeit  
- MakerDAO kann Parameter jederzeit ändern oder DAI einfrieren

**Fazit:**  
DAI ist ein **teil-dezentraler USD-Wrapper**, kein unabhängiges System.

---

# 4. Systemanalyse: GHO (Aave)

## 4.1 Governance
- Aave DAO kontrolliert GHO vollständig  
- Parameter, Zinssätze, Facilitators → **governance-driven**

## 4.2 Oracle
- GHO ist USD-pegged → externe Preisfeeds notwendig

## 4.3 Collateral
- basiert auf Aave-Vaults, die wiederum von zentralisierten Stablecoins abhängen  
→ indirekt zentralisiert

## 4.4 Systemrisiko
- gleiche Governance-Problematik wie Maker  
- GHO ist abhängig von externem USD-Markt

**Fazit:**  
GHO ist **hochgradig governance-zentralisiert** und **USD-orientiert**.

---

# 5. Systemanalyse: USDe (Ethena)

## 5.1 Governance
- vollständig zentral gesteuertes Protokoll  
- Emission, Parameter, Collateral → **zentral verwaltet**

## 5.2 Oracle
- hart USD-gepegtes System  
- abhängig von externen Preisfeeds

## 5.3 Collateral
- basiert auf hedged Derivatives + CEX-Strukturen  
- Verwahrung extern  
→ **extrem zentral**

## 5.4 Systemrisiko
- CEX-Risiko  
- Hedge-Failure-Risiko  
- Regulierung  
- systemische Gegenparteien

**Fazit:**  
USDe ist ein **komplett zentralisiertes synthetisches USD-Konstrukt**.

---

# 6. Systemanalyse: Zentrale Stablecoins (USDC, USDT)

## 6.1 Governance
- private Firmen mit vollständiger Kontrolle

## 6.2 Oracle
- externer USD-Preis  
- Bedeutung eines globalen Fiat-Markts

## 6.3 Collateral
- Banken, Geldmarktfonds, T-Bills  
- regulatorische Einbindung  
→ **zentrale Verwahrung**

## 6.4 Systemrisiko
- Kontoeinfrierungen  
- staatliche Intervention  
- Banking-Counterparty-Risiko

**Fazit:**  
USDC/USDT sind **rein zentralisierte USD-Geldmarktfonds**, nur tokenisiert.

---

# 7. Vergleichstabelle aller Systeme

| Kriterium | ProjectUSD | DAI | GHO | USDe | USDC/USDT |
|----------|------------|-----|-----|------|-----------|
| Governance | Keine | Stark | Stark | Voll | Voll |
| Oracle für Wert | Nein | Ja | Ja | Ja | Ja |
| Collateral zentralisiert? | Nein | Ja | Mittel | Stark | Stark |
| Protokolländerbarkeit | Nein | Ja | Ja | Ja | Voll |
| Angriffsflächen | Minimal | Mittel-Hoch | Hoch | Sehr Hoch | Extrem Hoch |
| Wertdefinition extern? | Nein | Ja | Ja | Ja | Ja |
| Systemischer Zwang zur Dollarbindung | Nein | Ja | Ja | Ja | Ja |
| End-to-End-Dezentralität | Vollständig | Gering | Gering | Keine | Keine |

**Ergebnis:**  
ProjectUSD ist das **einzige vollständig dezentralisierte System**.

---

# 8. Warum ProjectUSD strukturell dezentraler ist als alle Alternativen

## 8.1 Keine Governance
- Kernlogik unveränderbar  
- keine Parameter, die gehalten oder gehackt werden können  
- keine Upgrades, die Angreifer nutzen könnten

## 8.2 Keine Fiat-Bindung
- R wird intern definiert  
- keine Abhängigkeit zu USD  
- kein externer Oracle-Druck

## 8.3 Keine institutionellen Risiken
- keine Banken  
- keine CEX  
- keine RWAs  
- keine regulatorischen Einfallstore

## 8.4 Keine menschliche Kontrolle
- gesamte Ökonomie basiert auf Algorithmik  
- autonome Selbstregulierung  
- manipulationsresistent

## 8.5 Reine On-Chain-Werte
- ProjectUSD stützt sich nur auf PLS  
- kein Collateral, das eingefroren werden könnte  
- keine staatliche Zugriffsmöglichkeit

**Damit erreicht ProjectUSD einen Dezentralitätsgrad, der für stablecoins bisher unerreicht ist.**

---

# 9. Systemische Stabilität durch Dezentralität

Dezentralität ist nicht nur ein „Wahlversprechen“ – sie ist ein **Sicherheitsmechanismus**:

- keine Governance → keine Governance-Angriffe  
- kein Fiat-Peg → keine Death Spirals  
- kein zentralisiertes Collateral → keine Einfrierung  
- kein Upgrade-Mechanismus → kein Protokoll-Hijacking  
- kein externer Wertanker → keine Orakelabhängigkeit  

ProjectUSD ist nicht nur dezentral –  
es ist *immun* gegen die Systeme, die andere Stablecoins verwundbar machen.

---

# 10. Schlussfolgerung

ProjectUSD unterscheidet sich grundlegend von allen existierenden Stablecoins.

Andere Systeme basieren auf:

- zentralen Oracles,  
- zentralisierten Collaterals,  
- menschlicher Governance,  
- staatlichen Institutionen,  
- externen USD-Abhängigkeiten.

ProjectUSD dagegen:

- definiert seinen Wert intern,  
- stabilisiert sich autonom,  
- ist governance-frei,  
- ist manipulationsresistent,  
- ist vollständig dezentral.

Damit ist ProjectUSD nicht nur ein Stablecoin –  
sondern ein **neuer Geldtypus**, ein *autonomes On-Chain-Monetary System*,  
frei von externen Bindungen und menschlicher Kontrolle.

---

# 11. Verification

> ## 📘 Prüfkriterien für Reviewer
- Sind alle Stablecoins korrekt und fair charakterisiert?  
- Ist die Dezentralitätsmatrix vollständig?  
- Stimmt die Bewertung der externen Risiken von DAI, GHO, USDe, USDC/USDT?  
- Sind die Dezentralitätsmerkmale von ProjectUSD korrekt beschrieben?  
- Wird klar dargestellt, warum ProjectUSD vollständig unabhängig funktioniert?  

Diese Studie bildet die Grundlage für zukünftige Arbeiten zu Systemidentität, Protokollvergleich und Risikoarchitektur im Stablecoin-Sektor.
