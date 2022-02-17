# Custom install command

If you want to overwrite the install command

```yml
- uses: cypress-io/github-action@v4
  with:
    install-command: yarn --frozen-lockfile --silent
```

See [example-install-command.yml](.github/workflows/example-install-command.yml) workflow file.
