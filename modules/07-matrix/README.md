# 07 - Matrix strategies

Matrix jobs let one job definition run with several combinations of values. This is useful for supported language versions, operating systems, browsers, or databases.

## Run on GitHub

Hands-on is on **your personal GitHub repo**, not kubernetes-learn.

- **First time:** create a personal repo and push [`demo-app/`](../../demo-app) — [Run on GitHub](../../RUN-ON-GITHUB.md).
- **Already pushed:** use that **existing** personal repo. Do not create a new GitHub repo for this module.

Copy `matrix.yml` into that repo’s `.github/workflows/` when you want a run. Keep `demo-app` paths as written.

## Exercise

Add Node.js 22 to the matrix. Then use `exclude` to remove one unsupported operating-system/version combination and `include` to add a custom label.
