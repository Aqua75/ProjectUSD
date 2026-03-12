# Study 05 – Vergleichsanalyse: ProjectUSD vs. DAI, LUSD, GHO, USDe, USDC
*Strukturelle Analyse unterschiedlicher Stablecoin-Modelle im Hinblick auf Autarkie, Orakelabhängigkeit, Stabilität und Governance*  
*(Level-3 Research Format)*

---

## Abstract

Stablecoins bilden die monetäre Basis von DeFi – als Recheneinheit, Wertaufbewahrungsmittel und Settlement-Layer.  
Diese Studie vergleicht sechs grundverschiedene Konzepte:

- **ProjectUSD** – autonomes, on-chain gesteuertes, algorithmisches Wertmaß für PulseChain  
- **DAI** – überbesicherter, governance-intensiver Multi-Collateral-Stablecoin  
- **LUSD** – minimalistische, immutable, ETH-basierte Stablecoin-Architektur  
- **GHO** – Aaves nativ integrierter Stablecoin mit Facilitor-Struktur  
- **USDe** – synthetischer Dollar durch delta-neutrale Hedging-Strategien  
- **USDC** – vollständig fiat-besicherter, zentralisierter Custodial-Stablecoin  

Die Analyse vergleicht diese Systeme nach vier Kernkriterien:

1. **Autarkie** – Unabhängigkeit vom Bankensystem, Off-Chain-Infrastruktur oder Governance  
2. **Orakelabhängigkeit** – Quellen der Preisfeeds und Angriffsflächen  
3. **Liquidations- und Stabilitätsmechanik**  
4. **Governance & Änderbarkeit der Regeln**

Darauf aufbauend werden technische, ökonomische und regulatorische Risiken sowie Stress- und Black-Swan-Szenarien bewertet.

---

# 1. Einleitung – Warum Vergleiche unverzichtbar sind

Wer ein Ökosystem wie PulseChain mit einer eigenen stabilen Recheneinheit ausstatten will, muss die Designentscheidungen etablierter Stablecoins verstehen: ihre Stärken, Schwächen, Abhängigkeiten und Bruchstellen.

Diese Studie zeigt, wie sich ProjectUSD von existierenden Modellen differenziert und warum ein autarkes, oracle-internes, governance-minimiertes System für PulseChain sinnvoll ist.

---

# 2. Analyse der einzelnen Systeme

## 2.1 ProjectUSD

### Design & Zielsetzung
ProjectUSD ist ein vollständig on-chain operierendes, algorithmisches Geldsystem für PulseChain. Ziel ist nicht ein „digitaler Dollar“, sondern eine *eigene interne Recheneinheit*, definiert durch:

- **Gleichgewichtspreis R**  
- **Marktpreis P**  
- **Systemrate r**, gesteuert über einen autonomen Controller  

Weicht P von R ab, passt der Controller r an.  
Hohe r → weniger Geldschöpfung; niedrige r → Kreditaufnahme wird günstiger und wirtschaftliche Aktivität attraktiver.

Das System reguliert sich ausschließlich anhand eigener Zustände – ohne externes USD-Oracle.

### Kernkomponenten
- **Vaults**: Überbesicherte PLS-Positionen zur Prägung von ProjectUSD  
- **Stability Pool**: Löscht Schulden unterbesicherter Vaults und erhält deren PLS-Collateral  
- **Redemption Engine**: Einlösung von ProjectUSD zu R gegen PLS → harter interner Preisanker  

### Architektur & Governance
- **Immutable Core**: Nach Freeze unveränderlich; kein Admin-Key, keine Upgrades  
- **Peripherie-Schicht**: Optionale Module wie PSM, AMOs, Collateral-Adapter  

### Orakel
ProjectUSD ist nicht „orakellos“, sondern **orakel-autark**:  
Es verwendet ausschließlich *eigene* DEX-Paare auf PulseChain (Median-TWAP mit Outlier-Filtern).

---

## 2.2 DAI (MakerDAO)

### Mechanik
- überbesicherte CDPs (Vaults), multi-collateral  
- Stability Fee (Zins), DAI Savings Rate, Peg Stability Module  
- starker Einsatz von **Chainlink-Orakeln**

### Governance
- MKR-Tokenhalter steuern zentrale Parameter  
- hohe Flexibilität, aber Risiko von Governance-Capture

### Externe Abhängigkeiten
- RWA-Collateral und USDC im PSM → *starke* Abhängigkeit vom traditionellen Bankensystem

---

## 2.3 LUSD (Liquity)

### Mechanik
- nur ETH als Collateral  
- 110 % Mindest-CR  
- Stability Pool absorbiert Liquidationen  
- direkte Redemption diszipliniert Troves

### Governance
- vollständig immutable, keine Änderungen möglich

### Schwächen
- keine native Rendite für Halter → zyklische Kontraktionsphasen möglich

---

## 2.4 GHO (Aave)

### Mechanik
- durch Aave V3 besichert  
- Prägung durch spezielle Facilitators  
- Preisstabilität durch Aave-Stability-Module

### Governance
- vollständige DAO-Kontrolle  
- starke Abhängigkeit von Chainlink-Orakeln

---

## 2.5 USDe (Ethena)

### Mechanik
- synthetischer Dollar durch delta-neutrale Hedging-Strategien (Long stETH + Short Perps)  
- Funding-Spreads erzeugen Renditen (hohe APY)

### Risiken
- starke Abhängigkeit von Perpetual DEXs und CEXs → Gegenparteirisiko  
- Modellrisiko bei Funding-Regimewechseln  
- große operative Komplexität

---

## 2.6 USDC (Circle)

### Mechanik
- 1:1 fiat-besichert durch Cash und Treasuries  
- regulierter Custodial-Stablecoin

### Risiken
- Blacklisting, Einfrieren von Adressen  
- vollständige Abhängigkeit von Banken, Regulatoren und Marktbedingungen

---

# 3. Kriterienvergleich: Autarkie, Orakel, Liquidationen, Governance

## 3.1 Übersichtstabelle

| Kriterium | ProjectUSD | DAI | LUSD | GHO | USDe | USDC |
|----------|------------|------|-------|------|-------|-------|
| Typ | On-chain, alg. Geldsystem | Überbesicherter CDP | ETH-only CDP (immutable) | Overcollateral BorrowAsset | Synthetic, delta-neutral | Fiat-backed IOU |
| Autarkie | Hoch | Mittel | Hoch | Mittel | Niedrig–mittel | Niedrig |
| Orakelquelle | On-chain Median-TWAP | Externe Feeds | Externe Feeds | Chainlink | Perp & Spot Markets | Off-chain Banken |
| Liquidationen | Stability Pool | Auktionen | Stability Pool | Aave-Liquidationen | Hedge-Rebalancing | Keine |
| Redemption | R-basiert (intern) | PSM | ETH/USD | Stabilitätsmodule | Protokollabhängig | Custodial 1:1 |
| Governance | Peripherie-only | Vollständig | Keine | Vollständig | Stark zentral | Vollständig |
| Admin Keys | Nein (Core) | Ja | Nein | Ja | Ja | Ja |

---

## 3.2 Autarkie

ProjectUSD & LUSD sind die autarksten Systeme:

- Immutable Core  
- rein on-chain  
- keine Abhängigkeit von USD-Preisfeeds  

DAI & GHO besitzen Dezentralisierung, aber nicht Autarkie:  
Ihre Funktionsfähigkeit hängt direkt von Chainlink, Governance und RWAs ab.

USDe ist technisch innovativ, aber vollständig abhängig von Derivate-Infrastruktur (CEX/DEX).

USDC ist absichtlich *nicht autark*:  
Es ist ein Bankprodukt.

---

## 3.3 Orakelabhängigkeit

### ProjectUSD
- nutzt nur PulseChain-interne DEX-Daten  
- Median/TWAP/Outlier-Filter → extrem schwer manipulierbar

### DAI / LUSD / GHO
- Abhängigkeit von externen Preisfeeds  
- brauchen funktionierende Keeper, Feeds und Governance

### USDe
- abhängig von Derivate-Märkten → komplex und störanfällig

### USDC
- kein on-chain Oracle → Risiko liegt in Off-Chain-Reservetransparenz

---

## 3.4 Liquidationsmodell

ProjectUSD & LUSD:

- Vault → Stability Pool → Redemption  
- keine Collateral-Verkäufe auf AMMs  
- keine Keeper-Abhängigkeit

DAI & GHO:

- klassische Auktionen oder Borrow/Liquidation-Modelle  
- abhängig von Liquidatoren und Netzwerklatenz

USDe:

- nicht collateral-basiert → abhängig von Markt-Hedges

USDC:

- keine Liquidationsmechanik

---

## 3.5 Governance

ProjectUSD:

- Core ist unveränderlich  
- Governance nur in der Peripherie  
- Fehlentscheidungen können schaden, aber nicht das System zerstören

LUSD:

- governancefrei, maximal sicher, minimal flexibel

DAI / GHO:

- governanceintensiv  
- langsam, komplex, anfällig für Capture

USDe & USDC:

- quasi vollständig zentralisiert

---

# 4. Risikoanalyse

## 4.1 Technische Risiken

Alle Systeme teilen:

- Smart-Contract-Risiken  
- Chain-Risiken  
- MEV  
- Netzwerküberlastungen  

ProjectUSD:

- maximale Robustheit durch Immutable Core  
- aber: Fehler wären irreversibel → Audits entscheidend  
- Median-TWAP reduziert Oracle-Angriffe

DAI/GHO:

- können Fehler fixen, tragen aber Upgrade-Risiko

LUSD:

- Code ist final → Fehler wären final

USDe:

- zusätzlich Risiko durch Derivate-Märkte

USDC:

- größte Angriffsfläche im Off-Chain-Sektor

---

## 4.2 Ökonomische Risiken

### Collateral-Volatilität
ProjectUSD, DAI, LUSD, GHO und USDe sind volatilitätsabhängig.

### Liquiditätsrisiko
PulseChain-Liquidität ist ein kritischer Faktor für ProjectUSD.

### Modellrisiko (USDe)
Delta-neutrales Hedging bricht bei Funding-Regimewechseln.

### Bank-Run-Risiko
USDC (und indirekt DAI) sind anfällig für regulatorische Schocks.

---

## 4.3 Governance- und Umfeldrisiken

Regulatorisch:

- USDC, DAI und GHO stark betroffen  
- ProjectUSD und LUSD weitgehend immun  
- USDe abhängig von Partnern (CEX)

Governance Capture:

- DAI/GHO anfällig  
- ProjectUSD eingeschränkt  
- LUSD immun

Politikrisiken:

- USDC stark exponiert  
- andere Systeme sekundär

---

# 5. Stress- und Black-Swan-Szenarien

## 5.1 Szenario A: Starker Krypto-Crash (80 %)

ProjectUSD:

- große Liquidationswellen → Stability Pool absorbiert  
- r steigt stark, Supply sinkt  
- System bleibt stabil, R bleibt sauber definiert

LUSD:

- sehr ähnliche Dynamik wie ProjectUSD

DAI/GHO:

- Orakel-Lags → Fehl-Liquidationen möglich  
- abhängig von Keepern und Governance

USDe:

- Hedge könnte brechen → Underpeg-Risiko

USDC:

- nur betroffen, wenn Krypto-Crash mit Problemen am Treasury-Markt kollidiert

---

## 5.2 Szenario B: Orakel-/Marktmanipulation

ProjectUSD:

- Median-TWAP + Filter machen Manipulation teuer  
- rLimiter begrenzt Systemreaktion

DAI/GHO/LUSD:

- Chainlink-Fehler → Liquidationsfehler möglich

USDe:

- Perp-Preisfehler → Hedge bricht

---

## 5.3 Szenario C: Regulatorischer Druck

USDC:

- direkt betroffen

DAI:

- indirekt betroffen durch RWAs

USDe:

- betroffen durch CEX-Infrastruktur

GHO:

- betroffen durch Aave-Regulierung

ProjectUSD & LUSD:

- technisch robust gegen regulatorischen Zugriff

---

## 5.4 Szenario D: Derivate-Marktstörung (relevant für USDe)

- Hedge schlägt fehl  
- Funding dreht  
- Unterdeckung möglich  
- Pegverlust wahrscheinlich

ProjectUSD, LUSD, DAI, GHO, USDC: kaum betroffen

---

## 5.5 Szenario E: PulseChain-spezifische Störung

ProjectUSD:

- hängt vollständig an PulseChain  
- Reorgs / Congestion können Liquidationen verzögern

Andere Stablecoins auf PulseChain wären nur als Bridged-Assets betroffen.

---

# 6. Schlussfolgerung

## 6.1 Positionierung von ProjectUSD

ProjectUSD kombiniert Eigenschaften von:

- LUSD (Immutable Core + Stability Pool + Redemption)  
- DAI (Zinssteuerung), jedoch **automatisiert** statt governancegesteuert  

Unterschied zu USDC & DAI:

- keine Fiatbindung  
- keine Bankenabhängigkeit  
- interne Wertdefinition R

Unterschied zu USDe:

- kein Hedging  
- keine externen Gegenparteien  
- transparente Systemdynamik

---

## 6.2 Trade-offs

- weniger flexibel als DAI/GHO  
- sicherer und autarker als alle governance-intensiven Modelle  
- stabiler und transparenter als hedging-basierte Systeme wie USDe  
- weniger regulatorisch belastet als USDC

---

## 6.3 Relevanz für PulseChain

ProjectUSD eignet sich als:

- interne Recheneinheit  
- unabhängige Wertbasis  
- Fundament für DeFi-Ökosysteme  
- Schutz gegenüber Fiat-Risiken

---

## 6.4 Ausblick

Die größte Schwäche von ProjectUSD ist nicht struktureller Natur, sondern praktisch:

> **Es existiert noch nicht — es muss erst implementiert werden.**

Ob ProjectUSD sein Potenzial entfalten kann, hängt ab von:

- Qualität des Immutable Core  
- Integration in das PulseChain-Ökosystem  
- konservativer Nutzung der Peripherie-Governance  

Stablecoins werden nicht verschwinden — aber das Vertrauen verschiebt sich:  
Von zentralisierten Bank-IOUs hin zu autonomen, transparenten On-Chain-Systemen.

ProjectUSD könnte eine solche Rolle auf PulseChain einnehmen.

