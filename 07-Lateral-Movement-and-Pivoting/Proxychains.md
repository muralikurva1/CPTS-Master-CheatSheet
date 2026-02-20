# Proxychains Usage

Goal: Route traffic through SOCKS proxy.

---

# Configure Proxychains

nano /etc/proxychains.conf

---

# Example Usage

proxychains nmap -v -Pn -sT 172.16.5.19

proxychains msfconsole

proxychains xfreerdp /v:<IP> /u:victor /p:pass@123

---

# Tactical Notes

- Ensure SOCKS port matches SSH -D.
- DNS resolution may need proxychains DNS option.
