# GitHub Actions (`dan-petty/github-actions`)

Centralized collection of reusable GitHub Actions workflows (`workflow_call`) and composite actions for consistent CI/CD pipelines across repositories.

---

## 📦 Reusable Workflows

### 1. Python CI Quality Gate (`reusable-python-ci.yml`)
Runs formatting (`ruff format`), static linting (`ruff check`), strict typechecking (`mypy`), and unit tests with code coverage assertions (`pytest --cov`).

```yaml
jobs:
  ci:
    uses: dan-petty/github-actions/.github/workflows/reusable-python-ci.yml@main
    with:
      python-version: "3.14"
      min-coverage: 90
      run-mypy: true
```

### 2. CodeQL Security Scan (`reusable-codeql.yml`)
Runs GitHub Advanced Security CodeQL vulnerability scans across specified language sets.

```yaml
jobs:
  security:
    uses: dan-petty/github-actions/.github/workflows/reusable-codeql.yml@main
    with:
      languages: '["python", "actions"]'
```

### 3. GitHub Release (`reusable-release.yml`)
Publishes official GitHub Releases with automatically generated release notes.

```yaml
jobs:
  release:
    uses: dan-petty/github-actions/.github/workflows/reusable-release.yml@main
    with:
      tag-name: ${{ github.ref_name }}
```

---

## 🛠️ Composite Actions

### `actions/setup-uv`
Installs `uv`, configures the Python runtime, and handles fast dependency caching.

```yaml
steps:
  - uses: dan-petty/github-actions/actions/setup-uv@main
    with:
      python-version: "3.14"
      sync-deps: "true"
```

### `actions/install-k8s-tools`
Installs Kubernetes client tools (`kubectl` and `helm`) on Linux runners.

```yaml
steps:
  - uses: dan-petty/github-actions/actions/install-k8s-tools@main
```

---

## 📄 License
MIT License. See [LICENSE](LICENSE) for details.
