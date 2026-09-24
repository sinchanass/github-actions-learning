# 01 - Git and GitHub foundation

Before Actions can help, the project needs version control and a collaboration workflow.

## Run on GitHub

Hands-on is on **your personal GitHub repo**, not kubernetes-learn.

- **First time:** create a repository under your personal account and push [`demo-app/`](../../demo-app) so it sits at `demo-app/` on that repo. Full steps: [Run on GitHub](../../RUN-ON-GITHUB.md).
- **Already pushed:** use that **existing** personal repo. Do not create another GitHub repository.

Study notes stay in kubernetes-learn (`github-actions-learning/`).

## Practice

On github.com (personal account): **New repository**, for example `github-actions-learning`. Then, in a **copy** of this lab folder (not inside kubernetes-learn):

```bash
git init
git add .
git commit -m "Start TaskFlow learning lab"
git branch -M main
git remote add origin https://github.com/<your-github-username>/github-actions-learning.git
git push -u origin main
```

Create a feature branch **on that personal repo**, change `demo-app/src/calculator.js`, push it, and open a pull request **there**. Practice reviewing and merging it.

## Concepts

- repositories, commits, branches, remotes, and pull requests
- `.gitignore` and README files
- issues, collaborators, forks, and branch protection
- the difference between `git revert` and rewriting history with `git reset`

## Exercise

Add a `subtract()` function and a test on a feature branch under `demo-app` in the **personal** repo. Open a PR on that repo. To see a CI check, continue with [module 03](../03-ci-pipeline/README.md) and copy `ci.yml` into the personal repo `.github/workflows/`.
