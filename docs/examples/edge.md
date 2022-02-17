# Edge

```yml
name: Edge
on: push
jobs:
  tests:
    runs-on: windows-latest
    steps:
      - uses: actions/checkout@v2
      - uses: cypress-io/github-action@v4
        with:
          browser: edge
```

[![Edge example](https://github.com/cypress-io/github-action/workflows/example-edge/badge.svg?branch=master)](https://github.com/cypress-io/github-action/blob/master/.github/workflows/example-edge.yml)

**Note:** Microsoft has not released Edge for Linux yet, thus you need to run these tests on Windows or Mac runners with Edge preinstalled. You can use [`cypress info`](https://on.cypress.io/command-line#cypress-info) command to see the browsers installed on the machine.
