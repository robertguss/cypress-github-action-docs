# Node versions

You can run your tests across multiple Node versions.

```yml
name: Node versions
on: [push]
jobs:
  cypress-run:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        node: [10, 12]
    name: E2E on Node v${{ matrix.node }}
    steps:
      - uses: actions/setup-node@v1
        with:
          node-version: ${{ matrix.node }}
      - uses: actions/checkout@v2
      - uses: cypress-io/github-action@v4
```

[![Node versions example](https://github.com/cypress-io/github-action/workflows/example-node-versions/badge.svg?branch=master)](.github/workflows/example-node-versions.yml)

**Note:** because this action uses `npm ci` and `npx` commands, it requires at least Node 8.12 that includes the version of NPM with those commands.
