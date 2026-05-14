# Project: Hermes Agent Multi-Node System

## Overview
ระบบ AI agent orchestration แบบ multi-node บน Windows เครื่องเดียว

## Architecture

```
OwenGPT (GPT-5.5) = Planner/Architect/Secretary
    ↓ routes
┌─────────────────────────────────────────────────────────┐
│                     Hermes-PC (Worker)                   │
│  - WSL/Linux                                            │
│  - Git writer (push authority)                          │
│  - Sync/maintenance/recovery                            │
│  - Task execution                                       │
└─────────────────────────────────────────────────────────┘
    ↕ sync                      ↕ runtime
┌──────────────────┐       ┌──────────────────────────────┐
│   Hermes-Mac     │       │       OpenClaw-PC           │
│   (Read-only)    │       │   - Windows/Node.js          │
│   Helper/backup  │       │   - Telegram gateway         │
└──────────────────┘       │   - Browser automation      │
                           │   - Chrome/Camofox          │
                           └──────────────────────────────┘
                                    ↕
                           ┌──────────────────┐
                           │   OpenClaw-Mac   │
                           │   (Read-only)    │
                           └──────────────────┘
```

## Node Map

| Node | OS | Role | Git | Browser |
|------|-----|------|-----|---------|
| OwenGPT | Cloud | Planner/Architect | - | - |
| Hermes-PC | Windows/WSL | Worker/Sync/Maintenance | **Writer** | No (route) |
| Hermes-Mac | macOS | Helper/Backup | Read-only | No |
| OpenClaw-PC | Windows | Runtime/Gateway/Telegram | - | **Yes** |
| OpenClaw-Mac | macOS | Runtime (backup) | - | No |

## Current Goals
1. Brain documentation system (docs/brain/)
2. Task queue standardization (docs/secretary_tasks/)
3. Chrome relay via OpenClaw-PC
4. Safe auto-push workflow

## Active Stack

### Hermes Framework
- Language: Python
- Config: ~/AppData/Local/hermes/config.yaml
- Skills: ~/AppData/Local/hermes/skills/
- Memory: AGENTS.md (injected)

### OpenClaw Gateway
- Language: Node.js
- Platform: Windows
- Location: OpenClaw-PC (Hermes has NO process ownership)
- Restart: via task file only

### Task Queue
- Path: docs/secretary_tasks/
- Structure: inbox/ → in_progress/ → reports/ → done/

### Git
- Remote: github.com/owenzzz/hermes-config
- Branch: main (single main mode)
- Hermes-PC = writer authority

## Key Boundaries
- Hermes (WSL) ไม่ run Chrome/ไม่ทำ browser automation เอง
- Hermes (WSL) ไม่มี process ownership ของ OpenClaw gateway
- Mac ไม่ push (read-only เท่านั้น)