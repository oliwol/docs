# Contributing to docs

## Git-Governance bei oliwol

Kein Code darf ohne explizite Freigabe durch das Board in den `main`-Branch
gemerged werden. Diese Regeln gelten für alle Repositories der Organisation.

## Branch-Strategie

- Der `main`-Branch ist **geschützt**
- Direktes Pushen auf `main` ist **verboten**
- Force-Pushes auf `main` sind **dauerhaft deaktiviert**
- Merges sind **ausschließlich über Pull Requests** möglich

## PR-Prozess

### 1. Feature-Branch erstellen

```bash
git checkout main
git pull origin main
git checkout -b feature/dein-feature-name
```

Naming-Konventionen:
- `feature/` – neue Funktionen
- `fix/` – Bug-Fixes
- `docs/` – Dokumentation
- `chore/` – Maintenance, Dependencies

### 2. Änderungen commiten

```bash
git add .
git commit -m "feat: kurze Beschreibung der Änderung"
```

Commit-Konventionen (Conventional Commits):
- `feat:` – neue Funktion
- `fix:` – Bug-Fix
- `docs:` – Dokumentation
- `refactor:` – Umstrukturierung ohne Funktionsänderung
- `chore:` – Maintenance

### 3. Pull Request erstellen

Öffne einen Pull Request auf GitHub mit folgenden Pflichtangaben:

**PR-Beschreibung muss enthalten:**
- Was wurde geändert?
- Warum wurde es geändert?
- Welche Risiken gibt es?

### 4. Board-Freigabe (Pflicht)

Jeder PR benötigt **mindestens 1 Approval vom Board (Oliver)** bevor er
gemerged werden darf.

- Kein Agent darf ohne dieses Approval mergen
- Kein automatisierter Prozess darf ohne dieses Approval mergen
- Diese Regel ist **nicht verhandelbar**

### 5. Merge

Nach dem Board-Approval wird der PR von Oliver oder einem autorisierten
Teammitglied gemerged.

## Wichtige Regeln

| Regel | Status |
|-------|--------|
| Direktes Pushen auf `main` | VERBOTEN |
| Force-Push auf `main` | VERBOTEN |
| Merge ohne Board-Approval | VERBOTEN |
| PR ohne Beschreibung | VERBOTEN |
| PR mit Board-Approval | ERLAUBT |

## Fragen?

Bei Fragen zum Prozess wende dich an das Board (Oliver) oder öffne ein
Issue in diesem Repository.
