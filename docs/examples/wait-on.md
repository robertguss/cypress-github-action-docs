# Wait-on

If you are starting a local server and it takes a while to start, you can add a parameter `wait-on` and pass url to wait for the server to respond.

```yml
name: After server responds
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
          # quote the url to be safe against YML parsing surprises
          wait-on: "http://localhost:8080"
```

[![wait-on example](https://github.com/cypress-io/github-action/workflows/example-wait-on/badge.svg?branch=master)](https://github.com/cypress-io/github-action/blob/master/.github/workflows/example-wait-on.yml)

By default, `wait-on` will retry for 60 seconds. You can pass a custom timeout in seconds using `wait-on-timeout`.

```yml
- uses: cypress-io/github-action@v4
  with:
    start: npm start
    wait-on: "http://localhost:8080/status"
    # wait for 2 minutes for the server to respond
    wait-on-timeout: 120
```

See also [![Webpack Dev Server example](https://github.com/cypress-io/github-action/workflows/example-webpack/badge.svg?branch=master)](https://github.com/cypress-io/github-action/blob/master/.github/workflows/example-webpack.yml)

You can wait for multiple URLs to respond by separating urls with a comma

```yml
- uses: cypress-io/github-action@v4
  with:
    # API runs on port 3050
    # Web server runs on port 8080
    start: npm run api, npm run web
    # wait for all services to respond
    wait-on: "http://localhost:3050, http://localhost:8080"
```

The action will wait for the first url to respond, then will check the second url, and so on.

You can even use your own command (usually by using `npm`, `yarn`, `npx`) to wait for the server to respond. For example, if you want to use [wait-on](https://github.com/jeffbski/wait-on) utility to ping the server and run the Cypress tests after the server responds:

```yml
- uses: cypress-io/github-action@v4
  with:
    start: npm start
    wait-on: "npx wait-on --timeout 5000 http://localhost:3000"
```

See [example-wait-on.yml](https://github.com/cypress-io/github-action/blob/master/.github/workflows/example-wait-on.yml) workflow file.

If this action times out waiting for the server to respond, please see [Debugging](#debugging) section in this README file.
