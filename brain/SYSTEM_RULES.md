# System Rules: Core Operating Rules

> ย้ายมาจาก SOUL.md / MEMORY — เก็บ rules หลักของระบบ

## Git Node Ownership

| Node | Role | Authority |
|------|------|-----------|
| Hermes-PC | **Writer** | git status, fetch, pull, whitelist add, commit, push |
| Hermes-Mac | **Read-only** | git status, fetch, pull --all --prune, log, diff, check, report |
| Unknown | **STOP** | ห้ามทำ git ถ้าไม่รู้ว่าเป็น node ไหน |

**ห้าม:**
- ห้าม Mac push (read-only เท่านั้น)
- ห้าม mixed path/config/token ระหว่าง PC/Mac
- ห้าม git add . / git add -A
- ห้าม git reset / git clean / git rebase / git merge
- ห้าม force push

---

## Safe Autopush (Event-Based)

**Trigger events:**
- skill changes (create/patch/delete)
- memory changes
- workflow changes
- task DONE
- config changes
- install/recovery changes

**Workflow:**
```
1. gate check (preflight)
2. secret scan (token/key/password)
3. runtime scan (.pid, .lock, .db, .log)
4. whitelist add (ทีละไฟล์)
5. commit (with message)
6. push
7. verify
```

**Block list (ห้าม commit):**
- auth*, token*, session*
- *.db, *.lock
- gateway_state, processes.json
- SYSTEM_AGENTS_MAIN/sessions/
- SYSTEM_AGENTS_MAIN/agent/auth-*.json
- node_modules/, .playwright/
- generated/, memory/, .openclaw/
- cleanup-backup/
- *.checkpoint.*

**Exclude from block list:**
- SOUL.md, AGENTS.md, SKILL.md, *.md in docs/
- config.yaml, config.json
- scripts/, references/

---

## SocratiCode (Code Task Gate)

**Trigger:** ทุก task ที่มี keyword: code, edit, file, config, repo, debug, test, build, deploy, mcp, agent, github, script, workflow

**Gate Logic (Fail-Closed):**

1. **Classify:** task มี code keyword → เป็น CODE TASK
2. **SocratiCode Check:** ต้องเรียก context search จริงก่อน edit file ใด ๆ
3. **Evidence Required:**
   ```
   socraticode_used: true/false
   socraticode_tools_called: [list]
   relevant_files_from_socraticode: [list]
   impact_area: [what changed]
   ```
4. **Gate Decision:**
   - `socraticode_used == true` → ผ่าน Gate → ทำ impact → read/edit → check
   - `socraticode_used != true` → **STOP ทันที** → ห้าม edit file
   - SocratiCode unavailable → **STOP ทันที**

**Fallback Rules (ห้าม!):**
- ห้าม fallback ไปอ่านไฟล์เอง / grep / find / read / edit ถ้า SocratiCode ยังไม่ผ่าน
- ห้ามใช้ grep/search_files/terminal read ก่อน Gate ผ่าน
- ห้ามใช้ patch/write_file/execute_code ก่อน Gate ผ่าน

**Preflight before push:**
```bash
./scripts/code-task-gate.sh check
# exit != 0 → ห้าม push
```

---

## Process Owner Guard (OpenClaw Gateway)

**Core Principle:** Hermes (WSL/Linux) ไม่ใช่ process owner ของ OpenClaw gateway (Windows/Node.js)

Hermes รันบน WSL ส่วน OpenClaw gateway รันบน Windows เป็นคนละเครื่อง ไม่มี PID ร่วมกัน

**Blocked Actions (ห้ามเด็ดขาด):**
- `restart gateway` → `BLOCKED_BY_PROCESS_OWNERSHIP`
- `kill gateway` / `SIGTERM gateway` → `BLOCKED_BY_PROCESS_OWNERSHIP`
- `node gateway` / `node restart` → `BLOCKED_BY_PROCESS_OWNERSHIP`
- `pkill openclaw` / `taskkill` openclaw → `BLOCKED_BY_PROCESS_OWNERSHIP`
- `openclaw restart.cmd` / `launch.cmd` → `BLOCKED_BY_PROCESS_OWNERSHIP`
- `/restart` ที่หมายถึง OpenClaw → `BLOCKED_BY_PROCESS_OWNERSHIP`
- Scheduled Task restart trigger จาก Hermes → `BLOCKED_BY_PROCESS_OWNERSHIP`

**Safe Path — Delegate to OpenClaw-PC:**
1. สร้าง task file ใน `docs/secretary_tasks/inbox/`
2. `target: OpenClaw-PC`
3. `type: gateway_restart`
4. รอ OpenClaw-PC รายงานกลับ
5. ห้าม Hermes รัน `cmd.exe` หรือ PowerShell บน Windows

**Note:** `hermes gateway restart` ใช้กับ **Hermes gateway (Python/WSL)** เท่านั้น ไม่เกี่ยวกับ OpenClaw gateway

---

## Browser Routing Constraint

| Intent | Target | Action |
|--------|--------|--------|
| browser/GUI/ChatGPT/Chrome | OpenClaw-PC | Route ไป OpenClaw ผ่าน task file |
| Hermes internal | Hermes-PC | ทำเอง |

**ห้าม:** Hermes รัน Chrome/Camofox เอง

---

## Token Policy

- เช็ก token level ก่อนทำงานหนัก
- ประหยัดเสมอ: search/excerpt ก่อนอ่านเต็ม
- ระดับ: น้อย ≤25%, ปกติ 26-45%, สูง 46-70%, สูงมาก >70%

---

## Reply Format

- สั้น: 1-3 บรรทัด (ถ้าไม่จำเป็น)
- ไม่ log ยาว, ไม่ format ฟุ้ง
- ถ้าไม่มีอะไรตอบ → `NO_REPLY`

---

## RTK Command Policy

- ใช้ `rtk` prefix ก่อน terminal commands ที่มี output ยาว
- ถ้า RTK ไม่มี wrapper → ใช้คำสั่ง raw แบบจำกัด output
- ห้ามส่ง raw log ยาวให้โมเดล

---

**Last Updated:** 2025-05-14