# Marken

Eine **Marke** bündelt, was ein Portal ausmacht: das **Erscheinungsbild**, die **Anmeldung** und das **Angebot**.
Sie gehört zu Ihrer Organisation und gilt über alle Publikationen hinweg.

Führen Sie mehrere Portale auf denselben Rätseln, pflegen Sie eine Marke einmal statt einmal je Rätsel.
Vier Rätsel unter dreizehn Portalen sind dreizehn Marken, nicht 52 Wertesätze.

> [!INFO]
> Marken gehören zum Modul **Marken**. Ohne dieses Modul erscheint der Menüpunkt nicht, und Ihre Publikationen verhalten sich unverändert.

---

## Was eine Marke trägt

| Bereich | Inhalt |
| --- | --- |
| Erscheinungsbild | Logo, Symbol, Schrift, Akzentfarbe, individuelles CSS |
| Authentifizierung | die [Schnittstelle](./sso), über die sich Lesende anmelden |
| Angebot | die [Paywall](./paywall), die auf den Domains dieser Marke erscheint |

---

## Vererbung

Eine Marke **überschreibt** die Publikation, sie ersetzt sie nicht.

Jedes Feld wird einzeln aufgelöst. Was die Marke trägt, gilt. Wo sie leer ist, gilt der Wert der Publikation.

| Feld an der Marke | Ergebnis auf ihren Domains |
| --- | --- |
| Gefüllt | Der Wert der Marke gilt |
| Leer | Der Wert der Publikation gilt |

Ein leeres Feld ist also **keine Entscheidung gegen einen Wert**, sondern die Entscheidung, den der Publikation zu behalten.
Setzen Sie an einer Marke nur eine abweichende Akzentfarbe, bleiben Logo, Symbol und Schrift die Ihrer Publikation.

Dasselbe gilt für die Anmeldung: Trägt eine Marke keine eigene Schnittstelle, melden sich Lesende auf ihren Domains über die Schnittstelle der Publikation an.

### Die Reihenfolge

```
Domain  →  Marke  →  Publikation
```

Eine Domain zeigt auf höchstens eine Marke, und die Marke fällt auf die Publikation zurück.

### Domains ohne Marke

Eine Domain **braucht** keine Marke. Ohne eine zeigt sie das Erscheinungsbild ihrer Publikation und meldet sich über deren Schnittstelle an, genau wie vor der Einführung der Marken.
Das gilt auch für die [Cloud-Domain](./setup#cloud-domain).

---

## Eine Marke anlegen

Marken finden Sie in der Navigation neben **Publikationen**.

Eine neue Marke braucht nur einen **Namen**. Alles Weitere dürfen Sie leer lassen und später ergänzen; leer bedeutet, dass die Publikation den Wert liefert.

Wie viele Marken Sie führen, ist nicht begrenzt.

---

## Eine Marke zuordnen

Die Zuordnung geschieht an der **Domain**, denn eine Domain gehört zu einem Rätsel.

Öffnen Sie in Ihrer Publikation die [Domain-Verwaltung](./setup#eigene-domain) und dort die **Konfiguration** einer Domain, entweder über einen Klick auf die Zeile oder über das Aktionsmenü. Neben den DNS-Einträgen finden Sie dort die Auswahl der Marke.

Die Voreinstellung ist **Ohne Marke**.

> [!INFO]
> Eine Änderung an einer Marke oder an einer Zuordnung wird gesammelt und mit der nächsten [Bereitstellung](./setup#bereitstellung) auf die Domains übertragen.

---

## Die Reichweite einer Marke

Öffnen Sie eine Marke, sehen Sie unter **Domains** alle Domains, die sie zeigen, **über alle Publikationen hinweg**, jede mit ihrem Rätsel.

Dort steht auch, wie weit eine Änderung reicht, bevor Sie sie machen.

Eine Marke lässt sich **nicht löschen**, solange eine Domain auf sie zeigt. Andernfalls verlöre diese Domain ihr Erscheinungsbild, ohne dass es jemand gesagt hätte.

---

## Zustände und ihre Kurznamen

Trägt eine Marke eine **eigene Schnittstelle**, ist eine Bedingung zu beachten.

Seiten und Konfigurationswerte binden sich über den **Kurznamen** eines Zustands an diesen, nicht über eine interne Nummer.
Eine andere Schnittstelle trägt eine geschützte Seite deshalb, solange ihre Zustände **dieselben Kurznamen** führen.

Fehlt ein Kurzname, ist die betroffene Seite auf den Domains dieser Marke **ohne Anmeldung erreichbar**.

Beim Zuordnen nennt die Console die betroffenen Seiten namentlich. Sie hält Sie nicht auf, denn womöglich ist genau das gewollt.

| Zustand an der Publikation | Zustand an der Marke | Ergebnis |
| --- | --- | --- |
| `abonnentin` | `abonnentin` | Die Seite bleibt geschützt |
| `abonnentin` | `subscriber` | Die Seite ist frei zugänglich |

> [!WARNING]
> Legen Sie eine zweite Schnittstelle an, übernehmen Sie die Kurznamen der Zustände unverändert, sofern dieselben Inhalte geschützt bleiben sollen.

---

## Grenzen

**Werte je Zustand bleiben an der Publikation.** Umgebungs-Überschreibungen, etwa die Zahl der Archivtage je Zustand, kommen weiterhin aus der Publikation, während die Zustände von der Marke stammen können. Bei gleichen Kurznamen greifen sie, eine Marke kann dafür aber keine eigenen Werte setzen.

**Eine Marke wählt eine Paywall, sie ändert sie nicht.** Die gewählte Paywall gilt für alle Zustände der Marke. Gepflegt wird sie weiterhin an einer Stelle.

**Ein Anmeldesystem, ein Nutzerbestand.** Nutzen zwei Marken verschiedene Anmeldesysteme, sind es zwei getrennte Bestände. Konten werden nicht zusammengeführt.

Ein Konto gehört zu der Schnittstelle, über die es entstanden ist. Die Anmeldung findet deshalb nur Konten derselben Schnittstelle.

Das ist wichtig, wenn Ihre Systeme **fortlaufende Nummern** statt UUIDs vergeben: Zwei Portale können beide die Kennung `42` ausgeben, und ohne diese Bindung würde die zweite Person im Konto der ersten landen. Mit ihr sind es zwei Konten.

> [!INFO]
> Melden sich dieselben Lesenden über zwei Marken mit **derselben E-Mail-Adresse** an, bleibt es ein Konto je Publikation. Die E-Mail-Adresse gilt als Person, die Kennung als Konto im jeweiligen System.
