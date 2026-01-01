```markdown
# Study 15 – Extreme Stress Scenarios  
*Extremstresstests, Worst Case Szenarien und Black Swan Resilienz*  
*(Level-3 Research Format)*

---

## Abstract

ProjectUSD ist als vollständig on-chain operierendes, autonomes Geldsystem ohne Admin-Keys, ohne Pause-Mechanismus und mit einem nach dem Freeze Event unveränderlichen Kern entworfen.  
Diese Architektur maximiert Glaubwürdigkeit und Neutralität, verschiebt jedoch die gesamte Verantwortung für Stabilität und Überlebensfähigkeit auf Mechanik, Parameterwahl und Marktanreize.

Diese Studie untersucht die Robustheit von ProjectUSD unter extremen, aber plausiblen Stressbedingungen:

- 90 Prozent Preiscrash des Haupt-Collaterals PLS  
- abrupter Liquiditäts-Exodus auf DEXes  
- Chain-Reorgs und instabile Finalität  
- MEV-Extremphasen mit Front Running und Sandwiching  
- kombinierte Kaskadenszenarien

Ziel ist es, zu analysieren:  
> Unter welchen Bedingungen überlebt ProjectUSD systemisch, wo liegen strukturelle Grenzen und welche Maßnahmen erhöhen Black Swan Resilienz?

---

# 1. Einleitung – Warum Extremstresstests zentral sind

ProjectUSD folgt einer klaren Designphilosophie:

- vollständige On-Chain-Autonomie  
- kein Admin-Key  
- kein Pause-Button  
- unveränderlicher Core nach dem Freeze Event  
- Governance nur auf einer Peripherie-Ebene

Klassische Notfallmaßnahmen sind bewusst ausgeschlossen.  
Stabilität muss **emergent** entstehen – aus:

- Überbesicherung  
- Liquidationsmechanik  
- Stability Pool  
- Redemption Engine  
- Feedback-Controller über den Zinssatz r

Extremstresstests sind daher kein optionales Add-on, sondern **zwingende Voraussetzung** für ein glaubwürdiges System.

---

## 1.1 Relevante Systemkomponenten im Stressfall

Für Black Swan Szenarien sind insbesondere vier Mechanikblöcke kritisch:

**Vaults und Liquidationen**  
Nutzer hinterlegen primär PLS als Sicherheit. Fällt die Collateral Ratio unter den Liquidation Threshold, wird der Vault zwangsliquidiert.

**Stability Pool**  
Der Stability Pool begleicht Schulden liquidierter Vaults und erhält im Gegenzug deren Collateral. Überschüssiger Supply wird geburnt. Ziel ist Stressabsorption statt Eskalation.

**Redemption Engine**  
ProjectUSD kann jederzeit zum Gleichgewichtspreis R gegen Collateral eingelöst werden. Schwächste Vaults werden zuerst reduziert. Dies wirkt als innerer Preisanker.

**Controller und Zinssatz r**  
Abweichungen zwischen Marktpreis P und Gleichgewichtspreis R steuern r. Höhere r dämpfen Nachfrage, niedrigere r fördern Minting. Anpassungen sind bewusst begrenzt.

---

# 2. Stressszenarien

## 2.1 Szenario-Matrix

Es werden fünf Hauptszenarien definiert:

**S1 – PLS 90 Prozent Crash**  
Abrupter Preisverfall des Haupt-Collaterals innerhalb kurzer Zeit.

**S2 – Liquidity Exodus**  
Massiver Abzug von DEX-Liquidität, stark sinkendes Handelsvolumen.

**S3 – Reorg Storm**  
Serien von Chain-Reorgs mit instabiler Transaktionsfinalität.

**S4 – MEV Supercycle**  
Extrem erhöhte MEV-Aktivität mit Front Running, Sandwiching und Backrunning.

**S5 – Four Horsemen Kaskade**  
Kombination aller obigen Effekte mit selbstverstärkenden Feedback-Loops.

---

## 2.2 Stressparameter

Die Szenarien werden über Parametervektoren beschrieben:

- PLS-Preisprozesse mit Sprüngen und Nachbeben  
- DEX-Liquiditätseinbruch von 70 bis 95 Prozent  
- Oracle-Verzögerung und Datenrauschen  
- Reorg-Tiefe und Häufigkeit  
- MEV-Intensität und adversarialer Blockanteil

---

## 2.3 Erfolgskriterien

Ein Szenario gilt als bestanden, wenn:

1. **Solvenz** gewahrt bleibt oder Defizite klar sozialisiert werden  
2. **Peg-Resilienz** gegeben ist und Abweichungen temporär bleiben  
3. **Funktionalität** von Liquidation und Redemption erhalten bleibt  
4. **Manipulationsresistenz** gegenüber Oracle- und MEV-Angriffen besteht

---

# 3. Simulationsrahmen

Diese Studie ist konzeptionell. Konkrete Parameter sind bewusst nicht finalisiert und müssen vor Implementierung kalibriert werden.

---

## 3.1 Zustandsvariablen

- Vaults mit Collateral, Debt und Collateral Ratio  
- Stability Pool Einlage  
- Gesamt-Supply  
- DEX-Liquidität und Preisimpact  
- Oracle-Zustand  
- Controller-Zinssatz r  
- Surplus-Puffer

---

## 3.2 Liquidationslogik

Unterbesicherte Vaults werden liquidiert. Der Stability Pool begleicht Schulden und erhält Collateral.

**Offene Kernfrage:**  
Was passiert, wenn der Stability Pool nicht ausreicht?

Mögliche Fallback-Optionen:

- externe Liquidationen  
- Debt-Redistribution  
- Deckung über Surplus-Puffer

Ohne explizite Regel ist Solvenz im Worst Case nicht beweisbar.

---

## 3.3 Redemption-Mechanik

Redemptions reduzieren Supply und stabilisieren den Peg, entziehen jedoch Collateral aus den schwächsten Vaults. In illiquiden Phasen kann dies Stress verstärken.

---

## 3.4 Oracle- und Netzwerkmodell

- Median-TWAP-Orakel mit Outlier-Filter  
- Verzögerungen bei niedriger Liquidität  
- Reorgs können Oracle-Fenster und Transaktionsreihenfolge beeinflussen

---

## 3.5 MEV-Ebene

- Sandwiching  
- Front Running  
- Backrunning von Liquidationen und Redemptions  

Schutzmechanismen existieren, garantieren aber keine vollständige Immunität.

---

## 3.6 KPIs

- Peg-Abweichung und Erholungsdauer  
- Liquidationsvolumen  
- Stability-Pool-Depletion  
- Oracle-Fehler  
- r-Volatilität  
- geschätzte MEV-Extraktion  
- Nutzerbelastung durch Gas und Slippage

---

# 4. Szenarioanalyse

## 4.1 S1 – 90 Prozent PLS Crash

Ein 90 Prozent Preisverfall skaliert jede Collateral Ratio effektiv mit 0,1.

Beispiel:

- 300 Prozent CR werden zu 30 Prozent  
- 170 Prozent CR erfordern vorab ungefähr 1700 Prozent

Ergebnis:  
Ein solcher Crash liquidiert nahezu alle normal gehebelten Vaults.

---

## 4.2 Stability Pool unter Extremstress

- schneller Abbau des Stability Pools  
- Konzentration von Collateral bei SP-Einlegern  
- Risiko eines Stability-Pool-Runs aus psychologischen Gründen

---

## 4.3 Redemption im Crash

Redemption stabilisiert den Peg, kann aber Collateralbasis weiter schwächen, insbesondere bei Oracle-Lags und illiquiden Märkten.

---

## 4.4 S2 – Liquidity Exodus

Sinkendes Volumen verlangsamt Arbitrage. Oracle-Daten werden träger und unsicherer. Peg-Abweichungen können länger bestehen bleiben.

---

## 4.5 S3 – Reorg Storm

Reorgs können:

- Liquidationen reverteren  
- Reihenfolgen verändern  
- Oracle-Fenster verzerren

Ohne Pause-Mechanismus ist Reorg-Resilienz zwingend architektonisch zu lösen.

---

## 4.6 S4 – MEV Supercycle

MEV führt primär zu:

- Value Leakage  
- höheren Nutzerkosten  
- zusätzlichem Liquiditätsabzug

Der Peg kann formal halten, während Vertrauen schwindet.

---

## 4.7 S5 – Kaskade

Schutzmechanismen können gegeneinander arbeiten:

- Liquidationen  
- Oracle-Lags  
- MEV  
- Reorgs

Die Peg-Erholungszeit steigt stark. Vertrauen wird zum kritischen Faktor.

---

# 5. Maßnahmen und Designimplikationen

## 5.1 Konservatives Design vor dem Freeze

- Guarded Launch  
- niedrige Debt Caps  
- keine AMOs oder PSMs  
- intensive On-Chain-Beobachtung

---

## 5.2 Gegenmaßnahmen gegen Single-Collateral-Risiko

- höhere empfohlene Collateral Ratios  
- explizite Fallback-Liquidationsregeln  
- langfristige Collateral-Diversifikation

---

## 5.3 Maßnahmen gegen Liquidity Exodus

- tiefe Referenzpaare  
- PSM nur als Stoßdämpfer  
- streng budgetierte AMOs

---

## 5.4 Reorg-Resilienz

- reorg-sichere Oracle-Fenster  
- idempotente Liquidationen  
- klare Backlog-Fairnessregeln

---

## 5.5 MEV-Resilienz

- Batching  
- Commit-Reveal für große Redemptions  
- MEV-aware Execution  
- transparente On-Chain-Telemetrie

---

## 5.6 Surplus-Puffer

- klar definierte Einsatzregeln  
- harte Obergrenzen  
- keine implizite Rettungsgarantie

---

# 6. Fazit

ProjectUSD ist als selbstregulierendes, autonomes Geldsystem konzipiert. Gerade weil kein menschlicher Eingriff möglich ist, müssen Black Swan Risiken vor dem Freeze Event vollständig adressiert sein.

Zentrale Erkenntnisse:

- Single-Collateral-Systeme sind bei 90 Prozent Crash strukturell extrem gefordert  
- Liquidity Exodus verlängert Peg-Abweichungen  
- MEV erzeugt Reibungsverluste, auch ohne formalen Peg-Bruch  
- Reorgs sind ein ernstzunehmender Execution-Risiko-Faktor

Der konservative Pfad über Guarded Launch und späteren Freeze ist der einzig glaubwürdige Ansatz, um diese Risiken beherrschbar zu machen.

---

# 7. Verification

> ## 📘 Prüfkriterien für Reviewer

- Sind die Stressszenarien realistisch und vollständig?  
- Sind die beschriebenen Kaskadeneffekte logisch konsistent?  
- Sind offene Designfragen klar benannt?  
- Ist die Argumentation mit dem ProjectUSD-Design vereinbar?  
- Lassen sich die Szenarien in Simulationen und Testnet-Tests überführen?

Diese Studie dient als Grundlage für formale Simulationen, Audits und Testnet-Stresstests vor einem finalen Freeze Event.
```
