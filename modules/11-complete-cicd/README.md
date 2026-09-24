# 11 - Complete CI/CD pipeline

This final example combines validation, packaging, artifacts, and release automation. It is manual by default so you can inspect it before enabling tag-based releases.

## Run on GitHub

Hands-on is on **your personal GitHub repo**, not kubernetes-learn.

- **First time:** create a personal repo and push [`demo-app/`](../../demo-app) — [Run on GitHub](../../RUN-ON-GITHUB.md).
- **Already pushed:** use that **existing** personal repo. Do not create a new GitHub repo for this module.

Copy `release.yml` into that repo’s `.github/workflows/` when you want a run. Keep `demo-app` packaging paths as written. Prefer `workflow_dispatch` until you understand release permissions.

## Concepts

- gating release jobs with `needs`
- creating a distributable npm tarball
- uploading and downloading artifacts
- tag-based releases
- permissions required to create a GitHub release
- separating build, approval, and deployment concerns

## Exercise

Create a Git tag such as `v1.0.0`, run the workflow manually, and compare the uploaded artifact with the source repository. Only after understanding the permissions should you enable the `push.tags` trigger.
