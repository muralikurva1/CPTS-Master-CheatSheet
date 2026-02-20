# AppLocker Enumeration & Bypass

Goal: Identify application whitelisting policies.

---

# View Effective AppLocker Policy

Get-AppLockerPolicy -Effective | select -ExpandProperty RuleCollections

---

# Test AppLocker Policy

Get-AppLockerPolicy -Local | Test-AppLockerPolicy -path C:\Windows\System32\cmd.exe -User Everyone

---

# Tactical Notes

- Check if PowerShell is restricted.
- Look for writable directories allowed by policy.
- DLL hijacking often bypasses AppLocker.
