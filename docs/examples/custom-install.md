# Custom install

Finally, you might not need this GH Action at all. For example, if you want to split the NPM dependencies installation from the Cypress binary installation, then it makes no sense to use this action. Instead you can install and cache Cypress yourself. See [cypress-gh-action-split-install](https://github.com/bahmutov/cypress-gh-action-split-install) for working example.
