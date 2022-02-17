# Headless

Run the browser in headless mode

```yml
name: Chrome headless
on: [push]
jobs:
  cypress-run:
    runs-on: ubuntu-20.04
    steps:
      - uses: actions/checkout@v2
      - uses: cypress-io/github-action@v4
        with:
          browser: chrome
          headless: true
```
