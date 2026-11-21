# Task: Push the project to GitHub

## Findings
- Local git repo on `main`, no commits yet, no remote configured.
- Untracked: `index.html`, `css/`, `images/`, `task/`, `CLAUDE.md`, `.sf/`.
- `.sf/` is Salesforce CLI metadata (contains an org ID), unrelated to the website, so it should not be pushed.
- GitHub CLI (`gh`) token for account `AnatoliiA` is **invalid**, so re-login is needed first.

## Checklist
Decisions: repo `claude-course-2`, **private**, `.sf/` excluded.

- [x] User re-authenticates: `! gh auth login -h github.com`
- [x] Add `.gitignore` excluding `.sf/` (plus OS junk like `Thumbs.db`, `.DS_Store`)
- [x] Stage website files + `CLAUDE.md` + `task/` + `.gitignore`
- [x] Create initial commit on `main` (`60023bf`)
- [x] Create private GitHub repo `claude-course-2` and push with `gh repo create claude-course-2 --private --source . --push`
- [x] Verify: `git remote -v`, `git log`, and open the repo URL
- [x] Add review section to this file

## Review
- **Repo:** https://github.com/AnatoliiA/claude-course-2 (private), with `origin` set and `main` tracking `origin/main`.
- **Added `.gitignore`:** excludes `.sf/` (Salesforce CLI data), `Thumbs.db` and `.DS_Store`.
- **Commits:** the initial commit `60023bf` (website, CSS, images, `CLAUDE.md`, `task/`), then a follow-up commit with this finished checklist.
- **Not pushed:** the `.sf/` folder, which stays on this machine only.

---

# Previous task: Move inline CSS from index.html into an external stylesheet (done)

- [x] Create `task/todo.md` with this checklist
- [x] Create `css/styles.css` holding the full contents of the current `<style>` block, unchanged and in the same order
- [x] In `index.html`, replace the whole `<style>…</style>` block with `<link rel="stylesheet" href="css/styles.css">`, placed after the Google Fonts `<link>`
- [x] Leave the inline `<script>` and the form's `onsubmit` as they are (out of scope)
- [x] Verify: open the page, confirm the styles apply, and confirm no `<style>` tag is left in `index.html`
- [x] Add a review section to this file

## Review
- **New file `css/styles.css` (156 lines):** the CSS copied word for word from the old `<style>` block, in the same order. The only change is that the 4 spaces of indentation it had inside the HTML were removed.
- **`index.html`:** the `<style>…</style>` block is replaced by one line, `<link rel="stylesheet" href="css/styles.css">`, placed after the Google Fonts link. Nothing else changed.
- **Checks:** `index.html` has 0 `<style>` tags left. The page was opened in the browser for a visual check; it should look the same as before.
- **Not changed:** the small inline `<script>` for the scroll fade-in and the form's inline `onsubmit`.
