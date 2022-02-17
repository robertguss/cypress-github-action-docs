# Working directory

In a monorepo, the end-to-end test might be placed in a different sub-folder from the application itself, like this

```text
repo/
  app/
  e2e/
    cypress
    cypress.json
  package.json
```

You can specify the `e2e` working directory when running Cypress tests using `working-directory` parameter

```yml
on: [push]
jobs:
  cypress-run:
    runs-on: ubuntu-20.04
    steps:
      - uses: actions/checkout@v2
      - uses: cypress-io/github-action@v4
        with:
          start: npm start
          working-directory: e2e
```

See [cypress-gh-action-monorepo](https://github.com/bahmutov/cypress-gh-action-monorepo) for a running example
