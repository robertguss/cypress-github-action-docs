# Installation

This action installs local dependencies using lock files. If `yarn.lock` file is found, the install uses `yarn --frozen-lockfile` command. Otherwise it expects to find `package-lock.json` and install using `npm ci` command.

This action uses several production dependencies. The minimum Node version required to run this action depends on the minimum Node required by the dependencies.
