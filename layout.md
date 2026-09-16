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

### Dunkles Layout und CSS-Klassen

Alle Rätsel werden in einem **hellen und einem dunklen Layout** angeboten. Welches davon erscheint, bestimmt der [Farbmodus](#farbmodus).
Damit Ihr Logo in beiden Varianten korrekt dargestellt wird, können Sie innerhalb der SVG-Datei CSS-Klassen des Frameworks [Tailwind](https://tailwindcss.com/) verwenden.

```html
<svg class="dark:text-white fill-current" width="220" height="40" viewBox="0 0 110 20">...</svg>
```

Über `dark:` können Sie CSS-Klassen definieren, die im dunklen Layout zum Einsatz kommen.
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

## Farbmodus

Jedes Rätsel erscheint **hell oder dunkel**. Der Modus wird nicht im Rätsel umgeschaltet, sondern kommt von außen: vom **Gerät**, aus der **Adresse** oder von der **Seite**, in die das Rätsel eingebettet ist.
So zeigt Ihre Publikation denselben Modus wie die Umgebung, in der sie läuft.

> [!INFO]
> Ob das dunkle Layout überhaupt in Frage kommt, entscheidet die Einstellung [Dunkles Layout](./configuration#dunkles-layout). Ist sie aus, erscheint die Publikation immer hell, unabhängig von jedem Signal.

### Reihenfolge der Signale

Es gilt das zuletzt eingetroffene Signal:

| Reihenfolge | Signal | Wirkung |
| --- | --- | --- |
| 1 | Einstellung des **Geräts** | Steht das Betriebssystem auf dunkel, erscheint das Rätsel dunkel. Das ist die Voreinstellung. |
| 2 | Parameter **`color-scheme`** in der Adresse | Legt den Modus für diesen Aufruf fest und geht der Einstellung des Geräts vor. |
| 3 | **Laufzeitnachricht** der einbettenden Seite | Legt den Modus fest, während das Rätsel läuft, und geht Adresse und Gerät vor. |

### Parameter in der Adresse

Der Parameter `color-scheme` bestimmt den Modus beim Aufruf:

| Wert | Ergebnis |
| --- | --- |
| `light` | Das Rätsel erscheint hell. |
| `dark` | Das Rätsel erscheint dunkel. |
| Kein oder ein anderer Wert | Die Einstellung des Geräts gilt. |

```text
https://sudoku.example.com/?color-scheme=dark
```

Der Parameter wirkt auf Ihrer eigenen Domain genauso wie in der Adresse eines Iframes. Der [Embed-Code](./setup#iframe-script) bringt ihn auf Wunsch bereits mit.

### Laufzeitnachricht

Trägt Ihre Seite einen eigenen Umschalter, meldet sie den Modus per `postMessage` an die Publikation. Die Nachricht wirkt sofort, der Iframe wird dabei nicht neu geladen:

```javascript
document.getElementById('sudoku').contentWindow.postMessage(
    { source: 'oliwol', colorScheme: 'dark' },
    'https://sudoku.example.com'
);
```

| Property | Wert |
| --- | --- |
| `source` | Immer `oliwol`. Daran erkennt die Publikation Ihre Nachricht. |
| `colorScheme` | `light` oder `dark`. |

Angenommen wird allein die Nachricht des **direkten Elternfensters**. Steht zwischen Ihrer Seite und der Publikation ein weiterer Rahmen, reicht dieser die Nachricht weiter.

Senden Sie die Nachricht einmal, sobald die Publikation geladen ist, und danach bei jedem Wechsel.

Umgekehrt meldet die Publikation ihren Modus an Ihre Seite, siehe [Nachrichten an Ihre Seite](./setup#nachrichten-an-ihre-seite).

### Durchsichtigkeit in der Einbettung

Eingebettet zeichnet die Publikation **keinen eigenen Hintergrund**. Sie liegt in beiden Modi durchsichtig auf Ihrer Seite und zeigt deren Hintergrund.

Dafür muss der Iframe denselben Farbmodus tragen wie das eingebettete Rätsel. Andernfalls zeichnet der Browser hinter dem Rahmen eine deckende weiße Fläche.
Der [Embed-Code](./setup#iframe-script) bringt das passende `color-scheme` am Iframe schon mit.

> [!WARNING]
> Bauen Sie den Iframe selbst, gehört `color-scheme` an das Element:
>
> ```html
> <iframe src="https://sudoku.example.com" style="color-scheme: light dark; border: none;"></iframe>
> ```
>
> `light dark` gehört zu einem Rätsel, das dem Gerät folgt. Legen Sie den Modus über den Parameter fest, tragen Sie denselben Wert hier ein: `color-scheme: dark` zu `color-scheme=dark`.
>
> Setzt Ihre Seite den Modus über die [Laufzeitnachricht](#laufzeitnachricht), zieht der Wert am Element mit jeder Nachricht nach:
>
> ```javascript
> frame.style.colorScheme = 'dark';
> ```

Einen eigenen Hintergrund setzen Sie über [Individuelles CSS](#individuelles-css). Es wird nach allem anderen geladen und überschreibt es.

---

## Dunkle Grundfarbe

Im dunklen Layout liegt Ihre Publikation auf einem **dunklen Grundton**. Über das Feld *Dunkle Grundfarbe* bestimmen Sie diesen Ton, etwa passend zum Hintergrund Ihrer Seite.

Der eingetragene Wert erscheint **exakt** als Hintergrund. Alle weiteren dunklen Flächen, etwa Karten, Felder und Trennlinien, leiten sich daraus ab und werden schrittweise heller.
Das helle Layout und die [Akzentfarbe](#akzentfarbe) bleiben davon unberührt.

Neben dem Feld zeigt eine **Vorschau**, wie ein Rätsel mit dieser Farbe aussieht.

Bleibt das Feld leer, gilt das gewohnte Grau.

Eine Farbe, die als Hintergrund nicht mehr dunkel genug ist, wird **abgelehnt**. Bei sehr bunten Farben und bei zu geringem Abstand zur Akzentfarbe erscheint ein Hinweis, die Farbe lässt sich aber speichern.

Die dunkle Grundfarbe steht an der **Publikation** und an jeder [Marke](./brands). Sie wird wie die Akzentfarbe vererbt: Ist sie an der Marke gefüllt, gilt sie auf deren Domains, sonst die der Publikation. Siehe [Erscheinungsbild je Domain](#erscheinungsbild-je-domain).

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

Läuft eine Publikation unter **mehreren Domains**, kann jede Domain ein **eigenes Erscheinungsbild** tragen: Logo, Icon, Schrift, Akzentfarbe, dunkle Grundfarbe und individuelles CSS. Dasselbe Rätsel erscheint damit unter jeder Domain im passenden Layout.

Das Erscheinungsbild hängt dabei nicht an der Domain, sondern an einer [Marke](./brands): Die Domain zeigt auf eine Marke, die Marke trägt das Erscheinungsbild. Zeigen Domains mehrerer Publikationen auf dieselbe Marke, pflegen Sie deren Layout nur **einmal**.

> [!INFO]
> Das Erscheinungsbild je Domain gehört zum Modul **Marken**. Ohne dieses Modul erscheinen alle Domains einer Publikation gleich.
> Endet das Modul, bleiben bestehende Zuordnungen wirksam, lassen sich aber nicht mehr ändern.

### Vererbung

Die Layout-Werte Ihrer Publikation (Logo, Icon, Schrift, Akzentfarbe, dunkle Grundfarbe und individuelles CSS) sind der **Standard**. Eine Marke überschreibt ihn auf ihren Domains **feldweise**:

| Feld an der Marke | Ergebnis auf ihren Domains |
| --- | --- |
| Gefüllt | Der Wert der Marke gilt |
| Leer | Der Wert der Publikation gilt |

Sie pflegen an einer Marke also nur die Abweichungen: Setzt eine Marke nur Logo, Icon und Akzentfarbe, bleibt die Schrift die der Publikation.

Eine Domain **ohne** Marke zeigt das Erscheinungsbild der Publikation unverändert.

### CSS je Marke

Für das individuelle CSS gilt eine Ausnahme von der feldweisen Vererbung: Beide Ebenen werden **kombiniert**. Zuerst lädt das CSS der **Publikation**, danach das der **Marke**. Die Marke kann damit einzelne Regeln überschreiben, ohne das gesamte Stylesheet zu wiederholen.

Je Marke und Publikation stehen **8 KB** zur Verfügung.

> [!INFO]
> Änderungen am Erscheinungsbild werden gesammelt und mit der nächsten [Bereitstellung](./setup#bereitstellung) auf die Domains übertragen. Auf einer Live-Domain werden sie mit der nächsten [Synchronisation](./setup#nicht-synchronisiert) sichtbar.
