---
title: "ProjectUSD – R SPEZIFIKATION"
status: "Draft"
last_updated: "2026-03-16"
language: "de"
---

# ProjectUSD – R Spezifikation

## 1. Zweck

`R` definiert den internen Referenzpreis des ProjectUSD-Protokolls.

Er ist **kein Marktpreis** und wird nicht aus externen Preisfeeds abgeleitet.  
Stattdessen ist `R` eine vom Protokoll definierte Referenzgröße, die intern vom System verwendet wird.

`R` erfüllt zwei grundlegende Funktionen:

1. **Referenzwert für den Controller**  
   Der Controller vergleicht den Marktpreis `P` mit `R`, um Richtung und Stärke der Anpassung der Systemrate `r` zu bestimmen.

2. **Referenzpreis für Redemption**  
   Der Redemption-Mechanismus verwendet `R` als internen Umrechnungswert, wenn ProjectUSD innerhalb des Protokolls gegen Collateral eingelöst wird.

`R` fungiert somit als **interner Gleichgewichtsanker** des ProjectUSD-Systems.

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

`R` ist der vom Protokoll definierte interne Referenzpreis von ProjectUSD, ausgedrückt in **PLS pro ProjectUSD Coin**.

Dieser Wert stellt den internen Systempreis dar, der für Protokollberechnungen und Redemption-Operationen verwendet wird.

---

## 3. Einheit

Die kanonische Einheit für `R` lautet:

PLS pro ProjectUSD Coin

Diese Einheit muss in allen Protokollkomponenten konsistent verwendet werden.

Beispiel:

R = 0.002 PLS pro ProjectUSD

Das bedeutet:

1 ProjectUSD Coin = 0.002 PLS

Alle Controller-Berechnungen müssen für `P` dieselbe Einheit verwenden.

---

## 4. Interaktion mit dem Controller

Der Controller misst die Abweichung zwischen Marktpreis `P` und internem Referenzpreis `R`.

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

Der Controller **verändert `R` nicht**.  
Er reagiert ausschließlich auf Abweichungen zwischen `P` und `R`.

---

## 5. Interaktion mit Redemption

Der Redemption-Mechanismus ermöglicht es, ProjectUSD zum internen Referenzpreis `R` gegen Collateral einzulösen.

Normative Redemption-Formel:

PLS_out = ProjectUSD_redeemed × R

Beispiel:

R = 0.002 PLS pro ProjectUSD  
Redeem = 100 ProjectUSD

Ergebnis:

PLS_out = 100 × 0.002 = 0.2 PLS

Redemption definiert damit den **internen Systemwert** von ProjectUSD unabhängig von externen Fiat-Preisen.

---

## 6. System-Invarianten

Die folgenden Invarianten müssen jederzeit gelten.

| ID | Invariante |
|----|------------|
| R1 | R > 0 |
| R2 | P und R müssen in Controller-Berechnungen dieselbe Einheit besitzen |
| R3 | R muss durch deterministische On-Chain-Protokolllogik definiert sein |
| R4 | R darf nicht von Fiat-Referenzen oder Off-Chain-Preisfeeds abhängen |
| R5 | Governance darf R nicht manuell setzen oder überschreiben |
| R6 | derselbe aktuelle R-Wert muss konsistent von Controller, Redemption und Telemetrie verwendet werden |

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

Beim Deployment des Protokolls muss ein Anfangswert definiert werden:

R0

Anforderungen:

R0 > 0  
konsistent mit der Einheitsdefinition  
identisch in allen Modulen beim Deployment

---

## 9. Transparenzanforderung

`R` muss extern beobachtbar sein.

Implementierungen müssen `R` verfügbar machen für:

Indexing  
Monitoring  
Audits  
ökonomische Analyse

`R` wird als **zentrale Systemvariable** innerhalb der ProjectUSD-Telemetrie behandelt.

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

Eine produktive Implementierung muss alle in dieser Spezifikation definierten Invarianten und Verifikationstests erfüllen.
