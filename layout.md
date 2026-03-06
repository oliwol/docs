# Layout

Sie haben mit dem *oliwol Publisher Tool* die Möglichkeit, die Rätsel an Ihr **Layout anzupassen**.
Hierbei stehen das **Logo**, die **Markenfarbe**, das **Icon** und eine optionale **Custom Font** zur Verfügung.

---

## Logo

Das Logo wird innerhalb der Bearbeitungsmaske Ihrer Publikation im Bereich _Layout_ verwaltet.
Ihr Logo kann ausschließlich im **SVG-Format** hochgeladen werden.

![Logo](/images/upload-logo-light.png "dark:/images/upload-logo-dark.png")

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

![Akzentfarbe](/images/main-color-light.png "dark:/images/main-color-dark.png")

Einige Elemente, die mit Ihrer Akzentfarbe eingefärbt werden, enthalten Schrift.
Das *oliwol Publisher Tool* **prüft** hierbei den **Kontrast** von weißer Schriftfarbe auf Ihrer Akzentfarbe.
Ist dieser zu gering (gemäß [WCAG 2 Richtlinien](https://www.w3.org/TR/WCAG21/#dfn-contrast-ratio) für Barrierefreiheit), wird ein dunkler Farbwert für Text genutzt.

![Kontrast](/images/contrast-color-light.png "dark:/images/contrast-color-dark.png")

---

## Icon

Abgerundet wird das Layout durch ein **Icon**, das für **unterschiedliche Zwecke** innerhalb Ihrer Publikation verwendet wird.
Aus Ihrem Icon wird ein *Favicon* generiert sowie **verschiedene Auflösungen** für das [Web App Manifest](https://developer.mozilla.org/en-US/docs/Web/Manifest).

Da es sich bei den Publikationen um **PWAs** (Progressive Web Apps) handelt, können diese auf unterschiedlichen **Devices installiert** oder auf den **Homescreen** von Smartphones verlinkt werden. Zur Darstellung wird eine Auflösung Ihres Icons aus dem *Web App Manifest* genutzt.

![Icon](/images/upload-icon-light.png "dark:/images/upload-icon-dark.png")

### Anforderungen

- Format: **PNG**
- Form: **quadratisch**
- Minimale Kantenlänge: **100 × 100 Pixel**
- Empfohlene Größe: **512 × 512 Pixel** – dies ist die maximale Auflösung, von der alle anderen Auflösungen abgeleitet werden

---

## Custom Font

Sie können eine **eigene Schriftart** im Format **WOFF2** für Ihre Publikation hochladen. Die Schriftart wird als primäre Schrift in Ihrem Rätsel verwendet.