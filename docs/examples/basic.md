# Basic

```yml
name: End-to-end tests
on: [push]
jobs:
  cypress-run:
    runs-on: ubuntu-20.04
    steps:
      - name: Checkout
        uses: actions/checkout@v2
      # Install NPM dependencies, cache them correctly
      # and run all Cypress tests
      - name: Cypress run
        uses: cypress-io/github-action@v4
```

[![Basic example](https://github.com/cypress-io/github-action/workflows/example-basic/badge.svg?branch=master)](.github/workflows/example-basic.yml)

The workflow file [.github/workflows/example-basic.yml](.github/workflows/example-basic.yml) shows how Cypress runs on GH Actions using Ubuntu (16, 18, or 20), on Windows, and on Mac without additional OS dependencies necessary.

**Note:** this package assumes that `cypress` is declared as a development dependency in the `package.json` file. The `cypress` NPM module is required to run Cypress via its [NPM module API](https://on.cypress.io/module-api).
