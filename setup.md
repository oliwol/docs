# Einrichtung

## Voraussetzungen

Für die Installation einer Publikation benötigen Sie einen [Account](/preise) im oliwol Publisher Tool.
Wenn Sie eine eigene Domain nutzen möchten, sollten Sie über die technischen Möglichkeiten verfügen, die **DNS-Konfiguration** bei Ihrem Provider anzupassen.

---

## Publikation erstellen

Über das **Onboarding** auf dem Dashboard können Sie Ihre erste Publikation erstellen. 

![Onboarding-Assistent auf dem Dashboard zum Erstellen einer neuen Publikation](/images/onboarding-light.png "dark:/images/onboarding-dark.png")

Vergeben Sie im Formular einen **Titel** für Ihre Publikation und **wählen Sie ein Rätsel** aus.

Sobald Sie eine Publikation anlegen, wird automatisch eine **Cloud-Domain** eingerichtet, unter der Ihre Publikation als [Testumgebung](#cloud-domain) erreichbar ist.
**Bevor** Sie diese für Ihre Nutzer:innen **frei zugänglich** machen, können Sie Ihre Systeme anbinden und **alle Änderungen testen**.
Für den produktiven Einsatz können Sie zusätzlich eine [eigene Domain](#eigene-domain) hinterlegen.

Zu Beginn befindet sich Ihre Publikation im **Offline-Modus**.
Über ein Deployment können Sie in die Entwicklungsumgebung wechseln.
Hierfür ist es erforderlich, dass Sie die **Installation der Rätsel abgeschlossen** haben.

### Rätsel installieren

Bevor Sie die **täglichen Rätsel** für Ihr Spiel **installieren**, sollten Sie die [Spiel-Einstellungen](./configuration#spieleinstellungen) überprüfen.
Sobald die Rätsel installiert sind, lassen sich einige Einstellungen, beispielsweise das Punktesystem eines Spiels, im **laufenden Betrieb nicht mehr anpassen**.
Im **Offline-Modus** lassen sich **alle Einstellungen anpassen** und eine **Neuinstallation der Rätsel** anstoßen.

Nachdem Sie die **Konfiguration überprüft** haben, können Sie mit der **Installation der Rätsel** beginnen.

![Publikationsübersicht mit der Aktion zum Installieren der Rätsel](/images/canvas-install-puzzles-light.png "dark:/images/canvas-install-puzzles-dark.png")

Die **Installation** kann einige Minuten in Anspruch nehmen. Sie werden benachrichtigt, sobald diese abgeschlossen ist.

Nach erfolgreicher Installation können Sie erstmals Ihre Publikation in der [Entwicklungsumgebung](#entwicklung) bereitstellen.
Wenn sowohl die Installation als auch die Bereitstellung abgeschlossen sind, können Sie Ihre Publikation unter der eingerichteten **Cloud-Domain aufrufen**.

---

## Bereitstellung

Die Bereitstellung begleitet Sie auf dem Weg vom **Offline-Modus** bis hin zum **produktiven Einsatz** Ihrer Publikation.
Dieser Weg beinhaltet **5 Entwicklungsstufen**:

- Offline
- Entwicklung
- Test
- Nicht synchronisiert
- Live

![Bereitstellungsübersicht mit den Entwicklungsstufen von Offline bis Live](/images/deployment-dev-light.png "dark:/images/deployment-dev-dark.png")

Für die Stufen _Entwicklung_, _Test_ und _Live_ sind jeweils **Bereitstellungen notwendig**. Jede Entwicklungsstufe hat **Auswirkungen** auf Ihre Publikation.
Um Ihre Publikation für eine Stufe bereitzustellen, müssen gewisse **Voraussetzungen erfüllt** werden.

Bevor Sie die Bereitstellung starten, werden Ihnen die **Voraussetzungen** und **ob Sie diese erfüllen** angezeigt.
Daneben sehen Sie die Auswirkungen, die die jeweilige Bereitstellung mit sich bringt.

### Offline

Eine neu erstellte Publikation befindet sich **zu Beginn** im Offline-Modus.
Die Publikation ist **nicht aufrufbar**. Die Testdomain liefert einen **403 Status-Code** zurück.

### Entwicklung

Sobald sich die Publikation in der Entwicklung befindet, können Sie diese unter der Testdomain aufrufen.
Die Testumgebung ist für Suchmaschinen nicht sichtbar (`noindex, nofollow`).

**Voraussetzungen für eine Bereitstellung:**

- Rätsel sind installiert
- Es findet keine Bereitstellung statt
- Ihre Publikation ist offline

Im Entwicklungs-Modus sind **keine Caches und kein Service-Worker** aktiv.
Innerhalb der Konsole der Browser-DevTools werden Debug-Meldungen ausgegeben, darunter auch die aktuellen **Daten Ihrer Publikation**.
Dieser Modus eignet sich vor allem für den **Aufbau einer Publikation** (Layout, Inhalte, Anbindung der SSO und Paywall, etc.).

### Test

Der Testmodus **simuliert die produktive Umgebung**.
Sobald Sie Änderungen an Ihrer Publikation vornehmen, können Sie diese auf der Testdomain **unter Produktivbedingungen überprüfen**.
Im Testmodus ist der **Service-Worker aktiv**, wodurch sämtliche Assets und Rätsel im Browser abgespeichert werden.

**Voraussetzungen für eine Bereitstellung:**

- Rätsel sind installiert
- Es findet keine Bereitstellung statt
- Ihre Publikation befindet sich im [Entwicklungs-Modus](#entwicklung)

Publikationen können **jederzeit aktualisiert** werden. Nachdem Sie Änderungen vorgenommen und gespeichert haben, wird eine **neue Version erstellt**, die innerhalb weniger Minuten auf Ihrer Testdomain **automatisch publiziert** wird. Sie werden informiert, sobald die neue Version publiziert ist.

Beim Hinzufügen oder Ändern von [FAQs](./content#faqs) sowie einer verknüpften [SSO](./sso) oder [Paywall](./paywall) wird ebenfalls eine **neue Version** erstellt.

### Nicht synchronisiert

Sobald Ihre Publikation sich im Livemodus befindet, werden künftige Änderungen zunächst **automatisiert im Testmodus publiziert**.
Dadurch sind der Live- und Testmodus **nicht synchron**.
Um beide Umgebungen zu synchronisieren und Ihre Änderungen produktiv zu stellen, müssen Sie eine **Synchronisation** durchführen.

### Live

Ihre Publikation ist **online** und somit für jede Person **frei zugänglich**.

**Voraussetzungen für eine Bereitstellung:**

- [Eigene Domain](#eigene-domain) mit erfolgreich verifizierter DNS-Konfiguration
- Rätsel sind installiert
- Es findet keine Bereitstellung statt
- Ihre Publikation befindet sich im [Testmodus](#test) bzw. ist nicht synchronisiert
- Sie haben mindestens 1 freies Kontingent an Publikationen

---

## Rollback

Sie haben jederzeit die Möglichkeit, eine **Bereitstellung rückgängig** zu machen.
Um eine Publikation offline zu nehmen, müssen Sie, wie bei einer [Bereitstellung](#bereitstellung), jede Umgebung **nacheinander zurücksetzen**.

![Rollback-Dialog zum schrittweisen Zurücksetzen einer Publikation](/images/rollback-light.png "dark:/images/rollback-dark.png")

Sie können eine produktive Umgebung nicht direkt in den Offline-Modus versetzen.
Ein Rollback ist dann sinnvoll, wenn Sie Ihre Publikation generell **deaktivieren** möchten oder Sie die **Spiel-Konfiguration anpassen** wollen.

---

## Integration

Jede Publikation läuft auf einer eigenen [Domain](#domains). Sie können die Publikation **direkt** unter dieser Domain nutzen oder über einen **Iframe bzw. ein Script** in eine bestehende Seite einbinden.

### Direkte Nutzung

Bei der direkten Nutzung wird Ihre Publikation über die **verknüpfte Domain ausgespielt**.
Da es sich um eine eigenständige Seite handelt, empfiehlt es sich, weitere Anpassungen vorzunehmen.
Laden Sie Ihr **Logo** als SVG-Format hoch und wählen Sie Ihre **Markenfarbe** aus.

> [!INFO]
> Weitere Informationen zum Logo und dem Design im Allgemeinen finden Sie im Abschnitt [Layout](./layout).

Aus datenschutzrelevanten Gründen sollte neben dem [Impressum und den Datenschutzrichtlinien](./legal) auch eine [Consent Management Plattform](./cmp) angebunden werden.

Der entscheidende **Vorteil** dieser Integration ist das **Erlebnis** für Ihre Nutzer:innen.
Es steht einzig das **Spiel im Vordergrund** – ohne zu scrollen oder anderweitig abgelenkt zu werden.
Ihre Publikation ist auch **offline** oder bei sehr **schlechtem Netz** jederzeit erreichbar.
Zusätzlich können alle [Werbeplätze](./marketing) um das Spiel herum bestückt werden.

### Iframe & Script

Wenn Sie Ihre Publikation in eine bereits **bestehende Seite einbinden** möchten, können Sie dies via Iframe oder Script tun.
Den **Embed-Code** finden Sie in der Publikationsübersicht über das **Kontextmenü** (drei Punkte oben rechts) Ihrer Publikation.

Von dort können Sie den Integrations-Code in die Zwischenablage kopieren und auf Ihrer Seite an die **gewünschte Stelle einfügen**.

Sie können die **Breite** und den **CSS-Code** des Iframes auf Ihre Bedürfnisse **anpassen**.
Die **Höhe** wird über ein `postMessage`-Event gesteuert und passt sich an den Inhalt Ihrer Publikation an.

> [!INFO]
> Bei der Integration über Iframe oder Script wird **kein Logo** innerhalb der Publikation ausgespielt.

Die **Integration via Script** funktioniert auf dieselbe Art. Auch hierbei können **Breite und CSS angepasst** werden.
Die Script-Variante ist speziell bei der **Nutzung von Javascript-Frameworks**, wie React oder Vue, eine empfohlene Alternative.

```javascript
const puzzle = (node) => {
    const iframe = document.createElement('iframe');

    iframe.setAttribute('width', '450');
    iframe.setAttribute('src', 'https://sudoku.example.com');
    iframe.setAttribute('title', 'Sudoku');
    iframe.setAttribute('height', '720');
    iframe.style.border = '1px solid #e5e7eb';
    iframe.style.display = 'block';
    iframe.style.overflow = 'hidden';
    iframe.style.marginLeft = 'auto';
    iframe.style.marginRight = 'auto';
    iframe.onload = () => {
        window.addEventListener('message', function(e) {
            if (e.origin !== 'https://sudoku.example.com') {
                return;
            }

            const message = e.data;

            if (typeof message.height === 'number') {
                iframe.style.height = message.height + 'px';
            }
        }, false)
    };

    node.after(iframe);
}

puzzle(document.getElementById('sudoku-wrapper'));
```

---

## Domains

Jede Publikation benötigt mindestens eine Domain, um erreichbar zu sein. Das oliwol Publisher Tool unterscheidet zwischen **Cloud-Domains** und **eigenen Domains**.

### Cloud-Domain

Beim Anlegen einer Publikation wird **automatisch eine Cloud-Domain** erstellt. Hierbei handelt es sich um eine **Subdomain** unter der Domain des oliwol Publisher Tools.

Die Cloud-Domain ist **sofort einsatzbereit** — eine DNS-Konfiguration ist nicht erforderlich. Sie dient als **Testumgebung** und kann in der Übersicht Ihrer Publikationen auf der Karte _Domains_ eingesehen werden.

### Eigene Domain

Für den **produktiven Einsatz** können Sie eine eigene Domain hinterlegen. Navigieren Sie hierfür zur **Domain-Verwaltung** Ihrer Publikation und legen Sie eine neue Domain an.

![Domain-Verwaltung mit Cloud-Domain und eigener Domain inkl. Verifizierungsstatus](/images/domain-list-light.png "dark:/images/domain-list-dark.png")

Nach dem Anlegen einer eigenen Domain zeigt Ihnen das System die **erforderlichen DNS-Records** an, die Sie bei Ihrem DNS-Provider einrichten müssen. Je nach Konfiguration können dies Records vom Typ **A**, **AAAA**, **CNAME** oder **TXT** sein.

> [!INFO]
> Eigene Domains sind ab dem Paket **Starter** verfügbar.

**So richten Sie eine eigene Domain ein:**

1. Legen Sie die Domain in der **Domain-Verwaltung** Ihrer Publikation an
2. Übernehmen Sie die **angezeigten DNS-Records** in die DNS-Einstellungen Ihres Providers
3. Das System **prüft automatisch**, ob die DNS-Konfiguration korrekt hinterlegt ist
4. Bei erfolgreicher Überprüfung wechselt der Status auf **Verbunden**

> [!INFO]
> Es kann einige Stunden dauern, bis Ihre DNS-Einstellungen sichtbar sind.
> Sollte eine Überprüfung nach mehr als 48 Stunden fehlschlagen, kann dies auf eine falsche Konfiguration zurückzuführen sein.

#### WWW-Redirect

Beim Anlegen einer eigenen Domain können Sie festlegen, wie mit der **WWW-Variante** Ihrer Domain umgegangen werden soll:

- **Root → WWW:** Leitet `example.com` auf `www.example.com` weiter
- **WWW → Root:** Leitet `www.example.com` auf `example.com` weiter
- **Kein Redirect:** Beide Varianten werden nicht weitergeleitet

#### Status einer Domain

Eigene Domains durchlaufen nach dem Anlegen einen **Verifizierungsprozess**:

- **Ausstehend** — Domain wurde angelegt, DNS-Records müssen eingerichtet werden
- **Verifizierung** — DNS-Records werden geprüft
- **Verbunden** — DNS-Konfiguration ist korrekt, die Domain ist aktiv
- **Fehlgeschlagen** — DNS-Konfiguration konnte nicht verifiziert werden

#### SSL-Zertifikat

Für jede Domain wird automatisch ein **SSL-Zertifikat** bereitgestellt. Ein manueller Schritt ist hierfür nicht erforderlich.
