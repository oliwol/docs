# Contributing to docs

## Branch Strategy

- The `main` branch is **protected**
- Direct pushes to `main` are **not allowed**
- Force pushes to `main` are **disabled**
- All changes must go through **pull requests**

## Pull Request Process

### 1. Create a branch

```bash
git checkout main
git pull origin main
git checkout -b feature/short-description
```

Branch naming:
- `feature/` – new features
- `fix/` – bug fixes
- `docs/` – documentation
- `chore/` – maintenance

### 2. Commit your changes

```bash
git add .
git commit -m "type: short description"
```

Types: `feat`, `fix`, `docs`, `refactor`, `chore`

### 3. Open a pull request

PR description must include:
- What was changed?
- Why was it changed?
- Are there any risks?

### 4. Review and merge

Every PR requires at least **1 approval from the maintainer** before merging.
No automated process may merge without this approval.
