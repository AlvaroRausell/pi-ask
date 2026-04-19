# pi-ask

`pi-ask` is a Pi package for interactive multi-question clarification flows in Pi.

It adds:

- a marketplace-installable skill for multi-question clarification workflows
- an `ask_questions` tool that models can call directly
- an `/ask` command for manual invocation
- an interactive tabbed questionnaire UI inside Pi

## Install

From npm (recommended):

```bash
pi install npm:pi-ask
```

From the GitHub repo:

```bash
pi install git:github.com/AlvaroRausell/pi-ask
```

From a local clone:

```bash
git clone https://github.com/AlvaroRausell/pi-ask.git
cd pi-ask
pi install .
```

After installing, the `ask` skill, `ask_questions` tool, and `/ask` command will be available in your next Pi session.

## Recommended flow

The primary flow is: the model calls `ask_questions` directly.

That means when the assistant has several clarification questions, it can open the interactive questionnaire immediately instead of asking the user to manually run `/ask`.

`/ask` still exists as a manual fallback and for testing.

## What it does

When a model produces a message like:

```text
1. Which framework should I use?
2. Do you want TypeScript?
3. Should I optimize for speed or readability?
```

run:

```bash
/ask 1. Which framework should I use?
2. Do you want TypeScript?
3. Should I optimize for speed or readability?
```

You can also run `/ask` immediately after the assistant asks those questions; it will use the latest assistant message as input.

The ask flow will:

1. send the raw text to a smaller LLM
2. convert it into structured questions + options
3. open a tabbed UI, one tab per question plus a final `Submit` tab
4. show progress like `2/3 answered`
5. load a natural-language answer bundle into the editor

The package currently keeps answers in the editor only. It does not auto-send them back to the main model.

## Configuring the smaller LLM

Recommended model:

```bash
openai/gpt-4.1-mini
```

Resolution order:

1. `PI_ASK_MODEL`
2. `/ask-settings` saved configuration
3. current active Pi model

Commands:

```bash
/ask-model      # show which model will be used
/ask-settings   # save a default /ask model
```

Environment override:

```bash
export PI_ASK_MODEL="openai/gpt-4.1-mini"
```

## Commands and tool

- `ask_questions` — primary model-facing tool
- `/ask` — manual command for running the questionnaire flow from text or the latest assistant message
- `/ask-model` — shows which small model will be used
- `/ask-settings` — saves the default small model configuration

## Current questionnaire behavior

- tab labels use `1 2 3 ...` with type icons (`≡` multi, `☑` checkbox)
- final dedicated `Submit` tab
- auto-jumps to `Submit` after the last answer
- three question types:
  - **single** — pick one option (default, numbered list with `>`)
  - **checkbox** — yes/no toggle (radio-style `[●] / [○]` for Yes/No)
  - **multi-select** — pick multiple options (checkbox-style `[■] / [□]`, Space to toggle, Enter to confirm)
- freeform fallback via `Write my own answer` (single-select only)
- simple fallback parsing if the small model does not return valid JSON
- simple `A or B` option inference
- automatic type inference from question phrasing:
  - "all that apply", "which of", "select all" → multi-select
  - "do you want", "should I", "would you like" → checkbox
  - everything else → single
- multi-select answers display as comma-separated labels in the submit tab and summary

## Planned future enhancements

- priority ranking
- stronger validation and parsing
- custom option entry in multi-select mode
- conditional question flow (show q3 only if q2 is yes)

## Files

- `skills/ask/SKILL.md` — skill instructions for the main model
- `extensions/pi-ask/index.ts` — `/ask`, `/ask-model`, `/ask-settings`, `ask_questions`, and the interactive UI

## Publishing

This repo already uses the Pi package manifest in `package.json`, so once published to npm it should be installable with:

```bash
pi install npm:pi-ask
```
