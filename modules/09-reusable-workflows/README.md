# 09 - Reusable workflows and composite actions

Reusable workflows share complete jobs across repositories. Composite actions share a sequence of steps inside a single action interface.

Study both YAML files. `reusable-workflow.yml` is the provider and `caller.yml` invokes it with inputs.

## Run on GitHub

Hands-on is on **your personal GitHub repo**, not kubernetes-learn.

- **First time:** create a personal repo and push [`demo-app/`](../../demo-app) — [Run on GitHub](../../RUN-ON-GITHUB.md).
- **Already pushed:** use that **existing** personal repo. Do not create a new GitHub repo for this module.

Copy both YAML files into that repo’s `.github/workflows/`. Point `uses:` at `owner/personal-repo/.github/workflows/reusable-workflow.yml@ref` for **your** account. Keep `demo-app` paths as written.

## Exercise

Add an input named `node-version`, pass it from the caller, and expose the test result as a workflow output.
