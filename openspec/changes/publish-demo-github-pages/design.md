# Design

## Context

- The demo is fully static: `index.html` loads `styles.css` and `app.js` by relative path; `Sharon_Kitchen_Interactive_Demo.html` is the same app in a single file. State lives in `localStorage`; the only external requests go to Google Fonts and Unsplash images (with emoji fallbacks).
- The local repository has no commits yet. The remote `git@github.com:omerel/sharons-kitchen.git` exists, is public and empty. `gh` is authenticated as `omerel`.
- No `.gitignore` exists, so a plain `git add .` would stage the business documents.

## Goals / Non-Goals

**Goals:**
- A working public link to the demo with the least moving parts.
- Business documents physically excluded from git, not just left out of one commit.

**Non-Goals:**
- Custom domain, analytics, or `noindex` handling.
- Editing the demo's code or content (for example, replacing Unsplash images with local copies).
- Making the repository private or splitting the demo into its own repository.

## Decisions

- **Serve from `main` / `docs` instead of an Actions workflow.** Pages serves `/docs` natively, so there is no workflow file to maintain. Alternative considered: keep the folder name and deploy it with `actions/deploy-pages`. That works too, but adds CI for a folder of static files.
- **Move the folder with `git mv` after the initial add, or a plain `mv` before it.** Since there is no history yet, a plain `mv Sharon_Kitchen_Interactive_Demo_Package docs` is enough.
- **Add `docs/.nojekyll`.** Pages runs Jekyll on `/docs` by default. Nothing breaks today, but disabling it means files are served exactly as committed, and a future `_`-prefixed file won't silently disappear.
- **Leave `docs/README.md` and `docs/CLAUDE_DEMO_IMPLEMENTATION.md` in place.** `index.html` takes precedence at the site root, and the README still documents the demo when someone browses the folder on GitHub.
- **Exclude documents with `.gitignore`.** The entries are `sharons_kitchen_handoff/`, `Sharon_Kitchen_Complete_Specification.pdf` and `Sharon_Kitchen_Complete_Specification.docx`. This protects future commits too, which leaving them out of one commit would not.
- **Enable Pages through the API:** `gh api -X POST repos/omerel/sharons-kitchen/pages -f 'source[branch]=main' -f 'source[path]=/docs'`. This is scriptable and verifiable, with Settings → Pages as a manual fallback.

## Risks / Trade-offs

- [The push to a public repo is outward-facing and hard to undo] → Before pushing, review the staged file list with `git status` and confirm that none of the excluded documents are staged.
- [The demo's sample data or images could be mistaken for real business details] → The demo already labels itself as a demo with sample data; no change.
- [The first Pages build takes a minute or two, so the URL can briefly return 404] → Poll `gh api repos/omerel/sharons-kitchen/pages/builds/latest` until the status is `built` before checking the URL.
- [`.claude/` and `.agents/` become public] → They contain only OpenSpec skill and command scaffolding; check them for anything sensitive before the push.

## Migration Plan

1. Move the folder, add `.nojekyll`, `.gitignore` and the root README.
2. Make the initial commit on `main`, review the staged files, and push.
3. Enable Pages and wait for the first build.
4. Rollback: disable Pages with `gh api -X DELETE repos/omerel/sharons-kitchen/pages`. Removing files that were already pushed requires rewriting history, which is why the review before the push matters.
