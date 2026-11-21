# Task: Push the project to GitHub

## Findings
- Local git repo on `main`, no commits yet, no remote configured.
- Untracked: `index.html`, `css/`, `images/`, `task/`, `CLAUDE.md`, `.sf/`.
- `.sf/` is Salesforce CLI metadata (contains an org ID), unrelated to the website, so it should not be pushed.
- GitHub CLI (`gh`) token for account `AnatoliiA` is **invalid**, so re-login is needed first.

## Checklist
- [ ] User re-authenticates: `! gh auth login -h github.com`
- [ ] Add `.gitignore` excluding `.sf/` (plus OS junk like `Thumbs.db`, `.DS_Store`)
- [ ] Stage website files + `CLAUDE.md` + `task/` + `.gitignore`
- [ ] Create initial commit on `main`
- [ ] Create GitHub repo (name/visibility to be confirmed) and push with `gh repo create --source . --push`
- [ ] Verify: `git remote -v`, `git log`, and open the repo URL
- [ ] Add review section to this file

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
