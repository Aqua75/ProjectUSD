---
title: "ProjectUSD – Oracle SPEC v1"
status: "Draft"
last_updated: "2025-11-14"
author: "Aqua75"
language: "de"
related_whitepaper_sections: ["Kap. 4 – Preissignale", "Kap. 5.2 – MedianTWAP", "Glossar S. 22–24"]
---

# ProjectUSD – Oracle SPEC v1

## Zweck

Das Oracle liefert den Marktpreis P von ProjectUSD Coin in PLS an den Controller.
Es ist damit die primäre externe Eingabegröße für das Fehlersignal:

ε = P − R

Da ProjectUSD vollständig ohne Offchain-Preisfeeds, Banken oder zentrale Datenquellen auskommt, muss das Oracle:

ausschließlich on-chain arbeiten,

manipulationsresistent sein,

mit geringer Liquidität zurechtkommen,

mehrere DEX-Pools berücksichtigen,

fail-safe sein, ohne selbst Instabilität zu erzeugen.

Dieses Dokument beschreibt das v1-Design (Option B):
MedianTWAP über mehrere DEX-Pools, gewichtet nach Liquidität.

---

## 1. Grundprinzipien

Das ProjectUSD Oracle (v1) basiert auf vier Kernideen:

- **TWAP (Time-Weighted Average Price)**  
  → glättet einzelne Trades und kurzfristige Manipulationsversuche.

- **Mehrere Pools**  
  → mehrere Informationsquellen reduzieren Angriffsvektoren.

- **Liquiditätsgewichtung**  
  → tiefere Pools haben mehr Aussagekraft als dünne.

- **Medianbildung**  
  → schützt vor Ausreißern (einzelne manipulierte Pools).

---

## 2. Datenquellen (DEX-Pools)

Das Oracle nutzt ausschließlich PulseChain DEX-Paare, die ProjectUSD Coin gegen PLS handeln.

Bezeichnet als:

- `Pool1`: ProjectUSD/PLS (DEX A)  
- `Pool2`: ProjectUSD/PLS (DEX B)  
- `Pool3`: ProjectUSD/PLS (DEX C)  
- ...

**Einschränkungen:**

- nur Pools mit ausreichender historischer Liquidität  
- nur Pools mit gültiger Reservenstruktur (keine leeren oder pausierten Paare)  
- nur Pools mit konstanter Produktlogik (`x * y = k` bzw. V3-√K-Gewichtung)

---

## 3. Preisermittlung pro Pool

### 3.1 Instant-Preis (Spot)

Der Spotpreis eines AMM-Pools ist:
`P_spot = (Reserve_PLS / Reserve_ProjectUSD)`

### 3.2 TWAP pro Pool

Für jeden Pool wird ein TWAP über N Blöcke berechnet:
`P_twap = Σ (P_spot_i * Δt_i) / Σ Δt_i`

Parameter:
TWAPWindow = 900–3600 Blöcke
MinObservations = 3

### 3.3 Liquiditätsgewichtung

Jeder Pool erhält ein Gewicht proportional zur Tiefe:
`w_i = sqrt(Reserve_PLS_i * Reserve_ProjectUSD_i)`

Damit wird verhindert, dass dünne Pools das Ergebnis verzerren.

---

## 4. Aggregation über alle Pools

### 4.1 Gewichteter Preis

Für jeden Pool:
`P_weighted_i = P_twap_i * w_i`

Gesamtpreis:
`P_agg = (Σ P_weighted_i) / (Σ w_i)`

### 4.2 Medianbildung

Zur finalen Stabilisierung wird ein Median über alle gültigen P_twap_i gebildet:
`P_final = median(P_twap_1, P_twap_2, ..., P_twap_n)`

Warum Median?
robust gegen Ausreißer
resistent gegen einzelne manipulierte Pools
ideal bei unterschiedlichen Liquiditätsprofilen

Finaler Oracle-Output:
`P = P_final`
Einheit: PLS pro ProjectUSD Coin (Marktpreis)

---

## 5. Fail-Safe / STALE-Modus

Ein Pool gilt als **STALE**, wenn:

- keine neuen Beobachtungen innerhalb `STALEWindow` vorliegen  
- Reserven unverändert bleiben, obwohl auf der DEX Aktivität stattfindet  
- der TWAP nicht berechenbar ist  
- ein On-chain-Fehler im Reserveslot vorliegt  

**Regel:**

- STALE-Pools werden für diese Epoche ignoriert.  
- Wenn alle Pools STALE sind → Oracle liefert `P = P_prev` (Freeze).  
- Der Controller setzt in diesem Fall `Δr = 0`  
  (siehe Controller-SPEC).

Damit wird verhindert, dass ein defekter Pool Instabilität erzeugt.

---

## 6. Sicherheitsmechanismen

- **Time dilation** – Mindestdauer für TWAP, um Flash-Manipulation zu verhindern.  
- **Reserve Check** – validiert, dass `x * y` im erwarteten Rahmen bleibt.  
- **MaxDeviationFilter** – wenn ein Pool mehr als `10 %` von der Medianlinie abweicht → disqualifiziert.  
- **MinLiquidityFilter** – Pools unter `LiquidityFloor` werden nicht berücksichtigt.  
- **STALE-Marker** – automatische Kennzeichnung fehlerhafter Pools.

---

## 7. Integrationslogik mit dem Controller

**Ablauf pro Epoche:**

1. Oracle sammelt TWAP-Daten aus allen Pools.  
2. Filter anwenden (STALE, MinLiquidity, MaxDeviation).  
3. Median bestimmen.  
4. Wert als `P` publizieren.  
5. Controller liest `P` und berechnet `ε = P − R`.  
6. Controller erzeugt neues `r_next`.

Alle Werte werden on-chain geloggt, z. B.:

`OracleUpdate(P, poolsUsed, block.number)`

---

## 8. Offene Parameter (Design in Progress)

| Parameter        | Status          | Nächster Schritt                   |
| ---------------- | --------------- | ---------------------------------- |
| `TWAPWindow`     | 900–3600 Blöcke | Kalibrierung über SimKit           |
| `LiquidityFloor` | noch offen      | Analyse historischer PulseX-Daten  |
| `MaxDeviation`   | 10 %            | muss empirisch bestätigt werden    |
| `PoolWhitelist`  | dynamisch       | abhängig von DEX-Landschaft        |
| `STALEWindow`    | noch offen      | realistische Blockdauer definieren |

Hinweis: Alles klar als „Design in Progress“ markiert.

---

## 9. Verification (Prüf- & Validierungsleitfaden)

**Ziel:**  
Nachweis, dass `P` durch TWAP + Median stabil, robust und resistent gegen Manipulation ist.

Methoden:

- **SimKit Backtests**
– TWAP-Reaktion auf große Trades
– Liquiditäts-Drops simulieren
– Flash-Manipulationen testen

- **Manipulation Tests**
– Sandwich-Angriffe
– Fake-Liquidität
– Single-Pool-Angriffe

- **TelemetryAudit**
– Vergleich P_twap vs. P_spot
– Abweichung zu Median pro Pool
– Monitoring des STALE-Status

**Akzeptanzkriterien:**

- Medianabweichung < 1 % über 90 % der Epochen  
- kein Flash-Manipulationsfenster innerhalb `TWAPWindow`  
- Oracle-Ausfall führt zu kontrolliertem `Controller-Δr = 0`

---

## 10. Geplante Erweiterungen (Richtung Option C)

Dieser Abschnitt beschreibt bewusst zukünftige Features, die NICHT Teil des v1-Designs sind.

Potenzielle Erweiterungen:

- **MAD-Filter (Median Absolute Deviation)**  
  → noch stärkere Ausreißererkennung

- **Volatilitätskanal (interner PLS-Volatilitätsindikator)**  
  → Filterung extrem instabiler Marktphasen

- **Mehrstufige Preisglättung**  
  → Kombination aus MedianTWAP und Vorhersageband

Diese Elemente werden erst nach Backtesting & Simulation ergänzt.

---

## 11. Lizenz & Referenzen

© 2025 Aqua75 / ProjectUSD
Lizenz: MIT für Code, CC BY-NC-SA 4.0 für Dokumentation
Verweis: ProjectUSD Whitepaper V2.1 (Kap. 4, 5.2, Glossar S. 22–24)
