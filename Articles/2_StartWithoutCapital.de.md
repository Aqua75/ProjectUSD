# Einführung in ein natives, algorithmisches Geldsystem auf PulseChain
*Warum es ohne Startkapital, ohne LPs und ohne externe Reserven funktionieren kann*

## 1. Einleitung
Viele Fragen rund um ein internes, algorithmisches Geldsystem entstehen aus der Perspektive heutiger Token- und Stablecoin-Modelle. In diesen Modellen wird Stabilität oft über externe Reserven, Oracle-Feeds, Startliquidität oder komplexe Cross-Chain-Abhängigkeiten erzeugt.

Ein autonomes, rückgekoppeltes System wie ProjectUSD funktioniert grundlegend anders.  
Dieses Dokument erklärt verständlich und ohne Vorwissen, warum:

- kein Startkapital,
- keine Start-Liquidity-Pools (LPs),
- keine initialen Vaults,
- und keine externe Wertkopplung

für den Start eines solchen Systems erforderlich sind.

## 2. Warum ein algorithmisches Wertmaß keinen Kapitalstart benötigt
In klassischen Stablecoins basiert die Stabilität auf Reservewerten (z. B. USDC, USDT) oder externen Sicherheiten.  
In einem autonomen System dagegen ist der Startwert ein **Parameter**, kein Geldbetrag.

Der interne Gleichgewichtswert (R) wird beim Deployment definiert, z. B. als `R = 1`.  
Ab diesem Moment stabilisiert der Controller alle Abweichungen durch mathematische Rückkopplung.

Das System benötigt dafür keinerlei Startkapital.  
Es benötigt nur:

- Code  
- Parameter  
- Smart Contracts  
- einen funktionierenden Controller

## 3. Warum keine Vaults beim Start existieren müssen
Der Stablecoin entsteht durch **Nutzer**, nicht durch das System selbst.

- Ein Nutzer öffnet freiwillig den ersten Vault.
- Er hinterlegt Collateral (z. B. PLS).
- Er mintet die ersten Einheiten ProjectUSD.

Erst ab diesem Moment existiert Umlaufmenge.

Das System selbst öffnet **keine** Vaults und hält **keine** Collateralwerte.  
Es startet leer – und das ist beabsichtigt.

## 4. Warum Nutzer Vaults öffnen – und es nicht primär um Zinsen geht
Ein häufiger Irrtum ist, dass Nutzer Vaults öffnen, „um Zinsen zu verdienen“.  
Das ist falsch – zumindest als Hauptmotiv.

Vaults werden vor allem eröffnet, um:

- Liquidität zu erhalten, ohne PLS verkaufen zu müssen  
- ProjectUSD als stabile Recheneinheit zu nutzen  
- Arbitrage-Chancen zu nutzen  
- Hebelstrategien umzusetzen  
- Kaufkraft zu erhöhen  

Die **Systemrate (r)** ist ein geldpolitisches Regelinstrument:

- sie kann positiv sein (Zinskosten für Schuldner, Erträge für Sparer)  
- sie kann negativ sein (Anreiz ProjectUSD zu halten oder zu prägen)  
- sie kann neutral sein  

### Ergänzung:  
**Ja, einige Nutzer werden Vaults auch aufgrund möglicher Zinsgewinne eröffnen.**  
Positive r-Phasen können dazu führen, dass das Halten von ProjectUSD oder die Teilnahme am Stability Pool Rendite abwirft. Diese Zinsen sind jedoch:

- dynamisch,  
- nicht garantiert,  
- systemabhängig,  
- und dienen primär der **Preis-Stabilisierung**, nicht der Nutzerbelohnung.

Zinsgewinne sind ein **Nebenprodukt** der Rückkopplungsmechanik –  
nicht der Kernanreiz für das Öffnen eines Vaults.

## 5. Warum das System ohne LPs starten kann
Stablecoins brauchen erst dann LPs, wenn Nutzer aktiv handeln wollen.

Beim Start jedoch gibt es:

- keine Umlaufmenge  
- keine Trader  
- keine Nachfrage nach Pools  

Erst wenn ProjectUSD zirkuliert, entstehen LPs automatisch durch:

- Arbitrageure  
- Liquidity Provider  
- DEX-Nutzer

LPs sind eine **Anwendung**, nicht Teil der Stabilitätslogik.

## 6. Warum externe Liquidität und Token-Dynamiken irrelevant sind
Ein autonomes Wertmaß bewertet keine externen Assets und hängt nicht von komplexen Tokenmechaniken ab.

Stabilität entsteht intern durch:

- Overcollateralization  
- Redemption  
- Controller  
- Systemrate r  
- algorithmische Rückkopplung

HEX-Rückläufer, externe Chain-Liquidität oder verschachtelte Ökosysteme haben darauf keinen Einfluss.

## 7. Warum interne Stabilität nichts mit Fiat-Stabilität zu tun hat
Viele verwechseln „stabil gegenüber Dollar“ mit „stabil im System“.

Ein internes Wertmaß soll:

- innerhalb der Chain stabil sein  
- gegen volatile Assets als Messinstrument funktionieren  
- durch Rückkopplung konstant gehalten werden

Der Dollarpreis kann schwanken – das ist irrelevant.

Ein Meter bleibt ein Meter, auch wenn sein Dollarpreis schwankt.

## 8. Warum ein solches System nicht utopisch ist
DAI hat jahrelang gezeigt, dass ein dezentrales Wertmaß ohne zentrale Reserven funktionieren kann.  
Dass MakerDAO später zentralisierte Assets zuließ, war eine politische Entscheidung – kein technisches Problem.

ProjectUSD führt diese Logik weiter, jedoch ohne externe Abhängigkeiten.

## 9. Warum das System automatisch Adoption erzeugt
Adoption entsteht durch Nutzen, nicht durch Marketing.

Wenn ein internes Wertmaß:

- stabiler,  
- günstiger,  
- transparenter,  
- sicherer  
- und ökonomisch attraktiver ist  

dann wird es sich von selbst durchsetzen.

## 10. Zusammenfassung
Ein internes, algorithmisches Geldsystem:

- braucht kein Startkapital  
- braucht keine initialen Vaults  
- braucht keine Start-LPs  
- braucht keine externe Liquidität  
- muss keine bestehenden Projekte integrieren  
- stabilisiert sich rein mathematisch  
- funktioniert auch in chaotischen Ökosystemen  
- ist technisch bewährt und nicht utopisch  

Die Stabilität entsteht aus Logik – nicht aus Kapital.
