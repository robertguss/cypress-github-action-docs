# Record test results on Cypress Dashboard

```yml
name: Cypress tests
on: [push]
jobs:
  cypress-run:
    name: Cypress run
    runs-on: ubuntu-20.04
    steps:
      - name: Checkout
        uses: actions/checkout@v2

      - name: Cypress run
        uses: cypress-io/github-action@v4
        with:
          record: true
        env:
          # pass the Dashboard record key as an environment variable
          CYPRESS_RECORD_KEY: ${{ secrets.CYPRESS_RECORD_KEY }}
          # pass GitHub token to allow accurately detecting a build vs a re-run build
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

[![recording example](https://github.com/cypress-io/github-action/workflows/example-recording/badge.svg?branch=master)](.github/workflows/example-recording.yml)

**Tip 1:** We recommend using the action with `on: [push]` instead of `on: [pull_request]` to get the most accurate information related to the commit on the dashboard. With pull requests, the merge commit is created automatically and might not correspond to a meaningful commit in the repository.

**Tip 2:** we recommend passing the `GITHUB_TOKEN` secret (created by the GH Action automatically) as an environment variable. This will allow correctly identifying every build and avoid confusion when re-running a build.

**Tip 3:** if running on `pull_request` event, the commit message is "merge SHA into SHA", which is not what you want probably. You can overwrite the commit message sent to the Dashboard by setting an environment variable. See [issue 124](https://github.com/cypress-io/github-action/issues/124#issuecomment-653180260) for details.

**Tip 4:** to record the project needs `projectId`. Typically this value is saved in the `cypress.json` file. If you want to avoid this, pass the project id using an environment variable:

```yml
name: Cypress tests
on: [push]
jobs:
  cypress-run:
    name: Cypress run
    runs-on: ubuntu-20.04
    steps:
      - name: Checkout
        uses: actions/checkout@v2

      - name: Cypress run
        uses: cypress-io/github-action@v4
        with:
          record: true
        env:
          # pass the Dashboard record key as an environment variable
          CYPRESS_RECORD_KEY: ${{ secrets.CYPRESS_RECORD_KEY }}
          # pass GitHub token to allow accurately detecting a build vs a re-run build
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          # pass the project ID from the secrets through environment variable
          CYPRESS_PROJECT_ID: ${{ secrets.PROJECT_ID }}
```
