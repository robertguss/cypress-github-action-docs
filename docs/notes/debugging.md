# Debugging

This action uses the [debug](https://github.com/visionmedia/debug#readme) module to output additional verbose logs. You can see these debug messages by setting the following environment variable:

```
DEBUG: @cypress/github-action
```

You can set the environment variable using GitHub UI interface, or in the workflow file:

```yml
- name: Cypress tests with debug logs
  uses: cypress-io/github-action@v4
  env:
    DEBUG: "@cypress/github-action"
```

See the [example-debug.yml](https://github.com/cypress-io/github-action/blob/master/.github/workflows/example-debug.yml) workflow file.
