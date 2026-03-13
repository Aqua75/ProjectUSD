# Kapitel 8 - Risiken und Grenzen: Was ProjectUSD leisten kann ... und was nicht

Jedes System, das Werte verwaltet, trägt Risiko in sich.<br>
Der Unterschied liegt nicht darin, ob Risiken existieren,<br>
sondern wo sie liegen - und wer sie kontrolliert.

ProjectUSD kann vieles:
- Es kann Preisstabilität ohne Banken erzeugen,
- Marktdruck absorbieren,
- sich selbst steuern.

Aber es kann keine Wunder vollbringen.
Und gerade diese Ehrlichkeit ist Teil seiner Stärke.

---

## 8.1 Technische Risiken

**Smart-Contract-Fehler:**
Auch formale Audits und Verifikation bieten keine absolute Garantie.
Ein Bug im Core-Smart-Contract könnte trotz aller Tests existieren.
Da der Kern nach dem Freeze unveränderlich ist,
müssen Qualität und Prüfung vor dem Deployment kompromisslos sein.

**MEV-Manipulation und Netzwerk-Stress:**
PulseChain bietet hohe Geschwindigkeit und niedrige Gebühren,
doch auch hier sind Miner-Extractable-Value-Strategien möglich.
ProjectUSD reduziert diese Risiken mit Median-Orakeln, TWAPs und Rate-Limitern,
aber völlige Immunität gibt es nicht.

**Orakel-Bias:**
On-Chain-Preise spiegeln Liquidität und Marktvolumen wider.
In extrem illiquiden Phasen kann der Median-TWAP träge reagieren,
was temporäre Abweichungen im Gleichgewicht zur Folge hat.

---

## 8.2 Ökonomische Risiken

**Volatilität der Sicherheiten:**
ProjectUSD hängt direkt von der Stabilität der hinterlegten PulseChain-Assets ab.
Ein starker Preissturz bei PLS oder anderen Collaterals
kann zu Liquidationswellen führen,
die kurzfristig Druck auf den Marktpreis ausüben.

**Liquiditätsverlagerungen:**
Wenn DEX-Volumen sinkt,
verlangsamt sich die Arbitrage zwischen ProjectUSD und anderen Assets.
Das System bleibt funktionsfähig,
aber Preisabweichungen können länger bestehen.

**Psychologische Faktoren:**
Märkte sind keine Maschinen.
In Panikphasen handeln Menschen irrational -
verkaufen zu früh, hebeln zu hoch, ziehen Liquidität ab.
Auch ein perfekter Algorithmus kann Emotion nicht ausschalten.

---

## 8.3 Governance- und Umfeldrisiken

**Governance Capture:**
Obwohl der Kern unveränderlich ist,
könnte die Peripherie - etwa AMO- oder PSM-Parameter -
durch Mehrheiten beeinflusst werden.
Timelocks und transparente On-Chain-Abstimmungen minimieren das Risiko,
aber ausschließen lässt es sich nicht.

**Rechtliche Unsicherheiten:**
ProjectUSD ist kein reguliertes Finanzprodukt.
In manchen Jurisdiktionen kann die Nutzung steuerliche oder rechtliche Folgen haben.
Jeder Nutzer trägt die Verantwortung, die Gesetze seines Landes zu beachten.

---

## 8.4 Die Grenzen des Modells

ProjectUSD will nicht den US-Dollar ersetzen.
Es ist keine Fiat-Kopie, sondern eine **eigene, digitale Recheneinheit**.
Seine Stabilität ergibt sich nicht aus Bankreserven oder juristischen Versprechen,
sondern aus dem mathematischen Gleichgewicht seiner Mechanismen.

Das bedeutet:
ProjectUSD ist kein „digitaler Dollar“,
sondern ein *eigenständiges Maß für Wert und Tausch* innerhalb der PulseChain-Ökonomie.
Wer das versteht, erkennt den Unterschied zwischen **Abhängigkeit** und **Eigenständigkeit**.

---

## 8.5 Die philosophische Wahrheit des Risikos

Perfekte Sicherheit gibt es nicht -
aber es gibt **ehrliche Systeme**, die ihre Risiken offenlegen.
ProjectUSD verlagert das Risiko vom Menschen in den Code.
Nicht, um es zu verstecken,
sondern um es sichtbar, messbar und fair zu machen.

Denn am Ende ist Risiko nicht das Gegenteil von Vertrauen,
sondern seine Voraussetzung.
Nur wer versteht, wo Gefahr liegt,
kann ihr auf Dauer standhalten.
