# Glossar - Schlüsselbegriffe von ProjectUSD

## R - Gleichgewichtspreis (Redemption Price)

Der interne Referenzwert, um den sich der Marktpreis von ProjectUSD stabilisiert.

Er dient als mathematischer „Anker“ des Systems und wird ausschließlich durch On-Chain-Mechanismen bestimmt - nicht durch externe Orakel oder Fiat-Preise.

---

## r - Systemrate (Interest / Saving Rate)

Die variable Steuerungsgröße des Controllers.

r kann positiv (Zins) oder negativ (Sparerate) sein und reguliert das Verhalten von Schuldnern und Sparern.

Steigt r → Geldschöpfung wird teurer → Angebot sinkt.

Sinkt r → Halten und Prägen werden attraktiver → Nachfrage steigt.

So sorgt r für das Gleichgewicht zwischen Marktpreis (P) und internem Preis (R).

---

## Vault

Ein persönlicher Smart-Contract-Tresor, in dem Nutzer PulseChain-Assets (z. B. PLS) als Sicherheit hinterlegen, um ProjectUSD zu prägen.

Jeder Vault ist individuell, vollständig On-Chain und unterliegt klaren Regeln für Besicherung, Liquidation und Rückzahlung.

---

## Stability Pool

Ein kollektiver Sicherungspool, in dem Nutzer ProjectUSD hinterlegen, um Liquidationen zu ermöglichen und Belohnungen zu verdienen.

Wenn ein Vault unterbesichert ist, wird seine Schuld mit Mitteln aus dem Stability Pool beglichen, die Sicherheiten (PLS) gehen an die Einzahler.

So wird das System automatisch stabilisiert.

---

## Redemption-Engine

Der innere Preisanker von ProjectUSD.

Jeder Nutzer kann ProjectUSD jederzeit zum Gleichgewichtspreis R gegen PLS eintauschen.

Diese Einlösbarkeit schafft arbitragebasierte Rückkopplung: Preisabweichungen werden durch Marktteilnehmer automatisch ausgeglichen.

---

## AMO - Algorithmic Market Operations

Optionale, algorithmisch gesteuerte Module zur Feinsteuerung von Liquidität.

AMOs agieren innerhalb enger Preisränder, um Arbitrage-Spreads zu reduzieren, Überschüsse zu verwalten oder die Systemreserven (Surplus-Puffer) effizienter einzusetzen.

Alle AMO-Aktivitäten sind transparent und budgetiert.

---

## PSM - Peg Stability Module

Ein optionaler On-Chain-Korb anderer Stablecoins (z. B. USDL), der dazu dient, kurzfristige Marktfriktionen zu dämpfen.

Er ist strikt limitiert (Tagesgrenzen, Haircuts) und niemals Voraussetzung für die Funktionsfähigkeit von ProjectUSD.

Selbst ohne PSM bleibt das System vollständig autark.

---

## Surplus-Puffer

Ein gemeinsamer Reservepool, gespeist durch Gebühren aus Prägungen, Tilgungen und Liquidationen.

Er dient als ökonomisches Sicherheitsnetz, das Schwankungen der Systemrate r glättet und langfristige Sparerträge finanzieren kann.

---

## Immutable Core

Der unveränderliche Kerncode von ProjectUSD.

Er enthält alle kritischen Funktionen (Vaults, Liquidation, Controller, Orakel, Redemption) und kann nach dem Freeze-Event nicht mehr verändert werden.

Dadurch wird ProjectUSD zu einem autonomen, unbestechlichen System.

---

## Freeze-Event

Der Moment, in dem der Kerncode dauerhaft eingefroren wird.

Nach dem Freeze-Event ist ProjectUSD vollständig dezentralisiert, selbsttragend und nicht mehr von Governance oder Entwicklern abhängig.

---

## Controller

Das ökonomische Steuerzentrum von ProjectUSD.

Er misst die Preisabweichung zwischen Marktpreis (P) und Gleichgewichtspreis (R)

und passt daraufhin die Systemrate (r) an.

So reguliert er das gesamte System dynamisch und hält die Stabilität aufrecht.
