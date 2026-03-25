# Install go-task/task Action

This GitHub Action installs [go-task/task](https://github.com/go-task/task) to the GitHub Actions runner tool cache and adds it to the PATH. It **always** verifies the downloaded archive against official checksums.

## Platform Support

This action supports **Linux** and **macOS** runners only. Windows is not supported.

## Caching

The action uses [`actions/cache`](https://github.com/actions/cache) to persist the tool cache across workflow runs. On a cache hit the download and verification steps are skipped entirely, using a `.complete` sentinel file to validate cache integrity.

The cache key includes the runner OS, architecture, and resolved Task version:

```
install-task-{runner.os}-{runner.arch}-{version}
```

When no explicit version is provided, the latest release is resolved first so it still participates in caching.

## Usage

```yaml
jobs:
  build:
    runs-on: ubuntu-latest # or macOS-latest
    steps:
      - uses: actions/checkout@v4

      - name: Install Task
        uses: rsclarke/install-task@v1

      - name: Run Task
        run: task --list
```
