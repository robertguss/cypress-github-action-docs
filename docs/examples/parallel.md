# Parallel

**Note:** Cypress parallelization requires [Cypress Dashboard](https://on.cypress.io/dashboard-introduction) account.

You can spin multiple containers running in parallel using `strategy: matrix` argument. Just add more dummy items to the `containers: [1, 2, ...]` array to spin more free or paid containers. Then use `record` and `parallel` parameters to [load balance tests](https://on.cypress.io/parallelization)

```yml
name: Parallel Cypress Tests

on: [push]

jobs:
  test:
    name: Cypress run
    runs-on: ubuntu-20.04
    strategy:
      # when one test fails, DO NOT cancel the other
      # containers, because this will kill Cypress processes
      # leaving the Dashboard hanging ...
      # https://github.com/cypress-io/github-action/issues/48
      fail-fast: false
      matrix:
        # run 3 copies of the current job in parallel
        containers: [1, 2, 3]
    steps:
      - name: Checkout
        uses: actions/checkout@v2

      # because of "record" and "parallel" parameters
      # these containers will load balance all found tests among themselves
      - name: Cypress run
        uses: cypress-io/github-action@v4
        with:
          record: true
          parallel: true
          group: "Actions example"
        env:
          # pass the Dashboard record key as an environment variable
          CYPRESS_RECORD_KEY: ${{ secrets.CYPRESS_RECORD_KEY }}
          # Recommended: pass the GitHub token lets this action correctly
          # determine the unique run id necessary to re-run the checks
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

![Parallel run](/img/parallel.png)

**Warning ⚠️:** Cypress actions use `GITHUB_TOKEN` to get the correct branch and the number of jobs run, making it possible to re-run without the need of pushing an empty commit. If you don't want to use the `GITHUB_TOKEN` you can still run your tests without problem with the only note that Cypress Dashboard API connects parallel jobs into a single logical run using GitHub commit SHA plus workflow name. If you attempt to re-run GitHub checks, the Dashboard thinks the run has already ended. In order to truly rerun parallel jobs, push an empty commit with `git commit --allow-empty -m "re-run checks" && git push`. As another work around you can generate and cache a custom build id, read [Adding a unique build number to GitHub Actions](https://medium.com/attest-engineering/adding-a-unique-github-build-identifier-7aa2e83cadca)

The Cypress GH Action does not spawn or create any additional containers - it only links the multiple containers spawned using the matrix strategy into a single logical Dashboard run and into splitting the specs amongst the machines. See the [Cypress parallelization](https://on.cypress.io/parallelization) guide for the explanation.
