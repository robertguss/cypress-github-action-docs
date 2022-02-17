# Start server

If your tests run against a local server, use `start` parameter, the server will run in the background and will shut down after tests complete

```yml
name: With server
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
          start: npm start
```

**Note:** sometimes on Windows you need to run a different start command. You can use `start-windows` parameter for this

```yml
name: With server
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
          # Linux and MacOS
          start: npm start
          # Takes precedences on Windows
          start-windows: npm run start:windows:server
```

[![start example](https://github.com/cypress-io/github-action/workflows/example-start/badge.svg?branch=master)](https://github.com/cypress-io/github-action/blob/master/.github/workflows/example-start.yml)

**Note:** GitHub cleans up the running server processes automatically. This action does not stop them.
