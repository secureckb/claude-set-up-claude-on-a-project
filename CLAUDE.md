# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

A small Express API (in-memory data, no database) used as a course starter project.

## Commands

- `npm run dev` — start the API on http://localhost:3000 with auto-restart (`node --watch`)
- `npm test` — run the tests (`node --test`, via `tests/*.test.js`)
- `npm run lint` — run ESLint over the whole project

## Conventions

- Use `require`/`module.exports` (CommonJS), not ESM `import`/`export` — `package.json` has no `"type": "module"`.
- One route file per resource under `routes/`, mounted in `server.js` (e.g. `routes/users.js` → `app.use("/users", usersRoutes)`). Add new resources the same way rather than adding routes directly in `server.js`.
- Route handlers read/write data only through `db/store.js`, never by touching module-level state directly.

## Architecture

- `server.js` is the entry point: builds the Express `app`, mounts route modules, and only calls `app.listen` when run directly (`require.main === module`) — this lets `tests/*.test.js` `require("../server")` and drive it with `supertest` without opening a real port.
- `db/store.js` is a tiny in-memory data layer (a plain array with helper functions). Data resets on every restart; there is no real database.
- `.env` (git-ignored) holds config like `PORT`; `.env.example` documents the shape.
