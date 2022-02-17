# Print Cypress info

Sometimes you might want to print Cypress and OS information, like the list of detected browsers. You can use the [`cypress info`](https://on.cypress.io/command-line#cypress-info) command for this.

If you are NOT using the `build` command in your project, you can run the `cypress info` command:

```yml
name: info
on: [push]
jobs:
  cypress-run:
    runs-on: ubuntu-20.04
    steps:
      - name: Checkout
        uses: actions/checkout@v2
      - name: Cypress run
        uses: cypress-io/github-action@v4
        with:
          build: npx cypress info
```

If you are already using the `build` parameter, you can split the [installation and the test steps](#split-install-and-tests) and insert the `cypress info` command in between:

```yml
name: info
on: [push]
jobs:
  cypress-run:
    runs-on: ubuntu-20.04
    steps:
      - name: Checkout
        uses: actions/checkout@v2
      - name: Cypress install
        uses: cypress-io/github-action@v4
        with:
          # just perform install
          runTests: false
      - name: Cypress info
        run: npx cypress info
      - name: Cypress run
        uses: cypress-io/github-action@v4
        with:
          # we have already installed all dependencies above
          install: false
          # rest of your parameters
```
