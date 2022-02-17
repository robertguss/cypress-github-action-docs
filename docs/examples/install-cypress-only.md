# Install Cypress only

If the project has many dependencies, but you want to install just Cypress you can combine this action with `actions/cache` and `npm i cypress` commands yourself.

```yml
- uses: actions/checkout@v2
- uses: actions/cache@v2
  with:
    path: |
      ~/.cache/Cypress
      node_modules
    key: my-cache-${{ runner.os }}-${{ hashFiles('package-lock.json') }}
- run: npm i cypress
- uses: cypress-io/github-action@v4
  with:
    install: false
```

See [https://github.com/cypress-io/github-action/blob/master/.github/workflows/example-install-only.yml](https://github.com/cypress-io/github-action/blob/master/.github/workflows/example-install-only.yml) file.

[![Install only Cypress example](https://github.com/cypress-io/github-action/workflows/example-install-only/badge.svg?branch=master)](https://github.com/cypress-io/github-action/blob/master/.github/workflows/example-install-only.yml)
