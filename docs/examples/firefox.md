# Firefox

In order to run Firefox, you need to use non-root user (Firefox security restriction).

```yml
name: Firefox
on: push
jobs:
  firefox:
    runs-on: ubuntu-latest
    container:
      image: cypress/browsers:node12.16.1-chrome80-ff73
      options: --user 1001
    steps:
      - uses: actions/checkout@v2
      - uses: cypress-io/github-action@v4
        with:
          browser: firefox
```

[![Firefox example](https://github.com/cypress-io/github-action/workflows/example-firefox/badge.svg?branch=master)](https://github.com/cypress-io/github-action/blob/master/.github/workflows/example-firefox.yml)

**Note:** the magical user id `1001` works because it matches permissions settings on the home folder, see issue [#104](https://github.com/cypress-io/github-action/issues/104)
