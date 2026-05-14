# System Overview

## Architecture

```
OwenGPT (Cloud) → Hermes-PC (Worker) → OpenClaw-PC (Runtime)
```

## Nodes

| Node | OS | Role | Git |
|------|-----|------|-----|
| OwenGPT | Cloud | Planner/Architect | - |
| Hermes-PC | Windows/WSL | Worker/Sync | Writer |
| Hermes-Mac | macOS | Helper | Read-only |
| OpenClaw-PC | Windows | Runtime/Telegram | - |
| OpenClaw-Mac | macOS | Runtime backup | Read-only |

## Key Rules

- **Hermes-PC = Git writer** (push authority)
- **Mac = Read-only** (cannot push)
- **Browser = OpenClaw-PC only** (Hermes cannot run Chrome)
- **Task routing = docs/secretary_tasks/**

## Tools

- Hermes Framework (Python/WSL)
- OpenClaw Gateway (Node.js/Windows)
- Obsidian (Note-taking)
- Git (Version control)

## Last Updated
2025-05-14