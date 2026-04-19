# pi-ask

`pi-ask` is a Pi package for interactive multi-question clarification flows in Pi.

It adds:

- a marketplace-installable skill for multi-question clarification workflows
- an `ask_questions` tool that models can call directly
- an `/ask` command for manual invocation
- an interactive tabbed questionnaire UI inside Pi

## Install

```bash
pi install /path/to/pi-ask
# or, once published
pi install npm:pi-ask
```

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

- tab labels use `1 2 3 ...`
- final dedicated `Submit` tab
- auto-jumps to `Submit` after the last answer
- freeform fallback via `Write my own answer`
- simple fallback parsing if the small model does not return valid JSON
- simple `A or B` option inference

## Planned future enhancements

- richer question types like yes/no
- multi-select
- priority ranking
- stronger validation and parsing

## Files

- `skills/ask/SKILL.md` — skill instructions for the main model
- `extensions/pi-ask/index.ts` — `/ask`, `/ask-model`, `/ask-settings`, `ask_questions`, and the interactive UI

## Publishing

This repo already uses the Pi package manifest in `package.json`, so once published to npm it should be installable with:

```bash
pi install npm:pi-ask
```

## npm publish checklist

1. Log in to npm:

```bash
npm login
```

3. Preview the published tarball:

```bash
npm pack --dry-run
```

4. Publish the package:

```bash
npm publish --access public
```

5. Verify installation in Pi:

```bash
pi install npm:pi-ask
```
