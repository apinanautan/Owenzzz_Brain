# Decisions: Frozen Architecture Choices

> อะไรตัดสินใจไปแล้ว — ห้ามวนกลับมา debate เดิม

## OS & Platform

| Decision | Rationale |
|----------|-----------|
| Windows-first | เจ้านายใช้ Windows เป็นหลัก |
| WSL for Hermes | Hermes รันบน WSL (MSYS/Git-Bash compatible) |
| Node.js for OpenClaw | Gateway/Chrome runtime บน Windows native |

## Git Model

| Decision | Rationale |
|----------|-----------|
| Single-main (main only) | ไม่ใช้ temp/backup branches |
| Hermes-PC = writer | Hermes-PC มี push authority |
| Hermes-Mac = read-only | Mac ดึงได้อย่างเดียว |
| Whitelist-only add | ห้าม git add . / git add -A |
| Pre-push checks | status/diff/branch/remote ก่อน push |

## Browser & Chrome

| Decision | Rationale |
|----------|-----------|
| No Chrome on Hermes | Hermes (WSL) ไม่ run browser เอง |
| Chrome = OpenClaw-PC only | Browser automation ผ่าน OpenClaw |
| Route via task file | docs/secretary_tasks/inbox/ สำหรับ browser tasks |
| Camofox = OpenClaw | Camofox browser runtime อยู่บน OpenClaw เท่านั้น |

## Task Queue

| Decision | Rationale |
|----------|-----------|
| secretary_tasks structure | inbox → in_progress → reports → done |
| Task file format | markdown with target/objective/steps/safety/expected_report/timeout |
| Hermes → OpenClaw | สร้าง task file, monitor reports |
| No direct API calls to OwenGPT | ใช้ Chrome relay ผ่าน task file |

## System Rules

| Decision | Rationale |
|----------|-----------|
| SocratiCode gate | ทุก code task ต้องผ่าน context→impact→gate→edit→verify |
| Process ownership guard | Hermes ไม่มี process ownership ของ OpenClaw |
| Token policy | check ก่อนทำ/ตอบ, ประหยัดเสมอ |
| Reply format | สั้น, ไม่ log ยาว, ไม่ format ฟุ้ง |

## Storage & Memory

| Decision | Rationale |
|----------|-----------|
| No vector DB | ไม่ใช้ semantic search สำหรับ memory |
| Memory tool for durable facts | preferences, corrections, environment facts |
| Session search for cross-session | ใช้ session_search แทน long memory |
| Obsidian = external notes | อยู่นอก hermes-config repo |

## What We DECLINED

- ~~Vector DB / semantic memory~~
- ~~Sandbox browser on Hermes~~
- ~~Branching strategy (temp branches)~~
- ~~Direct API calls to OwenGPT~~
- ~~Mac push authority~~
- ~~git add . / git add -A~~
- ~~Hermes run Chrome~~

## Last Updated
2025-05-14