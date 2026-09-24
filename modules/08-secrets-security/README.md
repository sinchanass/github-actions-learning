# 08 - Secrets and workflow security

Security is part of CI/CD design, not an afterthought.

## Run on GitHub

Hands-on is on **your personal GitHub repo**, not kubernetes-learn.

- **First time:** create a personal repo and push [`demo-app/`](../../demo-app) — [Run on GitHub](../../RUN-ON-GITHUB.md).
- **Already pushed:** use that **existing** personal repo. Do not create a new GitHub repo for this module.

Copy `secure-workflow.yml` into that repo’s `.github/workflows/` when you want a run. Add secrets under **that** personal repo (Settings → Secrets).

## Concepts

- `GITHUB_TOKEN` and explicit permissions
- repository secrets versus environment secrets
- protected environments and approvals
- why secrets must never be echoed
- the danger of running untrusted pull-request code with write permissions
- pinning third-party actions and reviewing action ownership

The example is intentionally conservative: it only reads repository contents. To experiment with deployment, create a `staging` environment and add a harmless secret such as `DEPLOY_TARGET`.

## Exercise

Add `permissions: contents: read` to every read-only workflow. Then explain why a workflow that comments on pull requests needs a different permission from a workflow that only runs tests.
