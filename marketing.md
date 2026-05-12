# Vermarktung

Eine Publikation unterstützt insgesamt **5 Werbeslots**, die mit Ihren **eigenen Werbekampagnen** bestückt werden können.

> [!INFO]
> Der Ad-Manager ist ab dem Paket **Publisher** verfügbar.

![Positionen der Werbeslots im oberen Bereich: Header, linke und rechte Sidebar](/images/ads-top-light.png "dark:/images/ads-top-dark.png")

Zusätzlich zum *Header*, der *Left Sidebar*, der *Right Sidebar* und dem *Footer* gibt es noch einen Container für das *Interstitial*.

![Positionen der Werbeslots im unteren Bereich: Footer und Interstitial](/images/ads-bottom-light.png "dark:/images/ads-bottom-dark.png")

Jeder Werbe-Container kann **individuell konfiguriert** werden in Bezug auf HTML, CSS, Custom-Javascript, Breakpoints und Nutzer:innen-Gruppen.

---

## Bibliothek

Bevor die Werbe-Container erstellt werden können, wird eine **initiale Bibliothek** zu Ihrem Werbe-Netzwerk bzw. Ad-Server benötigt.
Die Einbindung der Bibliothek erfolgt über den Tab [Scripts](./tracking#integration-von-analyse-systemen) als **externes Script**.

---

## HTML

Um einen Werbeslot anzulegen, beginnen Sie mit der **Auswahl aus einer der 5 Positionen**.
Nachdem Sie die Position bestimmt haben, fügen Sie den Container im Feld „HTML" ein.
Sie können hierbei auf Script-Tags oder andere HTML-Elemente zurückgreifen.

Handelt es sich bei dem Container um **reines Javascript**, müssen Sie dieses in einen **Script-Tag einbetten**.

![Eingabefeld für den HTML-Code eines Werbeslots](/images/ads-html-light.png "dark:/images/ads-html-dark.png")

### Styles

Um Ihren **Container anzupassen**, haben Sie die Möglichkeit, **Custom CSS** zu hinterlegen.
Hierfür vergeben Sie Ihrem **HTML-Element eine Klasse**, die Sie im Feld CSS stylen können.

![Eingabefeld für Custom CSS zur individuellen Gestaltung des Werbe-Containers](/images/ads-css-light.png "dark:/images/ads-css-dark.png")

### Custom Javascript

Für **Custom Javascript** steht Ihnen ein weiteres Feld zur Verfügung.
Sie können Ihr Javascript direkt einfügen **ohne** die Verwendung eines **Script-Tags**.

![Eingabefeld für Custom JavaScript](/images/ads-js-light.png "dark:/images/ads-js-dark.png")

---

## Größe

Ein Ad-Slot hat **initial keine Ausdehnung** (0 × 0 Pixel).
Erst durch das **Laden und Rendern** von Inhalten über eine externe Quelle **dehnt sich ein Container aus**.
Um den Spielbereich zu schützen, können Sie bei den Positionen *Linke Seite* und *Rechte Seite* eine **maximale Breite** setzen.
Inhalte, die breiter als der gesetzte Wert sind, dehnen den Container nicht aus.

![Einstellung der maximalen Breite für Sidebar-Werbeslots zum Schutz des Spielbereichs](/images/ads-width-light.png "dark:/images/ads-width-dark.png")

Um **Layout-Shifts** für Nutzer:innen zu **verhindern** bzw. gering zu halten, können Sie bei den Positionen *Header* und *Footer* jeweils eine **Mindesthöhe** bestimmen.
Die Container werden dadurch bereits **vor dem Laden** der Werbemittel **ausgedehnt**.
Idealerweise kommt es dadurch zu keinem Layout-Shift, was sich positiv auf den [CLS-Wert](https://web.dev/articles/cls) auswirkt.
Sollte Ihr Werbemittel höher als der definierte Wert sein, dehnt sich der Container dennoch aus, um das **Werbemittel vollständig darzustellen**.

![Einstellung der Mindesthöhe für Header- und Footer-Slots zur Vermeidung von Layout-Shifts](/images/ads-min-height-light.png "dark:/images/ads-min-height-dark.png")

---

## Breakpoints

Wenn Sie alle Werbeplätze nutzen, kann dies vor allem auf mobilen Endgeräten zu Problemen führen, da der Spielbereich so weit eingeschränkt werden könnte, dass dieser unbenutzbar wird.
Insbesondere für die Positionen *Left Sidebar* und *Right Sidebar* sollten Sie Regeln definieren, wann diese dargestellt werden.

Für jeden Ad-Slot kann die Sichtbarkeit über Breakpoints konfiguriert werden. Hierbei sind zwei Einstellungen möglich:

- **Sichtbar ab Mindestbreite** — der Ad-Slot wird erst ab der gewählten Displaybreite angezeigt
- **Sichtbar bis zur maximalen Breite** — der Ad-Slot wird nur bis zur gewählten Displaybreite angezeigt

![Breakpoint-Konfiguration zur Steuerung der Sichtbarkeit eines Werbeslots nach Bildschirmbreite](/images/ads-viewability-light.png "dark:/images/ads-viewability-dark.png")

Die Breakpoints orientieren sich an gängigen Bildschirmgrößen: **640px**, **768px**, **1024px**, **1280px** und **1536px**.

---

## Zielgruppe

Bei Anbindung einer [SSO](./sso) können Sie pro Ad-Slot festlegen, **welcher Personengruppe** er angezeigt wird.
Die Steuerung erfolgt über zwei Felder:

- **Modus** — bestimmt, ob die gewählte Gruppe die Anzeige sehen soll (`Sichtbar für`) oder nicht (`Nicht sichtbar für`).
- **Zielgruppe** — die Personengruppe, auf die der Modus angewendet wird.

Folgende Standard-Gruppen stehen immer zur Verfügung:

- **Alle** — alle Besucher:innen Ihrer Publikation
- **Angemeldet** — alle eingeloggten Nutzer:innen

Zusätzlich können Sie **eigene Zustände** verwenden, die Sie unter [Authentifizierung → Zustände](./sso#zustand) angelegt haben — z. B. `Abonnent:in`, `Trial` oder `Spiele-Abo`. Über diese Zustände lassen sich Anzeigen feingranular auf bestimmte Nutzer:innen-Segmente ausspielen.

### Beispiele

| Modus | Zielgruppe | Effekt |
|---|---|---|
| Sichtbar für | Alle | Anzeige wird allen Besucher:innen angezeigt |
| Sichtbar für | Angemeldet | Anzeige wird nur eingeloggten Nutzer:innen angezeigt |
| Nicht sichtbar für | Angemeldet | Anzeige wird ausschließlich nicht eingeloggten Besucher:innen angezeigt |
| Sichtbar für | Abonnent:in | Anzeige wird nur Personen mit dem Zustand `Abonnent:in` angezeigt |
| Nicht sichtbar für | Abonnent:in | Anzeige wird allen außer Abonnent:innen angezeigt — z. B. um Abos zu bewerben |

Dadurch können Sie beispielsweise **Abonnent:innen** eine **werbefreie Plattform** anbieten, oder gezielt **Trial-Nutzer:innen** mit Aufruf-zum-Upgrade-Anzeigen ansprechen.

> [!INFO]
> Die Sichtbarkeits-Konfiguration ist nur verfügbar, wenn eine [SSO](./sso) angebunden ist. Eigene Zustände müssen vorher unter [Authentifizierung → Zustände](./sso#zustand) angelegt sein, bevor sie hier auswählbar werden.
