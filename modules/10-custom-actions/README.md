# 10 - Custom actions

Three kinds of actions: **JavaScript** (`using: node20`), **Docker** (`using: docker`), and **composite** (`using: composite`, module 09). This module builds a **local JS** action that comments on an issue or PR via the GitHub API, and a small **Docker** action that greets from a container.

Files: [`action.yml`](action.yml), [`index.js`](index.js), [`custom-action.yml`](custom-action.yml), [`docker-action/action.yml`](docker-action/action.yml), [`docker-action.yml`](docker-action.yml).

## Run on GitHub

Hands-on: [auxislabs/github-actions-learning](https://github.com/auxislabs/github-actions-learning). Keep the action directory in that repo (copy `modules/10-custom-actions/` or the whole lab). Copy `custom-action.yml` to `.github/workflows/` after reviewing **permissions**.

The workflow `uses: ./modules/10-custom-actions` and runs `npm install --ignore-scripts` there first.

Copy `docker-action.yml` to `.github/workflows/docker-action.yml` as well. It calls `uses: ./modules/10-custom-actions/docker-action`, so that folder stays in the repo. Run it with **Run workflow**. It only needs `contents: read`.

[Run on GitHub](../../RUN-ON-GITHUB.md).

## Exercise

Add an output with the created comment URL (`core.setOutput`). Then change the action to add a **label** instead of a comment (`issues.addLabels`).

---

## `action.yml`

```yaml
name: TaskFlow comment action
inputs:
  message:
    required: true
runs:
  using: node20
  main: index.js
```

Inputs → `core.getInput('message')`. Outputs → `core.setOutput`. Fail → `core.setFailed`.

---

## The workflow

Triggers: `issues: types: [opened]` and `pull_request: types: [opened]` (module 04 catalog).

```yaml
permissions:
  issues: write
  pull-requests: write
  contents: read
```

Tests-only CI must **not** have these write permissions (module 08).

`GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}` is passed into the action so Octokit can call the API.

---

## Docker action

[`docker-action/action.yml`](docker-action/action.yml) sets `using: docker` and `image: Dockerfile`. GitHub builds that image and runs [`entrypoint.sh`](docker-action/entrypoint.sh) inside it. `args` passes `who-to-greet` as `$1`. The script writes `greeting` to `GITHUB_OUTPUT`.

```yaml
runs:
  using: docker
  image: Dockerfile
  args:
    - ${{ inputs.who-to-greet }}
```

[`docker-action.yml`](docker-action.yml) calls the **folder**, the same way every action is called:

```yaml
- id: greet
  uses: ./modules/10-custom-actions/docker-action
  with:
    who-to-greet: TaskFlow
- run: echo "${{ steps.greet.outputs.greeting }}"
```

The image runs as UID 1001, the GitHub-hosted runner user, so the entrypoint can append to `GITHUB_OUTPUT`. The workflow does not pass `using`. That value stays in `action.yml`.

---

## Map onto kubernetes-learn

You do not ship a custom JS action there. You call **reusable actions** (`actions/checkout`, `setup-java`, `cisco-actions/docker-build-push-action`). Same interface: `uses:` + `with:` + `permissions`.

## Mental model

`uses: ./path` = action in **this** repo. `uses: owner/repo@v1` = action from GitHub. Review third-party actions before write permissions.

## Self-check

1. Which events start `custom-action.yml`?
2. Why `issues: write`?
3. Where is `message` defined vs consumed?
4. Three `runs.using` types?

## Review answers

1. Issue opened, PR opened.
2. Creating a comment (and labels) on the issue/PR API.
3. Defined in `action.yml` `inputs`; consumed in `index.js` via `core.getInput`.
4. `node20` (JS), `docker`, `composite`.

---

Next: [11 - Complete CI/CD](../11-complete-cicd/README.md).
