# Tracking

Um Klicks, Besuche, Engagement oder andere Metriken über Ihre Nutzer:innen zu sammeln,
können externe Analyse-Systeme angebunden werden.
Außerdem liefern die Publikationen `Custom Events`, auf die gelauscht werden kann.

> [!WARNING]
> Für das Tracking ist es erforderlich, die Zustimmung von Nutzer:innen einzuholen.
> Bitte beachten Sie hierzu auch den Bereich [CMP](./cmp).

---

## Integration von Analyse-Systemen

Die Integration erfolgt über den Tab _Scripts_ in der Bearbeitungsmaske einer Publikation.

> [!INFO]
> Der Tab _Scripts_ ist ab dem Paket **Starter** verfügbar.

Es gibt die Möglichkeit, sowohl externe Scripte als auch Inline-Javascript zu integrieren.
Das Javascript wird im `<head>` der Seite eingebunden.
Jedes **Inline-Javascript** wird in einem eigenen `<script>`-Tag integriert,
für den jeweils zusätzliche Attribute hinterlegt werden können.

Für **externe Scripte** stehen folgende Einstellungsmöglichkeiten zur Verfügung:

- **Source:** Das `src`-Attribut
- **Load method:** `sync`, `async`, `defer` oder `preload`
- **Position:** Auswahl, ob das Script vor oder nach den Inline-Scripts geladen werden soll
- **Attributes:** Möglichkeit, dem `<script>`-Tag weitere Attribute hinzuzufügen

![Konfiguration eines externen Scripts mit Source, Lademethode, Position und Attributen](/images/script-library-light.png "dark:/images/script-library-dark.png")

### Integration am Beispiel von Google Analytics 4

Google Analytics bietet die Möglichkeit, das Tracking via **Google Tag Manager** oder direkt über das **Google-Tag** einzubinden.

#### Google Tag Manager

Für den Google Tag Manager wird kein externes Script benötigt.
Das im Google Tag Manager [hinterlegte Script](https://support.google.com/tagmanager/answer/9442095) kann direkt inline integriert werden.

![Inline-Script mit dem Google Tag Manager Code-Snippet](/images/script-inline-light.png "dark:/images/script-inline-dark.png")

Wichtig ist, dass das `dataLayer`-Objekt **vor** der Integration des Google Tag Managers definiert wird.
Der Code kann direkt im selben oder einem eigenen Code-Block integriert werden.

```javascript
window.dataLayer = window.dataLayer || [];
```

![Separater Inline-Script-Block für die dataLayer-Initialisierung vor dem Tag Manager](/images/script-inline-gtm-light.png "dark:/images/script-inline-gtm-dark.png")

Damit ist die Integration abgeschlossen. Alle weiteren Einstellungen werden im *Google Tag Manager* durchgeführt.

#### Google Tag

Für die direkte Einbindung des *Google-Tag* muss zunächst ein externes Script für die Bibliothek angelegt werden.
Folgende Angaben sind erforderlich:

- **Source:** `https://www.googletagmanager.com/gtag/js?id=[G-ID]`
- **Load method:** `async`
- **Position:** „Before inline script"

Achten Sie darauf, dass als Position „Before inline script" ausgewählt wird,
da der `dataLayer` **nach** der Einbindung des Google-Tag definiert wird.

```javascript
window.dataLayer = window.dataLayer || [];
```

Die Integration ist damit abgeschlossen.
Für die Übergabe von Events oder anderen Daten kann das `dataLayer`-Objekt genutzt werden.

### Integration am Beispiel von Adobe Analytics

Für die Integration von *Adobe Analytics* ist die Einbindung des **Tags-Script** Voraussetzung.
Diese erfolgt mithilfe eines externen Scripts innerhalb einer Publikation.
Die Attribute sollten wie folgt ausgefüllt werden:

- **Source:** `https://assets.adobedtm.com/.../launch-[ID].min.js`
- **Load method:** `async`
- **Position:** „After inline script"

In diesem Fall muss „After inline script" ausgewählt werden.
Dies ermöglicht die [Übergabe von Objekten](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/adobe-client-data-layer/data-layer-overview.html?lang=de) an den *Adobe Data Layer*.

Der *Data Layer* wird als Inline-Script integriert:

```javascript
window.adobeDataLayer = window.adobeDataLayer || [];
```

![Inline-Script zur Initialisierung des Adobe Data Layers](/images/adobe-analytics-data-layer-light.png "dark:/images/adobe-analytics-data-layer-dark.png")

> [!INFO]
> Wenn Sie eine **Staging-Umgebung** für Ihre Publikation verwenden,
> können Sie das Staging-Script aus *Tags* hinterlegen.

> [!INFO]
> Die Publikationen senden für Aktionen `Custom Events`, die Sie in *Adobe Tags*
> entgegennehmen und auf `Custom Vars` mappen können.
> Näheres dazu finden Sie im Kapitel [Custom Events](#custom-events).

Die Integration ist damit abgeschlossen. Für die Übergabe von Events oder anderen Daten
kann der *Adobe Data Layer* verwendet werden.

### Integration am Beispiel der IVW

Bevor Seitenaufrufe gezählt werden können, ist es erforderlich,
den *INFOnline Measurement Manager* zu implementieren.
Hierfür stellt die *IVW* [zwei Methoden](https://docs.infonline.de/infonline-measurement/integration/web/measurement_manager/#bootstrapping) zur Verfügung:

#### Mit Preload und Bundle-Loader

Integrieren Sie zunächst die `bundle.js` als externes Script mit der Methode `preload`.
Erstellen Sie die Attribute `as="script"` und `crossorigin`.

> [!WARNING]
> Damit die Seitenaufrufe korrekt gezählt werden können,
> müssen Sie als Position **Before inline script** auswählen.

![Externes Script für die IVW bundle.js mit Preload-Methode](/images/ivw-tracking-light.png "dark:/images/ivw-tracking-dark.png")

Die Methode `preload` generiert keinen `<script>`-Tag, sondern einen `<link>`-Tag:

```html
<link rel="preload" href="//[domain service name]/iomm/latest/manager/base/es6/bundle.js" as="script" crossorigin>
```

Im nächsten Schritt wird die `loader.js` ebenfalls mit der Methode `preload` und denselben Attributen implementiert.

![Externes Script für die IVW loader.js mit Preload-Methode](/images/ivw-tracking-loader-preload-light.png "dark:/images/ivw-tracking-loader-preload-dark.png")

Zuletzt muss die `loader.js` **synchron** geladen werden.

![Externes Script für die IVW loader.js mit synchroner Lademethode](/images/ivw-tracking-loader-sync-light.png "dark:/images/ivw-tracking-loader-sync-dark.png")

Wenn Sie alle vorangegangenen Einstellungen korrekt implementiert haben, erzeugt dies folgende Ausgabe:

```html
<link rel="preload" href="//[domain service name]/iomm/latest/manager/base/es6/bundle.js" as="script" crossorigin>

<link rel="preload" href="//[domain service name]/iomm/latest/manager/base/es6/loader.js" as="script" crossorigin>

<script type="text/javascript" src="https://[domain service name]/iomm/latest/bootstrap/loader.js" crossorigin></script>
```

> [!INFO]
> Es ist empfehlenswert, exakt nach der [Anleitung der IVW](https://docs.infonline.de/infonline-measurement/integration/web/measurement_manager/) vorzugehen
> und sowohl die Reihenfolge der Tags als auch sämtliche Attribute zu beachten.

Nachdem die initialen Scripte implementiert sind, kann die **Konfiguration und die eigentliche Zählung** stattfinden.
Hierzu verwenden Sie ein **Inline-Script**:

```javascript
IOMm("configure", { st: "foo", dn: "data-acbd18db4c.example.com" }); // Configure IOMm
IOMm("pageview", { cp: "bar", co: "baz" }); // Count pageview
```

![Inline-Script mit IVW-Konfiguration und Pageview-Event](/images/ivw-trigger-light.png "dark:/images/ivw-trigger-dark.png")

> [!INFO]
> In der Dokumentation werden nur Beispielwerte angegeben. Bitte stellen Sie sicher,
> dass sowohl der *Domain Service Name* als auch die Attributswerte für die
> [Konfiguration](https://docs.infonline.de/infonline-measurement/integration/web/measurement_manager/#konfiguration)
> und das [Tracking](https://docs.infonline.de/infonline-measurement/integration/web/measurement_manager/#pageview) korrekt angegeben werden.

Damit ist die Integration abgeschlossen.
Sollten Sie neue Zählcodes verwenden, müssen diese bei der IVW zugeordnet werden,
damit die Messungen korrekt durchgeführt werden.

#### Ohne Preload und Bundle-Loader

Die Variante ohne Preload und Bundle-Loader unterscheidet sich vor allem in der Reihenfolge der auszuführenden Code-Blöcke.

Initial wird zunächst die `stub.js` **synchron** geladen.
Hierbei ist zu beachten, dass das externe Script **vor dem Inline-Javascript positioniert** werden muss.

![Externes Script für die IVW stub.js mit synchroner Lademethode, positioniert vor dem Inline-Script](/images/ivw-tracking-stub-light.png "dark:/images/ivw-tracking-stub-dark.png")

Im Nachgang erfolgt die Konfiguration Ihrer Zählung und das Pageview-Event:

```javascript
IOMm("configure", { st: "foo", dn: "data-acbd18db4c.example.com" }); // Configure IOMm
IOMm("pageview", { cp: "bar", co: "baz" }); // Count pageview
```

![Inline-Script mit IVW-Konfiguration und Pageview-Zählung](/images/ivw-trigger-light.png "dark:/images/ivw-trigger-dark.png")

Im letzten Schritt muss die `bundle.js` **asynchron** geladen werden.
Hier ist zu beachten, dass das externe Script **nach dem Inline-Javascript positioniert** wird.

![Externes Script für die IVW bundle.js mit async-Lademethode, positioniert nach dem Inline-Script](/images/ivw-tracking-bundle-light.png "dark:/images/ivw-tracking-bundle-dark.png")

Wenn Sie alle vorangegangenen Einstellungen korrekt implementiert haben, erzeugt dies folgende Ausgabe:

```html
<script type="text/javascript" src="https://[domain service name]/iomm/latest/bootstrap/stub.js" crossorigin></script>

<script type="text/javascript">
IOMm("configure", { st: "foo", dn: "data-acbd18db4c.example.com" }); // Configure IOMm
IOMm("pageview", { cp: "bar", co: "baz" }); // Count pageview
</script>

<script async type="text/javascript" src="https://[domain service name]/iomm/latest/manager/base/es5/bundle.js" crossorigin></script>
```

---

## Custom Events

Wenn Nutzer:innen mit Ihrer Publikation interagieren, werden `Custom Events` ausgelöst,
die von Tracking-Systemen entgegengenommen und analysiert werden können.

`Custom Events` werden wie folgt getriggert:

```javascript
window.dispatchEvent(new CustomEvent(EventAction, {
    detail: EventValue,
}));
```

`EventValue` ist ein Objekt, das wiederum Objekte, Strings oder Integer-Werte enthalten kann.

Die Events teilen sich in zwei Kategorien auf:

- **Allgemeine Events** — werden in jeder Publikation gefeuert, unabhängig vom Rätseltyp.
- **Rätselspezifische Events** — gelten nur für das jeweilige Spiel.

### Allgemeine Events

Diese Events sind in allen Publikationen verfügbar:

| EventAction | Interaktion | EventValue |
|---|---|---|
| `PageView` | Beim Navigieren durch die Publikation bzw. Aufruf einer neuen Seite (virtuelle Page-Impression). | <pre lang="json">{&#10;  "from": "Object",&#10;  "to": "Object"&#10;}</pre> Details siehe [Virtuelle Seitenaufrufe](#virtuelle-seitenaufrufe). |
| `Auth` | Sobald ein(e) Nutzer:in sich über die SSO erfolgreich authentifiziert. | – |
| `PaywallTriggered` | Ein Inhalt hinter der Paywall wurde aufgerufen. Das Event wird bei allen [Paywall-Varianten](./paywall#paywall-erstellen) gesendet, auch wenn die Publikation die Paywall selbst anzeigt. | <pre lang="json">{&#10;  "state": "String",&#10;  "trigger": "String",&#10;  "path": "String",&#10;  ...&#10;}</pre> Details siehe [Paywall-Kontakte](#paywall-kontakte). |
| `ShareResult` | Spiel-Ergebnis wird über die Teilen-Funktion (z. B. WebShare-API) geteilt. | Rätselspezifischer Payload — siehe jeweilige Tabelle. |
| `CopyResult` | Spiel-Ergebnis wird in die Zwischenablage kopiert. | – |
| `ClickOtherGame` | Klick auf eine verlinkte andere Publikation (z. B. im Footer). | <pre lang="json">{&#10;  "game": "String"&#10;}</pre> Name der Publikation. |
| `SwitchSetup` | Eine Einstellung (z. B. Dark Mode) wurde umgeschaltet. | <pre lang="json">{&#10;  "setup": "String",&#10;  "value": "Boolean &#124; String"&#10;}</pre> `setup` z. B. `dark_mode` oder `wordlist_sort`. `value` ist ein `Boolean` bei An/Aus-Einstellungen, sonst ein `String` bei mehrwertigen Einstellungen (z. B. Sortier-Modus `newest` / `alpha` / `points`). |
| `UseHeaderIcon` | Ein Icon im Header (Hilfe, Statistiken, Login) wurde angeklickt. | <pre lang="json">{&#10;  "icon": "String"&#10;}</pre> z. B. `help`, `stats`, `auth`. |
| `UseOffCanvasMenuItem` | Ein Eintrag im Off-Canvas-Menü wurde ausgewählt. | <pre lang="json">{&#10;  "item": "String"&#10;}</pre> Titel des Eintrags. |

### Worteck

Zusätzlich zu den [Allgemeinen Events](#allgemeine-events):

| EventAction | Interaktion | EventValue |
|---|---|---|
| `GameStarted` | Wird einmalig ausgelöst, wenn ein(e) Nutzer:in zum ersten Mal mit dem Rätsel interagiert. Bei einem Neustart oder der Wiederaufnahme eines bereits begonnenen Spiels wird das Event nicht erneut gefeuert. | <pre lang="json">{&#10;  "game_nr": "Integer"&#10;}</pre> |
| `GameSucceeded` | Ein Wort wurde erfolgreich erraten. | <pre lang="json">{&#10;  "game_nr": "Integer",&#10;  "game_success_row": "Integer"&#10;}</pre> |
| `GameFinished` | Ein Spiel wurde beendet, unabhängig davon ob das Wort erraten wurde oder nicht. | <pre lang="json">{&#10;  "game_nr": "Integer",&#10;  "game_success_row": "Integer"&#10;}</pre> |
| `GameFailed` | Ein Spiel wurde beendet, aber das Wort nicht erraten. | <pre lang="json">{&#10;  "game_nr": "Integer",&#10;  "game_success_row": "Integer"&#10;}</pre> |
| `RowCompleted` | Eine Reihe wurde vervollständigt (Wort ist valide und existiert). | <pre lang="json">{&#10;  "game_nr": "Integer",&#10;  "game_current_row": "Integer"&#10;}</pre> |
| `NewGame` | Nach Beendigung eines Spiels wird ein neues gestartet (nur wenn mehr als ein Wort pro Tag möglich ist). | <pre lang="json">{&#10;  "game_nr": "Integer",&#10;  "remaining_games": "Integer"&#10;}</pre> |
| `AllGamesCompleted` | Ein(e) Nutzer:in hat alle zur Verfügung gestellten Worte zu einem Datum beendet. | <pre lang="json">{&#10;  "date": "String"&#10;}</pre> Format `YYYY-MM-DD`. |
| `ShareResult` | Payload für das [Allgemeine Event](#allgemeine-events). | <pre lang="json">{&#10;  "game_nr": "Integer",&#10;  "game_success_row": "Integer"&#10;}</pre> |

### Sudoku

Zusätzlich zu den [Allgemeinen Events](#allgemeine-events):

| EventAction | Interaktion | EventValue |
|---|---|---|
| `GameStarted` | Wird einmalig ausgelöst, wenn ein(e) Nutzer:in zum ersten Mal mit dem Rätsel interagiert. Bei einem Neustart oder der Wiederaufnahme eines bereits begonnenen Spiels wird das Event nicht erneut gefeuert. | <pre lang="json">{&#10;  "game_nr": "Integer"&#10;}</pre> |
| `GameFinished` | Ein Sudoku wurde erfolgreich beendet. | <pre lang="json">{&#10;  "game_nr": "Integer",&#10;  "timer": "Integer"&#10;}</pre> `timer` in Sekunden. |
| `GameFailed` | Alle Zahlen wurden ausgefüllt, aber es sind noch Fehler enthalten. | <pre lang="json">{&#10;  "game_nr": "Integer",&#10;  "timer": "Integer"&#10;}</pre> `timer` in Sekunden. |
| `RestartGame` | Ein Sudoku wurde zurückgesetzt und erneut begonnen. | <pre lang="json">{&#10;  "game_nr": "Integer",&#10;  "timer": "Integer"&#10;}</pre> `timer` = Zeitpunkt der Zurücksetzung in Sekunden. |
| `PrintGame` | Ein Sudoku wurde gedruckt. | <pre lang="json">{&#10;  "game_nr": "Integer"&#10;}</pre> |
| `ShareResult` | Payload für das [Allgemeine Event](#allgemeine-events). | <pre lang="json">{&#10;  "game_nr": "Integer",&#10;  "timer": "Integer"&#10;}</pre> |

### Wortwabe

Zusätzlich zu den [Allgemeinen Events](#allgemeine-events):

| EventAction | Interaktion | EventValue |
|---|---|---|
| `GameStarted` | Wird einmalig ausgelöst, wenn ein(e) Nutzer:in zum ersten Mal mit dem Rätsel interagiert. Bei einem Neustart oder der Wiederaufnahme eines bereits begonnenen Spiels wird das Event nicht erneut gefeuert. | <pre lang="json">{&#10;  "game_nr": "Integer"&#10;}</pre> |
| `GameFinished` | Ein Spiel wurde erfolgreich beendet. | <pre lang="json">{&#10;  "game_nr": "Integer",&#10;  "count_words": "Integer",&#10;  "deviation": "Integer",&#10;  "count_isograms": "Integer"&#10;}</pre> |
| `WordFound` | Ein Wort wurde entdeckt. | <pre lang="json">{&#10;  "game_nr": "Integer",&#10;  "word": "String",&#10;  "is_isogram": "Boolean"&#10;}</pre> `word` in Großbuchstaben. |
| `ShuffleLetters` | Die Buchstaben werden manuell gemischt. | <pre lang="json">{&#10;  "game_nr": "Integer"&#10;}</pre> |
| `ExpandWordList` | Die Liste der gefundenen Wörter wurde aufgeklappt. | <pre lang="json">{&#10;  "game_nr": "Integer"&#10;}</pre> |
| `ShareResult` | Payload für das [Allgemeine Event](#allgemeine-events). | <pre lang="json">{&#10;  "game_nr": "Integer",&#10;  "count_words": "Integer",&#10;  "top_score": "Boolean",&#10;  "count_isograms": "Integer"&#10;}</pre> |

### Kreuzworträtsel

Zusätzlich zu den [Allgemeinen Events](#allgemeine-events):

| EventAction | Interaktion | EventValue |
|---|---|---|
| `GameStarted` | Wird einmalig ausgelöst, wenn ein(e) Nutzer:in zum ersten Mal mit dem Rätsel interagiert. Bei einem Neustart oder der Wiederaufnahme eines bereits begonnenen Spiels wird das Event nicht erneut gefeuert. | <pre lang="json">{&#10;  "game_nr": "Integer"&#10;}</pre> |
| `GameFinished` | Das Kreuzworträtsel wurde erfolgreich beendet. | <pre lang="json">{&#10;  "game_nr": "Integer",&#10;  "timer": "Integer"&#10;}</pre> `timer` in Sekunden. |
| `RestartGame` | Das Kreuzworträtsel wurde zurückgesetzt und erneut begonnen. | <pre lang="json">{&#10;  "game_nr": "Integer",&#10;  "timer": "Integer"&#10;}</pre> `timer` = Zeitpunkt der Zurücksetzung in Sekunden. |
| `ShareResult` | Payload für das [Allgemeine Event](#allgemeine-events). | <pre lang="json">{&#10;  "game_nr": "Integer",&#10;  "errors": "Integer",&#10;  "seconds": "Integer"&#10;}</pre> |

### Events in einer Einbettung

Ist Ihre Publikation [per Iframe oder Script](./setup#iframe-script) eingebunden, endet ein Custom-Event nicht an der Grenze des Iframes.
Ihre Publikation reicht jedes der oben genannten Events an die umgebende Seite weiter, die darauf reagieren kann, wie sie möchte:
Werbung nachladen, das Layout anpassen, ein eigenes Angebot einblenden, die Paywall bedienen oder das Event an ein Analyse-System übergeben.

Die Nachricht trägt drei Properties:

| Property | Bedeutung |
|---|---|
| `source` | Immer `oliwol-publisher`. Daran erkennt Ihre Seite unsere Nachrichten. |
| `event` | Der Name des Events, etwa `PageView` oder `PaywallTriggered`. |
| `detail` | Der Payload des Events, unverändert aus den Tabellen oben. |

Auf Ihrer Seite nimmt ein `EventListener` die Nachricht entgegen:

```javascript
window.addEventListener('message', (event) => {
    if (event.origin !== 'https://sudoku.example.com') {
        return;
    }

    if (event.data?.source !== 'oliwol-publisher') {
        return;
    }

    console.log(event.data.event, event.data.detail);
}, false);
```

> [!WARNING]
> Ohne die Prüfung von `event.origin` nimmt der Listener jede Nachricht an, die auf Ihrer Seite gesendet wird, auch die fremder Skripte.
> Vergleichen Sie den Wert mit der Adresse Ihrer Publikation, wie im Beispiel oben.

Nutzt Ihre Seite bereits Listener auf die Custom-Events, etwa für Ihr Analyse-System, lassen sich die Nachrichten in dieselben Events übersetzen.
Ihre bestehenden Listener laufen dann unverändert weiter, unabhängig davon, ob die Publikation eingebettet ist:

```javascript
window.addEventListener('message', (event) => {
    if (event.origin !== 'https://sudoku.example.com') {
        return;
    }

    if (event.data?.source !== 'oliwol-publisher') {
        return;
    }

    window.dispatchEvent(new CustomEvent(event.data.event, {
        detail: event.data.detail,
    }));
}, false);
```

> [!INFO]
> Die Höhe des Iframes wird über denselben Weg übertragen.
> Sie erkennen diese Nachricht daran, dass sie eine Property `height` enthält und keine Property `source`.

---

## Virtuelle Seitenaufrufe

Da es sich bei allen Publikationen um *Single Page Applications (SPA)* handelt,
wird beim Wechseln der URL kein Seiten-Reload ausgelöst.
Einige Analyse-Systeme lauschen auf das `popstate`-Event und können das Navigieren innerhalb von SPAs tracken.

Alle Publikationen senden beim Wechseln der URL das Custom-Event `PageView`.
Im **Payload** werden die Properties `to` und `from` übergeben:
`to` liefert die Daten zur angesteuerten Seite, `from` enthält die Daten zur Ausgangs-URL.

```javascript
{
  to: {
    fullPath: "/schwierig",
    hash: "",
    href: "/schwierig",
    name: "Home",
    params: {
        level: "schwierig"
    },
    path: "/schwierig",
    query: {}
  },
  from: {
    fullPath: "/",
    hash: "",
    href: "/",
    name: "Home",
    params: {
        level: "leicht"
    },
    path: "/",
    query: {}
  }
}
```

Um die Daten beim Seitenwechsel an ein Analyse-System weiterzuleiten,
können Sie auf das Custom-Event `PageView` lauschen und den Payload übergeben.
Hierfür nutzen Sie ein Inline-Script und integrieren den `EventListener`.

### Virtuelle Seitenaufrufe mit GA4

*GA4* lauscht in der Standard-Konfiguration auf das `popstate`-Event –
daher müssen virtuelle Seitenaufrufe **nicht manuell übergeben** werden.

![GA4-Einstellung für erweiterte Analysen: Option zum automatischen Tracking von Seitenänderungen im Browser-Verlauf](/images/virtual-pageviews-ga-light.png)

Wenn Sie diese Option deaktivieren, können Seitenaufrufe wie folgt übergeben werden:

```javascript
window.addEventListener("PageView", (e) => {
    gtag("event", "page_view", {
        page_title: document.title,
        page_location: e.detail.to.fullPath
    })
});
```

### Virtuelle Seitenaufrufe mit Adobe Analytics

Für *Adobe Analytics* müssen Sie keinen `EventListener` im **oliwol Publisher Tool** integrieren.
Das Regelset für *Custom Events* integrieren Sie direkt in *Adobe Tags*.

### Virtuelle Seitenaufrufe mit IVW

```javascript
window.addEventListener("PageView", (e) => {
    IOMm("pageview", { cp: "[code]" });
});
```

### Weitere Anwendungsmöglichkeiten

Das Custom-Event `PageView` kann auch dazu genutzt werden, **Werbemittel zu aktualisieren**.
Nachfolgend ein Beispiel, wie Werbemittel beim Wechseln der Seite aktualisiert werden,
sofern es sich bei der Zielseite und der vorherigen Seite nicht um den Statistik-Layer handelt:

```javascript
window.addEventListener("PageView", (e) => {
    if (e.detail && e.detail?.to?.name !== "Stats" && e.detail?.from?.name !== "Stats") {
        if (typeof OBR !== "") {
            OBR.extern.refreshWidget();
        }
    }
});
```

---

## Paywall-Kontakte

Erreichen Nutzende einen Inhalt hinter der Paywall, wird das Custom-Event `PaywallTriggered` gesendet.
Das geschieht bei allen [Paywall-Varianten](./paywall#paywall-erstellen), also auch dann, wenn die Publikation die Paywall selbst anzeigt.
Bei der Variante **Individuell** ist es zugleich das Signal, das eigene Angebot einzublenden.

Der Payload beschreibt die Situation, die zur Paywall geführt hat:

| Property | Immer enthalten | Bedeutung |
|---|---|---|
| `state` | ja | Der Zustand, der die Paywall ausgelöst hat. |
| `trigger` | ja | Die Art des Auslösers: `page`, `content`, `navigation`, `feature` oder `archive`. |
| `path` | ja | Der Pfad, den Nutzende angesteuert haben. |
| `type` | – | Die Variante der Paywall: `internal`, `piano` oder `custom`. |
| `paywall` | – | Die Kennung der konfigurierten Paywall. |
| `page` | – | Der interne Name der betroffenen Seite. |
| `title` | – | Der Titel der betroffenen Seite. |
| `feature` | – | Der Schlüssel einer Funktion hinter der Paywall, etwa `dark_mode`. |
| `date` | – | Der Tag eines archivierten Rätsels im Format `JJJJ-MM-TT`. |

Die Auslöserarten im Einzelnen:

| `trigger` | Situation |
|---|---|
| `page` | Eine geschützte Seite wurde aufgerufen. |
| `content` | Ein geschützter Abschnitt innerhalb einer Seite wurde erreicht. |
| `navigation` | Ein geschützter Eintrag in der Navigation wurde angeklickt. |
| `feature` | Eine geschützte Funktion wurde benutzt. |
| `archive` | Ein archiviertes Rätsel oder eine größere Archivtiefe wurde angesteuert. |

> [!INFO]
> Properties, die auf die jeweilige Situation nicht zutreffen, fehlen im Payload.
> Prüfen Sie daher auf das Vorhandensein einer Property, nicht auf einen leeren Wert.

```javascript
window.addEventListener("PaywallTriggered", (event) => {
    const paywall = event.detail;

    if (paywall.trigger === "feature") {
        // Ein Angebot, das die Funktion hinter der Paywall benennt.
        console.log(paywall.feature);
    }
});
```

Der Payload enthält keine Angaben zur Person: weder eine Kennung noch den Anmeldestatus oder die Mitgliedschaft.
