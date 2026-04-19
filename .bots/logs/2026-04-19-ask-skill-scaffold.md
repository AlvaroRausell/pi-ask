# Session Log: ask-skill-scaffold

## 2026-04-19

- Started session on topic: ask-skill-scaffold


## 2026-04-19

- Decision: packaged repo as a Pi marketplace package with a conventional package.json manifest, one skill (skills/ask), and one extension (extensions/pi-ask/index.ts).


## 2026-04-19

- Decision: /ask uses the current model by default and supports a smaller configurable model via PI_ASK_MODEL=provider/model-id.


## 2026-04-19

- Decision: /ask parses raw numbered questions with a secondary LLM pass, then renders answers in a custom tabbed questionnaire UI and loads the resulting reply into the editor.

