# 05 - Variables, contexts, expressions, and outputs

Study how values move through a workflow. Contexts are evaluated by GitHub, while shell variables are evaluated by the runner shell.

## Run on GitHub

Hands-on is on **your personal GitHub repo**, not kubernetes-learn.

- **First time:** create a personal repo and push [`demo-app/`](../../demo-app) — [Run on GitHub](../../RUN-ON-GITHUB.md).
- **Already pushed:** use that **existing** personal repo. Do not create a new GitHub repo for this module.

Copy `variables-contexts.yml` into that repo’s `.github/workflows/` when you want a run. Keep `demo-app/package.json` as written.

## Concepts

- workflow, job, and step-level `env`
- the `github`, `runner`, `job`, `steps`, and `needs` contexts
- `${{ }}` expressions and `if` conditions
- step IDs and outputs
- job outputs for passing values between jobs

## Exercise

Change the `prepare` job so it outputs the application version from `demo-app/package.json`. Display that value in the `report` job.
