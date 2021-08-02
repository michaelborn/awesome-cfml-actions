# CFFormat

Auto-format your CFML on every push and every PR, thanks to John Berquist's [commandbox-cfformat](https://github.com/jcberquist/commandbox-cfformat) package.

## Arguments

* `paths` - pass a comma-separated list of directories to scan and autoformat.
* `overwrite` - Overwrite files in place - defaults to `true`.
* `cfm` - format `.cfm` files as well as `.cfc` files - defaults to `false`.

## Example

```yml
# .github/workflows/format.yml
name: CFFormat
on:
  push:
    branches-ignore:
      - master
      - main
  pull_request:
    branches:
      - main
      - master
      - development

jobs:
  format:
    runs-on: ubuntu-latest
    steps:
      - uses: michaelborn/cfformat-action@v1.0.7
        with:
          paths: "models,handlers,interceptors,tests/specs"
          overwrite: true
      - name: Commit Format Changes
        uses: stefanzweifel/git-auto-commit-action@v4
        with:
          commit_message: Apply cfformat changes
```