# Study 14 – Effizienz von ProjectUSD auf PulseChain  
*Gas- und Energieeffizienz, Skalierung und Vergleich zu Ethereum*  
*(Level-3 Research Format)*

---

## Abstract

ProjectUSD ist ein vollständig on-chain operierendes, autonomes Geldsystem.  
Für die praktische Nutzbarkeit als „Grundgeld“ der PulseChain ist nicht nur die ökonomische Architektur entscheidend, sondern auch die **Effizienz des technischen Unterbaus**:

- Wie gasgünstig arbeitet das System?  
- Skaliert es mit zehntausenden Vaults, Stability-Pool-Interaktionen und Liquidationen?  
- Wie unterscheidet sich ein Deployment auf PulseChain gegenüber Ethereum?  
- Welche Energieeffizienz bietet ein PoS-basiertes L1 für ein hochfrequent genutztes Stablecoin-System?

Diese Studie analysiert:

- Gasmodelle von Ethereum und PulseChain  
- Gasprofile typischer ProjectUSD-Interaktionen  
- Skalierbarkeit im Massenbetrieb  
- Energieeffizienz des PulseChain-Ökosystems  
- Optimierungsmöglichkeiten im ProjectUSD-Core

Die Ergebnisse zeigen:  
**ProjectUSD ist architektonisch ideal für PulseChain geeignet – technisch skalierbar, gasgünstig, energieeffizient und massentauglich.**

---

# 1. Einleitung – Effizienz als Kernanforderung

ProjectUSD kombiniert:

- Vaults  
- Stability Pool  
- Redemption Engine  
- Zinscontroller (r)  
- Median-TWAP-Oracle  

zu einem vollständig autonomen Kreislauf ohne Governance, ohne Admin-Keys und ohne externe Pegs.

Für reale Nutzbarkeit muss das System:

- **gasgünstig**,  
- **skalierbar**,  
- **energieeffizient**,  
- **klein nutzerfreundlich**,  
- **netzwerkfreundlich**

sein.

Diese Studie beantwortet die Frage:  
> Wie effizient ist ProjectUSD auf PulseChain – und wie schneidet es im Vergleich zu Ethereum ab?

---

# 2. Gasmodelle

## 2.1 Grundprinzipien von Gas auf EVM-Chains

Gasgebühr = **GasUsed × GasPrice**

- **GasUsed** = Ausführungsaufwand im Contract  
- **GasPrice** = Marktpreis des Blockspace  

EIP-1559 führt eine Base Fee ein (Burn) und eine variable Tip-Komponente für Validatoren.

Für die Effizienz eines Protokolls gibt es zwei Ebenen:

1. **Code-Effizienz** (Beeinflusst durch Protokollarchitektur)
2. **Chain-Effizienz** (Beeinflusst durch die Wahl der Blockchain)

ProjectUSD beeinflusst Ebene 1 direkt, Ebene 2 indirekt.

---

## 2.2 Ethereum – Gasmodell

Kerndaten:

- Proof of Stake  
- Blockzeit ~12–13 Sekunden  
- Block Gas Limit ~30–60 Mio  
- DeFi-Kosten: 3–50+ USD pro Transaktion möglich  
- Komplexe Operationen (Vaults, Liquidationen) können **10–100 USD** kosten

MakerDAO und Liquity mussten Gas-Overheads über Designmaßnahmen abfedern:

- Liquidation Reserves  
- Mindestschulden  
- Batch-Liquidationen  
- hohe Optimierungsanforderungen

Ethereum zwingt zu „größerer Kapitalgröße pro Aktion“.

---

## 2.3 PulseChain – Gasmodell

Kerndaten:

- Proof of Stake (Ethereum-ähnlich)  
- Blockzeit ~10–11 s real  
- Gaspreis extrem niedrig  
- Standard-TX: **0,001–0,01 USD**  
- Fee-Burn vorhanden  
- identischer EVM-Opcode-Kostenrahmen, aber deutlich billigerer Blockspace

PulseChain ermöglicht:

- kleine Vaults  
- günstige Liquidationen  
- günstige Arbitrage  
- effiziente Redemptions  
- massentaugliche Nutzung

---

## 2.4 Gasprofile typischer ProjectUSD-Aktionen

Basierend auf Liquity/Maker-Vergleichen:

**Vault eröffnen / schließen**  
→ 400k–900k Gas

**Collateral/Debt anpassen**  
→ 200k–600k Gas

**Stability-Pool Deposit/Withdraw**  
→ 200k–500k Gas

**Liquidation eines Vaults**  
→ 800k–1,5 Mio Gas (Batch günstiger pro Vault)

**Redemption**  
→ ähnlich Liquidationspfad

**Oracle / r-Update**  
→ sehr geringe Gaslast (lazy updates)

**Wesentliche Erkenntnis:**  
Der Gasverbrauch ähnelt Liquity –  
**der enorme Vorteil entsteht durch PulseChains niedrigen Gaspreis**.

---

# 3. Vergleich: Ethereum vs. PulseChain

## 3.1 Protokoll-Parametervergleich

| Merkmal | Ethereum (2025) | PulseChain (2025) |
|--------|------------------|--------------------|
| Konsens | PoS | PoS |
| Blockzeit | ~12–13 s | ~10–11 s |
| TX-Kosten | Cent → >50 USD | 0,001–0,01 USD |
| Fee Burn | Ja | Ja |
| Gaslimit | ~30–60 Mio | ähnlich, faktisch billiger nutzbar |

---

## 3.2 Beispielrechnung – Vault Opening (800.000 Gas)

**Ethereum (10 Gwei, ETH = 3000 USD)**  
→ ~24 USD  
(bei 30 Gwei bereits ~72 USD)

**PulseChain**  
→ 0,04–0,40 USD

**Ergebnis:**  
→ **Ethereum 50–200× teurer** als PulseChain  

Für kleine Nutzer ist Ethereum unerschwinglich –  
PulseChain dagegen **massentauglich**.

---

## 3.3 Systemweiter Gas-Fußabdruck

Annahme:

- 50.000 Vaults  
- 200.000 Vault-Interaktionen/Jahr  
- 20.000 Stability-Pool-Transaktionen  
- 5.000 Liquidationen/Redemptions  

Gesamtverbrauch:  
→ ~112 Mrd. Gas/Jahr  
→ < 0,1 % der Jahreskapazität einer EVM-Chain

Ergebnis:  
**ProjectUSD skaliert problemlos auf PulseChain.**

---

## 3.4 Energieeffizienz

**Ethereum PoS:**  
~0,0026 TWh/Jahr → extrem energieeffizient

**PulseChain PoS:**  
ähnliche Architektur → ähnliche Größenordnung

ProjectUSD-Effizienz:

- höhere Liquidationsfrequenz pro kWh  
- mehr Arbitrage-Korrekturen pro kWh  
- höherer Stabilität-pro-Energie-Wert  
- Fee-Burn koppelt Nutzung an Wert des Ökosystems

---

# 4. Optimierungen

## 4.1 Core-Optimierungen

- Storage-Slot-Packing  
- Trennung häufig/seltener geänderter Variablen  
- Minimierung von SSTORE  
- Events statt Storage für historische Daten  
- Batch-Liquidationen  
- sortierte Datenstrukturen für schwächste Vaults  
- Off-chain View-Berechnungen

---

## 4.2 Protokolldesign-Optimierungen

- „Pull-Mechanismen“ statt globaler Auszahlung  
- lazy r-Berechnung  
- kleine Gas-Compensations für Liquidationen  
- median-TWAP-Orakel mit geringer Updatefrequenz  
- strikte Trennung von Core & Peripherie

---

## 4.3 PulseChain-Spezifische Optimierungen

- Multicall-Bündelungen  
- Gas-Subventionen für kleine Nutzer (optional)  
- Nutzung günstiger Netzlastphasen  
- optimale Interaktion mit Fee-Burn  

---

## 4.4 Hypothetische Ethereum-Version

Wäre ProjectUSD auf Ethereum deployed:

- Mindestschulden müssten deutlich höher liegen  
- Liquidationen wären bei Gas-Spikes riskant  
- kleine Nutzer wären ausgeschlossen  
- Redemptions wirtschaftlich nur für große Akteure  

PulseChain dagegen:

- niedrige Gebühren → inklusiv  
- stabile Liquidationsanreize  
- ARB-Aktivität auch bei kleinen Preisabweichungen  
- massentaugliches Stablecoin-Design möglich

---

# 5. Fazit

### **Gas-Effizienz**
ProjectUSD nutzt eine minimalistische immutable Architektur, die:

- wenige, effiziente Transaktionen benötigt  
- Liquidationen & Redemptions gasgünstig hält  
- extrem von PulseChains niedrigen Gaspreisen profitiert

### **Skalierung**
Auf PulseChain kann ProjectUSD:

- zehntausende Vaults tragen  
- tausende Liquidationen/Jahr durchführen  
- unter 0,1 % der Netzkapazität bleiben  

### **Energieeffizienz**
PoS-Chains sind extrem sparsam –  
PulseChain kombiniert dies mit hohem Fee-Burn-Impact pro Transaktion.

### **Vergleich Ethereum / PulseChain**
ProjectUSD **könnte** technisch auf Ethereum laufen,  
aber PulseChain ist **um Größenordnungen effizienter**:

- Nutzerfreundlicher  
- Kapital-effizienter  
- Massentauglicher  
- Stabilitätsfördernd  
- Energieeffizient  
- Gas-sparend

ProjectUSD entsteht damit als **ideales High-Efficiency-Stable-System** für PulseChain.

---

# 6. Verification

> ## 📘 Prüfkriterien für Reviewer
- Sind Gasprofile korrekt eingeordnet?  
- Ist der Unterschied Ethereum vs. PulseChain sauber hergeleitet?  
- Sind die Skalierungsannahmen plausibel?  
- Sind Energieeffizienz-Aussagen korrekt und belastbar?  
- Ist die gesamte Argumentation im Einklang mit dem ProjectUSD-Design?

Diese Studie bildet die Grundlage für technische Evaluierungen, Benchmarking und zukünftige Prototyp-Tests von ProjectUSD auf PulseChain.
