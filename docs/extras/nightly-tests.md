# Nightly tests

Sometimes you want to execute the workflow on a schedule. For example, to run Cypress tests nightly, you can schedule the workflow using `cron` syntax:

```yml
name: example-cron
on:
  schedule:
    # runs tests every day at 4am
    - cron: "0 4 * * *"
jobs:
  nightly:
    runs-on: ubuntu-20.04
    steps:
      - name: Checkout
        uses: actions/checkout@v2
      - name: Cypress nightly tests 🌃
        uses: cypress-io/github-action@v4
```

See the [example-cron.yml](https://github.com/cypress-io/github-action/blob/master/.github/workflows/example-cron.yml) workflow.

[![cron example](https://github.com/cypress-io/github-action/workflows/example-cron/badge.svg?branch=master)](https://github.com/cypress-io/github-action/blob/master/.github/workflows/example-cron.yml)
