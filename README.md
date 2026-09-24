# GitHub Actions Learning Lab

This is a hands-on learning project aligned with the major concepts in **GitHub Actions - The Complete Guide**. Each module contains a short explanation, a runnable or copyable workflow example, and an exercise.

The only demo application is **TaskFlow** in [`demo-app/`](demo-app/). Study it here; **push it to your personal GitHub** and do every hands-on exercise **from that personal repo**.

## Repositories

| Role | Details |
| --- | --- |
| Study notes (read here) | [WebexCloudPlatform/kubernetes-learn](https://github.com/WebexCloudPlatform/kubernetes-learn) · folder `github-actions-learning/` |
| Hands-on (create once, then reuse) | **Your personal GitHub repo** — push `demo-app/` at the repo root. Suggested: `https://github.com/<your-github-username>/github-actions-learning` |
| First time | Create the personal repo and `git push` (see [`RUN-ON-GITHUB.md`](RUN-ON-GITHUB.md)) |
| Later modules | **Use that existing personal repo.** Do not create a new GitHub repo per module. Do not run lab workflows on kubernetes-learn. |

Record your personal repo URL in [`progress.md`](progress.md).

kubernetes-learn `ci-validate.yml` is the real Java/Kubernetes CI. Leave it alone; lab experiments belong on the personal repo.

## Start here

Prerequisites:

- Git and a **personal** GitHub account
- Node.js 20 or newer
- A code editor such as VS Code
- Module 01: create the personal repo and push this lab ([`RUN-ON-GITHUB.md`](RUN-ON-GITHUB.md))

Run the demo application locally (from this folder or from your personal clone):

```bash
cd demo-app
npm test
npm run lint
npm run build
npm start
```

Copy a module YAML into the **personal** repo `.github/workflows/` when you want a GitHub run. YAML under `modules/` is study-only.

## Learning path

| Module | Topic | Main outcome |
| --- | --- | --- |
| 01 | Git and GitHub | Create personal repo, push demo-app, open a PR |
| 02 | Workflow building blocks | Create a first workflow — [notes](modules/02-foundations/README.md) |
| 03 | CI pipeline | Lint, test, and build on pushes and pull requests — [notes](modules/03-ci-pipeline/README.md) |
| 04 | Events and triggers | Push, pull request, manual, schedule, filters |
| 05 | Variables and contexts | Use expressions, environment variables, and outputs |
| 06 | Dependencies, cache, artifacts | Pass results between jobs and preserve build output |
| 07 | Matrix strategies | Test multiple runtimes and operating systems |
| 08 | Secrets and security | Least privilege, secrets, environments, and safe pull requests |
| 09 | Reusable workflows | Share CI logic across repositories |
| 10 | Custom JavaScript action | Build an action that uses the GitHub API |
| 11 | Complete CI/CD | Package, publish, and release the application |

## Suggested study rhythm

1. Read the module README (including **Run on GitHub**).
2. Copy the example into your **personal** repo `.github/workflows/` only when you are ready to run it.
3. Change one thing deliberately and observe the run on that personal repo.
4. Complete the exercise before moving to the next module.
5. Keep notes in `progress.md` and link successful workflow runs from the personal repo.

## Important safety note

The examples are educational. Before using them in a production repository, review action versions, pin third-party actions to trusted commit SHAs, set minimal `permissions`, and never print secrets. The security module explains these choices.
