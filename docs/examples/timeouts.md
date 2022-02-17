# Timeouts

You can tell the CI to stop the job or the individual step if it runs for longer then a given time limit. This is a good practice to ensure the hanging process does not accidentally use up all your CI minutes.

```yml
jobs:
  cypress-run:
    runs-on: ubuntu-20.04
    # stop the job if it runs over 10 minutes
    # to prevent a hanging process from using all your CI minutes
    timeout-minutes: 10
    steps:
      - uses: actions/checkout@v2
      - uses: cypress-io/github-action@v4
        # you can specify individual step timeout too
        timeout-minutes: 5
```

See [cypress-gh-action-example](https://github.com/bahmutov/cypress-gh-action-example)
