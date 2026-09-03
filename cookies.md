# Cookies

Zur Konfiguration einer [CMP](./cmp) werden nachfolgend alle **Daten aufgelistet**, die die Rätsel im Browser ablegen.
Es gibt 4 Kategorien: Notwendig, Präferenzen, Statistiken und Marketing.
Die Rätsel nutzen **ausschließlich notwendige** Einträge und Einträge für **Präferenzen**.

> [!INFO]
> Zum Einsatz kommen HTTP Cookies, HTML Local Storage, Session Storage, IndexedDB und der Zwischenspeicher der App. Zusammengefasst werden sie in diesem Abschnitt als *Cookies* bezeichnet.

Eine CMP-Lösung erfasst in der Regel nur HTTP Cookies und den HTML Local Storage.
Session Storage, IndexedDB und der Zwischenspeicher bleiben davon unberührt. Sie sind hier dennoch vollständig aufgeführt, da sie für eine Datenschutzerklärung relevant sind.

---

## Namensschema

Einträge werden nach folgendem Muster benannt: `[product identifier]-[bereich]-[name]`.
Ein Präferenz-Eintrag für die Einstellung des Dark-Modes unter Sudoku lautet `sdk-pref-darkmode`.

Die Product Identifier lauten wie folgt:

| Produkt | Identifier |
|---|---|
| Worteck | `wrdl` |
| Sudoku | `sdk` |
| Wortwabe | `wrtwb` |
| Kreuzworträtsel | `xwrt` |
| Kinonym | `knnym` |

Als Bereich kommen `user`, `pref` und `storage` vor.
Einige Einträge weichen vom Muster ab: `[product identifier]-token`, `[product identifier]-rank-shown`, `[product identifier]-record-shown` und `[product identifier]-streak-shown` tragen keinen Bereich. Der Eintrag `supporter:checkout` trägt keinen Identifier.

---

## Notwendige Einträge

Notwendige Einträge sind Voraussetzung für den Betrieb der Rätsel.
Werden sie unterdrückt oder gelöscht, gehen Spielstände und Statistiken der Nutzer:innen verloren, wodurch die **Spiele nicht nutzbar** sind.

Die Spalte *Gilt für* nennt die Rätsel, in denen ein Eintrag vorkommt, und die Bedingung, unter der er entsteht.

| Eintrag | Beschreibung | Typ | Gilt für | Ablauf | Bei Löschung |
|---|---|---|---|---|---|
| `[product identifier]-user-stats` | Speichert die Statistiken der Nutzer:innen | HTML Local Storage | Alle | Persistent, bleibt auch nach dem Abmelden | Alle Statistiken gehen verloren |
| `[product identifier]-user-games` | Speichert die Eingaben der Nutzer:innen zu den täglichen Rätseln | HTML Local Storage | Alle | Persistent, bleibt auch nach dem Abmelden | Alle Spielstände gehen verloren |
| `[product identifier]-storage-uploaded` | Vermerkt den Stand der zuletzt übertragenen Daten, damit unveränderte Daten nicht erneut gesendet werden | HTML Local Storage | Alle, mit Anmeldung | Persistent | Die nächste Synchronisation überträgt alle Daten erneut |
| `[product identifier]-storage-imported` | Vermerkt, dass die lokalen Daten gerade aus dem Konto übernommen wurden | HTML Local Storage | Alle, mit Anmeldung | Einmalig, wird direkt nach dem Lesen entfernt | Ohne Folge |
| `[product identifier]-streak-decay-anchored` | Vermerkt, dass der Verfall der Serie auf diesem Gerät bereits berücksichtigt wurde | HTML Local Storage | Worteck, mit Verfall der Serie | Persistent | Die Serie kann fälschlich verfallen |
| `[product identifier]-token` | Speichert die Anmeldung beim integrierten Anmelde-Interface | HTTP Cookie | Alle, mit Anmeldung | 7 Tage, wird beim Abmelden entfernt | Nutzer:innen werden abgemeldet |
| `XSRF-TOKEN` | Wird von Laravel gesetzt und bei einer Anmeldung über eine Session gelesen | HTTP Cookie | Alle, mit Anmeldung über eine Session | Laravel-Standard | Die Anmeldung schlägt fehl |
| Name aus der SSO-Konfiguration | Speichert das Token einer externen Anmeldung. Der Eintrag wird gelesen und beim Abmelden entfernt, jedoch nicht von den Rätseln gesetzt | HTTP Cookie | Alle, mit externer Anmeldung | Wird extern bestimmt | Nutzer:innen werden abgemeldet |
| `[product identifier]-token` | Sichert den Rahmen der externen Anmeldung ab. Der Eintrag trägt denselben Namen wie das Cookie, erfüllt aber eine andere Aufgabe | HTML Session Storage | Alle, mit externer Anmeldung | Bis zum Schließen des Tabs | Die Anmeldung beginnt von vorn |
| `supporter:checkout` | Vermerkt die Rückkehr aus einem Bezahlvorgang | HTML Session Storage | Alle, mit Bezahlfunktion | Einmalig, wird direkt nach dem Lesen entfernt | Die Bestätigungsseite erkennt die Rückkehr nicht |

---

## Präferenzen

Unter Präferenzen fallen Einstellungen, die für den **Betrieb** eines Rätsels **nicht notwendig** sind.
Präferierte Einstellungen können von Nutzer:innen dauerhaft gespeichert werden, wenn sie ihre **Zustimmung zur Speicherung** dieser Einträge zulassen.

Ebenfalls unter Präferenzen fallen Einträge, die den zuletzt angezeigten Stand einer Statistik festhalten. Sie dienen allein der Animation und lassen sich ohne Datenverlust entfernen.

| Eintrag | Beschreibung | Typ | Gilt für | Ablauf | Bei Löschung |
|---|---|---|---|---|---|
| `[product identifier]-pref-darkmode` | Speichert die Einstellung zum Dark-Mode | HTML Local Storage | Alle | Persistent | Der Dark-Mode fällt auf die Voreinstellung zurück |
| `[product identifier]-pref-contrast` | Speichert die Einstellung für einen stärkeren Kontrast der Farben | HTML Local Storage | Worteck | Persistent | Der Kontrast fällt auf die Voreinstellung zurück |
| `[product identifier]-pref-hardmode` | Speichert die Einstellung, ob Nutzer:innen bevorzugt im schwierigen Modus rätseln | HTML Local Storage | Worteck | Persistent | Der schwierige Modus ist wieder abgeschaltet |
| `[product identifier]-pref-handwritten` | Speichert die Einstellung, ob Zahlen in Schreibschrift dargestellt werden | HTML Local Storage | Sudoku | Persistent | Die Schreibschrift fällt auf die Voreinstellung zurück |
| `[product identifier]-pref-helpmode` | Speichert die Einstellung, ob die Tastatur bereits verbrauchte Ziffern kennzeichnet | HTML Local Storage | Sudoku | Persistent | Die Kennzeichnung fällt auf die Voreinstellung zurück |
| `[product identifier]-pref-wordlistsort` | Speichert die gewählte Sortierung der Wortliste | HTML Local Storage | Wortwabe | Persistent | Die Sortierung fällt auf die Voreinstellung zurück |
| `[product identifier]-pref-streak-decay-info` | Vermerkt, dass der Hinweis zum Verfall der Serie gesehen wurde | HTML Local Storage | Worteck, mit Verfall der Serie | Persistent | Der Hinweis erscheint erneut |
| `[product identifier]-rank-shown` | Speichert den zuletzt angezeigten Stand der Serie | HTML Local Storage | Worteck | Persistent | Die Animation läuft einmalig falsch |
| `[product identifier]-record-shown` | Speichert die zuletzt angezeigte längste Serie, um einen neuen Rekord zu erkennen | HTML Local Storage | Worteck | Persistent | Ein neuer Rekord wird einmalig nicht hervorgehoben |
| `[product identifier]-streak-shown` | Speichert den zuletzt angezeigten Stand der Serie | HTML Local Storage | Kinonym | Persistent | Die Animation läuft einmalig falsch |
| `[product identifier]-stats-shown-local`, `[product identifier]-stats-shown-cloud` | Speichert die zuletzt angezeigten Werte der Statistik, getrennt nach lokalem Spielstand und Spielstand im Konto | HTML Local Storage | Alle | Persistent | Die Animation läuft einmalig falsch |

---

## IndexedDB

Die täglichen Rätsel werden im **Browser des Clients** abgelegt, um **schneller und offline** zur Verfügung zu stehen.
Die Speicherung der Rätsel ist ebenfalls **notwendig**.

Der Name der Datenbank entspricht dem Product Identifier, der Objektspeicher darin trägt den Namen `puzzles`.
In den Entwicklertools des Browsers erscheint diese Kombination als `[product identifier]#puzzles`.

Gespeichert werden alle Rätsel der zukünftigen und vergangenen Tage gemäß der Anzahl an Tagen, die das Archiv für Nutzer:innen zugänglich ist.
Rätsel außerhalb dieses Zeitraums werden beim Aufruf automatisch entfernt, beim Einspielen einer neuen Version wird der Objektspeicher geleert.
Die Datenbank entsteht nur in der Produktions- und in der Stage-Umgebung.

Wird die Datenbank gelöscht, lädt das Rätsel die Daten beim nächsten Aufruf erneut.

---

## Zwischenspeicher der App

Die Rätsel werden als **progressive Web-App** ausgeliefert und legen dafür einen Zwischenspeicher an.
Er enthält die Dateien der App sowie bereits geladene Seiten, Bilder und Antworten der Schnittstelle.

| Eintrag | Inhalt |
|---|---|
| `[product identifier]-precache-v2-[revision]` | Dateien der App |
| `[product identifier]-runtime-[revision]` | Zur Laufzeit geladene Dateien |
| `[product identifier]-pages` | Aufgerufene Seiten |
| `[product identifier]-images` | Geladene Bilder |
| `[product identifier]-api` | Antworten der Schnittstelle, darunter Rätseldaten |

Der Bestandteil `[revision]` wechselt mit jeder Version der App.
Nicht mehr benötigte Zwischenspeicher werden beim Einspielen einer neuen Version automatisch entfernt.
