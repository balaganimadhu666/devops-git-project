# Interview Questions & Answers

## 1. What is Git?
Git is a free, open-source **distributed version control system** created by Linus Torvalds in 2005. It tracks changes to files, lets many people work on the same codebase, and keeps the full history on every developer's machine. **GitHub** is a hosting service for Git repositories; Git and GitHub are not the same thing.

## 2. What is the difference between merge and rebase?
| | `git merge` | `git rebase` |
|---|---|---|
| What it does | Combines two branches with a **merge commit** | **Replays** your commits on top of another branch |
| History | Preserved as-is, non-linear | Rewritten, linear |
| Commit hashes | Unchanged | New hashes |
| Safe on shared branches? | Yes | No – never rebase public branches |

```bash
git checkout main && git merge feature      # merge
git checkout feature && git rebase main     # rebase
```

## 3. What is a pull request?
A pull request (PR) is a GitHub feature that asks maintainers to **merge one branch into another**. It enables code review, comments, automated CI checks and approvals before the code reaches `dev` or `main`.

## 4. How do you resolve merge conflicts?
1. Run `git status` to see conflicted files.
2. Open each file and find the markers `<<<<<<<`, `=======`, `>>>>>>>`.
3. Edit the file to keep the correct code and remove the markers.
4. `git add <file>`
5. `git commit` (or `git rebase --continue` if rebasing).

Use `git merge --abort` to cancel. Tools like VS Code's merge editor help.

## 5. What are Git tags?
Tags are **named pointers to a specific commit**, mostly used to mark releases (e.g. `v1.0.0`).
- **Lightweight:** `git tag v1.0.0`
- **Annotated** (recommended, stores author, date, message): `git tag -a v1.0.0 -m "Release"`
- Push: `git push origin v1.0.0` or `git push --tags`

## 6. What is Git workflow?
A Git workflow is an agreed way a team uses branches and merges. Common ones:
- **Feature Branch workflow:** each feature in its own branch, merged via PR.
- **Gitflow:** `main`, `dev`, `feature/*`, `release/*`, `hotfix/*`.
- **GitHub Flow:** short-lived branches off `main`, merged via PR.
- **Trunk-based:** very short-lived branches, frequent merges to one trunk.

This project uses `feature/*` → `dev` → `main`.

## 7. Explain git stash.
`git stash` temporarily shelves **uncommitted changes** so you get a clean working directory, e.g. to switch branches urgently.
```bash
git stash push -m "message"   # save changes
git stash list                # view stashes
git stash pop                 # re-apply and remove latest stash
git stash apply               # re-apply, keep stash
git stash drop                # delete a stash
git stash -u                  # include untracked files
```

## 8. What is the use of .gitignore?
`.gitignore` lists files and folders Git should **not track**: secrets (`.env`), dependencies (`node_modules`, `venv`), build output, logs, OS and IDE files. It keeps the repo clean and prevents leaking credentials.
It does not affect files already tracked; remove them with `git rm --cached <file>`.
