# Hostinger ERR_REQUIRE_ASYNC_MODULE fix

Hostinger's LiteSpeed Node loader uses `require()` to load the configured entry file.
The previous `server.js` contained a top-level `await import(...)`, which made the ESM graph asynchronous and caused:

`ERR_REQUIRE_ASYNC_MODULE: require() cannot be used on an ESM graph with top-level await`

This build removes the top-level await. The backend is now loaded with a normal dynamic import promise and explicit error handling, so Hostinger can require the entry file successfully.

## Hostinger
- Framework: Express
- Node: 20.x or 22.x
- Root: ./
- Entry/main: server.js
- Build: default / npm install + npm run build
- Start script: npm start

Keep your production environment variables configured in hPanel.
