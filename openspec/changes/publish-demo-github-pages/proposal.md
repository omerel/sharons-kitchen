# Proposal

## Why

The interactive demo in `Sharon_Kitchen_Interactive_Demo_Package/` exists to show the business owners how the ordering system will work, but today it only lives on a local disk and has to be sent around as files. Publishing it on GitHub Pages gives them one link that opens on any phone or computer.

## What Changes

- Move `Sharon_Kitchen_Interactive_Demo_Package/` to `docs/` so GitHub Pages can serve it from `main` / `docs` with no build step or workflow.
- Add `docs/.nojekyll` so Pages serves the files as-is.
- Add a root `.gitignore` that keeps the business documents (`sharons_kitchen_handoff/`, `Sharon_Kitchen_Complete_Specification.pdf`, `Sharon_Kitchen_Complete_Specification.docx`) out of the public repository.
- Make the first commit on `main` with `docs/`, `openspec/`, `.claude/`, `.agents/` and `.gitignore`, and push it to the existing public remote `omerel/sharons-kitchen`.
- Turn on GitHub Pages for the repository (source: `main` branch, `/docs` folder).
- Add a short root `README.md` that links to the live demo URL `https://omerel.github.io/sharons-kitchen/`.

## Capabilities

### New Capabilities
- `demo-site-hosting`: The public hosting of the interactive demo: where it is reachable, what it serves, and which project files must stay out of the public repository.

### Modified Capabilities
<!-- None -->

## Impact

- Repository layout: the demo folder is renamed to `docs/`. Relative links inside the demo are unaffected.
- GitHub: the first push to an empty public repository, plus a Pages setting change on `omerel/sharons-kitchen`.
- Privacy: only the demo (which uses sample data) and the project scaffolding become public. The specification and handoff documents stay local and untracked.
- No application code changes; the demo's behaviour, including `localStorage` persistence and its external Google Fonts and Unsplash images, is unchanged.
