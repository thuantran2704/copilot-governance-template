---
description: 'Quick reference: lists the available slash commands, skills, and guideline docs with a one-line description of each and when to use it. Read-only — does not change code.'
---

# /help — what you can use

A short menu of this project's AI tooling. **Read-only — this command just
explains; it changes nothing.**

## Slash commands
| Command | Use it to… |
|---|---|
| `/start` | Set up the governance system — interview about purpose, stack, and environment, then fill in the template placeholders. |
| `/vibecode` | Build a feature the right way — research, plan, build, sync the contract, run tests, hand off to review. |
| `/review` | Review the current diff against the contract, style, and security; run PR-split; open a PR per slice. |
| `/help` | Show this menu. |

## Skills (auto-used by the agent, or ask for them by name)
| Skill | Use it to… |
|---|---|
| `generate-run-tests` | Generate and run fast unit tests (happy + error paths) with the boundaries mocked — never touches real secrets or live systems. |
| `pr-split` | Decide whether a change set ships as one PR or split/stacked slices; assigns every changed file to one slice and can open a PR per slice after you confirm. |

## Guideline docs (the rules everything follows)
| Doc | What it defines |
|---|---|
| [`.github/Template.md`](../Template.md) | The API & data contract — endpoints, payloads, response/error shapes, schema, helper signatures. |
| [`.github/Style.md`](../Style.md) | The clean-code guide — naming, functions, error handling, async, security, PR checklist. |
| [`.github/copilot-instructions.md`](../copilot-instructions.md) | Global rules + hard security boundaries. |
| [`.github/CUSTOMIZING.md`](../CUSTOMIZING.md) | How to adapt this template to a specific codebase. |
