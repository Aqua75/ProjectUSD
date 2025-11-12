---
title: "ProjectUSD – Controller SPEC v1"
status: "Draft"
last_updated: "2025-11-12"
author: "Aqua75"
language: "de"
related_whitepaper_sections: ["Kap. 3 – Rückkopplung (R/r)", "Kap. 5.3 – Rate Limiter & Security Stack", "Glossar S. 20 – 21"]
---

# ProjectUSD – Controller SPEC v1

## Zweck

Der Controller ist das Herz des Systems.  
Er übersetzt das **Fehlersignal ε = P − R** (Differenz zwischen Marktpreis P und internem Referenzpreis R) in eine neue **Systemrate r**, die über alle Vaults und Stabilitätsmechanismen wirkt.  
Damit ersetzt ProjectUSD externe Peg-Versprechen durch **Rückkopplungs-Regelung**.

---

## 1. Zentrale Begriffe & Parameter

| Parameter | Beschreibung | Beispielwert | Einheit |
|------------|---------------|---------------|----------|
| `R` | Gleichgewichtspreis (ProjectUSD → PLS) | 1.0000 | PLS pro ProjectUSD Coin (Systemgleichgewicht) |
| `P` | Marktpreis (ProjectUSD auf DEX / MedianTWAP) | 0.998–1.002 | PLS pro ProjectUSD Coin (Marktpreis) |
| `ε` | Abweichung = P − R | — | PLS pro ProjectUSD Coin (Marktpreis) |
| `r` | Systemrate (Zins/Schuldkosten p. Epoche) | 0 – 0.05 | 1/Epoche |
| `EpochLength` | Dauer einer Regelperiode (z. B. 3600 Blöcke) | — | Blöcke |
| `Kp` | Proportional-Verstärkung (des Controllers) | 0.5 – 1.5 | — |
| `Deadband` | Schwellenbereich, in dem ε ignoriert wird | 0.001 (0.1 %) | relativ |
| `δr_max` | Maximaler RateChange pro Epoche (RateLimiter) | 50 bp | — |
| `SurplusBuffer` | Systempuffer zur r-Glättung (Fees) | — | ProjectUSD |
| `LimiterHit%` | Anteil der Epochen, in denen δr_max erreicht wird | — | % Epoche |

---

## 2. Funktionsprinzip (Algorithmus)

```solidity
function controllerStep() external {
    epsilon = P - R;

    if (abs(epsilon/R) < Deadband) return; // keine Änderung

    delta_r = Kp * (epsilon / R);

    // RateLimiter
    delta_r = clamp(delta_r, -δr_max, +δr_max);

    r_next = r_prev + delta_r;

    emit ControllerUpdate(epsilon, r_next, block.number);
}
```

Erläuterung:

- Positive ε (P > R) → r steigt → Schulden werden teurer → Emission verlangsamt → P sinkt.

- Negative ε (P < R) → r sinkt → Schulden werden billiger → Emission steigt → P steigt.

- Ergebnis: P oszilliert um R – Stabilität durch Bewegung, nicht durch Fixierung.

---

## 3. Invarianten

| Kürzel | Bedingung | Bedeutung |
|---------|------------|-----------|
| I1 | &#124;P−R&#124;/R ≤ 2 % über N Epochen im Gleichgewicht | Peg bleibt innerhalb definierter Toleranz |
| I2 | &#124;Δr&#124; ≤ δr_max immer | RateLimiter greift korrekt |
| I3 | `r ≥ 0` und `r ≤ r_cap` | keine negativen oder explosiven Zinsen |
| I4 | `SurplusBuffer ≥ 0` | Puffer kann nie negativ werden |
| I5 | `LimiterHit% < 25 %` | System operiert meist innerhalb Regelbandes |

---

## 4. Telemetrie & Messgrößen

| KPI            | Beschreibung                             | Quelle                |
| -------------- | ---------------------------------------- | --------------------- |
| `PegDeviation` | |P − R| / R in bp                        | MedianTWAP Aggregator |
| `HalfLife_P→R` | Zeit, bis Abweichung halbiert ist        | ControllerLog         |
| `rVolatility`  | Standardabweichung von r über 30 Epochen | r-Historie            |
| `LimiterHit%`  | Epoche-Quote mit Δr = δr_max             | ControllerLog         |
| `SurplusLevel` | Höhe des Gebührenpuffers                 | Accounting Module     |

---

## 5. Integration in das System

- Controller ruft OrakelAggregator (MedianTWAP) pro Epoche auf.

- Ergebnisse (P) → Kontrollroutine controllerStep().

- r_next wird in VaultEngine und StabilityPool als aktuelle Systemrate übernommen.

- Gebührenflüsse → SurplusBuffer → ggf. r-Glättung in Folgeepochen.

---

## 6. Sicherheitsmechanismen

- Limiter: Verhindert Sprünge > δr_max pro Epoche.

- Deadband: verhindert Jitter durch DEX-Noise.

- Failsafe: Bei Orakelstatus STALE → Δr = 0.

- Transparency: alle Variablen (r, ε, P, R) onchain öffentlich.

- AuditLog: jede Regeländerung mit Blocknummer, ε, r_next.

---

## 7. Tests (Mindestanforderungen)

| Test-ID | Beschreibung                | Ziel                                                                 |
| ------- | --------------------------- | -------------------------------------------------------------------- |
| C-01    | Konvergenztest bei ε = +1 % | r erhöht sich und Peg kehrt binnen T Epochen zurück                  |
| C-02    | Limitertest                 | Δr überschreitet nie δr_max                                          |
| C-03    | Deadbandtest                | ε innerhalb Band → r unverändert                                     |
| C-04    | OrakelFailMode              | Status = STALE → Δr = 0                                              |
| C-05    | TelemetrieKonsistenz        | alle KPIs werden korrekt geloggt und nicht negativ                   |
| C-06    | StressSim                   | PLS −50 % → r reagiert innerhalb Epochenlimit und stabilisiert P → R |

---

## 8. Offene Parameter (Design in Progress)

| Parameter     | Status                                  | Nächster Schritt                               |
| ------------- | --------------------------------------- | ---------------------------------------------- |
| `Kp`          | Simulationsparameter (noch nicht final) | Backtest über 3 Schock-Szenarien (±5 %, ±10 %) |
| `δr_max`      | abhängig von Chain-Volatilität          | Empirische Ermittlung aus Testnet-Runs         |
| `Deadband`    | aktuell 0.1 %                           | Evaluation über DEX-Noise-Profil von PLS Pairs |
| `EpochLength` | 3600 Blöcke                             | Validierung im SimKit                          |
| `r_cap`       | 5 % pro Epoche                          | noch offen (ökonomisches Trade-off)            |

---

## 9. Verification (Prüf- & Validierungsleitfaden)

**Ziel:**  
Nachweis, dass der Controller **P → R** innerhalb definierter Halbwertszeit führt, ohne Über- oder Untersteuerung.

**Methoden:**

- **SimKit (Backtest)**  
  – PLS-Preisreihe mit ±30 %, ±50 %, ±70 % Schocks speisen  
  – `controllerStep()` pro Epoche anwenden  
  – Metriken: Halbwertszeit, LimiterHit %, rVolatility  

- **UnitTests (Foundry)**  
  – ε, Deadband, Limiter Testfälle C-01 – C-04 ausführen  

- **TelemetryAudit**  
  – Korrelation ε → Δr im Subgraph prüfen  
  – Veröffentlichung wöchentlicher *State of the Peg*-Berichte  

**Akzeptanzkriterium:**  
MedianPegAbweichung < 100 bp über 30 Epochen; Halbwertszeit ≤ 10 Epochen; LimiterHit % < 25 %.

---

## 10. Hinweise & Risiken

- Der Controller stabilisiert ausschließlich den **internen Gleichgewichtspreis R**, also das Verhältnis zwischen **PLS und ProjectUSD Coin**.  
  Der externe Marktwert von PLS bleibt dabei volatil.  

- Bei dauerhaftem Mangel an DEX-Liquidität greifen die Fallback-Mechanismen des Orakels und der RateLimiter.  

- Psychologische Marktphasen (Panik oder Überhitzung) können temporäre Abweichungen verlängern;  
  das System bleibt jedoch mathematisch messbar stabil.

---

## 11. Lizenz & Referenzen

© 2025 Aqua75 / ProjectUSD
Lizenz: MIT für Code, CC BY-NC-SA 4.0 für Dokumentation
Verweis: ProjectUSD Whitepaper V2.1 (Kap. 3, 5.3, Glossar S. 20 – 21)
