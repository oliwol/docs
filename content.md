# Inhalte

In der Bearbeitungsmaske einer Publikation verwalten Sie über den Tab _Inhalte_ die **Seiten und die Ansprache** Ihrer Publikation.
Über den Bereich **FAQs** können Sie ergänzend **häufig gestellte Fragen** anlegen, die auf der Hilfe-Seite angezeigt werden.

---

## Ansprache

Über die Ansprache legen Sie fest, ob Ihre Nutzer:innen **geduzt** oder **gesiezt** werden.
Diese Einstellung wirkt sich auf **alle systemgenerierten Texte** innerhalb Ihrer Publikation aus.

![Auswahl der Ansprache: Duzen oder Siezen für alle systemgenerierten Texte](/images/speech-light.png "dark:/images/speech-dark.png")

---

## Seiten

Jede Publikation verfügt über eine Reihe von **Seiten**, die je nach Rätsel und angebundener [Authentifizierungs-Schnittstelle](./sso) variieren können.
Je nach Seitentyp stehen unterschiedliche Einstellungen zur Verfügung.

![Bearbeitungsmaske einer Seite mit Menütitel, SEO-Einstellungen und Texteditor](/images/pages-light.png "dark:/images/pages-dark.png")

### Menütitel

Jede Seite hat einen **Menütitel**, der in der Navigation Ihrer Publikation angezeigt wird.
Sie können den Menütitel jederzeit anpassen.

### Zugangsbeschränkung

Für jede Seite können Sie festlegen, ob sie **freigegeben** oder **gesperrt** ist. Gesperrte Seiten werden nicht angezeigt und können nicht aufgerufen werden.

Ist eine [SSO](./sso) angebunden, stehen zusätzliche Optionen zur Verfügung:

- **Alle** — die Seite ist für alle Nutzer:innen zugänglich
- **Angemeldet** — nur eingeloggte Nutzer:innen haben Zugriff
- **Bestimmter Status** — nur Nutzer:innen mit einem bestimmten Status (z. B. Abonnent:innen) haben Zugriff

> [!INFO]
> Nicht alle Seiten können gesperrt werden. Die Startseite ist beispielsweise immer aktiv.

### Externer Link

Einige Seiten können als **externer Link** konfiguriert werden. In diesem Fall wird der Menüeintrag nicht auf eine Unterseite Ihrer Publikation verweisen, sondern auf eine **externe URL**.

### Texte

Für Seiten, die eigene Inhalte unterstützen, steht ein **Rich-Text-Editor** zur Verfügung.
Damit können Sie Texte mit **Formatierungen**, **Überschriften**, **Listen**, **Links**, **Bildern** und weiteren Elementen gestalten.

Je nach Seitentyp hat der Inhalt eine unterschiedliche Bedeutung:

- **Startseite** — der Text erscheint in einem Layer, der das Spielprinzip erklärt (siehe [Layer der Startseite](#layer-der-startseite))
- **Hilfe-Seite** — der Inhalt dient als Einleitung vor den [FAQs](#faqs)
- **Login / Registrierung** — der Inhalt wird über dem jeweiligen Formular dargestellt
- **Impressum / Datenschutz** — der Inhalt bildet die rechtlichen Texte

### Layer der Startseite

Der Text der Startseite heißt im Editor **Layer**. Er erscheint nicht auf der Seite selbst, sondern in einem Fenster über dem Rätsel:

- **automatisch**, solange Nutzer:innen noch kein Rätsel gespielt haben und nicht angemeldet sind
- **auf Wunsch** über das Hilfe-Symbol im Kopf der Publikation, sofern Sie keine [FAQs](#faqs) angelegt haben – mit FAQs führt das Symbol zur Hilfe-Seite

Ist kein Text hinterlegt, öffnet sich kein Layer. Unter dem Text ergänzt die Publikation automatisch eine kurze Übersicht der Vorteile (etwa Archiv und Spielstand-Speicher) und den Button *Start*.

Welche Seite die Startseite ist, hängt vom Rätsel ab. Bei **Sudoku** ist es die Schwierigkeitsstufe **Leicht**: Dort pflegen Sie den Layer.

### SEO

Für jede aktive Seite können **SEO-Einstellungen** vorgenommen werden:

- **SEO-Titel** — der Titel, der in Suchmaschinen angezeigt wird
- **Beschreibung** — die Meta-Beschreibung für Suchmaschinen
- **Index** — legt fest, ob die Seite von Suchmaschinen indexiert werden soll
- **Follow** — legt fest, ob Suchmaschinen den Links auf der Seite folgen sollen

Weitere Informationen finden Sie unter [SEO](./seo).

---

## FAQs

FAQs werden auf der **Hilfe-Seite** Ihrer Publikation angezeigt. Sie können beliebig viele FAQs anlegen, bearbeiten und per **Drag & Drop** sortieren.

### FAQ erstellen

Jede FAQ besteht aus einer **Frage** und einer **Antwort**. Die Antwort wird über einen **Rich-Text-Editor** verfasst und kann Formatierungen, Links und Bilder enthalten.

### FAQ als eigene Seite

Eine FAQ kann optional als **eigene Seite** veröffentlicht werden. Aktivieren Sie dazu die Option _Als Seite anzeigen_.

Dabei werden folgende Felder verfügbar:

- **Slug** — die URL, unter der die FAQ-Seite erreichbar ist (wird automatisch aus der Frage generiert)
- **Button-Label** — der Text des Links, über den Nutzer:innen von der Hilfe-Seite zur FAQ-Seite gelangen
- **SEO-Einstellungen** — Titel und Beschreibung für Suchmaschinen

> [!INFO]
> FAQ-Seiten eignen sich besonders für ausführliche Antworten, die den Rahmen der Hilfe-Seite sprengen würden, und können gezielt für Suchmaschinen optimiert werden.
