---
applyTo: "TODO/web/**"
---

# Web / client instructions

> TODO: Set the `applyTo` glob above to this project's frontend source path.

Rules for frontend code in this project. These extend
[`.github/copilot-instructions.md`](../copilot-instructions.md) and
[`.github/Style.md`](../Style.md).

- Route all network calls through one shared client module; never inline `fetch`.
- Handle the three states explicitly: **loading, empty, error**. A blank screen on
  error is a bug.
- Keep components small and presentational; lift shared logic into a hook or the
  client module.
- Reuse existing styles before adding new ones.
- Match request/response shapes to [`Template.md`](../Template.md); update the client
  wrapper when a payload changes.
