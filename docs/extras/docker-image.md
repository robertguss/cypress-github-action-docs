# Docker image

If your repository does not have `package.json` or `yarn.json` (maybe it contains a static site and does not need any dependencies), you can run Cypress tests using `cypress/included:...` [Cypress Docker images](https://github.com/cypress-io/cypress-docker-/img/tree/master/included). In that case you don't even need this GH Action, instead use the Docker container and write `cypress run` command like this example from [cypress-gh-action-included](https://github.com/bahmutov/cypress-gh-action-included)

```yml
name: included
on: [push]
jobs:
  cypress-run:
    runs-on: ubuntu-latest
    # Docker image with Cypress pre-installed
    # https://github.com/cypress-io/cypress-docker-/img/tree/master/included
    container: cypress/included:3.8.3
    steps:
      - uses: actions/checkout@v2
      - run: cypress run
```
