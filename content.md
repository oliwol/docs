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

### Gestaltung der Antwort

Neben Überschriften, Listen und Links bietet der Editor einige Mittel, die eine längere Antwort gliedern:

- **Hervorheben** tönt einen Satz in der Farbe Ihrer Publikation, etwa den Kernsatz eines Beispiels.
- **Zitat** erscheint als getönter Hinweiskasten. Beginnt er fett, etwa mit „Kurz gesagt“, steht dieser Anfang auf einer eigenen Zeile.
- **Aufklapper** verbergen eine Vertiefung hinter einer Frage, die Nutzer:innen bei Bedarf aufklappen, etwa „Warum ist das sicher?“.
- **Raster** stellt Inhalte nebeneinander, zum Beispiel zwei Varianten zum Vergleich. Auf dem Handy stehen die Spalten untereinander.
- **Nummerierte Listen** erscheinen als Schritte mit Ziffern in Kreisen und eignen sich für Anleitungen.

### Abbildung mit Legende

Für Diagramme gibt es unter den Blöcken die **Abbildung mit Legende**. Sie besteht aus:

- dem **Bild**, im Format WebP, PNG oder JPEG
- einem **Alternativtext**, der beschreibt, was das Bild zeigt
- einer **Legende** mit bis zu sechs Einträgen
- einer **Bildunterschrift**

Jeder Eintrag der Legende hat ein **Symbol**, eine **Farbe** und einen Text. Zur Wahl stehen Rahmen (gestrichelt oder durchgezogen), Kreis, Streichung, Balken, Linie (durchgezogen oder gestrichelt) und Fläche. Kreis und Streichung zeigen zusätzlich ein Zeichen, etwa eine Ziffer. Als Farbe wählen Sie **Akzent**, die Farbe Ihrer Publikation, oder **Signal** (Rot), etwa für Gestrichenes.

In der Publikation steht die Legende neben dem Bild, wenn genug Platz ist, auf dem Handy darunter. Die Bildunterschrift folgt darunter.

> [!INFO]
> Legende und Bildunterschrift gehören nicht ins Bild, sondern in die Abbildung. Als Text bleiben sie in jeder Größe lesbar, auch im Dunkelmodus, für Screenreader und für Suchmaschinen. Verwenden Sie im Bild dieselbe Akzentfarbe wie in Ihrer Publikation, damit Bild und Legende zusammenpassen.

### Entwurf und Veröffentlichen

Eine neue FAQ ist zunächst ein **Entwurf**. Entwürfe erscheinen nicht in Ihrer Publikation, Sie können sie in Ruhe ausarbeiten. Erst wenn Sie eine FAQ **veröffentlichen**, steht sie auf der Hilfe-Seite. Sie können eine veröffentlichte FAQ jederzeit wieder zum Entwurf machen, dann verschwindet sie aus der Publikation.

> [!NOTE]
> Wie jede Änderung erscheint eine veröffentlichte FAQ zuerst mit der nächsten Version im [Testmodus](./setup#test). Ist Ihre Publikation live, gelangt sie mit der nächsten [Synchronisation](./setup#nicht-synchronisiert) dorthin.

### Kategorien

Mit **Kategorien** gliedern Sie die Hilfe-Seite in Abschnitte, etwa „Spielregeln“ oder „Konto“. Die Kategorien legen Sie für jede Publikation selbst an und bringen sie in die gewünschte Reihenfolge.

Auf der Hilfe-Seite erscheint jede Kategorie als **Zwischenüberschrift** mit ihren FAQs darunter. FAQs ohne Kategorie stehen ganz oben, ohne eigene Überschrift. Solange Sie keine Kategorien verwenden, bleibt die Hilfe-Seite eine einfache Liste.

Eine Kategorie lässt sich direkt verlinken: `/hilfe#konto` führt zur Kategorie „Konto“. Wird eine Kategorie gelöscht, bleiben ihre FAQs erhalten und stehen danach ohne Kategorie oben.

### Adresse einer FAQ

Jede FAQ hat einen **Slug**, der aus der Frage entsteht und den Sie anpassen können. Über ihn ist die FAQ direkt erreichbar:

- `/hilfe#q-{slug}` öffnet die Hilfe-Seite und klappt die Frage auf, zum Beispiel `/hilfe#q-abo-kuendigen`
- `/hilfe/{slug}` führt zur eigenen Seite der FAQ, wenn sie [als eigene Seite](#faq-als-eigene-seite) veröffentlicht ist

Ältere Links mit einer Nummer, etwa `/hilfe#q-3`, öffnen weiterhin die FAQ an dieser Position.

> [!WARNING]
> Ändern Sie den Slug einer FAQ, funktionieren Links **von außen** auf die bisherige Adresse nicht mehr, etwa aus einem Newsletter oder von Ihrer Website. Interne Links innerhalb Ihrer Publikation passen sich dagegen von selbst an.

### Interne Links

In der Antwort einer FAQ und im Inhalt Ihrer [Seiten](#seiten) können Sie auf **andere FAQs und Seiten Ihrer Publikation** verlinken, ohne deren Adresse zu kennen. Sie wählen das Ziel einfach aus einer Liste aus.

- Zur Auswahl stehen veröffentlichte FAQs und aktive Seiten. Bei Seiten, die nur Angemeldete oder bestimmte Nutzer:innen sehen, ist das in der Auswahl vermerkt.
- Ein Link auf eine FAQ führt zu ihrer eigenen Seite oder, ohne eigene Seite, zur Hilfe-Seite mit aufgeklappter Frage.
- Interne Links öffnen sich ohne Neuladen innerhalb der Publikation, auch wenn sie [eingebettet](./setup#iframe-script) ist.
- Ändert sich die Adresse des Ziels, stimmt der Link automatisch wieder.
- Wird das Ziel gelöscht, deaktiviert oder wieder zum Entwurf, bleibt an der Stelle der Text stehen, ohne Link.

### FAQ als eigene Seite

Eine FAQ kann optional als **eigene Seite** veröffentlicht werden. In der Hilfe-Seite erscheint dann nur der Anfang der Antwort mit einem Link auf die vollständige Seite.

Dabei werden folgende Felder verfügbar:

- **Button-Label**: der Text des Links, über den Nutzer:innen von der Hilfe-Seite zur FAQ-Seite gelangen
- **SEO-Einstellungen**: Titel und Beschreibung für Suchmaschinen

> [!INFO]
> FAQ-Seiten eignen sich besonders für ausführliche Antworten, die den Rahmen der Hilfe-Seite sprengen würden, und können gezielt für Suchmaschinen optimiert werden.

Eine FAQ-Seite ist auf ruhiges Lesen ausgelegt: linksbündiger Text in einer gut lesbaren Zeilenlänge. Einiges ergänzt die Publikation dabei von selbst:

- **Kategorie und Lesezeit** stehen unter der Frage. Die Kategorie führt zu ihrem Abschnitt auf der Hilfe-Seite.
- **Vorspann:** Der erste Absatz der Antwort erscheint größer, wenn danach noch ein Absatz folgt. Es ist derselbe Text, der auf der Hilfe-Seite vor dem Link zur FAQ-Seite steht.
- **Inhaltsverzeichnis:** Ab drei Zwischenüberschriften erscheint ein Verzeichnis „Auf dieser Seite“. Auf breiten Bildschirmen steht es neben dem Text und zeigt, welcher Abschnitt gerade gelesen wird, sonst lässt es sich unter dem Vorspann aufklappen. Jede Zwischenüberschrift ist direkt verlinkbar, zum Beispiel `/hilfe/{slug}#beispiel`.
- **Mehr zu {Kategorie}:** Am Ende stehen bis zu drei weitere FAQs derselben Kategorie und ein Link zu allen Fragen.
