# Konfiguration

Je nach Rätsel gibt es **zusätzliche Konfigurationsmöglichkeiten**, um Ihre Publikation an Ihre Bedürfnisse anzupassen.
Die Konfiguration ist in die Bereiche **Funktionen**, **Spieleinstellungen** und ggf. **Farben** unterteilt.

---

## Funktionen

In der **Standardkonfiguration** sind alle Funktionen für **alle Nutzer:innen** freigegeben.
Bei Anbindung an eine [SSO](./sso) kann der [Zugriff eingeschränkt](#zugangsbeschränkung) werden — beispielsweise nur für **angemeldete Nutzer:innen** oder für Nutzer:innen mit einem **bestimmten Status**. So lassen sich Funktionen auch hinter eine [Paywall](./paywall) setzen.

> [!INFO]
> Einige Funktionen sind nur in **höheren Paketen** verfügbar. Ist eine Funktion für Ihr Paket nicht freigeschaltet, wird sie in der Konfiguration nicht angezeigt.

### Community Stats

Für *Worteck* können **Community Stats** aktiviert werden. Diese zeigen Nutzer:innen aggregierte Statistiken der Spielergemeinschaft an. Community Stats sind ab dem Paket **Publisher** verfügbar.

### Dark Mode

Der **Dark Mode** ist in der Standardkonfiguration aktiviert und für alle Nutzer:innen frei zugänglich.

---

## Spieleinstellungen

Jedes Spiel bringt **eigene Einstellungen** mit sich. In der Regel sind diese mit **Standardwerten befüllt**.
Sie können diese **Werte überschreiben** und die Regeln, Punkte und andere Einstellungen an Ihre Wünsche anpassen.

### Anzahl Tage im Archiv

Wenn Sie das **Archiv in den [Seiten](./content#seiten) aktivieren**, können Ihre Nutzer:innen **vergangene Rätsel** lösen.

Zunächst erhalten die Nutzer:innen bei Aktivierung Zugriff auf die vergangenen **7 Tage**.
Sie können diesen Wert über das Feld *Anzahl Tage im Archiv* auf bis zu **14 Tage** erhöhen.

### Errungenschaften

#### Worteck

Bei *Worteck* definiert das Feld *Errungenschaften* die **Ränge**, die Nutzer:innen erreichen können.
Der **Key** definiert den **Streak** — die Anzahl der hintereinander erratenen Wörter.
Der **Wert** stellt den **Rang** dar, den ein(e) Nutzer:in damit erreicht hat.

![Konfiguration der Worteck-Errungenschaften: Streak-Werte und zugehörige Ränge als Key-Value-Paare](/images/achievements-light.png "dark:/images/achievements-dark.png")

### Meilensteine

#### Wortwabe

Bei *Wortwabe* definieren die *Meilensteine* die **Schritte** auf dem Weg zur maximalen Punkteanzahl.
Mit jedem Schritt wird eine **Punkteanzahl** zugewiesen, wobei der **letzte Schritt** gleichzeitig die **maximal erreichbare Punkteanzahl** definiert.
Starten Sie immer mit Schritt 1 und 0 Punkten.

![Konfiguration der Wortwabe-Meilensteine: Schritte mit zugehörigen Punktewerten](/images/milestones-light.png "dark:/images/milestones-dark.png")

### Punktesystem

Einige Spiele enthalten ein **Punktesystem**.
Dieses ist in der Regel **ausbalanciert** und wurde bereits im Vorfeld mit einer **Community getestet**.
Sie können das System jedoch an Ihre Wünsche und Bedürfnisse **anpassen**.

Einige Werte des Punktesystems sind **nur solange editierbar**, bis die Rätsel **installiert** sind.
Änderungen sind dann nicht mehr möglich, es sei denn, Sie [deinstallieren](#deinstallation) die Rätsel und führen eine **erneute Installation** aus.
Felder, die nach einer Installation nicht mehr editierbar sind, **erkennen Sie am Schloss-Symbol**.

#### Wortwabe

Für *Wortwabe* können insgesamt **fünf Werte** angepasst werden, die das **Punktesystem** bilden.

##### Mindestanzahl an Buchstaben

Über die **Mindestanzahl an Buchstaben** legen Sie fest, über welche Länge ein Wort mindestens verfügen muss,
um als valide zu gelten und Punkte zu erhalten.
Gibt ein(e) Nutzer:in ein Wort ein, dessen Länge unter diesem Wert liegt, wird eine Fehlermeldung ausgegeben.

##### Maximale Anzahl an Buchstaben

Über *Maximale Anzahl an Buchstaben* begrenzen Sie die Wortlänge, die eingegeben werden kann.
Ein(e) Nutzer:in kann über die maximale Wortlänge hinaus keine Buchstaben mehr eingeben.
Wenn Sie das Feld leer lassen, gibt es keine Begrenzung bei der Wortlänge. Systemseitig sind maximal **20 Buchstaben** erlaubt.

##### Ein Punkt pro Buchstabe ab einer Wortlänge von...

Über dieses Feld bestimmen Sie, ab welcher **Wortlänge ein Punkt pro Buchstabe** vergeben wird.
Diese Einstellung steht mit dem Feld *Punkte für kurze Wörter* in Verbindung.
„Kurze Wörter" sind alle Wörter, für die **keine Punkte pro Buchstabe** vergeben werden.

**Beispiel:** Das Wort „Maus" hat 4 Buchstaben. Wenn im Feld *Ein Punkt pro Buchstabe ab einer Wortlänge von...* der Wert `5` eingetragen ist, erhält man für „Maus" die Anzahl Punkte, die im Feld *Punkte für kurze Wörter* festgesetzt wurden (Standard: 1 Punkt).
Für das Wort „Hallo" erhält man hingegen 5 Punkte – also einen Punkt pro Buchstaben, da die Wortlänge (5) dem Schwellenwert entspricht.

##### Punkte Isogramm

Für das **Isogramm** legen Sie eine **Punktezahl** fest, die Nutzer:innen erhalten, wenn sie das Wort des Tages finden.
Aus einem Isogramm können ggf. weitere Isogramme gebildet werden – hierfür erhalten Nutzer:innen ebenfalls die in diesem Feld festgelegte Punktzahl.

### Drucken

#### Sudoku

Wenn Sie das **Drucken aktivieren**, können Ihre Nutzer:innen **Rätsel ausdrucken**.

---

## Farben

### Worteck

Für *Worteck* können die **Farben** der Buchstaben-Zustände angepasst werden:

- **Korrekte Buchstaben** — Farbe für Buchstaben an der richtigen Position
- **Vorhandene Buchstaben** — Farbe für Buchstaben, die im Wort enthalten, aber an der falschen Position sind
- **Nicht vorhandene Buchstaben** — Farbe für Buchstaben, die nicht im Wort enthalten sind

---

## Zugangsbeschränkung

Funktionen können mit **individuellen Zugangsregeln** versehen werden.
So lässt sich pro Funktion steuern, ob sie **allen Nutzer:innen**, nur **authentifizierten Nutzer:innen** oder nur Nutzer:innen mit einem **bestimmten Status** zur Verfügung steht.

![Zugangsstufen pro Funktion: Alle, Angemeldet oder nach Zustand einschränkbar](/images/feature-access-light.png "dark:/images/feature-access-dark.png")

Eine ausführliche Beschreibung des Paywall-Systems finden Sie unter [Paywall](./paywall).

---

## Deinstallation

Eine **Deinstallation** ist in der Regel **nicht notwendig**.
Sobald Sie die Rätsel zu einer Publikation installiert haben, werden **zukünftige Rätsel automatisch** bei Verlängerung der Vertragslaufzeit **installiert**.
Eine Deinstallation ist dann **sinnvoll**, wenn Sie das [Punktesystem](#punktesystem) einer Publikation anpassen möchten.

Eine Deinstallation nimmt einige Sekunden in Anspruch. Sie werden informiert, wenn der Prozess abgeschlossen ist.
Im Nachgang können Sie die **Rätsel erneut installieren**. Im Anschluss wird eine neue Version Ihrer Publikation **mit der neuen Konfiguration** erstellt.

> [!DANGER]
> Durch eine erneute Installation wird die **Reihenfolge der Rätsel verändert**.
> Bitte beachten Sie, dass ggf. **Exporte für Ihre Offline-Produkte** neu erstellt werden müssen.
> Bei Wort-Rätseln könnte es vorkommen, dass erst vor kurzem **erratene Wörter** in naher Zukunft **erneut vorkommen**.