# Study 02 – Liquidationskaskaden und die Rolle des Stability Pools in Stressszenarien
*Wissenschaftliche Analyse der Liquidationsmechanik, des Risikotransfers und der Systemstabilität unter Extrembedingungen*  
*(Level-3 Research Format)*

---

## Abstract

Liquidationen sind ein zentraler Mechanismus in ProjectUSD:  
Sie entfernen unterbesicherte Positionen, vernichten ProjectUSD-Supply und verteilen PLS-Collateral an Stability-Pool-Teilnehmer.  

Diese Studie untersucht das Verhalten des Systems bei Einzel-Liquidationen, seriellen Liquidationen und Liquidationskaskaden in Stressszenarien. Besonderer Fokus liegt auf:

- dem Zusammenspiel von Collateral Ratio (CR), Price Floor und Liquidation Threshold  
- der Rolle des Stability Pools als Schockabsorber  
- der Dynamik bei starken Preisabfällen  
- den Eigenschaften von Kaskaden und deren Begrenzung  
- den Mechanismen, die verhindern, dass der Systemkern destabilisiert wird

Die Analyse zeigt: Liquidationen sind kein Fehlerzustand, sondern ein fundamentales Selbstreinigungsprinzip, das das System resilient gegen Marktstress macht.

---

# 1. Einleitung – Liquidationen als Stabilitätsmechanismus

In ProjectUSD dienen Liquidationen zur:

- Entfernung unterbesicherter Vaults  
- Rückführung überschuldeter Positionen  
- Sicherstellung, dass der Gesamt-Collateralwert jeder Zeit die Systemverpflichtungen übersteigt  
- Verteilung von PLS an Stability-Pool-Teilnehmer  
- Reduktion des umlaufenden ProjectUSD-Supply

Im Gegensatz zu zentralen Systemen trifft ProjectUSD rein **algorithmische**, **deterministische** Entscheidungen ohne Governance oder menschlichen Eingriff.

Das Liquidationsmodul ist so konzipiert, dass es:

- **frühzeitig** eingreift (bei Unterbesicherung)  
- **sofort** ausführt  
- **keine Schulden zurücklässt**  
- **keine Systemslippage erzeugt**  
- **keine Staatshilfen oder Backstop-Fonds benötigt**  

Liquidationen sind daher ein aktives Instrument der Systemgesundheit und nicht ein Fehlerfall.

---

# 2. Systemkomponenten und zentrale Begriffe

## 2.1 Liquidation Threshold (LT)

Die Liquidationsschwelle definiert den Punkt, an dem eine Vault unterbesichert ist.  
Typischerweise:

- **CR unter 110 % → liquidierbar**  
- Vault wird geschlossen  
- Schuld wird aus dem Stability Pool beglichen  

---

## 2.2 Collateral Ratio (CR)

> ## 📘 Definition – Collateral Ratio
> Die Collateral Ratio einer Vault berechnet sich als:
>
> $$
> CR = \frac{\text{PLS Collateral Wert}}{\text{ProjectUSD-Schuld}}
> $$

Der CR bestimmt, ob eine Position sicher, riskant oder liquidierbar ist.

---

## 2.3 Stability Pool

- Puffer gegen Schocks  
- nimmt Liquidationen auf  
- erhält PLS-Collateral  
- löscht die entsprechende ProjectUSD-Schuld  
- schützt das System vor „toxic debt“

Der Pool fungiert als **erstes Sicherheitsnetz** bei Marktstress.

---

## 2.4 Liquidator Reward

Jede Liquidation erzeugt einen Bonus für Stability-Pool-Teilnehmer, da sie PLS zu einem effektiven Abschlag erhalten.

Dies schafft einen ökonomischen Anreiz, im Stability Pool zu bleiben.

---

# 3. Dynamik von Einzel-Liquidationen

Eine Einzel-Liquidation erfolgt, wenn:

1. der PLS-Preis fällt  
2. die Collateral Ratio einer Vault unter die Liquidationsschwelle sinkt  
3. der Stability Pool genug ProjectUSD hält, um die Schuld zu decken  
4. das System automatisch die Liquidation ausführt

Ablauf:

- Stability Pool zahlt die geschuldete Menge ProjectUSD  
- Vault wird gelöscht  
- Collateral (PLS) geht an den Stability Pool  
- ein Liquidator Reward entsteht  
- der Gesamtsupply von ProjectUSD sinkt  

Dieses Verhalten stärkt das System:

- **mehr Collateral pro existierendem ProjectUSD**  
- **weniger Schulden**  
- **sauberere Risikoallokation**

---

# 4. Serielle Liquidationen (normale Stressphasen)

Bei moderaten Preisabfällen treten Liquidationen seriell auf:

- mehrere Vaults fallen nacheinander unter die Schwelle  
- der Stability Pool verarbeitet sie einzeln  
- zwischen Liquidationen erholt sich das Verhältnis von Collateral zu Schulden  
- der PLS-Preis stabilisiert sich intermittierend

Ökonomische Eigenschaften:

- Stability-Pool-Teilnehmer erhalten mehrfach Reward  
- ProjectUSD-Supply nimmt ab  
- der Systemkern bleibt stabil  
- es entsteht keine Überschuldung

Serielle Liquidationen sind der Normalfall in Stressphasen.

---

# 5. Liquidationskaskaden (starke Preiscrashs)

Eine Liquidationskaskade entsteht, wenn:

- der PLS-Preis sehr schnell und stark fällt  
- viele Vaults gleichzeitig unter die Schwelle rutschen  
- der Stability Pool nacheinander viele Schulden absorbiert  

Kennzeichen einer Kaskade:

- **hohe Frequenz an Liquidationen pro Block**  
- **rascher Transfer von PLS zu Stability-Pool-Teilnehmern**  
- **massive Reduktion des ProjectUSD-Supplys**  
- **Bereinigung schwacher Collateralpositionen**

Kaskaden sind intensiv, aber sie führen zu einer **sauberen Systemstruktur** nach dem Crash.

---

# 6. Begrenzung von Kaskaden – Warum das System nicht kollabiert

In zentralisierten Systemen wären Kaskaden ein Risiko.  
In ProjectUSD ist das Gegenteil der Fall:  
Sie sind ein **automatischer Selbstreinigungsprozess**.

Mehrere Eigenschaften begrenzen das Risiko:

## 6.1 Kein negatives Eigenkapital möglich

Das System kann **niemals** mehr ProjectUSD schulden als existiert.  
Jede Liquidation neutralisiert:

- Schuld  
- und Collateral  

→ Debt wird nicht systemweit verschoben.

---

## 6.2 Stability Pool absorbiert Schocks

Der Pool nimmt PLS auf und löscht ProjectUSD-Schulden.

Dadurch entsteht:

- mehr Collateral-Deckung  
- weniger Supply  
- höherer Wert pro ProjectUSD

Kaskaden **stärken** langfristig die Deckung.

---

## 6.3 Redemption als ultimative Stabilitätsschicht

Wenn der Marktpreis P unter R fällt, entsteht Redemption-Arbitrage:

- Buy ProjectUSD → Redeem → Erhalte PLS  
- reduziert schwache Vaults  
- stärkt die Gesamtbesicherung

Redemption wirkt auch während Kaskaden.

---

## 6.4 Keine Preis-Manipulation durch Liquidationen

Wichtig:

- Liquidationen verkaufen **kein Collateral auf dem Markt**  
- es entsteht **kein Verkaufsdruck**  
- PLS wird **intern** an Stability-Pool-Teilnehmer übertragen  
- Marktpreis P bleibt unbeeinflusst

Dadurch bleiben Kaskaden isoliert und systemintern.

---

## 6.5 Systemweite Rebalancings sind selbststabilisierend

Eine Kaskade führt zu:

- einem höheren Collateral-Überschuss  
- stärkerer Deckung pro ProjectUSD  
- einer Reduktion des Gesamtrisikos  
- einer Verlagerung des Collaterals zu den robustesten Teilnehmern  

Das System endet in einem **sichereren Zustand** als vor der Kaskade.

---

# 7. Rolle der Nutzerprofile

## 7.1 Stability-Pool-Teilnehmer  
- profitieren von Rewards  
- tragen Schockabsorption  
- erhalten unterbewertetes PLS  

## 7.2 Vault-Nutzer  
- tragen Marktrisiko  
- riskieren Liquidation  
- sind Teil der Deleveraging-Dynamik  

## 7.3 Arbitrageure  
- stabilisieren P → R  
- beschleunigen die Erholung nach Stress

---

# 8. Schlussfolgerung

Liquidationen sind ein integraler Bestandteil des Stabilitätsmechanismus von ProjectUSD.  
Sie:

- verhindern systemische Überschuldung  
- stärken die Collateralbasis  
- verteilen Risiko effizient  
- ermöglichen eine marktorientierte Bereinigung  
- wirken besonders effektiv in Stressphasen

Liquidationskaskaden sind kein Systemfehler, sondern ein notwendiger Reset-Mechanismus, der das System nach heftigen Marktbewegungen widerstandsfähiger macht.

---

# 9. Verification

> ## 📘 Prüfkriterien für Reviewer
- Entspricht die Darstellung den Spezifikationen?  
- Sind Liquidationspfade logisch konsistent?  
- Entsteht an keiner Stelle negatives Eigenkapital?  
- Ist die Rolle des Stability Pools korrekt modelliert?  
- Sind die Stressszenarien kohärent und reproduzierbar?  

Dieses Dokument dient als strukturelle Grundlage für weitere Studien zu Stressresilienz, Schockpropagation und Interaktion mit Controller-Logik und Redemption-Mechanismen.
