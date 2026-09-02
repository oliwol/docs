# Layout

Sie haben mit dem *oliwol Publisher Tool* die Möglichkeit, die Rätsel an Ihr **Layout anzupassen**.
Hierbei stehen das **Logo**, die **Markenfarbe**, das **Icon** und eine optionale **Custom Font** zur Verfügung.

---

## Logo

Das Logo wird innerhalb der Bearbeitungsmaske Ihrer Publikation im Bereich _Layout_ verwaltet.
Ihr Logo kann ausschließlich im **SVG-Format** hochgeladen werden.

![Upload-Bereich für das Logo im SVG-Format innerhalb der Publikationseinstellungen](/images/upload-logo-light.png "dark:/images/upload-logo-dark.png")

> [!INFO]
> Ihr Logo wird nur bei der [Integration](./setup#integration) vom Typ „DNS" dargestellt – also wenn es sich um eine eigenständige Seite handelt. Binden Sie Ihr Rätsel über Iframe bzw. Script ein, wird das Logo nicht angezeigt.

### Position und Größe

Die **Größe** Ihres Logos sowie die **Position** können **innerhalb der SVG-Datei** angepasst werden.

```html
<svg width="220" height="40" viewBox="0 0 110 20">...</svg>
```

In diesem Beispiel wird durch die Attribute `width` und `height` die Größe der Leinwand bestimmt.
Mit dem `viewBox`-Attribut wird Ihr Logo responsiv. Die vier Zahlen enthalten die Koordinaten *x*, *y*, *width* und *height*:

- Mit *x=0* und *y=0* nimmt das Logo die **ursprüngliche Position** ein.
- Die Koordinaten *x* und *y* verwenden Sie, um das Logo zu **positionieren** – hierbei sind auch **negative Werte** möglich.
- Die beiden darauf folgenden Zahlen geben Höhe und Breite ab x=0 und y=0 an, wodurch das Logo innerhalb des sichtbaren Bereichs herangezoomt oder verkleinert werden kann.
- Je größer der Viewport innerhalb Ihres SVGs, desto **kleiner** wird Ihr Logo auf der Leinwand dargestellt.

Im obigen Beispiel würde das Logo sowohl in der Breite als auch in der Höhe um das Doppelte seiner initialen Größe herangezoomt werden.

> [!INFO]
> Weitere Informationen zur Größe und Positionierung von SVGs finden Sie in der Dokumentation von [Mozilla](https://developer.mozilla.org/en-US/docs/Web/SVG/Tutorial/Positions).

### Darkmode und CSS-Klassen

Alle Rätsel werden mit einem **Darkmode** angeboten.
Nutzer:innen haben die Möglichkeit, je nach Präferenz zwischen heller und dunkler Darstellung zu wechseln.
Damit Ihr Logo in beiden Varianten korrekt dargestellt wird, können Sie innerhalb der SVG-Datei CSS-Klassen des Frameworks [Tailwind](https://tailwindcss.com/) verwenden.

```html
<svg class="dark:text-white fill-current" width="220" height="40" viewBox="0 0 110 20">...</svg>
```

Über `dark:` können Sie CSS-Klassen definieren, die im Darkmode zum Einsatz kommen.
Mit den Klassen `dark:text-white fill-current` wird Ihr SVG-Logo in Weiß dargestellt.
Sie können jedoch auch **andere Farben und Styles** für Ihr Logo definieren.

---

## Akzentfarbe

Neben Ihrem Logo haben Sie die Möglichkeit, einen **Farbwert** für ein Rätsel zu bestimmen,
der sich in einzelnen Elementen der Spiele widerspiegelt.

![Farbwähler für die Akzentfarbe, die in Spielelementen der Publikation verwendet wird](/images/main-color-light.png "dark:/images/main-color-dark.png")

Einige Elemente, die mit Ihrer Akzentfarbe eingefärbt werden, enthalten Schrift.
Das *oliwol Publisher Tool* **prüft** hierbei den **Kontrast** von weißer Schriftfarbe auf Ihrer Akzentfarbe.
Ist dieser zu gering (gemäß [WCAG 2 Richtlinien](https://www.w3.org/TR/WCAG21/#dfn-contrast-ratio) für Barrierefreiheit), wird ein dunkler Farbwert für Text genutzt.

![Automatische Kontrastprüfung: Schriftfarbe wird angepasst, wenn der Kontrast zur Akzentfarbe zu gering ist](/images/contrast-color-light.png "dark:/images/contrast-color-dark.png")

---

## Icon

Abgerundet wird das Layout durch ein **Icon**, das für **unterschiedliche Zwecke** innerhalb Ihrer Publikation verwendet wird.
Aus Ihrem Icon wird ein *Favicon* generiert sowie **verschiedene Auflösungen** für das [Web App Manifest](https://developer.mozilla.org/en-US/docs/Web/Manifest).

Da es sich bei den Publikationen um **PWAs** (Progressive Web Apps) handelt, können diese auf unterschiedlichen **Devices installiert** oder auf den **Homescreen** von Smartphones verlinkt werden. Zur Darstellung wird eine Auflösung Ihres Icons aus dem *Web App Manifest* genutzt.

![Verwendung des Icons in einer Publikation: als Favicon im Browser-Tab und als App-Icon auf dem Homescreen](/images/upload-icon-light.png "dark:/images/upload-icon-dark.png")

### Anforderungen

- Format: **PNG**
- Form: **quadratisch**
- Minimale Kantenlänge: **100 × 100 Pixel**
- Empfohlene Größe: **512 × 512 Pixel** – dies ist die maximale Auflösung, von der alle anderen Auflösungen abgeleitet werden

---

## Custom Font

Sie können eine **eigene Schriftart** im Format **WOFF2** für Ihre Publikation hochladen. Die Schriftart wird als primäre Schrift in Ihrem Rätsel verwendet.

---

## Individuelles CSS

Über eigene CSS-Regeln passen Sie das Erscheinungsbild Ihrer Publikation über Logo, Icon, Schrift und Akzentfarbe hinaus an.
Den Editor finden Sie in der Bearbeitungsmaske Ihrer Publikation im Bereich _Individuelles CSS_.

Die Regeln werden **nach dem Stylesheet** Ihrer Publikation geladen und überschreiben es. Zur Verfügung stehen **8 KB** je Publikation.

Individuelles CSS steht in **jedem Paket** zur Verfügung.

---

## Erscheinungsbild je Domain

Läuft eine Publikation unter **mehreren Domains**, kann jede Domain ein **eigenes Erscheinungsbild** tragen: Logo, Icon, Schrift, Akzentfarbe und individuelles CSS.
Damit erscheint dasselbe Rätsel unter zwei Marken jeweils im passenden Auftritt.

Das Erscheinungsbild einer Domain wird in der [Domain-Verwaltung](./setup#eigene-domain) Ihrer Publikation verwaltet. Öffnen Sie dort eine Domain, finden Sie den Bereich _Erscheinungsbild_.

> [!INFO]
> Das Erscheinungsbild je Domain gehört zum Modul **Branded Domains**. Ohne dieses Modul erscheinen alle Domains einer Publikation gleich.

### Standard-Domain

Eine Ihrer Domains ist die **Standard-Domain**. Sie zeigt immer das Layout Ihrer Publikation und hat daher keine eigenen Felder für das Erscheinungsbild.
Was auf der Standard-Domain zu sehen ist, bestimmen Sie in der Bearbeitungsmaske Ihrer Publikation.

Alle weiteren Domains richten sich nach der Standard-Domain, solange sie nichts Eigenes hinterlegt haben.

### Vererbung

Über den Schalter **Einstellungen der Standard-Domain nutzen** entscheiden Sie, ob eine Domain ein eigenes Erscheinungsbild führt:

- **Schalter aktiv:** Die Domain erscheint wie die Standard-Domain.
- **Schalter aus:** Es gelten die Werte, die Sie für diese Domain hinterlegen.

Die Vererbung greift **feldweise**. Ein leeres Feld ist keine Entscheidung gegen einen Wert, sondern übernimmt weiterhin den Wert der Standard-Domain.
Hinterlegen Sie also nur eine abweichende Akzentfarbe, bleiben Logo, Icon und Schrift die Ihrer Publikation.

| Feld auf der Domain | Ergebnis |
| --- | --- |
| Gefüllt | Der Wert der Domain gilt |
| Leer | Der Wert der Standard-Domain gilt |

Schalten Sie die Vererbung wieder ein, bleiben die hinterlegten Werte gespeichert und gelten erneut, sobald Sie den Schalter ausschalten.

### CSS je Domain

Beim CSS gilt die feldweise Vererbung nicht, denn hier **ergänzen** sich beide Ebenen:
Zuerst wird das individuelle CSS Ihrer **Publikation** geladen, danach das der **Domain**.
Damit hat die Domain das letzte Wort und kann einzelne Regeln überschreiben, ohne das gesamte Stylesheet zu wiederholen.

Auch je Domain stehen **8 KB** zur Verfügung.

> [!INFO]
> Änderungen am Erscheinungsbild werden gesammelt und mit der nächsten [Bereitstellung](./setup#bereitstellung) auf die Domain übertragen. Auf einer Live-Domain werden sie mit der nächsten [Synchronisation](./setup#nicht-synchronisiert) sichtbar.
