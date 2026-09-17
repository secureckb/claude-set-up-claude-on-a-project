# NOTES.md

## CLAUDE.md

Kept: a one-line description, the three npm commands, two conventions (CommonJS over ESM, one route file per resource mounted in `server.js`, route handlers going through `db/store.js`), and an architecture note on the `require.main` entry-point pattern and the in-memory store.

Left out: a file-by-file directory listing (Claude can already see the tree), generic advice like "write tests" or "handle errors" (not specific to this repo), and anything from `.env.example` beyond naming it (no real config values to document). Shorter felt stronger here — the whole app is four small files.

## .claude/settings.json

- **Allow**: `Bash(npm test:*)` and `Bash(npm run lint:*)` — safe, read-only-effect commands I run constantly; no reason to be prompted every time.
- **Ask**: `Bash(git push:*)` — pushing touches the shared remote, so I want a chance to look at what's about to go out.
- **Deny**: `Read(./.env)` — blocks Claude from ever reading real secrets, even by accident while exploring the repo. `Bash(git push --force:*)` — force-push can overwrite someone else's work on the remote; without this, a confused Claude session could rewrite shared history with no way to undo it.

Verified with `/memory` (shows `CLAUDE.md` loaded) and `/permissions` (shows the allow/ask/deny rules above).
