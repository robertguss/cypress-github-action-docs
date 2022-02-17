# Artifacts

If you don't record the test run on Cypress Dashboard, you can still store generated videos and screenshots as CI artifacts. See [cypress-gh-action-example](https://github.com/bahmutov/cypress-gh-action-example) and the workflow example below

```yml
name: Artifacts
on: [push]
jobs:
  cypress-run:
    runs-on: ubuntu-20.04
    name: Artifacts
    steps:
      - uses: actions/checkout@v2
      - uses: cypress-io/github-action@v4
      # after the test run completes
      # store videos and any screenshots
      # NOTE: screenshots will be generated only if E2E test failed
      # thus we store screenshots only on failures
      # Alternative: create and commit an empty cypress/screenshots folder
      # to always have something to upload
      - uses: actions/upload-artifact@v2
        if: failure()
        with:
          name: cypress-screenshots
          path: cypress/screenshots
      # Test run video was always captured, so this action uses "always()" condition
      - uses: actions/upload-artifact@v2
        if: always()
        with:
          name: cypress-videos
          path: cypress/videos
```
