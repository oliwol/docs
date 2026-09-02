# Paywall

Sie haben die Möglichkeit, **Seiten oder Funktionen** Ihrer Publikation **nur für bestimmte Nutzer:innen** freizugeben.
Das *oliwol Publisher Tool* bietet dafür ein flexibles System aus **Zuständen** und **Paywalls**, das Sie unter *Authentifizierung* verwalten.

Voraussetzung ist eine aktive [SSO-Anbindung](./sso).

---

## Zustände

Unter *Authentifizierung* → *Zustände* definieren Sie **Authentifizierungszustände**, die Nutzer:innen anhand ihres [Payloads](./sso#zustand) zugeordnet werden.
Zustände sind vergleichbar mit **Mitgliedschaften oder Abonnements** — z. B. *Premium*, *Basis* oder *Testphase*.

Beim Anlegen eines Zustands wählen Sie zunächst die **Schnittstelle** aus, zu der der Zustand gehört.
Anschließend vergeben Sie einen **Namen** und definieren die **Bedingungen**: einen oder mehrere Werte, die im Payload unter dem konfigurierten [Zustands-Key](./sso#zustand) erwartet werden.

Stimmt ein Wert aus dem Payload mit einer der Bedingungen überein, wird der/die Nutzer:in dem jeweiligen **Zustand zugeordnet**.

### Paywall zuordnen

Optional können Sie einem Zustand eine **Paywall** zuordnen.
Wird einem/einer Nutzer:in der Zugriff auf eine Funktion oder Seite verwehrt, weil der erforderliche Zustand nicht vorliegt, wird die **zugeordnete Paywall** angezeigt.

Wird **keine Paywall** zugeordnet, wird stattdessen die in der [Schnittstelle](./sso#login) hinterlegte **Anmeldeseite** angezeigt.

---

## Paywall erstellen

Unter *Authentifizierung* → *Paywalls* erstellen Sie Ihre Paywall-Inhalte.
Es stehen drei Varianten zur Verfügung: ein **interner Editor**, die **Piano-Integration** und eine **individuelle Lösung**, bei der die Publikation die Anzeige vollständig Ihnen überlässt.

### Interner Editor

Mit dem internen Editor gestalten Sie Ihre Paywall direkt im *oliwol Publisher Tool*.
Folgende Felder stehen Ihnen zur Verfügung:

![Interner Paywall-Editor mit Feldern für Überschrift, Text, CTA-Button und Icon](/images/paywall-internal-editor-light.png "dark:/images/paywall-internal-editor-dark.png")

Unterhalb des Editors hinterlegen Sie die **Landingpage-URL**, auf die der CTA-Button verweist — z. B. ein Abo-Angebot oder eine Registrierungsseite.
Zusätzlich definieren Sie einen **Weiterleitungs-Parameter**, über den Sie Nutzer:innen nach Abschluss **zurück zur Publikation** leiten können.

```
https://abo.example.com/spiele?redirect=https://sudoku.example.com
```

![Ablauf der Paywall: Nutzer:in sieht CTA, wird zur Landingpage geleitet und anschließend zurück zur Publikation](/images/paywall-flow-light.png "dark:/images/paywall-flow-dark.png")

### Piano

Alternativ können Sie Ihre eigene **Piano-Integration** nutzen.
Bei dieser Variante wird die **Darstellung der Paywall vollständig über Piano** gesteuert — Texte, Farben, Angebote und Aktionen konfigurieren Sie direkt im [Piano Publisher Dashboard](https://dashboard.piano.io).

#### Konfiguration im oliwol Publisher Tool

Im *oliwol Publisher Tool* hinterlegen Sie die Verbindungsdaten zu Ihrer Piano-Instanz:

| Feld | Beschreibung |
|---|---|
| **SDK-URL** | Die URL zum Piano JavaScript SDK, das in die Publikation eingebunden wird. |
| **Application-ID (AID)** | Ihre Piano Application-ID zur Identifikation Ihrer Anwendung. |
| **Icon** | Ein SVG-Icon, das bei geschützten Inhalten in der Navigation angezeigt wird. |

Zusätzlich steht Ihnen ein Bereich für **Custom Code** zur Verfügung, in dem Sie eigenes **HTML**, **JavaScript** und **CSS** einbinden können, um die Piano-Integration individuell anzupassen.

#### Konfiguration in Piano

Das **Erscheinungsbild der Paywall** gestalten Sie im _Piano Publisher Dashboard_.
Dort erstellen Sie eine **Experience**, die das Layout, die Texte und die Aktionen (z. B. Abo-Angebot, Login) Ihrer Paywall definiert.
Die Gestaltung erfolgt im integrierten **Visual Composer**.

**Wann** die Paywall angezeigt wird, steuert das *oliwol Publisher Tool* über die [Zugriffsteuerung](#zugriffsteuerung) — Piano ist ausschließlich für die **Darstellung** zuständig.

Achten Sie darauf, dass die in Piano hinterlegten **URL-Muster mit den URLs Ihrer Publikation übereinstimmen**, damit die Experience korrekt ausgeliefert wird.

> [!INFO]
> Detaillierte Informationen zur Konfiguration finden Sie in der [Piano-Dokumentation](https://docs.piano.io).

### Individuell

Bei dieser Variante zeigt die Publikation **keine Paywall** an.
Sie erhalten stattdessen ein **Browser-Event** und bestimmen selbst, wie und an welcher Stelle Ihr Angebot erscheint.

Ruft ein(e) Nutzer:in einen Inhalt hinter der Paywall auf, geschieht Folgendes:

1. Der eigentliche Inhalt wird verschleiert und bleibt unlesbar.
2. Das Event [`PaywallTriggered`](./tracking#paywall-kontakte) wird ausgelöst.

```javascript
window.addEventListener('PaywallTriggered', (event) => {
    const paywall = event.detail;

    // paywall.state nennt den Zustand, der die Paywall ausgelöst hat.
    // paywall.trigger nennt die Art des Auslösers, etwa 'page' oder 'feature'.
    // paywall.type ist bei dieser Variante 'custom'.
});
```

Der Payload beschreibt die Situation, die zur Paywall geführt hat: die betroffene Seite, die benutzte Funktion oder den Tag eines archivierten Rätsels.
Eine vollständige Übersicht der Properties steht unter [Paywall-Kontakte](./tracking#paywall-kontakte).
Ist die Publikation eingebettet, erreicht Sie derselbe Payload zusätzlich per `postMessage`.

Inhalte hinterlegen Sie für diese Variante nicht, es genügt ein **Name** zur Unterscheidung.
Ein **Icon** lässt sich weiterhin hinterlegen, denn es kennzeichnet die betroffenen Seiten in der Navigation.
Ohne Icon steht dort das **Schlosssymbol**.

> [!INFO]
> `PaywallTriggered` wird bei allen drei Varianten ausgelöst und eignet sich damit auch zum Zählen von Paywall-Kontakten.
> Die Variante steht im Payload unter `type`, sodass sich eine eigene Anzeige auf `custom` beschränken lässt.

---

## Zugriffsteuerung

Nachdem Sie Zustände und Paywalls eingerichtet haben, können Sie den **Zugriff auf Funktionen und Seiten** Ihrer Publikation steuern.

![Zugriffsteuerung: Funktionen und Seiten können nach Zugangsstufe eingeschränkt werden](/images/feature-access-light.png "dark:/images/feature-access-dark.png")

### Funktionen

In der Konfiguration Ihrer Publikation lässt sich für jede Funktion (z. B. Archiv, Dark Mode, Drucken) eine **Zugangsstufe** festlegen:

| Zugangsstufe | Beschreibung |
|---|---|
| **Alle** | Die Funktion ist für alle Nutzer:innen verfügbar. |
| **Angemeldet** | Die Funktion ist nur für angemeldete Nutzer:innen verfügbar. |
| **Zustand** | Die Funktion ist nur für Nutzer:innen mit einem bestimmten Zustand verfügbar. |

Wird eine Funktion auf einen **bestimmten Zustand** eingeschränkt, wird bei Nutzer:innen ohne passenden Zustand die dem Zustand zugeordnete **Paywall** oder alternativ die Anmeldeseite angezeigt.

### Seiten

Auch **Seiten** Ihrer Publikation können mit Zugangsstufen versehen werden.
Die verfügbaren Optionen entsprechen denen der Funktionen: *Alle*, *Angemeldet* oder ein bestimmter *Zustand*.

Bei eingeschränkten Seiten erscheint in der Navigation das **Paywall-Icon**, um Nutzer:innen zu signalisieren, dass es sich um Premium-Inhalte handelt.

### Level

In bestimmten Rätseln (z. B. Sudoku) können auch einzelne **Level** hinter eine Paywall gesetzt werden.
Level werden wie Seiten behandelt und sind unter *Inhalte* → *Seiten* sichtbar.
Die Einschränkung funktioniert identisch: Wird ein geschütztes Level aufgerufen, erscheint die dem Zustand zugeordnete **Paywall**.
