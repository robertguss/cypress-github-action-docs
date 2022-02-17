# Specs

Specify the [spec files to run](https://docs.cypress.io/guides/guides/command-line.html#cypress-run-spec-lt-spec-gt) with `spec` parameter

```yml
name: Cypress tests
on: [push]
jobs:
  cypress-run:
    name: Cypress run
    runs-on: ubuntu-20.04
    steps:
      - name: Checkout
        uses: actions/checkout@v2

      - name: Cypress run
        uses: cypress-io/github-action@v4
        with:
          spec: cypress/integration/spec1.js
```

You can pass multiple multiple specs and wild card patterns using multi-line parameter, see [example-config.yml](https://github.com/cypress-io/github-action/blob/master/.github/workflows/example-config.yml):

```yml
spec: |
  cypress/integration/spec-a.js
  cypress/**/*-b.js
```

For more information, visit [the Cypress command-line docs](https://on.cypress.io/command-line#cypress-run-env-lt-env-gt).
