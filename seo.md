# SEO

Publikationen sind in der **Basis** bereits für Suchmaschinen **optimal konfiguriert**.
Sie haben **zusätzlich** die Möglichkeit, **eigene Anpassungen** vorzunehmen,
um sich für Ihre Bedarfsgruppe in den Suchergebnissen zu präsentieren.

---

## Meta-Daten

SEO-Meta-Daten können für alle Inhaltsbereiche bearbeitet werden — sowohl für [Seiten](./content#seiten) als auch für [FAQs](./content#faqs), die als eigene Seite veröffentlicht werden.

### SEO-Title

Für jede Seite können Sie einen **SEO-Title hinterlegen**, der in den **Suchergebnissen angezeigt** wird.

![Eingabefelder für SEO-Title, Description und Robots-Einstellungen einer Seite](/images/seo-light.png "dark:/images/seo-dark.png")

Um Ihren SEO-Title vorab passgerecht für Google zu formulieren,
können Sie auf den **Snippet Generator** von [Sistrix](https://app.sistrix.com/de/serp-snippet-generator) zurückgreifen.

Sobald Sie Änderungen am SEO-Title vornehmen, wird dieser innerhalb Ihrer Publikation **aktualisiert**.
Es kann jedoch einige **Zeit in Anspruch nehmen**, bis die Änderung auch in den **Suchergebnissen sichtbar** wird.
Je nach Crawling-Frequenz des Suchmaschinen-Bots kann dies zwischen **wenigen Stunden und einigen Tagen** dauern.

![Vorschau eines Google-Suchergebnisses mit konfiguriertem SEO-Title und Description](/images/search-snippet-light.png "dark:/images/search-snippet-dark.png")

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

### indexifembedded

Wenn Sie Ihre Publikation über [Iframe oder Script](./setup#iframe-script) in eine bestehende Seite einbinden, stehen dieselben Inhalte an zwei Adressen: unter der Domain Ihrer Publikation und innerhalb Ihrer Seite. Suchmaschinen nehmen dann beide auf, und die Adresse der Publikation erscheint ohne Ihr Seitengerüst in den Suchergebnissen.

Für diesen Fall gibt es den Schalter **Publikation wird eingebettet betrieben**. Sie finden ihn im Dialog [Einbetten](./setup#iframe-script) unter **Suchmaschinen**, direkt unter dem Integrations-Code.

Ist er aktiv, gibt jede Seite Ihrer Publikation `noindex, indexifembedded` aus. Das bedeutet:

- Die **Adresse Ihrer Publikation** wird **nicht mehr** in die Suchergebnisse aufgenommen.
- Die **Inhalte bleiben auffindbar**, und zwar über die Seite, in die Sie sie eingebunden haben.

Seiten, die Sie über die [Robots-Einstellungen](#robots) ohnehin vom Index ausgenommen haben, bleiben vollständig ausgeschlossen.

> [!INFO]
> Die Umstellung wird mit der nächsten [Bereitstellung](./setup#bereitstellung) wirksam. Bis die Änderung in den Suchergebnissen ankommt, vergeht zusätzlich die Zeit bis zum nächsten Besuch des Suchmaschinen-Bots. Je nach Crawling-Frequenz sind das wenige Stunden bis einige Tage.

> [!WARNING]
> `indexifembedded` wird nicht von allen Suchmaschinen unterstützt. Wo die Angabe unbekannt ist, zählt allein das `noindex`: Der Inhalt wird dort weder unter der Adresse Ihrer Publikation noch über Ihre einbettende Seite aufgenommen.
