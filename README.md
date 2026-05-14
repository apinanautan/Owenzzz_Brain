# Owenzzz Brain — AI Second Brain

> Obsidian vault for Hermes Agent multi-node system

## Vault Structure

```
brain/          — System documentation (PROJECT, STATE, DECISIONS, etc.)
tasks/          — Task tracking
projects/       — Active projects
prompts/        — Reusable prompt templates
workflows/      — Workflow documentation
reports/        — Execution reports
recovery/       — Recovery procedures
agents/         — Agent configuration
skills/         — Skill documentation
automation/     — Automation scripts
archive/        — Archived items
```

## Repositories

| Repo | Role |
|------|------|
| **Owenzzz_Brain** (this) | Knowledge/brain — version controlled |
| [hermes-config](https://github.com/owenzzz/hermes-config) | Runtime/system repo |

> **Rule:** Vault git ≠ Runtime repo — แยกกันชัดเจน

## Sync Rules (DO NOT TRACK)

- ❌ sessions, tokens, auth
- ❌ runtime cache (.db, .sqlite)
- ❌ browser states, WebStorage
- ❌ .obsidian/ internal configs

## Last Updated

2025-05-14