# 06 - Job dependencies, caching, and artifacts

Jobs run in parallel by default. Use `needs` when one job requires the result of another. Caches speed up repeated dependency installation; artifacts preserve files produced by a run.

## Run on GitHub

Hands-on is on **your personal GitHub repo**, not kubernetes-learn.

- **First time:** create a personal repo and push [`demo-app/`](../../demo-app) — [Run on GitHub](../../RUN-ON-GITHUB.md).
- **Already pushed:** use that **existing** personal repo. Do not create a new GitHub repo for this module.

Copy `artifacts-and-cache.yml` into that repo’s `.github/workflows/` when you want a run. Artifacts use `demo-app/dist`.

## Exercise

Make the `test` job depend on `build`. Upload the generated `demo-app/dist` directory and download it in a separate `inspect` job.
