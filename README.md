# Install go-task/task Action

This GitHub Action installs [go-task/task](https://github.com/go-task/task) to the GitHub Actions runner tool cache and adds it to the PATH. It **always** verifies the downloaded archive against official checksums.

## Platform Support

This action supports **Linux** and **macOS** runners only. Windows is not supported.

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
