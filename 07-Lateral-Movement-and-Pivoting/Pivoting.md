# Pivoting & Tunneling

Goal: Access internal networks through compromised host.

---

# SSH Local Port Forward

ssh -L 1234:localhost:3306 ubuntu@<IP>

---

# SSH Dynamic SOCKS Proxy

ssh -D 9050 ubuntu@<IP>

---

# Proxychains Nmap

proxychains nmap -v -Pn -sT 172.16.5.19

---

# Proxychains Metasploit

proxychains msfconsole

---

# Metasploit Database Scan

db_nmap

---

# Tactical Notes

- Use dynamic SOCKS for full internal pivot.
- Always verify route before scanning.
- Combine with proxychains.conf update.
