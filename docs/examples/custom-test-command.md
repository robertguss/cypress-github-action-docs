# Custom test command

You can overwrite the Cypress run command with your own

```yml
steps:
  - name: Checkout 🛎
    uses: actions/checkout@v2

  - name: Custom tests 🧪
    uses: cypress-io/github-action@v4
    with:
      command: npm run e2e:ci
```

See [https://github.com/cypress-io/github-action/blob/master/.github/workflows/example-custom-command.yml](https://github.com/cypress-io/github-action/blob/master/.github/workflows/example-custom-command.yml) file.
