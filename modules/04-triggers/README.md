# 04 - Events and triggers

The same workflow can respond to different GitHub events. Study the branch and path filters, manual inputs, and scheduled execution in `triggers.yml`.

## Run on GitHub

Hands-on is on **your personal GitHub repo**, not kubernetes-learn.

- **First time:** create a personal repo and push [`demo-app/`](../../demo-app) — [Run on GitHub](../../RUN-ON-GITHUB.md).
- **Already pushed:** use that **existing** personal repo. Do not create a new GitHub repo for this module.

Copy `triggers.yml` into that repo’s `.github/workflows/` when you want a run. Keep `demo-app` paths as written.

## Concepts

- `push`, `pull_request`, `workflow_dispatch`, and `schedule`
- branch filters, path filters, and tag filters
- manual input values
- cron schedules, which use UTC

## Exercise

Add a manual input named `message`. Print it from the workflow. Then add a path filter so documentation-only changes do not run the application tests.
