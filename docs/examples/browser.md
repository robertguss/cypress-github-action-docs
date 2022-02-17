# Browser

Specify the browser name or path with `browser` parameter

```yml
name: E2E on Chrome
on: [push]
jobs:
  cypress-run:
    runs-on: ubuntu-20.04
    # let's make sure our tests pass on Chrome browser
    name: E2E on Chrome
    steps:
      - uses: actions/checkout@v2
      - uses: cypress-io/github-action@v4
        with:
          browser: chrome
```

[![Chrome example](https://github.com/cypress-io/github-action/workflows/example-chrome/badge.svg?branch=master)](https://github.com/cypress-io/github-action/blob/master/.github/workflows/example-chrome.yml)
