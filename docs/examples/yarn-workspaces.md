# Yarn workspaces

This action should discover Yarn workspace correctly. For example, see folder [examples/start-and-yarn-workspaces](https://github.com/cypress-io/github-action/tree/master/examples/start-and-yarn-workspaces) and workflow file [example-start-and-yarn-workspaces.yml](https://github.com/cypress-io/github-action/blob/master/.github/workflows/example-start-and-yarn-workspaces.yml)

```yaml
name: example-start-and-yarn-workspaces
on: [push]
jobs:
  single:
    # the example has Yarn workspace in its "root" folder
    # examples/start-and-yarn-workspaces
    # and tests in a subfolder like "workspace-1"
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: cypress-io/github-action@v4
        with:
          working-directory: examples/start-and-yarn-workspaces/workspace-1
          build: yarn run build
          start: yarn start
          wait-on: "http://localhost:5000"
```

[![Yarn workspaces example](https://github.com/cypress-io/github-action/workflows/example-start-and-yarn-workspaces/badge.svg?branch=master)](https://github.com/cypress-io/github-action/blob/master/.github/workflows/example-start-and-yarn-workspaces.yml)
