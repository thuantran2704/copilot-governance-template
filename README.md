# copilot-governance-template

A **portable, project-agnostic governance + AI-tooling layer** for VS Code Copilot.
Lift the `.github/` folder into any repo to get a consistent contract-driven
workflow: build features the right way, review them against a contract, decide PR
slices, and keep humans in control of shipping.

This template is the genericized distillation of a working setup. Anything
project-specific has been replaced with a `TODO:` placeholder or a clearly marked
fill-in.

## What's inside (`.github/`)

| Path | Purpose | Portable? |
|---|---|---|
| `Template.md` | The **API & data contract** skeleton — endpoints, payloads, response/error shapes, schema. | Skeleton; fill per project |
| `Style.md` | Clean-code guide (naming, functions, errors, async, security, PR checklist). | Mostly portable |
| `copilot-instructions.md` | Global rules + hard security boundaries that tie everything together. | Skeleton; fill per project |
| `pull_request_template.md` | PR checklist mirroring the contract + style. | Portable |
| `prompts/vibecode.prompt.md` | `/vibecode` — research-backed feature workflow (plan → build → contract-sync → test → ship). | Portable structure |
| `prompts/review.prompt.md` | `/review` — review a diff vs. contract/style/security, run PR-split, open PRs. | Portable structure |
| `prompts/start.prompt.md` | `/start` — interview about the project (purpose, stack, environment) and fill in the template placeholders. | Portable |
| `prompts/help.prompt.md` | `/help` — brief menu of commands, skills, and docs. | Portable |
| `skills/pr-split/SKILL.md` | Advisory PR-split analyzer (every file → one slice; opens a PR per slice on confirmation). | Portable |
| `skills/generate-run-tests/SKILL.md` | Generate + run unit tests with the boundaries mocked; never touches secrets. | Adapt to test runner |
| `instructions/*.instructions.md` | Path-scoped rules (`applyTo` globs). | Example; adapt globs |
| `workflows/contract-check.yml` | CI: fail on contract drift + run tests. | Adapt paths |
| `SECURITY.md` | The hard security baseline every layer enforces. | Portable; fill disclosure channel |
| `CUSTOMIZING.md` | How to adapt this template to a specific codebase. | Portable |

> **New here?** Read [`.github/CUSTOMIZING.md`](./.github/CUSTOMIZING.md) to adapt
> the template, and [`.github/SECURITY.md`](./.github/SECURITY.md) for the security
> baseline.

## The enforcement ladder (why this layered approach)

Agent instructions are **soft** (judgment). Push each rule as far down this ladder
as you can so it *fails the build* instead of *reminding the agent*:

1. Chat instructions / prompts (soft) — this template.
2. Linters / formatters (hard, local).
3. Unit / contract tests (hard, local + CI).
4. Git hooks — `husky` + `lint-staged`, secret scanning (`gitleaks`).
5. CI workflows (hard, server-side) — `workflows/contract-check.yml`.
6. Branch protection / rulesets (unbypassable) — configure in repo settings.

The prompts and skills here are layer 1; `contract-check.yml` is a layer-5 start.
Add layers 2–4 and 6 per project for stronger guarantees.

## How to adopt in a new repo

1. Copy this `.github/` into the target repo.
2. Search for `TODO:` and fill in project-specifics (stack, endpoints, schema,
   file paths, test commands).
3. Fill `Template.md` with the real contract and `copilot-instructions.md` with
   the project's one-line pitch + hard rules.
4. Adjust `instructions/*.instructions.md` `applyTo` globs and
   `workflows/contract-check.yml` paths to match your tree.
5. Optionally promote the generic parts to an **org-level `.github` repo** or
   **reusable workflows** so multiple repos share one source of truth.

## Reuse strategies across many projects

- **Template repository** — mark this repo as a GitHub *template*; new repos start
  from it.
- **Org `.github` repo** — a repo named `.github` in your org supplies default
  community files (PR template, workflows, instructions) to every repo.
- **Reusable workflows** — keep CI jobs in one repo, call them with
  `uses: <org>/<repo>/.github/workflows/<file>.yml@main`.

## License

Use freely within your own projects. No warranty.
