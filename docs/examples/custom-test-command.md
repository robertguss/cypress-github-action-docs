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

See [.github/workflows/example-custom-command.yml](.github/workflows/example-custom-command.yml) file.
