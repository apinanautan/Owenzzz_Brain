# Agent Map: Who Does What

> ใครทำอะไร — responsibility matrix ของระบบ

## Nodes

### OwenGPT (Cloud / Planner)
| Role | Responsibility |
|------|---------------|
| Architect | ออกแบบ architecture, ตัดสินใจ |
| Planner | วางแผน, สั่งงาน Hermes |
| Secretary | รับ input จากเจ้านาย, route ไป |
| Browser | ใช้ ChatGPT ตอบคำถาม |

**How to reach:** Telegram DM (▫️), ChatGPT (via browser on OpenClaw-PC)

---

### Hermes-PC (Windows/WSL) ← MAIN WORKER
| Role | Responsibility |
|------|---------------|
| Worker | Execute tasks, sync, maintenance, recovery |
| Git Writer | Push authority to hermes-config repo |
| Sync Manager | Brain sync, file sync, task monitoring |
| SocratiCode Gate | Code task gate before edit |
| Safe Autopush | Event-based auto commit/push |

**How to reach:** Telegram, terminal, Hermes CLI

**Boundaries:**
- ✅ Can: git push, file edit, sync, monitor, task execution
- ❌ Cannot: run Chrome, browser automation, restart OpenClaw directly

---

### Hermes-Mac (macOS) ← READ-ONLY
| Role | Responsibility |
|------|---------------|
| Helper | Backup worker, fetch/pull only |
| Read-only | ดึงข้อมูล, ไม่ push |

**How to reach:** Terminal (ssh ถ้ามี)

**Boundaries:**
- ✅ Can: git fetch, git pull, git log, git diff
- ❌ Cannot: git push, file edit ใน repo

---

### OpenClaw-PC (Windows) ← RUNTIME GATEWAY
| Role | Responsibility |
|------|---------------|
| Gateway | Hermes gateway runtime (Node.js) |
| Telegram | Telegram bot runtime |
| Browser | Chrome/Camofox automation, ChatGPT access |
| Process Owner | เจ้าของ OpenClaw process (Hermes ไม่มี ownership) |

**How to reach:** Task file (docs/secretary_tasks/inbox/), Windows terminal

**Boundaries:**
- ✅ Can: run Chrome, browser automation, restart gateway
- ❌ Cannot: edit hermes-config repo

---

### OpenClaw-Mac (macOS) ← READ-ONLY BACKUP
| Role | Responsibility |
|------|---------------|
| Runtime backup | OpenClaw runtime (fallback) |
| Read-only | ไม่ push, ไม่ edit |

**How to reach:** Terminal (ถ้าต้องการ)

**Boundaries:**
- ✅ Can: fetch/pull, รัน OpenClaw ถ้าต้องการ
- ❌ Cannot: push, edit repo

---

## Task Routing Matrix

| Task Type | Target | Via |
|-----------|--------|-----|
| Code/edit/build/deploy | Hermes-PC | ทำเอง |
| Git push | Hermes-PC | ทำเอง (writer) |
| Sync/report/recovery | Hermes-PC | ทำเอง |
| Browser/Chrome/ChatGPT | OpenClaw-PC | Task file → docs/secretary_tasks/inbox/ |
| Gateway restart | OpenClaw-PC | Task file → docs/secretary_tasks/inbox/ |
| Telegram runtime | OpenClaw-PC | (รันอยู่แล้ว) |
| Obsidian/external notes | External | Manual หรือ skill |

---

## Communication Flow

```
เจ้านาย (▫️)
    ↓ Telegram
OwenGPT (Cloud)
    ↓ สั่ง
Hermes-PC (Worker)
    ↓ route
├── OpenClaw-PC (Browser/Telegram)
│       ↓
│       docs/secretary_tasks/reports/
│               ↓
└── Hermes-PC (Monitor → Report back)
```

---

## Node Health Check

| Node | Status | How to check |
|------|--------|--------------|
| Hermes-PC | 🟢 OK | hermes health |
| Hermes-Mac | 🟡 Unknown | git fetch test |
| OpenClaw-PC | 🟡 Check | docs/secretary_tasks/reports/ |
| OpenClaw-Mac | ⚪ N/A | - |

**Last check:** 2025-05-14