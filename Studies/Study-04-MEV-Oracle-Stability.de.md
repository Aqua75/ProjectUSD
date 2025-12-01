# Study 04 – MEV-Widerstandsfähigkeit, Median-Oracle und TWAP-Stabilität in ProjectUSD
*Analyse der Manipulationsresilienz, der Orakelarchitektur und der systemischen Stabilität unter MEV-Bedingungen*  
*(Level-3 Research Format)*

---

## Abstract

MEV (Miner / Maximal Extractable Value) stellt auf allen EVM-basierten Blockchains ein systemisches Risiko dar.  
Insbesondere Stablecoins sind anfällig für Preismanipulationen, da schon geringe Verzerrungen des Oracles Reflexketten auslösen können, die Peg-Stabilität und Systemvertrauen gefährden.

ProjectUSD begegnet diesem Risiko mit einer kombinierten Architektur aus:

- Median-TWAP-Oracle über mehrere DEX-Paare,  
- Outlier-Filtern und STALE-Logik,  
- Liquiditätsgewichtung über alle validen Pools,  
- rLimiter zur Begrenzung der Systemreaktion,  
- deterministischen Rate-Limits gegen Spam und Cluster-MEV,  
- einer stabilen Redemption-Engine und Arbitragekräften.

Diese Studie untersucht die Stabilität des Oracle-Systems gegen Sandwich-Angriffe, Flash-Manipulationen, koordinierte TWAP-Attacken und korrelierte LP-Strukturen. Die Analyse zeigt, dass ProjectUSD kurzfristige MEV-Angriffe weitgehend neutralisiert und langfristige TWAP-Manipulationen ökonomisch unattraktiv macht.

---

# 1. Einleitung – MEV als systemisches Risiko für on-chain Geldsysteme

MEV beschreibt den extrahierbaren Mehrwert aus:

- Re-Ordern von Transaktionen,  
- Priorisieren oder Verzögern von Ausführungen,  
- gezielten Preisverschiebungen in AMMs,  
- Ausnutzen von Liquidationen, Oracle-Fenstern oder arbitragebasierten Pfaden.

Bei Stablecoins ist MEV besonders kritisch:

- Preismanipulationen → falsches Orakel → falsche r-Anpassung  
- falsche r-Anpassung → falsche wirtschaftliche Signale → reflexive Effekte  
- reflexive Effekte → Risiko für Peg-Stabilität

ProjectUSD adressiert dieses Problem mit einer bewusst robusten Architektur:

- ein **Median-TWAP-Oracle**, das mehrere Pools aggregiert,  
- **Outlier-Filter**, die extreme Abweichungen ausblenden,  
- **STALE-Mechanismen**, die im Zweifel nicht reagieren statt falsch reagieren,  
- **Rate-Limits** und **rLimiter**, die systemische Überreaktionen verhindern,  
- ein **nicht-verkaufsbasiertes Liquidationssystem**, das PLS niemals aktiv auf dem Markt dumpt.

---

# 2. Angriffsarten auf Preisfeeds und Orakel

## 2.1 Sandwich-Angriffe

Mechanik:

1. Angreifer kauft vor dem Nutzer (Front-Run), erhöht den Preis,  
2. Nutzer handelt zu schlechteren Konditionen,  
3. Angreifer verkauft nach dem Nutzer (Back-Run) und realisiert den Spread.

Relevanz für ProjectUSD:

- betrifft primär Nutzer, nicht das Oracle,  
- verschiebt Spotpreise nur kurzzeitig,  
- wird durch TWAP-Glättung stark reduziert,  
- beeinflusst P_final kaum, da nur wenige Beobachtungen betroffen sind,  
- hat bei Medianbildung praktisch keinen Effekt auf das Gesamtorakel.

---

## 2.2 Flash-Manipulation von Spot-Preisen

Mechanik:

- FlashLoan → massiver Pump/Dump eines Pools → Oracle-Update abwarten → Reversal.

In Systemen mit Spot-Oracles ein kritisches Risiko.

Relevanz für ProjectUSD:

- TWAP über hunderte bis tausende Blöcke,  
- ein einzelner manipulierte Block hat nur Gewicht **1/TWAPWindow**,  
- Median über mehrere Pools neutralisiert Einzelmanipulationen,  
- Outlier-Filter disqualifiziert extreme Verzerrungen.

Ein Ein-Block-Angriff erzeugt typischerweise Effekte von **0,1 % oder weniger**.

---

## 2.3 TWAP-Attacken über mehrere Blöcke

Mechanik:

- dauerhafte, koordinierte Preisverschiebung innerhalb eines Pools,  
- über 50–80 % der TWAP-Fensterblöcke,  
- in dünnen Pools mit niedriger Liquidität einfacher durchzuführen.

Relevanz:

TWAP-Attacken sind die realistischste und gefährlichste Form der Oracle-Manipulation.  
ABER:

- Medianbildung macht Single-Pool-Angriffe wirkungslos,  
- Angreifer müsste **mindestens 2–3 große Pools gleichzeitig** manipulieren,  
- Arbitrage korrigiert Abweichungen zwischen Pools,  
- hohe Kapitalbindung → extrem teuer,  
- rLimiter begrenzt selbst bei Erfolg die Systemwirkung.

---

# 3. Schutzmechanismen: Median-Oracle, TWAP, Filter & rLimiter

## 3.1 TWAP-Glättung – Schutz gegen zeitliche Manipulation

TWAP:  

$$
P_{\text{twap}} = \frac{\sum (P_{\text{spot},i} \cdot \Delta t_i)}{\sum \Delta t_i}
$$

Eigenschaften:

- Flash-Manipulationen wirken nur in 1 von N Beobachtungen,  
- kurzzeitige Sandwich-Spikes verschwinden im Rauschen,  
- Preisreihe ist träge, reagiert nur auf echte Marktbewegungen.

---

## 3.2 Multi-Pool-Ansatz und Liquiditätsgewichtung

Für jeden gültigen Pool:

$$
w_i = \sqrt{\text{Reserve}_{PLS,i} \cdot \text{Reserve}_{PUSD,i}}
$$

Dadurch:

- Tiefe Pools dominieren, dünne Pools verlieren Relevanz,  
- Angriffe auf dünne Pools sind ineffektiv,  
- Angreifer bräuchte Kapitaldominanz in mehreren Pools gleichzeitig.

---

## 3.3 Medianbildung & Outlier-Filter

Oracle-Endwert:

$$
P_{\text{final}} = \text{median}(P_{\text{twap},1}, P_{\text{twap},2}, \dots)
$$

Filterlogik:

- **MaxDeviationFilter**: Pools >10 % Abweichung werden ignoriert.  
- **MinLiquidityFilter**: dünne Pools werden ausgeschlossen.  

Effekte:

- Extreme Einzelwerte verlieren Einfluss,  
- Manipulation erfordert Mehrheitskontrolle über mehrere gewichtige Pools.

---

## 3.4 STALE-Mechanismus

Wenn Pools:

- keine neuen Beobachtungen liefern,  
- unplausibel konstante Daten zeigen,  
- nicht berechenbar sind → STALE.

Konsequenz:

- STALE-Pools werden ignoriert,  
- wenn alle Pools STALE → System übernimmt P_prev und friert r-Anpassung ein.

**Lieber nicht reagieren als falsch reagieren**.

---

## 3.5 Rate-Limits & rLimiter

Rolle:

- begrenzen Benutzeraktivität pro Adresse,  
- verhindern Spam-MEV-Transaktionen,  
- dämpfen scharfe Sprünge der Systemrate r.

Selbst bei manipuliertem P:

- r kann sich nur langsam verändern (z. B. ≤50 bp/Epoche),  
- keine schockartigen Reaktionen,  
- System bleibt stabil.

---

# 4. Analyse der Angriffsmodelle im Kontext des Oracles

## 4.1 Sandwich-Angriffe

- können Nutzerpreise verschlechtern,  
- beeinflussen Oracle nur minimal,  
- Median-TWAP neutralisiert Einzelspitzen.

**Systemrelevanz: gering.**

---

## 4.2 Flash-Manipulation in dünnen Pools

- Ein-Block-Manipulation erzeugt TWAP-Effekte <0,2 %,  
- Median bildet überwiegend unverzerrte Pools ab,  
- hohe ökonomische Kosten für den Angreifer.

**Systemrelevanz: sehr gering.**

---

## 4.3 Langsame TWAP-Attacken (mehrere Pools)

Ein Angreifer müsste:

- zwei oder mehr große Pools dauerhaft manipulieren,  
- über hunderte Blöcke Arbitrageverluste tragen,  
- Liquidität nachschießen, um den Preis stabil zu halten.

Ökonomische Realität:

- Angriffe extrem teuer,  
- Arbitrage arbeitet ständig gegen Manipulation,  
- Redemption & Mint-Arbitrage erzeugen zusätzliche Gegenkräfte.

**Systemrelevanz: relevant, aber nur unter extremen Bedingungen.**

---

# 5. Struktur der MEV-Resilienz in ProjectUSD

## 5.1 Stärken

- robust gegen Flash-Manipulationen,  
- robust gegen Sandwich-Angriffe,  
- robust gegen Single-Pool-Manipulationen,  
- rLimiter verhindert reflexive Systemreaktionen,  
- hohe Kosten für jeden langfristigen Angriff.

---

## 5.2 Rolle der ökonomischen Kräfte

Neben dem Orakel selbst stabilisieren:

- **Arbitrage zwischen Pools**,  
- **Redemption (P < R)**,  
- **Mint-Arbitrage (P > R)**,  
- **natürliche Nutzeraktivität** (Vaults, Stability-Pool, Liquidationen).

Angreifer handeln permanent **gegen** ein System, das Preisabweichungen ausnutzt.

---

## 5.3 Systemische Eigenschaft

ProjectUSD ist:

- **träge**,  
- **robust**,  
- **deterministisch**,  
- **unbeeindruckt von kurzzeitigem Rauschen**.

Diese Trägheit ist ein Feature, kein Fehler.

---

# 6. Risiken, Modellannahmen & Grenzen

## 6.1 Geringe DEX-Liquidität
Unter sehr niedriger Liquidität kann der Median verzerrt werden.

## 6.2 Korrelation zwischen Pools
LP-Konzentration kann Manipulation erleichtern.

## 6.3 Kapitalintensive Langfrist-Manipulationen
Nicht ausgeschlossen, aber ökonomisch unattraktiv.

## 6.4 STALE-Modus
Informationsstillstand möglich, aber sicherer als falsche Daten.

## 6.5 Modellannahmen
Studie basiert auf bestimmten Liquiditäts- und Arbitragebedingungen.

---

# 7. Schlussfolgerung

ProjectUSD erreicht eine außergewöhnlich hohe MEV-Resilienz durch:

- Median-TWAP-Orakel,  
- Multi-Pool-Design,  
- Outlier-Filter,  
- STALE-Mechanismen,  
- deterministische Rate-Limits,  
- Arbitrage und Redemption als ökonomische Korrekturkräfte.

Kurzfristige Manipulationen werden zuverlässig neutralisiert.  
Langfristige Angriffe sind nur unter extremen Bedingungen möglich und ökonomisch teuer.

Der Oracle-Stack von ProjectUSD ist damit ein **bewusst träges, robustes und selbststabilisierendes System**, das nicht auf Governance, Parameteränderungen oder externe Eingriffe angewiesen ist.

---

# 8. Verification

> ## 📘 Prüfkriterien für Reviewer
- Sind alle Angriffsarten korrekt klassifiziert?  
- Sind TWAP- und Medianmechaniken korrekt beschrieben?  
- Werden Outlier-Filter und STALE-Logik korrekt wiedergegeben?  
- Ist die Interaktion mit r und ε = P − R konsistent?  
- Sind die Grenzen und Risiken vollständig dargestellt?  

Dieses Dokument bildet die Grundlage für weiterführende Studien zu Oracle-Stabilität, MEV-Ökonomie und Stresssimulationen.

