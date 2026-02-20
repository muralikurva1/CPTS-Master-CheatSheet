# Passive Information Gathering Checklist

Goal: Expand attack surface without triggering alerts.

---

## 1️⃣ Domain Intelligence

☐ WHOIS lookup  
☐ Identify registrar  
☐ Identify nameservers  
☐ Check domain creation / expiration  
☐ Extract contact emails (if visible)  

Command:
whois domain.com

---

## 2️⃣ DNS Records Enumeration

☐ A record  
☐ AAAA record  
☐ MX record  
☐ TXT record  
☐ SOA record  
☐ NS records  

Commands:
dig domain.com A
dig domain.com AAAA
dig domain.com MX
dig domain.com TXT
dig domain.com SOA
dig domain.com NS

---

## 3️⃣ Zone Transfer Attempt

☐ Attempt AXFR on all nameservers  

Commands:
dig axfr domain.com @ns1.domain.com
dig @ns1.domain.com domain.com axfr

---

## 4️⃣ Certificate Transparency (CT Logs)

☐ Extract subdomains from crt.sh  
☐ Remove wildcard entries  
☐ Deduplicate results  

Commands:
curl -s "https://crt.sh/?q=%25.domain.com&output=json" | jq -r '.[].name_value'
curl -s "https://crt.sh/?q=%25.domain.com&output=json" | jq -r '.[].name_value' | sed 's/\*\.//g' | sort -u

---

## 5️⃣ Subdomain Enumeration (Passive)

☐ sublist3r  
☐ amass (passive mode)  
☐ crt.sh  
☐ search engines  

Commands:
sublist3r -d domain.com
amass enum -passive -d domain.com

---

## 6️⃣ Google Dorking

☐ site:domain.com  
☐ site:*.domain.com  
☐ site:domain.com inurl:admin  
☐ filetype:pdf  
☐ intitle:indexof  
☐ cache:domain.com  

---

## 7️⃣ Email & Employee Harvesting

☐ theHarvester  
☐ hunter.io  
☐ phonebook.cz  
☐ clearbit connect  

Commands:
theHarvester -d domain.com -b all

---

## 8️⃣ Breach Data Check

☐ haveibeenpwned  
☐ dehashed  
☐ breach-parse  

---

## 9️⃣ Infrastructure Intelligence

☐ Shodan host search  
☐ Check exposed ports  
☐ Identify technologies  

Command:
for i in $(cat ip-addresses.txt); do shodan host $i; done

---

## 🔟 Web Footprint

☐ /robots.txt  
☐ /sitemap.xml  
☐ Technology detection (WhatWeb / BuiltWith / Wappalyzer)  
☐ Check WAF presence  

Commands:
whatweb domain.com
wafw00f domain.com
host domain.com

---

## 1️⃣1️⃣ IP Mapping

☐ Map domain → IP  
☐ Reverse IP lookup  
☐ Identify shared hosting  

---

# Final Passive Recon Output

You should have:

☐ Master subdomain list  
☐ DNS record map  
☐ Email list  
☐ Employee list  
☐ Technology stack  
☐ Publicly exposed services  
☐ Potential staging/dev targets  
☐ Possible attack entry points  

---

# Passive Recon Rule

❌ Do NOT:
- Port scan
- Brute force
- Directory fuzz
- Send active probes

That belongs in Active Recon phase.

---

# End Goal

Build a complete attack surface map before touching the target directly.
