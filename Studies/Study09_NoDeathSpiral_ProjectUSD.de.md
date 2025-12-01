# Study 09 – Warum ProjectUSD keine Death Spirals entwickeln kann
*Systemische Analyse der Gegenkräfte, Rückkopplungsmechanismen und strukturellen Barrieren gegen Abwertungskaskaden*  
*(Level-3 Research Format)*

---

## Abstract

Viele algorithmische Stablecoins scheiterten aufgrund sogenannter **Death Spirals**:  
Kaskaden selbstverstärkender Abwertung, in denen Preisverfall → Panik → weitere Abwertung → Systemkollaps erzeugt.  

Diese Studie zeigt, warum ProjectUSD **strukturell immun** gegen Death Spirals ist.  
Grund: ProjectUSD besitzt weder die Mechanismen noch die Feedback-Schleifen, die Death Spirals ermöglichen.  
Wesentliche Ursachen solcher Kollapsdynamiken – wie reflexive Token-Dualitäten, ungesicherte Arbitrage, exogene Peg-Bindung oder unlimitierte Supply-Ausdehnung – existieren in ProjectUSD **nicht**.

Die Stabilität entsteht durch drei fundamentale Elemente:

1. **interner Wertanker R**, unabhängig von externem Fiat,  
2. **Redemption-Mechanik**, die P immer zu R zurückführt,  
3. **Controller (r)**, der systemweite Verstärkungsschleifen dämpft statt verstärkt.

Damit ist ProjectUSD das Gegenteil klassischer algorithmischer Stablecoins:  
Es hat *keine* direkte Abhängigkeit zwischen Marktpreis und existenzieller Systemsolvenz – und kann deshalb *keine* Death Spiral erzeugen.

---

# 1. Einleitung – Was ist eine „Death Spiral“?

Eine Death Spiral ist eine Dynamik, in der:

1. Preis fällt  
2. Systemdruck entsteht (z. B. durch Collateralverlust, Peg-Verlust, Arbitrage­druck)  
3. Marktteilnehmer reagieren reflexiv (Verkauf, Exit, Burn/Mint-Fehler)  
4. daraus weiterer Preisverfall entsteht  
5. schließlich das System vollständig kollabiert

Beispiele:

- **Terra/UST** – reflexive Burn/Mint-Dualität  
- **ESD/DSD** – ungesicherter Rebase-Mechanismus  
- **IRON / TITAN** – instabiles Collateral + reflexive Governance-Token  
- **AMPL** – Rebase-bedingte Vertrauensverluste  
- **USTC** – Verlust externer Reserven → vollständige Entankerung

Charakteristisch:  
Das System beginnt, **seine eigene Wertbasis zu zerstören**, wodurch der Preisverfall auf sich selbst zurückwirkt.

---

# 2. Warum Death Spirals in ProjectUSD strukturell unmöglich sind

Death Spirals benötigen mindestens einen der folgenden Mechanismen:

| Mechanismus | Beschreibung | Führt zu Death Spirals |
|-------------|--------------|-------------------------|
| 1. Reflexive Token-Dualität | Stablecoin + Volatilitäts-Token minten/burnen einander | Ja |
| 2. Peg-Abhängigkeit vom Markt | Peg hängt vom Vertrauen oder Außenmarkt ab | Ja |
| 3. Unbegrenzte Expansion | System mintet unbegrenzt, um Peg zu halten | Ja |
| 4. Collateral-Dumping | System muss Assets verkaufen, wenn Preis fällt | Ja |
| 5. Exogene Orakel mit Fehlpreisrisiko | Fehlerhafte Feeds erzeugen falsche Liquidationen | Ja |

None of these mechanisms exist in ProjectUSD.

---

# 3. Fundamentale Unterschiede zu klassischen algorithmischen Stablecoins

## 3.1 Keine Token-Dualität  
Es gibt **keinen zweiten Token**, der:

- den Preis von ProjectUSD stützen müsste,  
- geburnt oder gemintet würde, um den Peg zu halten,  
- reflexive Abwärtsspiralen erzeugen könnte.

ProjectUSD ist ein **Eintoken-System** (plus PLS als Collateral),  
nicht ein reflexives Duo wie UST/LUNA.

---

## 3.2 Kein externer Peg  
ProjectUSD versucht **nicht**, einen externen Dollarpreis zu halten.  
Der Wertanker ist intern:

$$
R = \text{interner Gleichgewichtspreis}
$$

Wichtig:

- R hängt nicht von USD ab  
- R hängt nicht von externen Orakeln ab  
- R wird nicht durch Marktvertrauen bestimmt  

Der Wert wird **systemintern** definiert – nicht von außen aufgezwungen.

---

## 3.3 Redemption erzeugt negativen Feedback-Loop (stabilisierend)

Wenn **P < R**, entsteht eine absolute Arbitrage:

- Nutzer kaufen ProjectUSD billig  
- lösen ihn zu R ein  
- erhalten PLS  
- der Supply sinkt  
- P steigt → Rückkehr Richtung R

Dies ist ein **negativer Rückkopplungsmechanismus**  
= dämpfend, nicht verstärkend.

Er verhindert:

- Underpegs  
- Vertrauensabfluss  
- reflexive Panik

---

## 3.4 Der Controller r wirkt gedämpft statt verstärkend

Fehlerhafte Systeme verstärken Preisbewegungen (positive Rückkopplung).  
ProjectUSD dagegen dämpft Preisbewegungen:

- P > R → r steigt → Emission sinkt → P fällt  
- P < R → r sinkt → Nachfrage steigt → P steigt

Der Controller kann *keine* Abwärtsspirale erzeugen, weil:

- er Supply reduziert, wenn P fällt,  
- er Nachfrage erhöht, wenn P fällt,  
- er Supply reduziert, wenn Collateral fällt,  
- er niemals reflexiv in falscher Richtung reagiert.

---

## 3.5 Keine Abhängigkeit von Marktpreisen zur Solvenz

Ein wesentliches Merkmal kollabierter Systeme:  
**Sinkender Tokenpreis zerstört die Solvenz des Systems selbst.**

Beispiele:

- LUNA sinkt → UST verliert Deckung → UST sinkt → LUNA mintet → Totalverlust  
- IRON verliert Vertrauen → TITAN kollabiert → IRON entankert  

ProjectUSD ist immun:

- Die Solvenz hängt von Vault-Collateral (PLS) ab, nicht vom Preis von ProjectUSD.  
- ProjectUSD-Verkäufe verursachen *keine* Liquidationen.  
- Der Systemwert kann nicht durch Verkäufe von ProjectUSD zerstört werden.

---

# 4. Warum Liquidationen keine Spiralen auslösen können

Liquidationen in anderen Systemen führen zu Sell Pressure:

- Collateral wird verkauft  
- Preis fällt  
- mehr Liquidationen  
- weitere Verkäufe → Spirale

In ProjectUSD:

- Liquidationen verkaufen *keinen* PLS auf dem Markt  
- Collateral wird **intern** umverteilt (Stability Pool)  
- keine Auswirkung auf den PLS-Marktpreis durch Systemaktionen  
- keine Sell-Kaskaden möglich

Das System verschiebt Vermögen intern und zerstört Schulden – es erzeugt keinerlei reflexive Downward-Ketten.

---

# 5. Warum Emissionsmechanismen keine Spiralen erzeugen können

UST/LUNA scheiterte, weil das System im Stress:

- immer mehr LUNA mintete  
- um UST bei $1 zu halten  
- wodurch LUNA kollabierte → UST kollabierte → Death Spiral

In ProjectUSD ist dies **prinzipiell ausgeschlossen**:

- Emission ist limitiert durch r  
- r reagiert konträr zu Preisverlusten  
- Minting wird *unattraktiv*, wenn P fällt  
- Supply kann nicht reflexiv explodieren  

Es gibt **keinen Mechanismus**, der im Stress:

- zusätzliche Coins mintet,  
- um einen externen Preis zu verteidigen.

---

# 6. Warum fehlende externe Bindung ein Vorteil ist

Death Spirals sind fast immer an **externe Pegs** gebunden.  
Wenn das System „den Dollar“ halten muss, entstehen:

- Attack Vectors  
- selbstverstärkende Verkaufsmechanismen  
- Oracle-Abhängigkeit  
- Vertrauensabriss bei De-Pegs  

ProjectUSD besitzt diesen Angriffspunkt **nicht**.

Die Wertdefinition ist intern und algorithmisch, nicht extern oder politisch.

---

# 7. Systemische Gegenkräfte, die Death Spirals verhindern

ProjectUSD besitzt vier starke dämpfende Kräfte:

## 1) **Redemption**  
Korrigiert sofort Unterbewertungen.

## 2) **Controller r**  
Passt Angebot/Nachfrage an und verhindert Supply-Überexpansion.

## 3) **Liquidationsmechanik**  
Zerstört Schulden statt Assets zu verkaufen.

## 4) **Surplus-Puffer**  
Fängt Schocks ab und stabilisiert langfristig.

Gemeinsam erzeugen sie ein **anti-spiralisches Design**:  
Jeder Stress führt nicht zu Verstärkung, sondern zu Dämpfung.

---

# 8. Mögliche Risiken (keine Spiralen, aber realistische Stresspunkte)

Auch wenn Death Spirals ausgeschlossen sind, existieren Risiken:

## 8.1 Sehr niedrige DEX-Liquidität  
Kann Preissprünge erzeugen, aber keine Spirale.

## 8.2 Extrem volatile PLS-Märkte  
Können Redemption dämpfen, aber r stabilisiert langfristig.

## 8.3 Oracle-Ausfälle  
STALE-Modus friert r ein → verhindert falsche Reaktionen.

## 8.4 Psychologische Marktreaktionen  
Panik ist möglich, aber systemisch folgen keine reflexiven Supply-Schäden.

---

# 9. Schlussfolgerung

ProjectUSD ist eines der wenigen Geldsysteme, das **nicht** die strukturellen Voraussetzungen für Death Spirals besitzt.

Death Spirals benötigen:

- reflexive Token-Dualität  
- externe Peg-Abhängigkeit  
- unlimitierte Emission  
- Marktverkauf von Collateral  
- fehlende negative Feedback-Loops  

ProjectUSD besitzt **keinen einzigen** dieser Mechanismen.  
Im Gegenteil:  
Jede Komponente wirkt *gegen* Spiralbildung.

**ProjectUSD kann volatil sein – aber es kann nicht kollabieren, indem es sich selbst zerstört.**

Damit ist es eines der strukturell stabilsten on-chain Geldsysteme, die je entworfen wurden.

---

# 10. Verification

> ## 📘 Prüfkriterien für Reviewer
- Sind alle Spiralmechanismen korrekt identifiziert und ausgeschlossen?  
- Ist die Argumentation konsistent mit Redemption und Controller-Logik?  
- Sind Vergleiche zu historischen Death Spirals korrekt?  
- Sind Risiken korrekt klassifiziert (Stress ≠ Death Spiral)?  
- Wird der systemische Dämpfungscharakter klar dargestellt?  

Diese Studie bildet die Grundlage für tiefergehende Analysen zu Robustheit, Attack Vectors und Systemidentität in Bezug auf Stabilitätsmechanismen.
