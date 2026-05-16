# Local Context Bloat Fix Report

## Problem
- local model context เต็มเร็วผิดปกติ
- request ก่อนแก้มี bloat จาก system + tool schema หนักมาก

## Evidence Before
- body=84275
- tools=20
- system=34743
- tool_schema=44006
- dominant=93.4%

## Fix
- local provider ใช้ minimal system prompt
- lazy tool allowlist
- ไม่ inject AGENTS / MEMORY / SOUL / MCP เต็มก้อนเข้า local
- cloud planner ยังใช้ full brain ตามปกติ
- local worker ใช้ minimal context
- tools ใช้ lazy allowlist ตามงาน

## Evidence After
- body=1536
- tools=0
- system=513
- dominant=33.4%

## Tests
- CHAT10 PASS
- SUMMARY PASS
- TOOL allowlist PASS
- 15 tests passed

## Architecture Rule
- cloud planner = full brain
- local worker = minimal context
- tools = lazy allowlist

## Manifest Summary
- prompt assembly
- tool injection
- context compaction
- provider routing
- local/cloud split
- model validation
- REQDBG flow

## Risk Notes
- ถ้า system + tools โตเกินไป local จะตันเร็ว
- ถ้า history/tool logs ไม่ prune จะสะสม context โดยไม่จำเป็น
- ถ้า tool schema inject ทุก turn ต้องแยก lazy tools ออกจาก core prompt
