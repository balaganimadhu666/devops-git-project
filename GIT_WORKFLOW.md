# Git Workflow – Step by Step

Every command used in this task, in order.

## 0. Prerequisites
```bash
git --version
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```
Create an **empty** repo named `devops-git-project` on GitHub (no README, no .gitignore).

## 1. Initialize repo and push to GitHub (hint a)
Put the project files in a folder, then:
```bash
cd devops-git-project
git init
git branch -M main
git remote add origin https://github.com/<your-username>/devops-git-project.git
```

Make **small, meaningful commits** instead of one big one:
```bash
git add .gitignore requirements.txt
git commit -m "chore: add .gitignore and requirements"

git add README.md CHANGELOG.md
git commit -m "docs: add README and changelog"

git add app/
git commit -m "feat: add Flask app with home and health endpoints"

git add tests/
git commit -m "test: add pytest tests for endpoints"

git add Dockerfile
git commit -m "build: add Dockerfile"

git add .github/
git commit -m "ci: add GitHub Actions workflow"

git add docs/ screenshots/
git commit -m "docs: add git workflow and interview questions"

git push -u origin main
```

## 2. Create the dev branch (hint b)
```bash
git checkout -b dev
git push -u origin dev
```

## 3. Create a feature branch and open a pull request (hints b, c)
```bash
git checkout -b feature/readme-update dev
# make a change, e.g. add a line to README.md
git add README.md
git commit -m "docs: improve README usage section"
git push -u origin feature/readme-update
```
On GitHub:
1. Click **Compare & pull request**
2. Base: `dev` ← Compare: `feature/readme-update`
3. Add title and description, wait for CI to pass
4. **Merge pull request**, then delete the branch

Sync locally:
```bash
git checkout dev
git pull origin dev
git branch -d feature/readme-update
```

## 4. Release: merge dev into main with a pull request (hint c)
On GitHub: **New pull request** → base `main` ← compare `dev` → merge.
```bash
git checkout main
git pull origin main
```

## 5. Tag the release (hint e)
```bash
git tag -a v1.0.0 -m "Release v1.0.0"
git push origin v1.0.0
git tag            # list tags
```
On GitHub: **Releases → Draft a new release → choose v1.0.0**.

## 6. Practice: resolve a merge conflict
```bash
git checkout -b feature/conflict-a dev
# edit line 1 of README.md, commit
git checkout -b feature/conflict-b dev
# edit the SAME line differently, commit
git merge feature/conflict-a      # CONFLICT
```
Open the file, keep the correct version, delete the markers (`<<<<<<<`, `=======`, `>>>>>>>`), then:
```bash
git add README.md
git commit
```
Abort at any time with `git merge --abort`.

## 7. Practice: git stash
```bash
# edit a file but don't commit
git stash push -m "wip: readme tweak"
git stash list
git checkout other-branch
git checkout -
git stash pop
```

## 8. Practice: rebase vs merge
```bash
git checkout feature/readme-update
git rebase dev      # replay your commits on top of latest dev
```
Never rebase branches others are using.

## Useful commands
| Command | Purpose |
|---|---|
| `git status` | Show working tree state |
| `git log --oneline --graph --all` | Visual history |
| `git diff` | Unstaged changes |
| `git branch -a` | List all branches |
| `git restore <file>` | Discard local changes |
| `git revert <commit>` | Undo a commit safely |
