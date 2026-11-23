# Task: Keep `git.md` out of Git and expand `.gitignore`

Approved by the user, including the `.history/` option.

## Findings
- `git.md` is **untracked** (never committed or staged), so `git rm --cached git.md` would fail with "pathspec did not match". Ignoring it in `.gitignore` is enough.
- The current `.gitignore` has `.sf/`, `Thumbs.db` and `.DS_Store`. The pasted list doesn't include `.sf/`, but it must stay because that folder holds Salesforce org data.

## Checklist
- [x] Merge the pasted rules into `.gitignore`: keep `.sf/`, add every pasted section, and don't duplicate `Thumbs.db` or `.DS_Store`
- [x] Add `.history/` and unstage the 7 `.history/CLAUDE_*.md` files with `git restore --staged .history`
- [x] Verify: `git check-ignore -v git.md` shows the rule, and `git status` no longer lists `git.md`
- [x] Check that no tracked file is now ignored (`git ls-files -ci --exclude-standard`)
- [x] Security review, then add a review section to this file
- No commit or push unless asked

## Review
- **`.gitignore`:** now holds `.sf/` (kept), `git.md`, `.history/`, plus all the pasted sections: temp files, logs, cache, IDE settings, OS files, env/secrets (with `!.env.example` allowed) and build and temp directories. `Thumbs.db` and `.DS_Store` appear only once.
- **`git.md`:** ignored by `.gitignore` line 5. It stays on disk and no longer shows in `git status`. `git rm --cached` wasn't needed because the file was never tracked.
- **`.history/`:** the 7 backup files are unstaged and ignored. They are still on disk.
- **Checks:** `git ls-files -ci --exclude-standard` returns nothing, so no committed file is affected by the new rules. `git status` shows only `.gitignore` and `task/todo.md` (modified) and `CLAUDE.md` (staged by the user earlier).
- **Security:** the new `.env` / `.env.*` rules guard against committing secrets. Nothing sensitive was added to any file.
- **Not done:** no commit or push.

---

# Previous task: Create `git.md` Git management guide (done)

Approved by the user ("yes go ahead").

- [x] Create `git.md` at the repo root with these sections:
  - [x] Branch management: create, switch, merge and delete branches (local and remote)
  - [x] Naming conventions: `main` is the main branch, `feature/feature-name` for new features (lowercase, hyphens)
  - [x] Feature workflow: branch from an up-to-date `main`, commit, keep the branch in sync, merge back into `main`, push, clean up
  - [x] Verification commands, each with an example and sample output: `git status`, `git diff`, `git diff --staged`, `git log --oneline`, `git branch`, `git branch -a`
  - [x] Quick-reference table at the end
- [x] Security review: no personal data (emails, tokens) in the examples
- [x] Add a review section to this file
- Not included: committing or pushing. The repo is public and served on GitHub Pages, so this only happens if the user asks.

## Review
- **New file `git.md`** at the repo root, with 5 sections and a table of contents:
  1. **Branch management:** create (`git switch -c`), switch (`git switch`, `git switch -`, `git stash`), merge (fast-forward vs three-way, `--no-ff`, resolving conflicts, `--abort`), delete (`-d`, `-D`, the remote branch) and rename (`-m`).
  2. **Naming conventions:** `main` and `feature/feature-name`, with a table of good and bad names.
  3. **Feature workflow:** 7 steps from updating `main` to cleaning up, with both a local merge and a GitHub PR as ways to merge. Also includes commit-message tips and a note that pushing `main` re-deploys GitHub Pages.
  4. **Verification commands:** all 6 requested commands, each with an explanation, an example and sample output, plus useful variations (`-s`, `-v`, `--graph --all`, `main..HEAD`, `-r`, `--merged`, `fetch --prune`).
  5. **Quick-reference table.**
- **Security review:** a grep for emails, tokens, passwords, usernames and personal paths found nothing. The only `@` characters are diff hunk headers (`@@`). All hashes, file names and sample output are made up.
- **Not changed:** no other files except this log. Nothing was committed or pushed.

---

# Previous task: Enable GitHub Pages (done)

Approved by the user ("yes enable GitHub Pages").

- [x] Enable Pages via the API, serving from branch `main`, folder `/` (root, where `index.html` lives)
- [x] Wait for the first build to finish (status `built`)
- [x] Verify the live URL returns the page, and that the CSS and images load (all HTTP 200)
- [x] Add a review section, then commit and push this file

## Review
- **Live site:** https://anatoliia.github.io/claude-course-2/
- **How it's published:** from `main` at the repo root, with no build step. Each push to `main` re-deploys automatically within a minute or two.
- **Checked:** `/`, `/css/styles.css`, `/images/hero.svg` and `/images/app-mockup.svg` all return HTTP 200, so the relative paths work under the `/claude-course-2/` subpath.

---

# Previous task: Make the GitHub repo public (done)

## Findings
- Repo `AnatoliiA/claude-course-2` is currently private.
- Pre-publish scan: no secrets, tokens or Salesforce org IDs in tracked files.
- Both commits carry the author email `kamaralia@gmail.com`, which becomes publicly visible once the repo is public.

## Checklist
- [x] User approves: hide the email first, then make the repo public
- [x] Set this repo's `user.email` to `13355525+AnatoliiA@users.noreply.github.com`
- [x] Rewrite the existing commits' author/committer email to the noreply address, keeping their dates
- [x] Check that no commit still uses the old email, then force-push `main`
- [x] Run `gh repo edit AnatoliiA/claude-course-2 --visibility public --accept-visibility-change-consequences`
- [x] Verify with `gh repo view --json visibility` (shows `PUBLIC`)
- [x] Add a review section, then commit and push this file

## Review
- **Commits rewritten:** both commits (now `1021279` and `f1b27fb`) use the noreply email instead of the personal one. Their content and dates are unchanged, and `main` was force-pushed.
- **Future commits:** the local git config for this repo (`user.email`) is set to the noreply address, so they won't expose the personal email either. The global git config is unchanged.
- **Visibility:** the repo is now **public** at https://github.com/AnatoliiA/claude-course-2.
- **For the user:** turn on GitHub Settings → Emails → "Keep my email addresses private" (and optionally "Block command line pushes that expose my email").

---

# Previous task: Push the project to GitHub (done)

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
- [x] Create initial commit on `main` (`1021279`; originally `60023bf`, its ID changed when the commit emails were rewritten)
- [x] Create private GitHub repo `claude-course-2` and push with `gh repo create claude-course-2 --private --source . --push`
- [x] Verify: `git remote -v`, `git log`, and open the repo URL
- [x] Add review section to this file

## Review
- **Repo:** https://github.com/AnatoliiA/claude-course-2 (private), with `origin` set and `main` tracking `origin/main`.
- **Added `.gitignore`:** excludes `.sf/` (Salesforce CLI data), `Thumbs.db` and `.DS_Store`.
- **Commits:** the initial commit `1021279` (website, CSS, images, `CLAUDE.md`, `task/`), then a follow-up commit with this finished checklist.
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
