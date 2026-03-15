[← Kapitel 9](09-kapitel-9.md) | [Inhaltsverzeichnis](README.md)

---

# Glossar - Schlüsselbegriffe von ProjectUSD

## R - Gleichgewichtspreis (Redemption Price)<br>
Der interne Referenzwert, um den sich der Marktpreis von ProjectUSD stabilisiert.<br>
Er dient als mathematischer „Anker“ des Systems und wird ausschließlich durch On-Chain-<br>
Mechanismen bestimmt - nicht durch externe Orakel oder Fiat-Preise.

---

## r - Systemrate (Interest / Saving Rate)<br>
Die variable Steuerungsgröße des Controllers.<br>
**r** ist die Systemrate (Zins- bzw. Sparrate) und reguliert das Verhalten von Schuldnern und Sparern.<br>
- Steigt r → Geldschöpfung wird teurer → Angebot sinkt.<br>
- Sinkt r → Halten und Prägen werden attraktiver → Nachfrage steigt.<br>
So sorgt r für das Gleichgewicht zwischen Marktpreis (P) und internem Preis (R).

---

## Vault<br>
Ein persönlicher Smart-Contract-Tresor, in dem Nutzer PulseChain-Assets (z. B. PLS) als Sicherheit<br> 
hinterlegen, um ProjectUSD zu prägen.<br>
Jeder Vault ist individuell, vollständig On-Chain und unterliegt klaren Regeln für Besicherung,<br> 
Liquidation und Rückzahlung.

---

## Stability Pool<br>
Ein kollektiver Sicherungspool, in dem Nutzer ProjectUSD hinterlegen, um Liquidationen zu<br>
ermöglichen und Belohnungen zu verdienen.<br>
Wenn ein Vault unterbesichert ist, wird seine Schuld mit Mitteln aus dem Stability Pool beglichen, die<br>
Sicherheiten (PLS) gehen an die Einzahler.<br>
So wird das System automatisch stabilisiert.

---

## Redemption-Engine<br>
Der innere Preisanker von ProjectUSD.<br>
Jeder Nutzer kann ProjectUSD jederzeit zum Gleichgewichtspreis R gegen PLS eintauschen.<br>
Diese Einlösbarkeit schafft arbitragebasierte Rückkopplung: Preisabweichungen werden durch<br>
Marktteilnehmer automatisch ausgeglichen.

---

## AMO - Algorithmic Market Operations<br>
Optionale, algorithmisch gesteuerte Module zur Feinsteuerung von Liquidität.<br>
AMOs agieren innerhalb enger Preisränder, um Arbitrage-Spreads zu reduzieren, Überschüsse zu<br>
verwalten oder die Systemreserven (Surplus-Puffer) effizienter einzusetzen.<br>
Alle AMO-Aktivitäten sind transparent und budgetiert.

---

## PSM - Peg Stability Module<br>
Ein optionaler On-Chain-Korb anderer Stablecoins (z. B. USDL), der dazu dient, kurzfristige<br>
Marktfriktionen zu dämpfen.<br>
Er ist strikt limitiert (Tagesgrenzen, Haircuts) und niemals Voraussetzung für die Funktionsfähigkeit<br>
von ProjectUSD.<br>
Selbst ohne PSM bleibt das System vollständig autark.

---

## Surplus-Puffer<br>
Ein gemeinsamer Reservepool, gespeist durch Gebühren aus Prägungen, Tilgungen und Liquidationen.<br>
Er dient als ökonomisches Sicherheitsnetz, das Schwankungen der Systemrate r glättet und langfristige<br>
Sparerträge finanzieren kann.

---

## Immutable Core<br>
Der unveränderliche Kerncode von ProjectUSD.<br>
Er enthält alle kritischen Funktionen (Vaults, Liquidation, Controller, Orakel, Redemption) und kann<br>
nach dem Freeze-Event nicht mehr verändert werden.<br>
Dadurch wird ProjectUSD zu einem autonomen, unbestechlichen System.

---

## Freeze-Event<br>
Der Moment, in dem der Kerncode dauerhaft eingefroren wird.<br>
Nach dem Freeze-Event ist ProjectUSD vollständig dezentralisiert, selbsttragend und nicht mehr von<br>
Governance oder Entwicklern abhängig.

---

## Controller<br>
Das ökonomische Steuerzentrum von ProjectUSD.<br>
Er misst die Preisabweichung zwischen Marktpreis (P) und Gleichgewichtspreis (R)<br>
und passt daraufhin die Systemrate (r) an.<br>
So reguliert er das gesamte System dynamisch und hält die Stabilität aufrecht.

---

[← Kapitel 9](09-kapitel-9.md) | [Inhaltsverzeichnis](README.md)
