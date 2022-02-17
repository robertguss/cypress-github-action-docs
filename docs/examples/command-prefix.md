# Command prefix

You can prefix the default test command using the `command-prefix` option. This is useful for example when running [Percy](https://docs.percy.io/docs/cypress), which requires the test command to be wrapped with `percy exec --`.

```yml
name: Visual
on: [push]
jobs:
  e2e:
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
          # the entire command will automatically be prefixed with "npm"
          # and we need the second "npm" to execute "cypress run ..." command line
          command-prefix: "percy exec -- npx"
```

See live example [angular-pizza-creator](https://github.com/cypress-io/angular-pizza-creator).
