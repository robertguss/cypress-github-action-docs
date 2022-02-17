# Logs from the test runner

The above `ACTIONS_STEP_DEBUG` setting enables the debug logs from the action itself. To see the [Cypress debug logs](http://on.cypress.io/troubleshooting#Print-DEBUG-logs) add an environment variable to the action:

```yml
- name: Cypress tests with debug logs
  uses: cypress-io/github-action@v4
  env:
    DEBUG: "cypress:*"
```
