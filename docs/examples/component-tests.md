# Component tests

You can run [Cypress component tests](https://on.cypress.io/component-testing) in a job separate from E2E tests by adding `component: true`:

```yml
- name: Run E2E tests 🧪
  uses: cypress-io/github-action@v4

- name: Run Component tests 🧪
  uses: cypress-io/github-action@v4
  with:
    # we have already installed everything
    install: false
    # to run component tests we need to use "component: true"
    component: true
```

See the example project [component-test](/examples/v10/component-tests/) and the [example-component-test-workflow](.github/workflows/example-component-test.yml) for more details.
