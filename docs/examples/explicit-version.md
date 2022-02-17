# Explicit version

**Best practice:**

Our examples specify the tag of the action to use listing only the major version `@v2`

```yml
- name: Cypress run
  uses: cypress-io/github-action@v4
```

When using `cypress-io/github-action@v4` from your workflow file, you automatically will be using the latest [tagged version from this repository](https://github.com/cypress-io/github-action/tags). If you want to precisely control the version of this module, use the full tag version, for example:

```yml
- name: Cypress run
  uses: cypress-io/github-action@v4.x.x
```

By using the full version tag, you will avoid accidentally using a newer version of the action.
