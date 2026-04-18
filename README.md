# Install go-task/task Action

This GitHub Action installs [go-task/task](https://github.com/go-task/task) to the GitHub Actions runner tool cache and adds it to the PATH. It **always** verifies the downloaded archive against official checksums.

## Versioning

From **v2.0.0** onwards this action uses **immutable releases** with full semantic versioning (`vMAJOR.MINOR.PATCH`). Floating major tags (e.g., `v2`) are **not** provided.

When referencing this action, either use the full version string or pin to a commit SHA:

```yaml
# Full version string
uses: rsclarke/install-task@v2.0.0

# Pinned to SHA (recommended)
uses: rsclarke/install-task@<COMMIT_SHA> # v2.0.0
```

## Platform Support

This action supports **Linux** and **macOS** runners only. Windows is not supported.

## Caching

The action uses [`actions/cache`](https://github.com/actions/cache) to persist the tool cache across workflow runs. On a cache hit the download and verification steps are skipped entirely, using a `.complete` sentinel file to validate cache integrity.

The cache key includes the runner OS, architecture, and resolved Task version:

```
install-task-{runner.os}-{runner.arch}-{version}
```

When no explicit version is provided, the latest release is resolved first so it still participates in caching.

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `version` | Version of go-task/task to install (e.g., `v3.29.1`). If not specified, the latest release will be resolved automatically. | No | Latest |

The action uses the caller workflow's `GITHUB_TOKEN` automatically via `github.token`, so no token input is required.

## Usage

```yaml
jobs:
  build:
    runs-on: ubuntu-latest # or macOS-latest
    steps:
      - uses: actions/checkout@v4

      - name: Install Task
        uses: rsclarke/install-task@v2.0.0

      - name: Run Task
        run: task --list
```
