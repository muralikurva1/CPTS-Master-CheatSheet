# Windows Defender Evasion

Goal: Disable or bypass Microsoft Defender protections.

---

# Check Defender Status

Get-MpComputerStatus

---

# Disable Real-Time Monitoring

Set-MpPreference -DisableRealtimeMonitoring $true

---

# Tactical Notes

- Requires elevated privileges.
- May trigger alerts.
- Use briefly and re-enable if OPSEC required.
