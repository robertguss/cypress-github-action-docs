# Outputs

This GH Action sets an output `dashboardUrl` if the run was recorded on [Cypress Dashboard](https://on.cypress.io/dashboard-introduction), see [action.yml](action.yml). To use this output:

```yml
- name: Cypress tests
  uses: cypress-io/github-action@v4
  # let's give this action an ID so we can refer
  # to its output values later
  id: cypress
  # Continue the build in case of an error, as we need to set the
  # commit status in the next step, both in case of success and failure
  continue-on-error: true
  with:
    record: true
  env:
    CYPRESS_RECORD_KEY: ${{ secrets.RECORDING_KEY }}
- name: Print Dashboard URL
  run: |
    echo Cypress finished with: ${{ steps.cypress.outcome }}
    echo See results at ${{ steps.cypress.outputs.dashboardUrl }}
```

[![recording example](https://github.com/cypress-io/github-action/workflows/example-recording/badge.svg?branch=master)](.github/workflows/example-recording.yml)

**Note:** every GH workflow step can have `outcome` and `conclusion` properties. See the documentation at [steps context](https://docs.github.com/en/actions/reference/context-and-expression-syntax-for-github-actions#steps-context) page. In particular, the `output` value can be `success`, `failure`, `cancelled`, or `skipped` which you can use the next steps that follow.
