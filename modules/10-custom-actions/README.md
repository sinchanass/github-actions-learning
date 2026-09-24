# 10 - Custom JavaScript action

This module builds a local JavaScript action. It reads the current event, accepts a message input, and uses the GitHub API to create a comment on the current issue or pull request.

The action demonstrates `action.yml`, inputs, outputs, `@actions/core`, `@actions/github`, and event payloads.

## Run on GitHub

Hands-on is on **your personal GitHub repo**, not kubernetes-learn. Copy the action directory into that repo (for example `./modules/10-custom-actions` or `./.github/actions/custom`).

- **First time:** create a personal repo and push [`demo-app/`](../../demo-app) — [Run on GitHub](../../RUN-ON-GITHUB.md).
- **Already pushed:** use that **existing** personal repo. Do not create a new GitHub repo for this module.

Copy `custom-action.yml` to `.github/workflows/custom-action.yml` on the personal repo after reviewing permissions. Point `uses:` at the path **in that repo** and install the action’s npm dependencies there.

## Exercise

Add an output containing the created comment URL. Then change the action so it adds a label instead of a comment.
