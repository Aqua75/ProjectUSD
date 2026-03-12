# Studie 19 - Analyse der optimalen Grenzen der Systemrate r im ProjectUSD-Protokoll
*Wissenschaftliche Untersuchung der zulässigen Unter- und Obergrenzen von `r` im Core-Design von ProjectUSD*  
*(Level-3 Research Format)*

---

## Abstract

Diese Studie untersucht, welche Unter- und Obergrenzen für die Systemrate `r` im ProjectUSD-Protokoll technisch, ökonomisch und systemisch sinnvoll sind. Im Zentrum steht die Frage, ob der Core von ProjectUSD negative Werte für `r` zulassen sollte oder ob ein strikt nichtnegativer Bereich die robustere Architektur darstellt.

Die Analyse basiert primär auf den normativen Core-Spezifikationen, da diese nach dem Freeze-Ereignis bindend wären. Dabei zeigt sich zunächst eine Dokumentationsspannung: Einerseits definieren die Spezifikationen `r` als nichtnegative System- beziehungsweise Schuldrate, andererseits diskutieren einzelne Studien konzeptionell auch negative `r`-Phasen. Gerade deshalb ist die Frage nach dem unteren Grenzwert nicht bloß eine Parametrierungsfrage, sondern eine Frage der Core-Semantik.

Im weiteren Verlauf wird gezeigt, dass ein negatives `r` im aktuellen Design nicht einfach eine lockerere geldpolitische Stellung bedeutet, sondern mechanisch eine Reduktion von Vault-Schulden. Dadurch entsteht kein neutraler Stabilisierungsimpuls, sondern potenziell ein regelbasierter Transfer zugunsten von Schuldnern. Zwar erweitert ein negativer Untergrenzwert die Eingriffsreichweite des Controllers in Unterpeg-Phasen, doch erzeugt er keinen garantierten Erholungsmechanismus. Für ein unveränderliches Protokoll überwiegen deshalb die Risiken.

Die Studie kommt zu dem Ergebnis, dass unter der derzeit dokumentierten Core-Architektur die Option `0 ≤ r ≤ +20 %` klar vorzuziehen ist. Negative `r`-Werte sind in autonomen Geldsystemen prinzipiell nicht illegitim, wirken im vorliegenden Design jedoch auf dem falschen Kanal und sollten daher nicht Teil eines eingefrorenen Core-Systems sein.

---

# 1. Einleitung

## 1.1 Problemstellung - Die Frage nach der unteren Grenze von r

ProjectUSD verwendet `r` als zentrale Regelgröße seines internen Stabilisierungsmechanismus. Der Controller misst Abweichungen zwischen Marktpreis `P` und Gleichgewichtspreis `R` und passt daraufhin die Systemrate `r` an. Diese beeinflusst Vault-Anreize, Schuldendynamik, Arbitrageverhalten und damit mittelbar die monetäre Stabilisierung.

Die entscheidende offene Frage lautet jedoch: Wie weit darf `r` nach unten reichen.

Drei Grundoptionen stehen zur Debatte:

1. **Option A:** negativer Floor bei `-5 %`  
2. **Option B:** negativer Floor bei `-2 %`  
3. **Option C:** Floor bei `0 %`

Auf den ersten Blick könnte ein negativer Bereich attraktiv wirken, weil er dem Controller in längeren Unterpeg-Phasen zusätzlichen Handlungsspielraum verschafft. Doch gerade im aktuellen Core-Design wirkt `r` direkt auf Vault-Schulden. Deshalb ist die technische und ökonomische Bedeutung eines negativen Bereichs wesentlich tiefgreifender, als es eine reine Parameterdebatte vermuten lässt. :contentReference[oaicite:1]{index=1}

## 1.2 Methodische Grundlage

Diese Untersuchung basiert primär auf den normativen Core-Spezifikationen, insbesondere auf:

- `controller-spec`
- `vaultengine-spec`
- `liquidation-redemption-spec`
- `Glossary`

Diese Quellen sind maßgeblich, weil sie nach dem Protokoll-Freeze bindend wären. Studien und konzeptionelle Texte werden ergänzend berücksichtigt, haben jedoch nicht denselben normativen Rang. Bereits daraus ergibt sich, dass jede Einführung negativer `r`-Werte nicht bloß als Parameterverschiebung, sondern als Eingriff in Typen, Semantik und Abrechnungssystem verstanden werden muss. :contentReference[oaicite:2]{index=2}

## 1.3 Zwei Vorbemerkungen

Zwei Vorbemerkungen sind für die gesamte Analyse entscheidend.

Erstens ist die Dokumentation derzeit nicht vollständig konsistent. Die normativen Spezifikationen definieren `r` als nichtnegative System- oder Schuldrate, während einzelne Studien negative `r`-Phasen konzeptionell mitdenken. Daraus folgt unmittelbar, dass ein negativer Floor nicht nur eine andere Einstellung derselben Logik wäre, sondern eine Änderung der Core-Bedeutung von `r`. :contentReference[oaicite:3]{index=3}

Zweitens ist der Wirkkanal von `r` auf den Marktpreis `P` noch nicht vollständig mechanisch spezifiziert. Manche Formulierungen legen nahe: `P < R -> r sinkt -> P steigt`. Der eindeutig definierte On-Chain-Effekt einer Senkung von `r` ist jedoch im aktuellen Core nur, dass Vault-Schulden langsamer wachsen oder schrumpfen. Ob daraus zuverlässig eine Preisstabilisierung entsteht, hängt zusätzlich von Verhalten, Liquidität und Marktbedingungen ab. Gerade deshalb ist die Wahl eines negativen Floors besonders sensibel. :contentReference[oaicite:4]{index=4}

---

# 2. Systemtheoretische Analyse

## 2.1 Sind negative Raten grundsätzlich legitim

Negative Zinsen oder negative Regelraten sind als regulatorisches Instrument nicht grundsätzlich illegitim. In der Makroökonomie wurden negative Zinsen eingesetzt, um Kreditaufnahme, Ausgaben und Investitionen anzuregen. Auch im Kryptobereich existieren Systeme wie RAI, in denen positive und negative Signale verwendet wurden. Daraus folgt: Ein autonomes Geldsystem kann prinzipiell mit einem bidirektionalen Signal arbeiten. :contentReference[oaicite:5]{index=5}

## 2.2 Entscheidend ist nicht das Vorzeichen, sondern der Wirkkanal

Die bloße Existenz negativer Werte sagt jedoch noch nichts über ihre Legitimität im konkreten Design aus. Entscheidend ist die Stelle, an der das Signal angreift.

Im Fall von RAI wirkt das Vorzeichen auf die Redemption- oder Zielpreisdynamik, also auf die interne Preisverankerung. Im Fall von ProjectUSD wirkt `r` gemäß Core-Spezifikation direkt auf die Vault-Schuld:

`debt_next = debt_prev * (1 + r_epoch)`

Damit ist ein negatives `r` hier nicht bloß eine lockerere geldpolitische Stellung, sondern ökonomisch eine regelbasierte Schuldreduktion. Das ist ein qualitativ anderer Aktor. :contentReference[oaicite:6]{index=6}

## 2.3 Strukturelle Asymmetrie des Controllers

Ein Controller mit `r ∈ [0, r_max]` ist strukturell asymmetrisch. Nach unten ist sein Eingriffsraum abgeschnitten. Formal ergibt sich ein gesättigter Regler:

`r_(t+1) = sat(r_t + K * ε_t, r_min, r_max)`

Mit `r_min = 0` kann ein anhaltend negativer Fehler `ε < 0` in einen Bereich führen, in dem die gewünschte Reglerreaktion unterhalb des Floors läge. Dann tritt Residualfehler auf. Der Controller würde weiter lockern wollen, kann es aber nicht. :contentReference[oaicite:7]{index=7}

## 2.4 Interimsschluss

Aus systemtheoretischer Sicht kann negatives `r` also durchaus legitim sein, aber nur dann, wenn der negative Ast über einen klar definierten Kanal mit begrenztem Budget und eindeutigem Zieleffekt arbeitet. Im gegenwärtig dokumentierten ProjectUSD-Core ist genau das nicht erfüllt. Daher folgt aus der Asymmetrie des Controllers noch nicht, dass negative Werte notwendig oder ratsam wären. :contentReference[oaicite:8]{index=8}

---

# 3. Ökonomische Analyse

## 3.1 Mechanische Wirkung auf Schulden

Im aktuellen Design ist `r` eine Schuldrate. Daraus folgt unmittelbar:

`D_(t+1) = D_t (1 + r_t)`

Für `r_t < 0` gilt daher:

`D_(t+1) < D_t`

Dies ist keine Interpretation, sondern Mechanik. Der Schuldner schuldet in der nächsten Epoche weniger als zuvor. Ein negativer Wert bedeutet also unmittelbare Entlastung bestehender Vault-Schulden. :contentReference[oaicite:9]{index=9}

## 3.2 Rational entstehende Arbitragestrategien

Sobald `r < 0` zulässig ist, entstehen mehrere rationale Strategien:

- **Passive Carry-Subvention:** Vault öffnen, ProjectUSD minten und einfach halten, während die Schuld automatisch sinkt  
- **Hebelung externer Nutzung:** ProjectUSD minten, anderweitig einsetzen oder in andere Assets verschieben, während die Verbindlichkeit sinkt  
- **Zeit-Arbitrage:** heute minten und später mit geringerer Restschuld zurückzahlen

Alle drei Strategien werden umso attraktiver, je länger eine negative Phase andauert. Damit wirkt negatives `r` nicht neutral, sondern als systematischer Anreiz zugunsten von Schuldnern. :contentReference[oaicite:10]{index=10}

## 3.3 Subventionscharakter und Überschusspuffer

Im VaultEngine-Design fließt die Differenz `debt_next - debt_prev` systemweit in den `surplusBuffer`. Bei positivem `r` wächst dieser Puffer. Bei negativem `r` müsste dieselbe Logik den Puffer reduzieren. Gleichzeitig ist `surplusBuffer ≥ 0` als Invariante definiert.

Daraus entsteht eine ernste semantische Spannung. Entweder:

1. der `surplusBuffer` finanziert die Schuldenreduktion  
2. die Implementierung kappt negative Raten implizit  
3. die Invariante wird verletzt

Genau diese Frage ist derzeit nicht sauber spezifiziert. Für ein unveränderliches System ist das ein zentrales Problem. :contentReference[oaicite:11]{index=11}

## 3.4 Langfristige Wirkung auf Angebotsdynamik

Ein oft unterschätzter Punkt ist, dass negatives `r` das zirkulierende Tokenangebot nicht direkt reduziert. Es reduziert lediglich die Verbindlichkeiten der Schuldner.

Daraus können gleichzeitig zwei Effekte entstehen:

- bestehende Schulden werden subventioniert  
- neue Verschuldung wird attraktiver

Gerade dadurch steigt die Wahrscheinlichkeit, dass Marktteilnehmer größere oder länger laufende Positionen halten. Das ist besonders relevant, weil Stabilisierung in Unterpeg-Phasen typischerweise eher zusätzliche Rückkäufe und Redemption-Nachfrage benötigt als sinkenden Rückzahlungsdruck. :contentReference[oaicite:12]{index=12}

## 3.5 Größenordnung des Effekts

Die PDF liefert dazu eine illustrative Epochenrechnung:

- `r = -2 %` über 20 Epochen reduziert die Schuld auf etwa `0.98^20 ≈ 0.668`, also rund **33 %** Reduktion  
- `r = -5 %` über 20 Epochen reduziert die Schuld auf etwa `0.95^20 ≈ 0.359`, also rund **64 %** Reduktion

Das zeigt, dass auch scheinbar kleine negative Floors kumulativ keineswegs klein sind. :contentReference[oaicite:13]{index=13}

## 3.6 Folgen für Vault-Anreize und Holder

Wenn `r < 0` ist, werden Vaults nicht nur günstiger, sondern potenziell zu Subventionscontainern. Das verschiebt die Anreize in Richtung:

- höherer gewünschter Hebelung  
- längerer Positionsdauer  
- geringerer Rückzahlungsdringlichkeit  
- geringerer Bereitschaft, ProjectUSD am Markt zurückzukaufen

Für Holder entsteht dabei kein direkter Vorteil. Begünstigt wird primär die Schuldnerseite, während das System gleichzeitig mit geringerem Puffer, kleinerer zukünftiger Gebührenbasis und potenziell größerem ausstehenden Schuldvolumen belastet wird. Ökonomisch ähnelt dies eher einem Transfer von der Sicherheitsmarge des Systems zugunsten der Schuldner. :contentReference[oaicite:14]{index=14}

## 3.7 Begrenzende Mechanismen reichen nicht aus

Andere Mechanismen des Systems begrenzen das Problem nur teilweise:

- `DELTA_R_MAX` begrenzt die Geschwindigkeit, nicht den kumulativen Transfer  
- Mindestbesicherungsquoten begrenzen Teilnahme, nicht das Vorzeichen des Transfers  
- die Stability Pool absorbiert Liquidationen, nicht Schuldnersubventionen  
- Redemption verknappt Angebot nur, wenn tatsächlich aktiv gekauft und eingelöst wird

Deshalb verändern diese Mechanismen negatives `r` nicht von einer Subvention in ein neutrales Signal. :contentReference[oaicite:15]{index=15}

---

# 4. Stressszenarioanalyse

## 4.1 Ausgangsszenario

Die Studie betrachtet ein klares Stressszenario:

- `P` bleibt über Wochen unter `R`  
- Redemption-Ziele sind erschöpft oder praktisch inaktiv  
- Arbitragekapital fehlt  
- das Marktvertrauen ist schwach

Die eigentliche Frage lautet dann nicht, ob negatives `r` theoretisch helfen könnte, sondern ob es unter diesen Bedingungen das System verlässlich zurück ins Gleichgewicht bringt. :contentReference[oaicite:16]{index=16}

## 4.2 Verlauf ohne negatives r

Ohne negative Werte senkt der Controller `r` schrittweise auf null und sättigt dort. Ab diesem Punkt verliert er zusätzliche Lockerungskapazität. Das ist ein realer Nachteil, weil dem System ein Freiheitsgrad verloren geht. :contentReference[oaicite:17]{index=17}

## 4.3 Verlauf mit negativem Floor

Mit einem negativen Floor gewinnt der Controller zusätzlichen Handlungsspielraum. Die Studie beschreibt diesen Zusatzraum näherungsweise durch:

`N_extra ≈ |r_min| / Δr_max`

Mit einem illustrativen `Δr_max = 50` Basispunkten pro Epoche ergäbe das ungefähr:

- bei **Option B** (`-2 %`) etwa vier zusätzliche limitergebundene Epochen  
- bei **Option A** (`-5 %`) etwa zehn zusätzliche limitergebundene Epochen

Das ist das stärkste Argument zugunsten eines negativen Floors: Er erweitert den aktiven Regelbereich des Controllers. :contentReference[oaicite:18]{index=18}

## 4.4 Warum das dennoch kein verlässlicher Erholungsmechanismus ist

Der entscheidende Punkt ist jedoch: Selbst mit `r < 0` kann der Controller keine Erholung erzwingen.

Er:

- kauft keine Tokens automatisch am Markt  
- führt keine automatischen Buybacks aus  
- erzwingt keine Redemption-Nachfrage  
- erzeugt kein externes Arbitragekapital

Er verändert nur Anreize. In moderatem Stress kann das hilfreich sein. In tiefem Stress mit wenig Vertrauen und schwacher Liquidität bleibt dieser Kanal jedoch schwach. Schlimmer noch: Weil der einzig garantierte mechanische Effekt von `r < 0` Schuldnerentlastung ist, kann das Signal gerade in dieser Situation in die falsche Richtung wirken. :contentReference[oaicite:19]{index=19}

## 4.5 Präzisierter Stressschluss

Die starke Behauptung, ohne negatives `r` habe das System keinen internen Erholungsmechanismus, ist daher zu grob. Präziser ist:

- ohne negatives `r` verliert der Controller einen Teil seiner Autorität in längeren Unterpeg-Phasen  
- mit negativem `r` gewinnt er zusätzliche Autorität zurück, aber keinen garantierten Recovery-Mechanismus

Genau darin liegt die eigentliche Abwägung. :contentReference[oaicite:20]{index=20}

---

# 5. Regelungstechnische Perspektive

## 5.1 Der Controller als PI-ähnlicher Regler

Aus regelungstechnischer Sicht ist der Controller kein klassischer PI-Block, aber PI-ähnlich, weil `r` selbst den integrierten Reglerzustand darstellt:

`r_(t+1) = r_t + K_p * ε_t`

ergänzt um Deadband, Limiter und Sättigung. Diese Architektur erklärt sowohl die Attraktivität eines symmetrischeren Aktorraums als auch die Gefahren eines negativen Bereichs. :contentReference[oaicite:21]{index=21}

## 5.2 Sättigung bei r = 0

Ein Floor bei null erzeugt Sättigung. In der Regelungstechnik ist bekannt, dass Sättigung die Leistung verschlechtert und langsamere Erholung aus nichtlinearen Zuständen verursacht. Im vorliegenden System existiert jedoch keine versteckte Integratorstruktur mit klassischem Windup. `r` selbst ist der Zustand und wird direkt geclippt. Daher ist klassisches Windup-Risiko geringer als in einem Standard-PID mit separatem Integrator. :contentReference[oaicite:22]{index=22}

## 5.3 Was tatsächlich bleibt

Auch ohne klassisches Windup bleiben jedoch:

- autoritätsbedingter Verlust durch Sättigung  
- Residualfehler  
- langsamere Erholung aus Unterpeg-Zuständen

Ein negativer Bereich macht den Aktorraum zwar symmetrischer, doch Symmetrie im Regelraum ist nicht identisch mit Symmetrie der ökonomischen Wohlfahrtseffekte. :contentReference[oaicite:23]{index=23}

## 5.4 Oszillationsrisiken

Je breiter der negative Bereich, desto größer wird das Risiko von:

- Überlockerung in illiquiden Phasen  
- verzögerter Gegenreaktion durch TWAP- oder Oracle-Lag  
- Rebound-Oszillation  
- späterem Overshoot, wenn das Vertrauen plötzlich zurückkehrt

Die Studie betont ausdrücklich, dass **Option A** dieses Risiko deutlich stärker erhöht als **Option B**. :contentReference[oaicite:24]{index=24}

---

# 6. Risikoanalyse

## 6.1 Nüchterner Vergleich der Optionen

Die Studie vergleicht die drei Varianten entlang von Kontrollgewinn, Subventionsrisiko und Eignung für ein unveränderliches Design:

| Option | Untergrenze | Kontrollgewinn im Unterpeg | Subventionsrisiko | Eignung für Immutable Design |
|---|---:|---|---|---|
| A | -5 % | hoch | sehr hoch | schwach |
| B | -2 % | niedrig bis moderat | moderat bis hoch | fraglich |
| C | 0 % | kein negativer Ast | kein Schuldensubventionsast | am stärksten |

Dieser Vergleich verdichtet die gesamte Untersuchung sehr klar. :contentReference[oaicite:25]{index=25}

## 6.2 Risiko 1 - Subvention durch negatives r

Die Eintrittswahrscheinlichkeit dieses Risikos ist unter Option A hoch und unter Option B weiterhin substanziell, sobald längere Unterpeg-Phasen auftreten. Das Schadenspotenzial ist ebenfalls hoch, weil:

- Puffer erodieren können  
- Schuldner systematisch begünstigt werden  
- Preiswirkungen unsicher bleiben  
- der Effekt in einem Immutable Core nicht nachträglich korrigiert werden kann

Damit ist dieses Risiko für ein eingefrorenes Protokoll besonders kritisch. :contentReference[oaicite:26]{index=26}

## 6.3 Risiko 2 - Kontrollverlust bei r >= 0

Auch ein nichtnegativer Bereich hat ein Risiko: Der Controller kann im Unterpeg-Fall bei null sättigen und zusätzliche Lockerungskapazität verlieren. Die Eintrittswahrscheinlichkeit dieses Problems ist jedoch stärker szenarioabhängig. Außerdem löst negatives `r` tiefe Krisenlagen eben nicht zuverlässig. :contentReference[oaicite:27]{index=27}

## 6.4 Langfristige Systemstabilität

Für ein unveränderliches System zählt nicht nur, welche Controller-Variante im Normalbetrieb besser performt. Noch wichtiger ist, welcher Fehlermodus klarer, weniger ausnutzbar und strukturell robuster ist.

Option C erzeugt einen klaren Fehlermodus:

- Der Controller sättigt bei null.

Optionen A und B erzeugen dagegen einen zweiten und gefährlicheren Fehlermodus:

- Das Protokoll wird zu einem automatischen und potenziell langanhaltenden Schuldenentlastungsmechanismus.

Für eine eingefrorene monetäre Architektur ist dieser zweite Fehlermodus gefährlicher. :contentReference[oaicite:28]{index=28}

---

# 7. Empfehlung

## 7.1 Klare Empfehlung

Die Studie empfiehlt eindeutig:

`0 ≤ r ≤ +20 %`

Diese Empfehlung ergibt sich nicht daraus, dass negative Raten immer falsch wären, sondern daraus, dass sie in der vorliegenden Architektur auf dem falschen Wirkkanal operieren. :contentReference[oaicite:29]{index=29}

## 7.2 Begründung in einem Satz

ProjectUSD sollte im aktuellen Core keinen negativen Ast in Form negativer Schuldrate implementieren. Wenn ein negativer Stabilisierungsmechanismus jemals gewünscht ist, müsste er als separater, explizit budgetierter Kanal entworfen werden und nicht als automatische Schuldenreduktion. :contentReference[oaicite:30]{index=30}

## 7.3 Warum nicht Option A

`-5 %` ist für ein unveränderliches Schuldratensystem deutlich zu aggressiv. Die zusätzliche Kontrollautorität rechtfertigt weder die Größenordnung kumulierter Schuldnersubventionen noch die Overshoot-Risiken. Diese Option sollte daher verworfen werden. :contentReference[oaicite:31]{index=31}

## 7.4 Warum auch Option B problematisch bleibt

`-2 %` ist weniger extrem als Option A, bleibt aber unter dem aktuellen Core weiterhin problematisch. Sie wäre nicht bloß Parametrierung, sondern reale Schuldenvergebung, ohne verlässlich Gleichgewicht im Krisenfall herzustellen. Zudem ist die Dokumentation für diesen Ast noch nicht vollständig spezifiziert. Zulässig würde Option B allenfalls nach grundlegender Neugestaltung mit expliziter Finanzierungslogik, strikten Grenzen und präzisen Rechnungsregeln. :contentReference[oaicite:32]{index=32}

## 7.5 Warum Option C trotz Asymmetrie vorzuziehen ist

Ja, bei einem Floor von null kann der Controller sättigen. Ja, tiefe Unterpeg-Phasen können dadurch länger andauern. Trotzdem ist diese Asymmetrie das kleinere Risiko, weil sie verhindert, dass das Protokoll in Stressphasen automatisch Schuldner bezahlt, ohne einen garantierten stabilisierenden Preiseffekt zu liefern. :contentReference[oaicite:33]{index=33}

---

# 8. Schlussurteil

Negative Werte für `r` sind in autonomen Geldsystemen nicht grundsätzlich illegitim. Als allgemeines Prinzip können bidirektionale Signalsysteme sinnvoll sein. Unter der derzeit dokumentierten Core-Architektur von ProjectUSD ist negatives `r` jedoch kein notwendiger Stabilitätsbaustein, sondern ein vermeidbares systemisches Risiko.

Daraus ergibt sich folgende Rangfolge:

1. **Option C (`0 %`)** - klar bevorzugt  
2. **Option B (`-2 %`)** - nur nach grundlegender Neugestaltung des negativen Astes  
3. **Option A (`-5 %`)** - verwerfen

Die technisch wichtigste Schlussfolgerung vor dem Freeze geht sogar noch tiefer als die reine Floor-Frage: Die Vorzeichenlogik des Übertragungskanals `r -> P` muss vollständig spezifiziert und intern konsistent sein. Solange der einzig garantierte On-Chain-Effekt von negativem `r` die Reduktion von Schulden ist, sollte ein unveränderlicher Core diesen Ast nicht enthalten. :contentReference[oaicite:34]{index=34}

---

# 9. Verifikation

> ## 📘 Reviewer-Checkliste

- Ist sauber zwischen Controller-Asymmetrie und ökonomischer Symmetrie unterschieden  
- Ist die mechanische Bedeutung von `r < 0` als Schuldreduktion korrekt dargestellt  
- Ist die Spannung zwischen Spezifikation und konzeptionellen Studien klar benannt  
- Ist die Rolle des `surplusBuffer` als zentraler semantischer Konflikt korrekt beschrieben  
- Ist der Unterschied zwischen zusätzlicher Controller-Autorität und einem echten Recovery-Mechanismus sauber herausgearbeitet  
- Sind die Optionen A, B und C konsistent nach Kontrollgewinn, Subventionsrisiko und Immutable-Eignung bewertet  
- Ist die Empfehlung `0 ≤ r ≤ +20 %` logisch aus der Gesamtanalyse abgeleitet  
- Ist das Schlussurteil konsistent mit der dokumentierten Core-Architektur von ProjectUSD

Diese Studie dient als Grundlage für die Entscheidung über die zulässigen Grenzen von `r` vor dem Protokoll-Freeze und für die Einordnung, ob ein negativer Ast als legitimer Stabilisierungsmechanismus oder als systemischer Designfehler zu bewerten ist.
