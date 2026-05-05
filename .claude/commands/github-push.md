---
description: Push current project to GitHub — scans for secrets, generates/updates README, configures the remote repo (description, topics, homepage), and pushes.
---

# /github-push

Run a complete "ship to GitHub" flow for the current repository.

Perform the following steps in order. Stop and ask the user if any step needs a decision (e.g. repo name, visibility) — never silently choose.

## 1. Pre-flight safety checks

- Run `git status` and `git rev-parse --show-toplevel` to confirm we're inside a git repo.
- Verify `.gitignore` exists and contains at minimum: `.env`, `node_modules/`, `.DS_Store`. Add any missing entries.
- Scan staged + tracked files for accidentally committed secrets (look for `API_KEY=`, `SECRET=`, `TOKEN=`, `PASSWORD=`, AWS access key patterns `AKIA[0-9A-Z]{16}`, OpenAI keys `sk-[A-Za-z0-9]{20,}`, Resend keys `re_[A-Za-z0-9_]+`, etc).
- If any secrets are found in tracked files, **STOP** and report to the user before proceeding.
- Run `git check-ignore .env` (and any other dotenv files) to confirm they are ignored.

## 2. Generate / update README.md

If `README.md` is missing or stale, generate one covering:

- **Project title** and a one-line tagline
- **Overview** — 2-3 sentences on what the project does
- **Features** — bullet list of key capabilities (inspect the codebase to derive these)
- **Tech stack** — list languages, frameworks, key libraries
- **Project structure** — short tree of the top-level folders with one-line descriptions
- **Getting started** — install + run commands (detect from `package.json`, `requirements.txt`, or static-site indicators)
- **Configuration** — env vars or config files needed (reference `.env.example` if present)
- **Sub-projects** — if multiple apps live in subfolders (e.g. `lead-generation/`, `bride-booking/`), list them with one-line descriptions and links
- **License** — note if a `LICENSE` file is present, else say "All rights reserved" or ask user

Keep it concise — no filler, no emoji unless the user has used them elsewhere in the project.

## 3. Commit any pending changes

- Show `git status` and `git diff --stat` to the user.
- If there are uncommitted changes, ask the user whether to commit them and what message to use.
- Use a HEREDOC for the commit message; include the standard `Co-Authored-By` trailer.
- Never use `--no-verify` or `--amend` unless the user explicitly asks.

## 4. Configure / verify GitHub remote

- Run `git remote -v` to check for an existing `origin`.
- If no remote: ask the user for the repo name (default: current folder name) and visibility (`public` / `private`), then create it with `gh repo create <name> --source=. --remote=origin --<visibility> --push`.
- If a remote exists, skip creation.

## 5. Push

- Determine the current branch with `git rev-parse --abbrev-ref HEAD`.
- Push with `git push -u origin <branch>` (only `-u` if upstream not already set).
- Never force-push without explicit user request.

## 6. Update GitHub repo metadata

Use `gh repo edit` to set:

- **Description** — one-line summary derived from the README tagline (≤ 100 chars).
- **Homepage** — if the project has a deployed URL (Vercel, GitHub Pages, etc.), set it. Otherwise skip.
- **Topics** — 3-8 relevant topics derived from the tech stack and domain (e.g. `javascript`, `vanilla-js`, `lead-generation`, `apify`, `static-site`).

Example:
```bash
gh repo edit --description "<desc>" --add-topic <t1> --add-topic <t2> ...
```

## 7. Final report

Print a short summary to the user:

- Repo URL (`gh repo view --json url -q .url`)
- Branch pushed
- Commit hash
- Topics applied
- Any follow-ups (e.g. "remember to confirm Formsubmit activation email")

## Notes

- Always prefer the dedicated `github-push`, `readme`, and `github-about` skills if they are available — they handle edge cases (auto-detecting deploy URLs, secret scanning patterns) more thoroughly than reimplementing the logic here.
- This command is read-mostly until step 5 — never push or call `gh repo edit` without first showing the user what will change.
