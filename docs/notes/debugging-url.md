# Debugging waiting for URL to respond

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
