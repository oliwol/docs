# Cookies

Zur Konfiguration einer [CMP](./cmp) werden nachfolgend **verwendete Cookies** aufgelistet und kategorisiert.
Es gibt 4 Kategorien: Notwendig, Präferenzen, Statistiken und Marketing.
Die Rätsel setzen **ausschließlich notwendige** Cookies und Cookies für **Präferenzen**.

> [!INFO]
> Es werden keine HTTP Cookies gesetzt. Es kommen nur HTML Local Storage und IndexedDB zum Einsatz. Zusammengefasst werden sie in diesem Abschnitt als *Cookies* bezeichnet.

---

## Cookie-Name

Cookies werden nach folgendem Muster benannt: `[product identifier]-[category]-[name]`.
Ein Präferenz-Cookie für die Einstellung des Dark-Modes unter Sudoku würde wie folgt lauten: `sdk-pref-darkmode`.

Die Product Identifier lauten wie folgt:

| Produkt | Identifier |
|---|---|
| Worteck | `wrdl` |
| Sudoku | `sdk` |
| Wortwabe | `wrtwb` |
| Kreuzworträtsel | `xwrt` |

---

## IndexedDB

Die täglichen Rätsel werden im **Browser des Clients** abgelegt, um **schneller und offline** zur Verfügung zu stehen.
Die Speicherung der Rätsel ist ebenfalls **notwendig**.
Der Name einer Datenbank folgt immer dem gleichen Schema: `[product identifier]#puzzles`.

---

## Notwendige Cookies

Notwendige Cookies müssen **zwingend zugelassen** werden und sollten von Ihrer CMP-Lösung **nicht gelöscht** bzw. unterdrückt werden.
Werden notwendige Cookies nicht zugelassen, führt dies dazu, dass Statistiken und Spieldaten der Nutzer:innen nicht gespeichert werden, wodurch die **Spiele nicht nutzbar** sind.

| Cookie | Beschreibung | Typ | Ablauf |
|---|---|---|---|
| `[product identifier]-user-stats` | Speichert die Nutzer:innen-Statistiken | HTML Local Storage | Persistent |
| `[product identifier]-user-games` | Speichert die Nutzer:innen-Eingaben zu den täglichen Rätseln | HTML Local Storage | Persistent |
| `[product identifier]-user-data` | Speichert bei erfolgreichem Login die Nutzer:innen-Daten (E-Mail oder Username, Benachrichtigungen und verifiziert am) | HTML Local Storage | Nach Logout |
| `[product identifier]-user-token` | Speicherung bei erfolgreichem Login und Nutzung der Authentifizierung via Token | HTML Local Storage | Nach Logout |
| `[product identifier]-user-synced` | Speichert die Information, ob die Synchronisation der Spieldaten zwischen HTML Local Storage und Datenbank erfolgreich war | HTML Local Storage | Persistent |
| `[product identifier]#puzzles` | Speichert alle Rätsel der zukünftigen und vergangenen Tage gemäß der Anzahl an Tagen, die das Archiv für Nutzer:innen zugänglich ist | IndexedDB | Persistent |

---

## Präferenzen

Unter Präferenzen fallen Einstellungen, die für den **Betrieb** eines Rätsels **nicht notwendig** sind.
Präferierte Einstellungen können von Nutzer:innen dauerhaft gespeichert werden, wenn sie ihre **Zustimmung zur Speicherung** dieser Cookies zulassen.

| Cookie | Beschreibung | Typ | Ablauf |
|---|---|---|---|
| `[product identifier]-pref-darkmode` | Speichert die Einstellung zum Dark-Mode | HTML Local Storage | Persistent |
| `[product identifier]-pref-hardmode` | Speichert die Einstellung, ob Nutzer:innen bevorzugt im schwierigen Modus rätseln | HTML Local Storage | Persistent |
| `[product identifier]-pref-contrast` | Speichert die Einstellung für einen stärkeren Kontrast der Farben | HTML Local Storage | Persistent |
| `[product identifier]-pref-handwritten` | Speichert die Einstellung, ob Zahlen bzw. Buchstaben in Schreibschrift dargestellt werden | HTML Local Storage | Persistent |