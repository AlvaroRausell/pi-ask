---
name: ask
description: Helps when the model has multiple clarification questions for the user, especially numbered lists like 1, 2, 3. Use this when the assistant should gather several user answers efficiently and route them through the /ask command for an interactive tabbed questionnaire.
license: MIT
---

# Ask

Use this skill when you need multiple clarifications from the user and a plain text reply would be clumsy.

## When to use

Use this skill when:

- you have 2 or more clarification questions
- the questions are naturally presented as a numbered list
- you want the user to answer in an interactive questionnaire instead of a long freeform reply

## Workflow

1. Write the questions as a concise numbered list.
2. Prefer using the `ask_questions` tool directly when it is available.
3. If direct tool use is not available, tell the user they can run `/ask` with that exact block.
4. Keep each question short, specific, and independent.
5. Prefer multiple-choice style wording when possible because the `/ask` rewriter will try to infer options.

## Preferred output pattern

```text
I need a few clarifications before I proceed:

1. Which framework should I target?
2. Do you want TypeScript or JavaScript?
3. Should I optimize for implementation speed or long-term maintainability?

If the `ask_questions` tool is available, I’ll open an interactive questionnaire for these now. Otherwise, you can run `/ask` with the questions above.
```

## Authoring guidance

- Aim for 2-7 questions.
- Avoid compound questions.
- If a question has obvious options, mention them explicitly.
- Do not ask unnecessary questions just to use this workflow.
- If only one clarification is needed, ask it normally instead of using `/ask`.
- Prefer `ask_questions` over asking the user to manually run `/ask` when the tool is available.
