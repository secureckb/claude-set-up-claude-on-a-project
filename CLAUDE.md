# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

A starter Express API used for a Claude Code course exercise. It exposes `/health` and `/users` endpoints backed by an in-memory store (no real database, no persistence).

The app code itself (`server.js`, `routes/`, `db/`) is not meant to be changed — it exists only to give Claude a real codebase to be configured against. Work in this repo is about `CLAUDE.md` and `.claude/settings.json`, not the API.

## Commands

- `npm install` — install dependencies
- `npm run dev` — start the API on http://localhost:3000 with `--watch` (auto-restart on change)
- `npm test` — run tests (`node --test`, via `tests/*.test.js`)
- `npm run lint` — run ESLint (`eslint .`)

To run a single test file: `node --test tests/users.test.js`

## Architecture

- `server.js` — entry point; builds the Express app, mounts routers, starts listening. Exports `app` without starting the server when required (not run directly), so tests can import it via `supertest` without binding a real port.
- `routes/` — one router file per resource (`users.js`, `health.js`), mounted in `server.js` under `/users` and `/health`.
- `db/store.js` — in-memory data access layer; all data resets on restart. Routes call into this module rather than manipulating data directly.
- `tests/` — one `*.test.js` file per resource, using Node's built-in `node:test` + `supertest` against the exported `app`.

## Conventions

- Routes validate input and return JSON error bodies (`{ error: "..." }`) with the appropriate status code (400, 404) rather than throwing.
- Data access goes through `db/store.js`; route handlers do not touch the `users` array directly.
- Real secrets go in `.env` (git-ignored); `.env.example` documents the shape but is never given real values.
