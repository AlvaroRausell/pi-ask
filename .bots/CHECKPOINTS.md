# pi-ask - Project Checkpoints

> **This is a living project document.** Update it as decisions are made and work progresses.

---

## Current Checkpoint

- **Project**: pi-ask
- **Started**: 2026-04-19
- **Last session log**: `.bots/logs/2026-04-19-release-cleanup.md`
- **Status**: Release-polished pi package with direct tool flow, settings command, submit-tab UX, and publish scaffolding

---

## Project Phases

| Phase | Description | Status | Started | Completed |
|-------|-------------|--------|---------|-----------|
| 1     | Project setup | [x] | 2026-04-19 | 2026-04-19 |
| 2     | Pi package scaffold | [x] | 2026-04-19 | 2026-04-19 |
| 3     | Interactive /ask workflow | [x] | 2026-04-19 | 2026-04-19 |
| 4     | Production hardening and publish prep | [x] | 2026-04-19 | 2026-04-19 |
| 5     | Release cleanup and docs polish | [x] | 2026-04-19 | 2026-04-19 |

---

## Key Decisions

- Package uses Pi package conventions via `package.json` with `pi.extensions` and `pi.skills`.
- Skill name is `ask`, focused on multi-question clarification workflows.
- `/ask` uses the current model by default, with `PI_ASK_MODEL=provider/model-id` override and `/ask-settings` for saved configuration of a cheaper/smaller LLM.
- `/ask` parses question blocks into structured JSON and presents them as a tabbed questionnaire UI.
- The extension also exposes an `ask_questions` custom tool so models can launch the questionnaire directly, and that is now the preferred flow.
- Invalid JSON from the smaller model falls back to local numbered-list parsing with simple `or` option inference.

---

## Open Questions

- The questionnaire schema is inferred by the small model first, then normalized with a fallback parser; future versions may still want richer validation.
- Future versions should add richer question types such as yes/no, multi-select, and priority ranking.
- Placeholder `repository`/`homepage`/`bugs` URLs in `package.json` should be replaced with the real project URLs before publishing.

---
