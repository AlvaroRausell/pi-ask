# AI Agent Instructions

This project uses the **bots** framework for AI agent coordination.

## Quick Start

Before doing anything, read:
1. This file (`.bots/AGENTS.md`) for instructions
2. `.bots/CHECKPOINTS.md` for current project state

## Directory Structure

- `.bots/AGENTS.md` - AI agent instructions (this file)
- `.bots/CHECKPOINTS.md` - Living project state document
- `.bots/logs/` - Session decision logs
- `.bots/tasks/` - Task handoff files
- `.bots/skills/` - AI agent skills

## Workflow

### Before Starting Work

1. Read `.bots/CHECKPOINTS.md` for current project state
2. Check `.bots/logs/` for recent session context
3. Start a new session log: `bots log start <topic>`

### During Work

1. Log decisions as they are made: `bots log append <slug> "Decision: ..."`
2. Use skills from `.bots/skills/` as needed

### When Completing Work

1. Update `.bots/CHECKPOINTS.md` with new state
2. Link to the session log with decisions
3. Commit changes: `bots git_commit_checkpoint "message"`

## Project Rules

### Code Style

- Follow existing code conventions
- Keep functions small and focused
- Add comments for non-obvious decisions

### Git Workflow

- Commit checkpoints when project state changes
- Link session logs in commit messages when relevant
- Use descriptive commit messages

---

*Add project-specific rules in this section as needed.*
