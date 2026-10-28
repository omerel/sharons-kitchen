# Tasks

## 1. Prepare the repository layout

- [x] 1.1 Move `Sharon_Kitchen_Interactive_Demo_Package/` to `docs/` and verify `docs/index.html`, `docs/styles.css` and `docs/app.js` exist and the old folder is gone
- [x] 1.2 Add an empty `docs/.nojekyll` and verify the file exists
- [x] 1.3 Create a root `.gitignore` listing `sharons_kitchen_handoff/`, `Sharon_Kitchen_Complete_Specification.pdf` and `Sharon_Kitchen_Complete_Specification.docx`, and verify that `git check-ignore` reports all three
- [x] 1.4 Add a short root `README.md` (Hebrew, matching the demo README) that describes the project and links to `https://omerel.github.io/sharons-kitchen/`, and verify the link text and URL are correct
- [x] 1.5 Open `docs/index.html` locally in a browser (or via `python3 -m http.server -d docs`) and verify the demo still loads with styles and works after the move

## 2. Commit and push

- [x] 2.1 Review `.claude/` and `.agents/` for anything sensitive, and verify they contain only skill and command scaffolding
- [x] 2.2 Stage with `git add .` and verify with `git status` that only `docs/`, `openspec/`, `.claude/`, `.agents/`, `.gitignore` and `README.md` are staged and that no excluded document appears
- [ ] 2.3 Create the initial commit on `main` and push to `origin main`, and verify that `gh repo view omerel/sharons-kitchen` shows `main` as the default branch

## 3. Enable GitHub Pages

- [ ] 3.1 Enable Pages from `main` `/docs` via `gh api -X POST repos/omerel/sharons-kitchen/pages -f 'source[branch]=main' -f 'source[path]=/docs'`, and verify that `gh api repos/omerel/sharons-kitchen/pages` reports that source
- [ ] 3.2 Wait for the first build, and verify that `gh api repos/omerel/sharons-kitchen/pages/builds/latest` reports `status: built`

## 4. Verify the live site

- [ ] 4.1 Verify that `https://omerel.github.io/sharons-kitchen/`, `styles.css`, `app.js` and `Sharon_Kitchen_Interactive_Demo.html` each return HTTP 200 (`curl -sI`)
- [ ] 4.2 Verify that `https://github.com/omerel/sharons-kitchen` does not list `sharons_kitchen_handoff/` or the specification PDF/DOCX (`gh api repos/omerel/sharons-kitchen/contents`)

## Workflow follow-up

- Archive the change once the live link has been shared and confirmed working.
