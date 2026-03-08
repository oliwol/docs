# CMP

Mithilfe einer **Consent Management-Plattform** (CMP) können Sie DSGVO-konform die Daten Ihrer Besucher:innen schützen.
Das **oliwol Publisher Tool** enthält keine integrierte CMP-Lösung, liefert Ihnen aber alle Möglichkeiten, **gängige CMPs zu integrieren**.

---

## Integration von CMPs

Ähnlich wie bei der [Integration von Tracking-Systemen](./tracking) werden CMPs in der jeweiligen Publikation im Bereich „Scripts" über *External Scripts* eingebunden.
Mithilfe von *Inline Scripts* können CMPs oder auch Erweiterungen, wie beispielsweise sogenannte **PUR-Modelle**, konfiguriert werden.

Das Javascript wird im `<head>` der Seite integriert.
Jedes **Inline-Javascript** wird in einem eigenen `<script>`-Tag integriert, für den jeweils zusätzliche Attribute hinterlegt werden können.
Für externe Scripts gibt es diverse Einstellungsmöglichkeiten:

- **Source:** Das `src`-Attribut
- **Load method:** `sync`, `async`, `defer` oder `preload`
- **Position:** Auswahl, ob das Script vor oder nach den Inline-Scripts geladen werden soll
- **Attributes:** Möglichkeit, dem `<script>`-Tag weitere Attribute hinzuzufügen

### Link zum Öffnen des CMP-Layers

Damit Nutzer:innen jederzeit und von jeder Seite aus die Datenschutzeinstellungen einsehen, aufrufen und ändern können, gibt es die Möglichkeit, über einen `<script>`-Tag die Methode **zum Öffnen eines CMP-Layers** zu hinterlegen.

![Eingabefeld für den JavaScript-Aufruf zum Öffnen des CMP-Layers](/images/cmp-trigger-js-light.png "dark:/images/cmp-trigger-js-dark.png")

Sobald dieses Feld ausgefüllt wird, erscheint im Menü das Symbol für die Datenschutzeinstellungen.

![Datenschutz-Symbol im Menü der Publikation, über das der CMP-Layer geöffnet wird](/images/cmp-trigger-light.png "dark:/images/cmp-trigger-dark.png")

### Integration am Beispiel von *Sourcepoint*

Für die vollständige Integration der CMP-Lösung von *Sourcepoint* benötigen Sie einen Account und eine konfigurierte *Property*.
Die Integration beinhaltet drei Komponenten: Stub-Code, Ihre Konfiguration und die Messaging-Bibliothek.

> [!WARNING]
> Der Stub-Code dient nur als Beispiel. *Sourcepoint* weist in ihrer [Dokumentation](https://docs.sourcepoint.com/hc/en-us/articles/4405412395667-CMP-web-implementation) darauf hin, die im Portal generierte Stub-Datei zu implementieren, da sich der Code regelmäßig ändern kann.

```javascript
// Stub-Code
function _typeof(t){return(_typeof="function"==typeof Symbol&&"symbol"==typeof Symbol.iterator?function(t){return typeof t}:function(t){return t&&"function"==typeof Symbol&&t.constructor===Symbol&&t!==Symbol.prototype?"symbol":typeof t})(t)}!function(){var t=function(){var t,e,o=[],n=window,r=n;for(;r;){try{if(r.frames.__tcfapiLocator){t=r;break}}catch(t){}if(r===n.top)break;r=n.parent}t||(!function t(){var e=n.document,o=!!n.frames.__tcfapiLocator;if(!o)if(e.body){var r=e.createElement("iframe");r.style.cssText="display:none",r.name="__tcfapiLocator",e.body.appendChild(r)}else setTimeout(t,5);return!o}(),n.__tcfapi=function(){for(var t=arguments.length,n=new Array(t),r=0;r<t;r++)n[r]=arguments[r];if(!n.length)return o;"setGdprApplies"===n[0]?n.length>3&&2===parseInt(n[1],10)&&"boolean"==typeof n[3]&&(e=n[3],"function"==typeof n[2]&&n[2]("set",!0)):"ping"===n[0]?"function"==typeof n[2]&&n[2]({gdprApplies:e,cmpLoaded:!1,cmpStatus:"stub"}):o.push(n)},n.addEventListener("message",(function(t){var e="string"==typeof t.data,o={};if(e)try{o=JSON.parse(t.data)}catch(t){}else o=t.data;var n="object"===_typeof(o)?o.__tcfapiCall:null;n&&window.__tcfapi(n.command,n.version,(function(o,r){var a={__tcfapiReturn:{returnValue:o,success:r,callId:n.callId}};t&&t.source&&t.source.postMessage&&t.source.postMessage(e?JSON.stringify(a):a,"*")}),n.parameter)}),!1))};"undefined"!=typeof module?module.exports=t:t()}();

// Ihre Konfiguration
window._sp_queue = [];
window._sp_ = {
    config: {
        accountId: 1234,
        baseEndpoint: 'https://cdn.privacy-mgmt.com',
        isSPA: true,
        targetingParams: {
            acps: "false"
        },
    }
}
```

Diesen Code-Block können Sie in Ihrer Publikation als **internes Script** einbinden.
Idealerweise trennen Sie den Stub-Code von der Konfiguration auf zwei interne Script-Blöcke – dadurch bleibt Ihr Code übersichtlich und Sie können Ihre Konfiguration leichter anpassen.

![Inline-Scripts für Sourcepoint: Stub-Code und Konfiguration als separate Code-Blöcke](/images/cmp-js-sourcepoint-light.png "dark:/images/cmp-js-sourcepoint-dark.png")

Die letzte Komponente – die *Messaging-Bibliothek* – wird als asynchrones **externes Script** eingebunden und nach den *Inline-Scripts* positioniert.

![Externes Script für die Sourcepoint Messaging-Bibliothek mit async-Lademethode](/images/cmp-sourcepoint-library-light.png "dark:/images/cmp-sourcepoint-library-dark.png")

Damit sind alle drei initialen Komponenten für Sourcepoint implementiert.
Sofern Sie alles bereits im Portal von Sourcepoint konfiguriert haben, sollte beim Erstaufruf Ihrer Publikation der CMP-Layer erscheinen.

#### CMP-Layer manuell öffnen

Um den **Layer manuell per Link anzusteuern**, verwenden Sie beim Editieren Ihrer Publikation das Feld im Bereich *Scripts* unter *CMP-Trigger* und nutzen folgenden Code:

```javascript
window._sp_.loadPrivacyManagerModal([Privacy-Manager ID])
```

In Ihrer Publikation erscheint ein Link, der Nutzer:innen das **Öffnen ihrer Datenschutz-Einstellungen** ermöglicht.

#### Externe Ressourcen entsprechend Consent-Status laden

Sobald Sourcepoint integriert ist, können Sie auf das Event `__tcfapi` lauschen, um auf Änderungen des Consent-Status der Nutzer:innen zu reagieren und entsprechend externe Ressourcen zu laden.

```javascript
__tcfapi('addEventListener', 2, (tcdata, success) => {
    console.log(tcdata)

    if (success && tcdata.eventStatus === 'loaded') {
        // Inject scripts by vendor
    }
})
```

> [!INFO]
> Weitere Informationen zum `tcdata`-Objekt sowie zu den enthaltenen Properties finden Sie in der [API-Dokumentation](https://sourcepoint-public-api.readme.io/reference/tcdata-object) von *Sourcepoint*.