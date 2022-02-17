## Notes

### Installation

This action installs local dependencies using lock files. If `yarn.lock` file is found, the install uses `yarn --frozen-lockfile` command. Otherwise it expects to find `package-lock.json` and install using `npm ci` command.

This action uses several production dependencies. The minimum Node version required to run this action depends on the minimum Node required by the dependencies.

## Debugging

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

See the [example-debug.yml](./.github/workflows/example-debug.yml) workflow file.

### Logs from the test runner

The above `ACTIONS_STEP_DEBUG` setting enables the debug logs from the action itself. To see the [Cypress debug logs](http://on.cypress.io/troubleshooting#Print-DEBUG-logs) add an environment variable to the action:

```yml
- name: Cypress tests with debug logs
  uses: cypress-io/github-action@v4
  env:
    DEBUG: "cypress:*"
```

### Debugging waiting for URL to respond

If you have a problem with `wait-on` not working, you can check the [src/ping.js](src/ping.js) logic from the local machine.

- clone this repository to the local machine
- install dependencies with `npm install`
- start your server
- from another terminal call the `ping` yourself to validate the server is responding:

```
$ node src/ping-cli.js <url>
```

For example

```
$ node src/ping.js https://example.cypress.io
pinging url https://example.cypress.io for 30 seconds
::debug::pinging https://example.cypress.io has finished ok
```

## Development

Read [DEVELOPMENT.md](DEVELOPMENT.md)

## More information

- Read our blog post [Drastically Simplify Testing on CI with Cypress GitHub Action](https://www.cypress.io/blog/2019/11/20/drastically-simplify-your-testing-with-cypress-github-action/)
- Read [Test the Preview Vercel Deploys](https://glebbahmutov.com/blog/develop-preview-test/) blog post
- [Building actions](https://help.github.com/en/actions/automating-your-workflow-with-github-actions/building-actions) docs
- practice using the Cypress GitHub Action by following the [Cypress on CI Workshop](https://github.com/cypress-io/cypress-workshop-ci)

## Extras

### Manual trigger

If you add `workflow_dispatch` event to your workflow, you will be able to start the workflow by clicking a button on the GitHub page, see the [Test External Site Using GitHub Actions](https://www.youtube.com/watch?v=4TeSOj2Iy_Q) video.

### Outputs

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

### Docker image

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

### Print Cypress info

Sometimes you might want to print Cypress and OS information, like the list of detected browsers. You can use the [`cypress info`](https://on.cypress.io/command-line#cypress-info) command for this.

If you are NOT using the `build` command in your project, you can run the `cypress info` command:

```yml
name: info
on: [push]
jobs:
  cypress-run:
    runs-on: ubuntu-20.04
    steps:
      - name: Checkout
        uses: actions/checkout@v2
      - name: Cypress run
        uses: cypress-io/github-action@v4
        with:
          build: npx cypress info
```

If you are already using the `build` parameter, you can split the [installation and the test steps](#split-install-and-tests) and insert the `cypress info` command in between:

```yml
name: info
on: [push]
jobs:
  cypress-run:
    runs-on: ubuntu-20.04
    steps:
      - name: Checkout
        uses: actions/checkout@v2
      - name: Cypress install
        uses: cypress-io/github-action@v4
        with:
          # just perform install
          runTests: false
      - name: Cypress info
        run: npx cypress info
      - name: Cypress run
        uses: cypress-io/github-action@v4
        with:
          # we have already installed all dependencies above
          install: false
          # rest of your parameters
```

### Nightly tests

Sometimes you want to execute the workflow on a schedule. For example, to run Cypress tests nightly, you can schedule the workflow using `cron` syntax:

```yml
name: example-cron
on:
  schedule:
    # runs tests every day at 4am
    - cron: "0 4 * * *"
jobs:
  nightly:
    runs-on: ubuntu-20.04
    steps:
      - name: Checkout
        uses: actions/checkout@v2
      - name: Cypress nightly tests 🌃
        uses: cypress-io/github-action@v4
```

See the [example-cron.yml](./.github/workflows/example-cron.yml) workflow.

[![cron example](https://github.com/cypress-io/github-action/workflows/example-cron/badge.svg?branch=master)](.github/workflows/example-cron.yml)

## Migration guide

### v1 to v2

This is noted as a breaking change ... but you should not see any changes. We have changed how we run Cypress (from using the command line to using the [NPM module API](https://on.cypress.io/module-api)), which is a big change. But hopefully our examples are complete and we did not break anyone's code.

## License

[MIT License](./LICENSE.md)

[renovate-badge]: https://img.shields.io/badge/renovate-app-blue.svg
[renovate-app]: https://renovateapp.com/
