# SEO

Publikationen sind in der **Basis** bereits für Suchmaschinen **optimal konfiguriert**.
Sie haben **zusätzlich** die Möglichkeit, **eigene Anpassungen** vorzunehmen,
um sich für Ihre Bedarfsgruppe in den Suchergebnissen zu präsentieren.

---

## Meta-Daten

SEO-Meta-Daten können für alle Inhaltsbereiche bearbeitet werden — sowohl für [Seiten](./content#seiten) als auch für [FAQs](./content#faqs), die als eigene Seite veröffentlicht werden.

### SEO-Title

Für jede Seite können Sie einen **SEO-Title hinterlegen**, der in den **Suchergebnissen angezeigt** wird.

![SEO](/images/seo-light.png "dark:/images/seo-dark.png")

Um Ihren SEO-Title vorab passgerecht für Google zu formulieren,
können Sie auf den **Snippet Generator** von [Sistrix](https://app.sistrix.com/de/serp-snippet-generator) zurückgreifen.

Sobald Sie Änderungen am SEO-Title vornehmen, wird dieser innerhalb Ihrer Publikation **aktualisiert**.
Es kann jedoch einige **Zeit in Anspruch nehmen**, bis die Änderung auch in den **Suchergebnissen sichtbar** wird.
Je nach Crawling-Frequenz des Suchmaschinen-Bots kann dies zwischen **wenigen Stunden und einigen Tagen** dauern.

![SEO](/images/search-snippet-light.png "dark:/images/search-snippet-dark.png")

### Description

Bei der Description handelt es sich um den **Beschreibungstext unter dem Titel** eines Suchergebnisses (auch *SERP-Snippet* genannt).

Sie haben die Möglichkeit, eine **längere Meta-Description** zu hinterlegen –
diese könnte im *SERP-Snippet* jedoch **abgeschnitten** werden.

### Robots

Über die **Robots-Einstellungen** bestimmen Sie, ob Seiten in den **Suchergebnissen gelistet** werden (`index` / `noindex`)
und ob **Suchmaschinen-Crawler Links** innerhalb einer Seite **folgen** dürfen (`follow` / `nofollow`).
Die Robots-Einstellungen sind für alle Seiten bereits vorkonfiguriert und können **bei Bedarf angepasst** werden.

- **Index entfernen:** Entfernen Sie den Haken bei „Index", um eine Seite aus dem Index einer Suchmaschine zu löschen.
- **Follow entfernen:** Entfernen Sie den Haken bei „Follow", um einer Suchmaschine den Zugriff auf Links innerhalb einer Seite zu sperren.

> [!INFO]
> Auf allen [Umgebungen](./) außer der **Live-Umgebung** wird per `X-Robots-Tag`-Header jede Seite automatisch auf `noindex, nofollow` gesetzt. So wird verhindert, dass Testumgebungen in den Suchergebnissen erscheinen.
