# DevOps Git Project

![CI](https://github.com/<your-username>/devops-git-project/actions/workflows/ci.yml/badge.svg)

A small Flask service used to practice **Git and GitHub best practices**: branching, pull requests, tags, `.gitignore`, CI and documentation.
Built for **Task 4 – DevOps Internship (Elevate Labs)**.

## Objective
Manage a DevOps project using Git best practices.

## Tech Stack
Git · GitHub · GitHub Actions · Python (Flask) · Docker · Markdown

## Project Structure
```
devops-git-project/
├── app/                     # Flask application
├── tests/                   # pytest tests
├── docs/
│   ├── GIT_WORKFLOW.md      # Step-by-step commands used in this task
│   └── INTERVIEW_QUESTIONS.md
├── screenshots/             # Proof of branches, PRs, tags
├── .github/workflows/ci.yml # CI pipeline
├── .gitignore
├── CHANGELOG.md
├── Dockerfile
├── requirements.txt
└── README.md
```

## Run Locally
```bash
git clone https://github.com/<your-username>/devops-git-project.git
cd devops-git-project
python -m venv venv && source venv/bin/activate   # Windows: venv\Scripts\activate
pip install -r requirements.txt
python -m app.app
```
Open http://localhost:5000 and http://localhost:5000/health

## Run Tests
```bash
python -m pytest -v
```

## Run with Docker
```bash
docker build -t devops-git-project .
docker run -p 5000:5000 devops-git-project
```

## Branching Strategy
| Branch | Purpose |
|---|---|
| `main` | Stable, production-ready code. Only updated via pull request from `dev`. Tagged for releases. |
| `dev` | Integration branch. Feature branches merge here via pull request. |
| `feature/*` | One branch per feature or fix, created from `dev`. |

```
feature/health-endpoint ──PR──> dev ──PR──> main ──> tag v1.0.0
```

## What Was Done
- [x] Initialized the repo and pushed to GitHub
- [x] Created `main`, `dev` and `feature/*` branches
- [x] Merged changes using pull requests
- [x] Added this README
- [x] Added `.gitignore` and release tags (`v1.0.0`)
- [x] Documented every step in markdown ([docs/GIT_WORKFLOW.md](docs/GIT_WORKFLOW.md))
- [x] Answered interview questions ([docs/INTERVIEW_QUESTIONS.md](docs/INTERVIEW_QUESTIONS.md))

## Commit Convention
Commits follow [Conventional Commits](https://www.conventionalcommits.org/): `feat:`, `fix:`, `docs:`, `test:`, `build:`, `ci:`, `chore:`.

## Releases
See [CHANGELOG.md](CHANGELOG.md) and the repo's **Releases / Tags** page.

## Author
`<Your Name>` – DevOps Intern, Elevate Labs
