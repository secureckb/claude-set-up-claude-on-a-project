# NOTES.md

## CLAUDE.md

I kept it to four short parts: a one-line description, the four commands I actually run (`install`, `dev`, `test`, `lint`), an architecture summary (entry point → routers → store), and two conventions I could read directly off the code (JSON error responses instead of throwing, and all data access going through `db/store.js`).

I deliberately left out:
- The course instructions and submission checklist from `README.md` — that's meta information about the exercise, not something Claude needs to work in the codebase.
- The contents of `.env.example` — there's nothing there Claude needs to act on, and I didn't want to normalize pasting env-shaped content into a file Claude reads on every session.
- Any "tips" or "common tasks" sections — the repo doesn't document any, and I didn't want to invent generic advice that isn't actually true of this project.
- A note that the app code isn't meant to change, so Claude doesn't get "helpful" and start refactoring `server.js` or the routes when the actual task is configuration, not app changes.

Shorter felt stronger here: this is a five-file starter app, so anything longer would just be restating the code.

## .claude/settings.json

- **Allow**: `npm test`, `npm run lint`, `npm run dev` — the three commands I run constantly while iterating, all safe and non-destructive.
- **Ask**: `git push` — I want to confirm before anything leaves my machine, even a normal push.
- **Deny**: reading `.env` (keeps real secrets out of context even if a `.env` ever exists locally), `git push --force`, `git reset --hard`, and `rm -rf` — all destructive/irreversible operations that could lose work or history.

Without the deny rules, a bad prompt or a wrong assumption from Claude (e.g. "let me clean this up" or "let me force-push to fix that") could silently wipe local changes, rewrite shared branch history, or leak a secret from `.env` into the conversation. The `ask` rule on `git push` is a lighter guard — pushing itself isn't destructive, but I still want visibility before it happens.
