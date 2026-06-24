# Setup — using this template in a project

This guide takes you from cloning the template to a working, enforced governance
layer in a target repo. For *what to change*, see
[`.github/CUSTOMIZING.md`](./.github/CUSTOMIZING.md); for the security baseline, see
[`.github/SECURITY.md`](./.github/SECURITY.md).

## Prerequisites
- Git, and (optional but recommended) the GitHub CLI `gh`.
- VS Code with GitHub Copilot, so the `/` prompts and skills are picked up from
  `.github/`.

## Option A — start a brand-new repo from this template
1. On GitHub, mark this repo as a **template** (Settings → *Template repository*).
2. Click **Use this template** → create your new repo → clone it.
3. Continue to **Fill in the placeholders** below.

## Option B — drop the layer into an existing repo
1. Copy this repo's `.github/` folder into the root of your project.
2. Merge the `.gitignore` entries into your existing `.gitignore`.
3. Continue to **Fill in the placeholders** below.

## Fill in the placeholders
Search the project for `TODO:` and resolve each one. At minimum:
- `.github/copilot-instructions.md` — project one-liner, stack, hard rules.
- `.github/Template.md` — real schema, endpoints, payloads, error conventions.
- `.github/prompts/start.prompt.md` — install/test/run commands and URLs.
- `.github/skills/generate-run-tests/SKILL.md` — test runner + boundary modules to mock.
- `.github/instructions/*.instructions.md` — `applyTo` globs for your source paths.
- `.github/workflows/contract-check.yml` — contract/schema globs + install/test commands.
- `.github/SECURITY.md` — your private vulnerability-disclosure channel.

## Verify the commands load in VS Code
1. Open the project in VS Code.
2. In Copilot Chat, type `/` — you should see `start`, `vibecode`, `review`, `help`.
3. Run `/help` to confirm the menu renders and links resolve.

## Turn soft rules into hard gates (recommended)
Agent prompts are advisory. Add real enforcement (see the ladder in
`CUSTOMIZING.md`):
- **Lint**: a linter that bans interpolated queries and risky patterns.
- **Secret scanning**: `gitleaks` as a pre-commit hook *and* a CI job.
- **CI**: enable `.github/workflows/contract-check.yml` after wiring its globs/commands.
- **Branch protection**: require the contract-check and secret-scan jobs before
  merge; disallow direct pushes to the default branch.

## Smoke-test the workflow
- Open a throwaway PR that intentionally changes a route without updating
  `Template.md` → CI `contract-drift` should fail.
- Run `/review` on a small diff → it should cite the contract and offer a PR split.
- Run `/vibecode` on a tiny feature → it should plan, test, and **ask before**
  shipping.

## Publish this template to your own GitHub (one-time, for the template repo itself)
```pwsh
cd copilot-governance-template
git init
git add .
git commit -m "feat: portable Copilot governance template"
gh auth login                     # choose your account
gh repo create copilot-governance-template --public --source=. --push
```
> If you prefer it private, swap `--public` for `--private`.
