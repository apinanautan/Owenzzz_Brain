# Handoff: Context for Next Agent/Session

> ส่ง context ให้ session ถัดไป — current task, exact next step, avoid mistakes

## Current Task

**Phase:** Brain Documentation Restructure (docs/brain/)
**Status:** In progress — สร้าง 9 ไฟล์, เหลือ 4 ไฟล์

**Files done (5/9):**
- [x] PROJECT.md
- [x] STATE.md
- [x] DECISIONS.md
- [x] KNOWN_ISSUES.md
- [x] WORKLOG.md

**Files pending (4/9):**
- [ ] HANDOFF.md (this file)
- [ ] AGENT_MAP.md
- [ ] TOOLCHAIN.md
- [ ] SYSTEM_RULES.md

## Exact Next Step

1. สร้าง HANDOFF.md (สร้างเสร็จแล้ว ← current)
2. สร้าง AGENT_MAP.md — ใครทำอะไร (OwenGPT, Hermes-PC, Hermes-Mac, OpenClaw-PC, OpenClaw-Mac)
3. สร้าง TOOLCHAIN.md — เก็บ tool/credential list
4. สร้าง SYSTEM_RULES.md — git rules, safe autopush, SocratiCode, node ownership
5. Push to git หลังจาก done

## Avoid Mistakes

### ⚠️ DO NOT
- ห้าม Hermes run Chrome/Camofox เอง
- ห้าม Hermes restart OpenClaw gateway ตรง ๆ (ต้องผ่าน task file)
- ห้าม Mac push to git (read-only)
- ห้าม git add . / git add -A
- ห้าม direct API call ไป OwenGPT (ต้องผ่าน Chrome relay)

### ✅ DO
- Route browser task ไป OpenClaw-PC ผ่าน docs/secretary_tasks/inbox/
- Monitor reports ที่ docs/secretary_tasks/reports/
- ใช้ SocratiCode gate ก่อน edit code
- Whitelist add files ก่อน commit

## Blocked Areas

| Area | Status | Note |
|------|--------|------|
| ChatGPT login | ⚠️ Unstable | Monitor, อาจต้อง re-login |
| UFO stability | ⚠️ Known issue | Watchdog pattern |
| Provider quota | 🟡 Monitoring | Check token level |

## Session Context

- **Model:** deepseek-v4-flash:cloud via ollama-pay
- **Source:** Telegram
- **User:** ▫️ (robberzaz)
- **Token usage:** 41% (ระดับปกติ)

## For Next Session

ถ้า session ถัดไปเจอ task "brain restructure" ให้:
1. อ่าน docs/brain/STATE.md ก่อน
2. ดูว่า files ไหน done แล้ว
3. ทำต่อจากจุดที่ค้าง
4. Push เมื่อ done