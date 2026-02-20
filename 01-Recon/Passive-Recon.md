# Passive Reconnaissance

Passive reconnaissance involves gathering information about the target
without directly interacting with it in a detectable manner.

Risk Level: LOW  
Goal: Expand attack surface before active probing.

---

# WHOIS Enumeration

whois example.com

### Tactical Notes
- Identify domain owner
- Registrar
- Creation & expiration dates
- Nameservers
- Contact emails
- Privacy masking detection

---

# Certificate Transparency (CT Logs)

## Basic JSON Dump

curl -s https://crt.sh/\?q\=<target-domain>\&output\=json | jq .

## Extract Subdomains

curl -s "https://crt.sh/?q=%25.example.com&output=json" | jq -r '.[].name_value'

## Alternative Extraction with Cleanup

curl -s "https://crt.sh/?q=%25.example.com&output=json" | jq -r '.[].name_value' | sed 's/\*\.//g' | sort -u

### Tactical Notes
- Completely passive
- Reveals staging/dev subdomains
- Often exposes forgotten services
- Combine with DNS brute force later

---

# DNS Passive Enumeration

## Query A Record

dig example.com A

## Query Specific Nameserver

dig ns <domain.tld> @<nameserver>

## ANY Record Request

dig any <domain.tld> @<nameserver>

### Tactical Notes
- ANY may be restricted
- Identify NS servers for potential zone transfer testing
- Identify mail servers (MX records)

---

# Certificate Transparency via Direct JSON API

curl -s "https://crt.sh/?q=%25.example.com&output=json"

---

# Shodan Enumeration

for i in $(cat ip-addresses.txt);do shodan host $i;done

### Tactical Notes
- Identify exposed ports
- Identify known vulnerabilities
- Service fingerprinting
- Passive infrastructure mapping

---

# DNS Records Overview

## A Record

dig example.com A

## AAAA Record

dig example.com AAAA

## MX Record

dig example.com MX

## TXT Record

dig example.com TXT

## SOA Record

dig example.com SOA

---

# Zone Transfer Attempt (Still Low-Noise)

dig axfr <domain.tld> @<nameserver>

dig @ns1.example.com example.com axfr

### Tactical Notes
- If misconfigured → full DNS blueprint
- Rare but high impact
- Always attempt once

---

# Subdomain Discovery (Passive)

## Using Certificate Transparency

curl -s "https://crt.sh/?q=%25.example.com&output=json" | jq -r '.[].name_value'

---

# Infrastructure-Based Enumeration

## Certificate Transparency with jq formatting

curl -s https://crt.sh/\?q\=<target-domain>\&output\=json | jq .

---

# General Web Recon Principles

Passive Techniques Include:
- WHOIS lookups
- DNS enumeration
- Certificate Transparency logs
- Search engine queries
- Web archive analysis
- Social media intelligence

Active Techniques (covered in Active-Recon.md):
- Port scanning
- DNS brute forcing
- VHost brute forcing
- Directory fuzzing

---

# Passive Recon Workflow

1. WHOIS
2. DNS A / MX / NS records
3. Certificate Transparency logs
4. Extract subdomains
5. Enumerate infrastructure with Shodan
6. Map IP → domain relationships
7. Identify potential exposed services

Goal: Expand attack surface without triggering alerts.
