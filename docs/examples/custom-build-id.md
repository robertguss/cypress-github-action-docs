# Custom build id

You can overwrite [`ci-build-id`](https://on.cypress.io/parallelization#Linking-CI-machines-for-parallelization-or-grouping) used to link separate machines running tests into a single parallel run.

```yml
name: Parallel
on: [push]
jobs:
  test:
    runs-on: ubuntu-20.04
    strategy:
      matrix:
        # run 3 copies of the current job in parallel
        containers: [1, 2, 3]
    steps:
      - uses: actions/checkout@v2
      - uses: cypress-io/github-action@v4
        with:
          record: true
          parallel: true
          group: "Actions example"
          ci-build-id: "${{ github.sha }}-${{ github.workflow }}-${{ github.event_name }}"
        env:
          # pass the Dashboard record key as an environment variable
          CYPRESS_RECORD_KEY: ${{ secrets.CYPRESS_RECORD_KEY }}
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

**Tip:** see GitHub Actions [environment variables](https://help.github.com/en/actions/automating-your-workflow-with-github-actions/using-environment-variables) and [expression syntax](https://help.github.com/en/actions/automating-your-workflow-with-github-actions/contexts-and-expression-syntax-for-github-actions).

## Robust custom build id

If you re-run the GitHub workflow, if you use the same custom build id during recording, the Dashboard will cancel the run with "Build already finished" error. To avoid this, you need to generate a _new_ custom build id on every workflow re-run. A good solution showing in the [example-custom-ci-build-id.yml](./.github/workflows/example-custom-ci-build-id.yml) file is to run a common job first that just generates a new random ID. This ID can be used by the testing jobs to tie the build together. If the user re-runs the workflow a new unique build id is generated, allowing recording the new Dashboard run.

```yml
jobs:
  # single job that generates and outputs a common id
  prepare:
    outputs:
      uuid: ${{ steps.uuid.outputs.value }}
    steps:
      - name: Generate unique ID 💎
        id: uuid
        # take the current commit + timestamp together
        # the typical value would be something like
        # "sha-5d3fe...35d3-time-1620841214"
        run: echo "::set-output name=value::sha-$GITHUB_SHA-time-$(date +"%s")"
  smoke-tests:
    needs: ["prepare"]
    steps:
      - uses: actions/checkout@v2
      - uses: cypress-io/github-action@v4
        with:
          record: true
          parallel: true
          ci-build-id: ${{ needs.prepare.outputs.uuid }}
        env:
          # pass the Dashboard record key as an environment variable
          CYPRESS_RECORD_KEY: ${{ secrets.EXAMPLE_RECORDING_KEY }}
```

See the [example-custom-ci-build-id.yml](./.github/workflows/example-custom-ci-build-id.yml) for the full workflow
