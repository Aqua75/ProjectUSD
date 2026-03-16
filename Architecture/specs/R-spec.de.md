---
title: "ProjectUSD – R SPEZIFIKATION"
status: "Draft"
last_updated: "2026-03-16"
language: "de"
---

# ProjectUSD – R Spezifikation

## 1. Zweck

`R` definiert den **internen Referenzpreis** des ProjectUSD-Protokolls.

Er ist **kein Marktpreis** und wird nicht aus externen Preisfeeds abgeleitet.  
Stattdessen entsteht `R` **aus den internen Zuständen des Systems** und dient als
interne Bewertungseinheit innerhalb des Protokolls.

`R` erfüllt drei grundlegende Funktionen:

1. **Referenzwert für den Controller**  
   Der Controller vergleicht den Marktpreis `P` mit `R`, um Richtung und Stärke
   der Anpassung der Systemrate `r` zu bestimmen.

2. **Referenzpreis für Redemption**  
   Der Redemption-Mechanismus verwendet `R` als internen Umrechnungswert,
   wenn ProjectUSD innerhalb des Protokolls gegen PLS-Collateral aus
   bestehenden Vaults eingelöst wird.

3. **Referenzwert für Vault-Operationen**  
   Bei der Erzeugung von ProjectUSD aus Vault-Collateral dient `R`
   als interner Bewertungsmaßstab für das Verhältnis zwischen
   hinterlegtem PLS und erzeugter ProjectUSD-Schuld.

`R` fungiert somit als **interner Gleichgewichtsanker des Systems** und als
Bewertungseinheit für alle zentralen Protokollmechanismen.

---

## 2. Formale Definition

| Eigenschaft | Definition |
|-------------|------------|
| Variable | `R` |
| Typ | interner Protokoll-Referenzpreis |
| Einheit | `PLS pro ProjectUSD Coin` |
| Wertebereich | `R > 0` |
| Zugriff | lesbar für Controller, Redemption-Logik und Telemetrie |

Normative Definition:

`R` ist der **interne Referenzpreis des ProjectUSD-Systems**, ausgedrückt in
PLS pro ProjectUSD Coin.

Der Wert von `R` ergibt sich aus den **inneren Zuständen des Protokolls**,
insbesondere aus:

- den Collateral- und Schuldpositionen der Vaults
- den Redemption-Operationen
- der Systemschuldstruktur
- den Liquidationsdynamiken
- dem Surplus- und BadDebt-Zustand des Systems

`R` wird **nicht durch Governance gesetzt** und **nicht durch externe
Preisfeeds bestimmt**.

---

## 3. Einheit

Die kanonische Einheit für `R` lautet:

PLS pro ProjectUSD Coin

Diese Einheit muss in allen Protokollkomponenten konsistent verwendet werden.

Beispiel (Momentaufnahme):

R = 0.002 PLS pro ProjectUSD

Das bedeutet in diesem Systemzustand:

1 ProjectUSD Coin entspricht intern 0.002 PLS.

Dieser Wert ist **kein fixer Systemparameter** und kann sich
durch Veränderungen der Systemzustände verändern.

Alle Controller-Berechnungen müssen für `P` dieselbe Einheit verwenden.

---

## 4. Interaktion mit dem Controller

Der Controller misst die Abweichung zwischen Marktpreis `P`
und internem Referenzpreis `R`.

Abweichungssignal:

ε = (P − R) / R

Interpretation:

| Zustand | Bedeutung |
|--------|-----------|
| P > R | ProjectUSD wird über dem internen Referenzwert gehandelt |
| P < R | ProjectUSD wird unter dem internen Referenzwert gehandelt |
| P ≈ R | System befindet sich nahe dem Gleichgewicht |

Controller-Reaktion:

wenn P > R → Systemrate `r` steigt  
wenn P < R → Systemrate `r` sinkt

Der Controller **berechnet `R` nicht** und **verändert `R` nicht**.

Er reagiert ausschließlich auf Abweichungen zwischen
Marktpreis `P` und internem Referenzwert `R`.

---

## 5. Interaktion mit Redemption

Der Redemption-Mechanismus ermöglicht es, ProjectUSD
zum **aktuellen internen Referenzpreis `R`** gegen
Collateral einzulösen.

Normative Redemption-Formel:

PLS_out = ProjectUSD_redeemed × R

Beispiel (bei aktuellem Systemzustand):

R = 0.002 PLS pro ProjectUSD  
Redeem = 100 ProjectUSD

Ergebnis:

PLS_out = 100 × 0.002 = 0.2 PLS

Redemption definiert damit den **internen Systemwert von ProjectUSD**
auf Basis des aktuell gültigen Referenzpreises `R`.

Die Auswahl der Vaults, aus denen Collateral für Redemption
entnommen wird, ist nicht Bestandteil dieser Spezifikation.

Der genaue Ablauf der Redemption-Operation wird in der
Liquidation-Redemption-Spezifikation definiert.

---

## 6. System-Invarianten

Die folgenden Invarianten müssen jederzeit gelten.

| ID | Invariante |
|----|------------|
| R1 | R > 0 |
| R2 | P und R müssen in Controller-Berechnungen dieselbe Einheit besitzen |
| R3 | R muss deterministisch aus Systemzuständen ableitbar sein |
| R4 | R darf nicht direkt von Fiat-Referenzen oder Off-Chain-Preisfeeds abhängen |
| R5 | Governance darf R nicht manuell setzen oder überschreiben |
| R6 | derselbe aktuelle R-Wert muss konsistent von Controller, Redemption und Telemetrie verwendet werden |
| R7 | der Controller verändert R nicht |

---

## 7. Speicherung und Präzision

Implementierungen müssen die numerische Präzision von `R` definieren.

Empfohlener Standard:

Fixed-Point-Darstellung mit **18 Dezimalstellen**

Beispiel:

R = 0.002 PLS pro ProjectUSD  
gespeichert als 0.002 × 10¹⁸

Die gleiche Präzision muss konsistent verwendet werden in:

Controller  
Redemption  
Vault-Berechnungen

---

## 8. Initialisierung

Beim Deployment des Protokolls muss ein initialer Referenzwert definiert werden:

R₀

R₀ dient als **Startwert für das System**, bis sich durch
die internen Systemzustände ein stabiler Referenzwert entwickelt.

Anforderungen:

R₀ > 0  
R₀ muss in der Einheit PLS pro ProjectUSD Coin definiert sein  
R₀ muss bei Deployment für alle Module identisch initialisiert werden

Der spätere Wert von `R` ergibt sich aus den **dynamischen Zuständen
des Systems**.

---

## 9. Transparenzanforderung

`R` muss extern beobachtbar sein.

Implementierungen müssen `R` verfügbar machen für:

Indexing  
Monitoring  
Audits  
ökonomische Analyse

`R` wird als **zentrale Systemvariable** innerhalb der
ProjectUSD-Telemetrie behandelt.

---

## 10. Verifikation

Die folgenden Tests müssen für jede Implementierung erfolgreich sein.

| Test | Beschreibung |
|-----|--------------|
| R-01 | R > 0 gilt für alle erreichbaren Zustände |
| R-02 | Controller verwendet dieselbe Einheit für P und R |
| R-03 | Redemption verwendet die kanonische Darstellung von R |
| R-04 | Governance kann R nicht überschreiben |
| R-05 | R ist extern lesbar |

Eine produktive Implementierung muss alle in dieser
Spezifikation definierten Invarianten und
Verifikationstests erfüllen.
