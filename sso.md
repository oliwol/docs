# Schnittstelle

Das *oliwol Publisher Tool* bietet Ihnen die Möglichkeit, **ohne weiteren Entwicklungsaufwand Ihre SSO anzubinden**.
Spieldaten und Statistiken Ihrer Nutzer:innen können so **persistent gespeichert** werden.
Darüber hinaus ermöglicht die SSO-Anbindung, **erweiterte Spielfunktionen** oder Vorteile nur **für Abonnent:innen** freizugeben.

![Auswahl der Authentifizierungsmethode: Session, JWT oder Token](/images/sso-auth-method-light.png "dark:/images/sso-auth-method-dark.png")

Die **Anbindung einer bestehenden SSO** (Single Sign-On) an Ihre Publikation beginnt mit der Einrichtung eines **Identity Providers** unter dem Menüpunkt *Schnittstellen* im Bereich *Authentifizierung*.

---

## Authentifizierung

Sie können zwischen **drei Authentifizierungsmethoden** wählen: *Session*, *JWT* und *Token*.
Die Methoden *Session* und *Token* erwarten einen `2XX`-Statuscode für eine erfolgreiche Authentifizierung.
*JWT* validiert mithilfe des **Public Keys** den im Cookie hinterlegten **Token**.

### Session

Eine **Authentifizierung über eine Session** benötigt die Angabe einer **URL**, die via **XMLHttpRequest** (GET) angefragt wird.
Sobald die Anfrage einen **2XX-Statuscode zurückliefert**, findet eine Authentifizierung statt.

### JWT

Bei Verwendung der [JWT](https://jwt.io)-Methode hinterlegen Sie den **Namen des Cookies**, das den **Token** enthält.
Das Cookie darf **kein `httpOnly`-Flag** enthalten, da die Anwendung den Wert sonst nicht auslesen kann.
Zusätzlich muss der **Public Key** hinterlegt werden, um den Token zu **validieren**.

### Token

Bei der **Token-Variante** geben Sie sowohl eine **URL** als auch den **Namen des Cookies** an, das den Token enthält.
Ein **XMLHttpRequest** (GET) stellt zusammen mit dem **Autorisierungs-Token** eine Anfrage an die hinterlegte URL.
Wird diese mit einem **2XX-Statuscode** beantwortet, findet eine Authentifizierung statt.

Optional können Sie ein **Authentifizierungsschema** angeben, z. B. `Bearer`.
In diesem Fall wird der Token als `Authorization: Bearer <token>` im Header übermittelt.

```http
// GET <url>
Authorization: Bearer <token>
```

---

## Aktivierung der SSO

**Identity Provider** werden nicht innerhalb von Publikationen angelegt, sondern zentral unter *Authentifizierung* → *Schnittstellen*.
Dadurch können Sie eine konfigurierte SSO **mehrfach verwenden**.
Änderungen am Identity Provider wirken sich auf **alle verbundenen Publikationen** aus.

Innerhalb einer Publikation wählen Sie den gewünschten **Identity Provider** in der Bearbeitungsmaske in der rechten Spalte unter *Schnittstelle* aus.

![Dropdown zur Auswahl eines konfigurierten Identity Providers für die Publikation](/images/sso-select-provider-light.png "dark:/images/sso-select-provider-dark.png")

---

## Synchronisation

Die Spieldaten (Statistiken, letzte Spielergebnisse etc.) werden im `localStorage` des Browsers abgelegt.
Es findet somit nur eine **temporäre Speicherung** statt.
Wenn Nutzer:innen verschiedene Browser bzw. Geräte nutzen oder Browserdaten löschen, werden die Daten **nicht synchronisiert**.

Sobald Sie Ihre SSO anbinden, werden bei einer Authentifizierung die Daten **persistent gespeichert**.
Bei der **ersten Authentifizierung** wird im System **ein Datensatz pro Nutzer:in angelegt**.
Unter dem Menüpunkt *Spieler:innen* finden Sie **alle Nutzer:innen**, die eine oder mehrere Publikationen verwenden.

![Schnittstellen-Karte in der Publikationsübersicht mit Anzahl registrierter Spieler:innen: heute, diesen Monat und insgesamt](/images/sso-overview-light.png "dark:/images/sso-overview-dark.png")

### Payload

Um Daten von Nutzer:innen korrekt zuzuordnen sowie im Profil darzustellen, können Sie **Werte aus dem Payload extrahieren**.
Bei den Methoden *Session* und *Token* wird jeweils auf den **JSON-Response** zugegriffen, bei *JWT* wird der **Payload** des Tokens ausgelesen.
Verschachtelte Objekte im Payload trennen Sie mit einem Punkt (z. B.: `data.user.id`).

#### User-ID

Bei der User-ID handelt es sich um eine von Ihnen festgelegte, **eindeutige ID**, worüber Sie Nutzer:innen identifizieren.
Die Spieldaten und Statistiken werden der **ID zugeordnet**. Die **User-ID** ist ein **Pflichtfeld** und muss als **String** übergeben werden.

```json
// GET Response
{
    "auth": true,
    "user": {
        "id": "1234-5678-9000",
        "email": "muster@example.com",
        "name": "M. Muster"
    }
}
```

![Konfiguration der Payload-Keys für User-ID, E-Mail und Zustand aus dem SSO-Response](/images/sso-data-light.png "dark:/images/sso-data-dark.png")

Für den obigen Response können Sie die User-ID über den Key `user.id` extrahieren.

#### E-Mail

Die E-Mail-Adresse wird im **Profil der Spieler:innen angezeigt** und kann unter dem Menüpunkt *Spieler:innen* zur **Suche** genutzt werden.
Wenn Sie keinen Key für die E-Mail angeben, wird im Profil der Nutzer:innen *Anonym* ausgegeben.

> [!INFO]
> **E-Mail-Adressen** werden im Profil zum Schutz **maskiert**. Dennoch erkennen Nutzende, dass es sich um ihr Profil handelt. Adressen werden **ausschließlich für die Ausgabe** im Profil oder in der Spieler:innen-Liste genutzt und für **keinerlei Marketingzwecke** verwendet.

Damit die E-Mail-Adresse im Profil dargestellt werden kann, muss eine **Übergabe im JSON-Response** bzw. **JWT-Payload** stattfinden.
Der Wert muss als **String** übergeben werden.

```json
// JWT Payload
{
  "sub": "1234567890",
  "email": "muster@example.com",
  "iat": 1516239022
}
```

#### Zustand

Optional können Sie einen **Key für den Zustand** der Nutzer:innen angeben.
Zustände sind vergleichbar mit **Mitgliedschaften oder Abonnements**, die Nutzer:innen in Ihrem System besitzen — z. B. `premium`, `basic` oder `trial`.
Da die Werte unter *Authentifizierung* → *Zustände* gemappt werden, können auch **interne Bezeichnungen** verwendet werden.

Der Wert im Payload kann ein **String**, ein **Array** oder ein **Objekt** sein.

```json
// String
{ "membership": "premium" }

// Array
{ "membership": ["premium", "games"] }

// Objekt
{ "membership": { "type": "premium" } }
```

Der extrahierte Wert wird verwendet, um Nutzer:innen einem unter *Authentifizierung* → *Zustände* definierten **Authentifizierungszustand** zuzuordnen.
Über Zustände lässt sich der **Zugriff auf bestimmte Funktionen oder Inhalte** steuern.

Weitere Informationen finden Sie unter [Paywall](./paywall#zustände).

---

## Login

Beim Anlegen eines **Identity Providers** hinterlegen Sie die **URL zur Anmeldeseite** Ihrer SSO.

Zusätzlich geben Sie den **Namen des Parameters** an, über den Sie auf Ihrer Login-Seite die **Weiterleitungs-URL auslesen** können.
Der Parameter enthält als Wert die URL, auf die Sie die Nutzer:innen nach erfolgreichem Login **zurückleiten**.

Nach erfolgreichem Login landen Nutzende auf der URL, die im Parameter `redirect` angegeben ist:

```
https://sso.example.com/login?redirect=https://sudoku.example.com
```

### Login über iframe

Alternativ können Sie die **iframe-Variante für den Login** nutzen.
In diesem Fall öffnet sich beim Login ein **Layer mit iframe**, das die Login-URL lädt.
Sie können den Layer in **Breite und Höhe** (in Pixeln) anpassen.

#### iframe-Aktionen

Die Publikation kann auf `postMessage`-Events reagieren, die von der **im iframe geladenen Anmeldeseite** gesendet werden.
Dafür stehen drei Aktionen zur Verfügung:

| Aktion | Beschreibung |
|---|---|
| **Reload** | Lädt die Publikation neu — z. B. nach erfolgreichem Login. |
| **Close** | Schließt den iframe-Layer. |
| **Resize** | Passt die Höhe des iframes dynamisch an. |

Beim Anlegen einer Aktion definieren Sie ein **Key-Value-Pair**, das im Payload des `postMessage`-Events erwartet wird.
Enthält der Payload das definierte Key-Value-Pair, wird die jeweilige Aktion **ausgeführt**.

![Konfiguration einer iframe-Aktion mit Key-Value-Pair, Nachricht und Anzeigedauer](/images/sso-iframe-action-light.png "dark:/images/sso-iframe-action-dark.png")

Optional können Sie eine **Nachricht** hinterlegen, die nach Ausführung der Aktion angezeigt wird, sowie die **Dauer** (in Sekunden), wie lange die Nachricht sichtbar bleibt.

Auf Ihrer Anmeldeseite integrieren Sie die `postMessage`-Events wie folgt:

```javascript
// Reload nach erfolgreichem Login auslösen
window.parent.postMessage({
    "action": "loggedIn"
});
```

```javascript
// Höhe des iframes an den Inhalt anpassen
window.parent.postMessage({
    "height": document.body.scrollHeight
});
```
