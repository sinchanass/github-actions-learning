# 09 - Reusable workflows and composite actions

**Reusable workflows** share whole **jobs** (`on: workflow_call`). **Composite actions** share a sequence of **steps**.

Study [`reusable-workflow.yml`](reusable-workflow.yml) (provider) and [`caller.yml`](caller.yml) (caller). The caller starts the reusable workflow and also runs the composite action.

## Run on GitHub

Hands-on: [auxislabs/github-actions-learning](https://github.com/auxislabs/github-actions-learning).

Copy:

- `reusable-workflow.yml` → `.github/workflows/reusable-taskflow-ci.yml` (name must match `uses:` in the caller)
- `caller.yml` → `.github/workflows/call-reusable.yml`

The caller uses `uses: ./.github/workflows/reusable-taskflow-ci.yml`. Same repo only for that relative path. Cross-repo: `owner/repo/.github/workflows/file.yml@v1`.

[Run on GitHub](../../RUN-ON-GITHUB.md).

## Exercise

Add input `node-version` (already in the example). Pass it from the caller. Expose a test result as a **workflow output** (`on.workflow_call.outputs`).

---

## Provider

```yaml
on:
  workflow_call:
    inputs:
      node-version:
        required: false
        type: string
        default: '20'
```

`workflow_call` workflows are **not** started by push unless you also add `push`. The caller starts them.

## Caller

```yaml
jobs:
  call-ci:
    uses: ./.github/workflows/reusable-taskflow-ci.yml
    with:
      node-version: '20'
    secrets: inherit   # optional; pass secrets explicitly when you can
```

`with:` → inputs. `secrets:` → secrets. A called workflow cannot use the caller’s `env:` magically.

---

## Composite action (same module)

Reusable workflows share **jobs**. A **composite** action shares **steps** on the caller’s VM.

Example: [`composite-setup/action.yml`](composite-setup/action.yml), called from the `test` job in [`caller.yml`](caller.yml) after checkout:

```yaml
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: ./modules/09-reusable-workflows/composite-setup
        with:
          node-version: '20'
      - run: npm test
        working-directory: demo-app
```

`runs.using: composite` — every step is `run:` or `uses:`. Composite cannot set `runs-on` (it is not a job). Every `run:` step needs `shell:`.

## Docker action

`runs.using: docker` runs the action inside a container image. The full example is in module 10: [`docker-action/action.yml`](../10-custom-actions/docker-action/action.yml), [`Dockerfile`](../10-custom-actions/docker-action/Dockerfile), and [`docker-action.yml`](../10-custom-actions/docker-action.yml).

```yaml
runs:
  using: docker
  image: Dockerfile
  args:
    - ${{ inputs.who-to-greet }}
```

The caller still names the folder:

```yaml
- uses: ./modules/10-custom-actions/docker-action
  with:
    who-to-greet: TaskFlow
```

## Reusable vs composite vs JS action

| | Reusable workflow | Composite action | JS/Docker action |
|---|---|---|---|
| Runs | Whole jobs (own `runs-on`) | Steps **inside** the caller’s job | Steps inside the job |
| File | `.github/workflows/*.yml` | `action.yml` `using: composite` | `action.yml` + JS/Docker |
| Good for | Shared CI across repos | Repeated step sequences | JS logic (`node20`) or a container (`docker`). See module 10 `docker-action/` |

---

## Map onto kubernetes-learn

CI Validate and Publish are **separate** workflow files, not `workflow_call` yet. You *could* extract “setup Java + Maven test” into a reusable workflow. `workflow_run` is the other way to chain (“when CI completes”).

## Mental model

Caller says **when**. Called file says **what jobs**. Checkout in the called workflow still needs `actions/checkout` — it does not inherit the caller’s workspace.

## Self-check

1. What `on:` key makes a workflow callable?
2. How does the caller pass `node-version`?
3. Why copy to `reusable-taskflow-ci.yml` specifically?
4. Reusable workflow vs composite action?

## Review answers

1. `workflow_call`.
2. `with: node-version: '20'` (maps to `inputs.node-version`).
3. That is the path in `caller.yml` `uses:`.
4. Reusable = jobs (new VMs). Composite = steps on the **current** VM.

---

Next: [10 - Custom actions](../10-custom-actions/README.md).
