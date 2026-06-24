<div align="center">

# 🛡️ Copilot Governance Template

### Drop-in guardrails that make GitHub Copilot ship *your* way — not just *some* way.

Copy **one folder** into any repo and get a contract-driven workflow: build
features the right way, review them against a contract, keep docs and code in sync,
and stay in control of shipping.

<br/>

[![VS Code Copilot](https://img.shields.io/badge/VS%20Code-Copilot-007ACC?logo=visualstudiocode&logoColor=white)](https://github.com/features/copilot)
[![Drop-in](https://img.shields.io/badge/setup-one%20folder-success)](#-quick-start--paste-into-your-terminal)
[![Artifacts over judgement](https://img.shields.io/badge/design-artifacts%20%3E%20judgement-blueviolet)](#-design-principle-artifacts-not-llm-judgement)
[![License](https://img.shields.io/badge/license-use%20freely-lightgrey)](#license)

<br/>

`/start` · `/doctor` · `/forge` · `/vibecode` · `/review` · `/sync` · `/help`

</div>

---

## ✨ Why you want this

|  | Without it | **With this template** |
|---|---|---|
| 📐 **Consistency** | Copilot guesses your conventions | Reads your contract & style guide every time |
| 🔒 **Safety** | Secrets & bad SQL slip through | Hard rules + CI gates block them |
| 🧭 **Drift** | Docs rot, code wanders | Code & docs must change together |
| 🚢 **Shipping** | Agent merges on a vibe | Plans, reviews, then **asks** before pushing |

---

## 🚀 Quick start — paste into your terminal

Run these from the **root of the repo you want to add governance to**. They copy
the `.github/` folder (commands, skills, contract docs, CI) into your project.

### Windows (PowerShell)

```pwsh
# 1. Pull the template into a temp folder
git clone --depth 1 https://github.com/thuantran2704/copilot-governance-template.git "$env:TEMP\cgt"

# 2. Copy the governance layer into your repo
Copy-Item "$env:TEMP\cgt\.github" -Destination . -Recurse -Force

# 3. Merge the secret-ignoring rules into your .gitignore
Get-Content "$env:TEMP\cgt\.gitignore" | Add-Content .gitignore

# 4. Clean up
Remove-Item "$env:TEMP\cgt" -Recurse -Force

# 5. Commit it
git add .github .gitignore
git commit -m "chore: add Copilot governance layer"
```

### macOS / Linux (bash)

```bash
# 1. Pull the template into a temp folder
git clone --depth 1 https://github.com/thuantran2704/copilot-governance-template.git /tmp/cgt

# 2. Copy the governance layer into your repo
cp -R /tmp/cgt/.github .

# 3. Merge the secret-ignoring rules into your .gitignore
cat /tmp/cgt/.gitignore >> .gitignore

# 4. Clean up
rm -rf /tmp/cgt

# 5. Commit it
git add .github .gitignore
git commit -m "chore: add Copilot governance layer"
```

> 💡 Starting a brand-new repo instead? On GitHub click **Use this template** →
> create your repo → clone it. The `.github/` folder is already there.

---

## 🧩 Then: let Copilot fill in the blanks

The template ships with `TODO:` placeholders for anything project-specific. You
don't have to fill them by hand:

```text
┌─────────────────────────────────────────────────────────────┐
│  1. Open your repo in VS Code with GitHub Copilot           │
│  2. In Copilot Chat, type  /  → see start vibecode review … │
│  3. Run  /start  → it interviews you & fills the TODOs       │
│  4. Run  /help   → see everything you can do                 │
└─────────────────────────────────────────────────────────────┘
```

That's it — you're governed. 🎉

---

## 🎯 Design principle: artifacts, not LLM judgement

The whole template is built on one idea: **don't rely on the model to remember the
rules — write the rules down as artifacts the model (and the build) must obey.**

- **Ground truth lives in files, not in the agent's head.** The contract
  (`Template.md`), the style guide (`Style.md`), and the hard rules
  (`copilot-instructions.md`) are checked-in artifacts. The agent reads them every
  time instead of guessing.
- **Code and docs must never drift.** Change a route or schema and the matching
  artifact must change in the *same* diff. `/sync` reconciles them; CI fails the
  build when they diverge.
- **Push every rule down the enforcement ladder** (below) so it *fails the build*
  rather than merely *reminding the agent*. LLM judgement is the weakest layer —
  use it only for what can't be encoded as an artifact or a check.
- **Humans stay in control of shipping.** Prompts plan, build, and review, but they
  ask before they push, split, or merge.

> **Remember one thing:** prefer a file or a check over a polite instruction.

---

## 📦 What you just added (`.github/`)

| Path | What it gives you |
|---|---|
| `prompts/start.prompt.md` | `/start` — interview + fill in placeholders |
| `prompts/doctor.prompt.md` | `/doctor` — build, run, test & health-check the whole system |
| `prompts/forge.prompt.md` | `/forge` — author a new skill or agent, philosophy-first |
| `prompts/vibecode.prompt.md` | `/vibecode` — research → plan → build → test → ship a feature |
| `prompts/review.prompt.md` | `/review` — review a diff vs. contract/style/security; PR-split |
| `prompts/sync.prompt.md` | `/sync` — reconcile docs with the real code |
| `prompts/help.prompt.md` | `/help` — the menu of commands, skills, docs |
| `skills/pull-request-splitter/SKILL.md` | Split a change set into reviewable PR slices |
| `skills/unit-test-generator/SKILL.md` | Generate + run unit tests with boundaries mocked |
| `Template.md` | The **API & data contract** (endpoints, payloads, schema) |
| `Style.md` | The clean-code guide |
| `PHILOSOPHY.md` | The core principle every command reviews first |
| `copilot-instructions.md` | Global rules + hard security boundaries |
| `instructions/*.instructions.md` | Path-scoped rules (`applyTo` globs) |
| `workflows/contract-check.yml` | CI: fail on contract drift + run tests |
| `SECURITY.md` · `CUSTOMIZING.md` | Security baseline · how to adapt the template |

For deeper setup (turning soft rules into hard CI gates, branch protection, etc.)
see [SETUP.md](./SETUP.md) and [`.github/CUSTOMIZING.md`](./.github/CUSTOMIZING.md).

---

## 🪜 The enforcement ladder

Agent instructions are **soft** (judgement). Push each rule as far down this ladder
as you can so it *fails the build* instead of *reminding the agent*:

```text
        weakest ┌──────────────────────────────────────────┐
   (judgement)  │ 1 · Chat instructions / prompts  ← here   │
                │ 2 · Linters / formatters                 │
                │ 3 · Unit / contract tests                │
                │ 4 · Git hooks · secret scanning          │
                │ 5 · CI workflows  ← contract-check.yml   │
  strongest     │ 6 · Branch protection / rulesets         │
  (unbypassable)└──────────────────────────────────────────┘
```

The prompts and skills here are layer 1; `contract-check.yml` is a layer-5 start.
Add layers 2–4 and 6 per project for stronger guarantees.

---

<div align="center">

### Built for teams who want Copilot to move fast **and** stay in the lines.

`/start` to set up · `/vibecode` to build · `/review` before you ship

</div>

## License

Use freely within your own projects. No warranty.
