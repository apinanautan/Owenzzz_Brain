# Known Issues: Things That Are Still Broken

> อัปเดตเมื่อเจอปัญหาใหม่ หรือเมื่อแก้แล้ว

## Active Issues

### 🔴 ChatGPT Login/Session
- **Problem:** ChatGPT/OwenGPT หลุด session บ่อย
- **Symptom:** UFO/Camofox login ต้องทำใหม่
- **Workaround:** ใช้ browser บน OpenClaw-PC, monitor session
- **Last seen:** 2025-05-14

### 🟡 Path Translation (Windows ↔ WSL)
- **Problem:** path ต่างกันระหว่าง Windows และ WSL
- **Symptom:** `C:\Users\Apinan` vs `/c/Users/Apinan`
- **Workaround:** ใช้ `/c/Users/` prefix ใน WSL commands
- **Status:** Known, manageable

### 🟡 Provider Quota (ollama-pay)
- **Problem:** deepseek-v4-flash อาจ quota exhausted
- **Symptom:** Model switch หรือ API error
- **Workaround:** ตรวจ token level ก่อนทำงานหนัก
- **Status:** Monitoring

### 🔴 UFO Instability
- **Problem:** UFO browser automation ค้าง/ตายบ่อย
- **Symptom:** UFO process ไม่ตอบสนอง
- **Workaround:** OpenClaw-PC watchdog, manual restart
- **Last seen:** 2025-05-14

### 🟡 Hermes Gateway (Python)
- **Problem:** Hermes gateway บน WSL อาจต้อง restart
- **Symptom:** Telegram disconnect
- **Workaround:** `hermes gateway restart`
- **Status:** Occasional

## Resolved Issues

### ✅ Safe Autopush
- **Problem:** git hooks ไม่ทำงาน
- **Solution:** ใช้ skill safe-autopush แทน
- **Resolved:** 2025-05-14

### ✅ Task File Routing
- **Problem:** Hermes ไม่รู้จะ route task ไปไหน
- **Solution:** docs/secretary_tasks/ + target field
- **Resolved:** 2025-05-14

### ✅ Chrome Relay Protocol
- **Problem:** Hermes พยายาม run Chrome เอง
- **Solution:** Chrome relay via OpenClaw task
- **Resolved:** 2025-05-14

## Notes
- ปัญหา Chrome/ChatGPT login เป็นปัญหาหลักที่ต้อง monitor
- UFO instability ทำให้ต้องมี watchdog เสมอ