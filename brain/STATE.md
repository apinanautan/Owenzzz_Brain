# State: Current Work Snapshot

> อันนี้สำคัญสุด — อัปเดตทุกครั้งที่เปลี่ยน phase

## Current Phase

**Phase:** Brain Documentation Restructure
- **Started:** 2025-05-14
- **Task:** สร้าง docs/brain/ สำหรับ system documentation แบบ custom
- **Status:** In progress (สร้าง 9 ไฟล์)

## Latest Successful Workflows

1. **Hermes brain sync** — สร้าง skill hermes-brain-sync ใช้ sync brain ข้าม node
2. **Task file routing** — docs/secretary_tasks/ สำหรับ route งานไป OpenClaw-PC
3. **Chrome relay** — task file + report path สำหรับถาม OwenGPT ผ่าน ChatGPT
4. **Safe auto-push** — skill safe-autopush สำหรับ event-based push

## Active Blockers

| Issue | Status | Workaround |
|-------|--------|------------|
| ChatGPT login/session | Active | UFO/Camofox ต้องรันบน OpenClaw-PC |
| Path translation (Win↔WSL) | Known | ใช้ /c/Users/... for Windows path in WSL |
| Provider quota (ollama-pay) | Monitoring | ใช้ deepseek-v4-flash:cloud |

## Pending Tasks

- [ ] docs/brain/ (กำลังทำ)
  - [x] PROJECT.md
  - [x] STATE.md (current)
  - [ ] DECISIONS.md
  - [ ] KNOWN_ISSUES.md
  - [ ] WORKLOG.md
  - [ ] HANDOFF.md
  - [ ] AGENT_MAP.md
  - [ ] TOOLCHAIN.md
  - [ ] SYSTEM_RULES.md

- [ ] Push to git after done
- [ ] Update SOUL.md — ย้าย system rules ไป docs/brain/SYSTEM_RULES.md

## Session Context (Last)

- **Model:** deepseek-v4-flash:cloud via ollama-pay
- **Source:** Telegram DM
- **Conversation:** Brain restructure planning
- **Input:** 41% token usage

## Notes
- เจ้านายต้องการ customize scaffold ให้เข้าระบบ (Hermes/OpenClaw/multi-node)
- ไม่ใช่ copy template ตรง ๆ