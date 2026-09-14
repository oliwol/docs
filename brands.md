# Marken

Eine **Marke** bündelt das **Erscheinungsbild**, die **Schnittstelle** für die Anmeldung und das **Icon** der Paywall.
Marken gehören zu Ihrer **Organisation** und stehen damit in allen Publikationen zur Verfügung.

Marken sind für Organisationen gedacht, die dieselben Rätsel unter **mehreren eigenständigen Auftritten** betreiben, etwa ein Verlag, der ein Sudoku unter allen seinen Zeitungsmarken anbietet.
Statt Logo, Farben und Schnittstelle in jeder Publikation einzeln zu hinterlegen, pflegen Sie sie **einmal je Marke**: Bei drei Rätseln und fünf Marken pflegen Sie fünf Konfigurationen statt 15.

> [!INFO]
> Marken gehören zum **gleichnamigen Modul**. Ohne dieses Modul erscheint der Menüpunkt nicht, und Ihre Publikationen verhalten sich unverändert.
> Endet das Modul, bleiben bestehende Zuordnungen wirksam, lassen sich aber nicht mehr ändern.

---

## Was eine Marke trägt

| Bereich | Inhalt |
| --- | --- |
| Erscheinungsbild | Logo, Icon, Schrift, Akzentfarbe, individuelles CSS |
| Authentifizierung | die [Schnittstelle](./sso), über die sich Nutzer:innen anmelden |
| Paywall | das [Icon](./paywall#ein-eigenes-icon-je-marke) der Paywall |

---

## Vererbung

Eine Marke **überschreibt** die Werte ihrer Publikation **feldweise**:

| Feld an der Marke | Ergebnis auf ihren Domains |
| --- | --- |
| Gefüllt | Der Wert der Marke gilt |
| Leer | Der Wert der Publikation gilt |

Sie müssen an einer Marke also nur die Werte pflegen, die vom Standard der Publikation **abweichen**.
Setzt eine Marke beispielsweise nur Logo, Icon und Akzentfarbe, bleibt die Schrift die der Publikation.
Dasselbe gilt für die Anmeldung: Trägt eine Marke keine eigene Schnittstelle, gilt die [Schnittstelle der Publikation](./sso#aktivierung-der-sso).

Die Auflösung folgt immer derselben Reihenfolge:

```
Domain  →  Marke  →  Publikation
```

Eine Domain zeigt auf **höchstens eine Marke**; für jedes leere Feld der Marke gilt der Wert der Publikation.

### Domains ohne Marke

Eine Domain benötigt **keine** Marke. Ohne Marke gelten Erscheinungsbild und Schnittstelle der Publikation.

---

## Eine Marke anlegen

Marken verwalten Sie in der Navigation Ihrer Organisation unter **Marken**.

Beim Anlegen ist nur der **Name** ein Pflichtfeld. Alle weiteren Werte können Sie leer lassen und später ergänzen; leere Felder erben von der jeweiligen Publikation.
Die Anzahl der Marken ist nicht begrenzt.

---

## Eine Marke zuordnen

Die Zuordnung erfolgt an der **Domain**.

Öffnen Sie dazu in Ihrer Publikation die [Domain-Verwaltung](./setup#eigene-domain) und anschließend die **Konfiguration** der gewünschten Domain, per Klick auf die Zeile oder über das Aktionsmenü. Oberhalb der DNS-Einträge finden Sie dort die Auswahl der Marke.
Die Voreinstellung ist **Ohne Marke**.

> [!INFO]
> Änderungen an einer Marke oder Zuordnung werden gesammelt und mit der nächsten [Bereitstellung](./setup#bereitstellung) auf die Domains übertragen.

---

## Domains einer Marke

In der Detailansicht einer Marke sehen Sie unter **Domains** alle Domains, die auf die Marke zeigen, **über alle Publikationen hinweg** und jeweils mit ihrer Publikation.
Prüfen Sie diese Liste vor größeren Änderungen: Sie zeigt, welche Domains eine Änderung an der Marke betrifft.

Eine Marke kann erst **gelöscht** werden, wenn keine Domain mehr auf sie zeigt.

---

## Eigene Schnittstelle je Marke

Trägt eine Marke eine eigene Schnittstelle, melden sich Nutzer:innen auf ihren Domains über diese Schnittstelle an. Für die [Zugriffsteuerung](./paywall#zugriffsteuerung) ist dabei eine Bedingung zu beachten.

Eine Schnittstelle umfasst **Anmeldeseite**, **Schlüssel** und **Zustände**. Marken mit unterschiedlicher Anmeldung brauchen deshalb jeweils eine eigene Schnittstelle, auch wenn ihre Konten im selben System liegen.
In der Liste der Schnittstellen zeigt die Spalte **Verwendet von**, welche Marken und Publikationen eine Schnittstelle verwenden.

Zeigt **jede** Domain einer Publikation auf eine Marke mit eigener Schnittstelle, braucht die Publikation selbst keine.

### Übereinstimmende Zustände

Geschützte Seiten, Funktionen und Werbeplätze sind an einen [Zustand](./paywall#zustände) gebunden, nicht an eine bestimmte Schnittstelle.
Eine Bindung greift deshalb auf jeder Domain, deren Schnittstelle einen **gleichnamigen Zustand** führt.

Führt eine Schnittstelle **keinen** gleichnamigen Zustand, setzt das System die betroffene Bindung beim Speichern auf **Angemeldet**. Der Inhalt bleibt damit hinter der Anmeldung geschützt und verhält sich auf allen Domains gleich; nur die feinere Unterscheidung nach Zustand entfällt.

| Zustand an der Publikation | Zustand an der Marke | Ergebnis |
| --- | --- | --- |
| `abonnentin` | `abonnentin` | Die Seite bleibt auf den Zustand beschränkt |
| `abonnentin` | `subscriber` | Die Bindung wird auf **Angemeldet** gesetzt |

Vor dem Speichern warnt das System und nennt die betroffenen Seiten, Funktionen und Werbeplätze namentlich. Die Warnung erscheint in drei Situationen:

- beim **Zuordnen** einer Marke mit eigener Schnittstelle, auch direkt beim Anlegen einer Domain
- beim **Wechsel** der Schnittstelle einer Marke oder der Publikation
- beim **Umbenennen oder Verschieben** eines Zustands

Zur Auswahl stehen nur die aktiven Zustände, die **alle** auf der Publikation antwortenden Schnittstellen führen, etwa unter **Erlaubt für**.

> [!WARNING]
> Wenn Sie eine weitere Schnittstelle anlegen, übernehmen Sie die Namen der bestehenden Zustände unverändert, sofern dieselben Inhalte geschützt bleiben sollen.

---

## Grenzen

**Ein Zustand, ein Wert.** Umgebungs-Überschreibungen, etwa die Zahl der Archivtage, stehen an den Zuständen einer Schnittstelle. Es zählen die Zustände aller Schnittstellen, die auf der Publikation antworten. Führen mehrere denselben Zustand, gilt der Wert der Schnittstelle der Publikation, danach der Wert der Marke, deren Name alphabetisch zuerst kommt. Unterschiedliche Werte je Marke für denselben Zustand sind nicht vorgesehen.

**Eine Marke ersetzt nur das Icon der Paywall.** Überschrift, Text und Schaltfläche bleiben die der jeweiligen [Paywall](./paywall#ein-eigenes-icon-je-marke). Welche Paywall erscheint, bestimmt wie bisher der Zustand.

**Je Schnittstelle ein eigener Nutzerbestand.** Ein Konto gehört zu der Schnittstelle, über die es angelegt wurde; die Anmeldung findet nur Konten derselben Schnittstelle. Das gilt auch für die E-Mail-Adresse: Sie findet ein Konto nur innerhalb derselben Schnittstelle, etwa wenn eine Schnittstelle einer Person eine neue User-ID vergibt. Nutzen zwei Marken verschiedene Schnittstellen, sind es zwei getrennte Bestände. Konten werden nicht zusammengeführt.

Diese Bindung verhindert Kollisionen, wenn Ihre Systeme fortlaufende Nummern statt UUIDs als [User-ID](./sso#user-id) vergeben: Zwei Systeme können dieselbe Kennung ausgeben, ohne dass sich zwei Personen ein Konto teilen.

Daraus folgt für den **Wechsel der Schnittstelle** einer Marke: Auf den Domains der Marke startet der Nutzerbestand leer, Nutzer:innen melden sich neu an. Gelöscht wird nichts. Die bestehenden Konten bleiben der bisherigen Schnittstelle zugeordnet und stehen überall dort zur Verfügung, wo diese weiterhin antwortet. Bevor Sie speichern, nennt das System, wie viele Konten der bisherigen Schnittstelle auf den betroffenen Publikationen bestehen.

> [!INFO]
> Melden sich dieselben Nutzer:innen über zwei Marken mit derselben E-Mail-Adresse an, entsteht je Schnittstelle ein eigenes Konto.
> Eine Adresse kann auf einer Publikation nur einmal vergeben sein. Das zweite Konto bleibt deshalb ohne [E-Mail-Adresse](./sso#e-mail).
