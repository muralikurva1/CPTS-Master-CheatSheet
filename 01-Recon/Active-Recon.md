# Active Reconnaissance

Active reconnaissance involves directly interacting with the target.
Higher detection risk but deeper visibility.

Risk Level: MEDIUM–HIGH  
Goal: Discover live hosts, open ports, services, and attack surface.

---

# Network Interface & Routing Enumeration

## Linux

ifconfig

netstat -r

## Windows

ipconfig

ipconfig /all

arp -a

route print

---

# Host Discovery

## Ping Sweep

fping -asgq 172.16.5.0/23

### Tactical Notes
- Fast subnet sweep
- May be blocked by firewall
- Use before full port scan

---

# Packet Capture

sudo tcpdump -i ens224

### Tactical Notes
- Identify broadcast traffic
- Detect LLMNR / NBNS
- Discover internal hosts passively

---

# Nmap Scanning

## Full Scan with OS + Scripts

sudo nmap -v -A -iL hosts.txt -oN /home/User/Documents/host-enum

## Targeted Port Scan

nmap -sT -p22,3306 <IPaddressofTarget>

## Scan Through Local Tunnel

nmap -v -sV -p1234 localhost

---

# DNS Enumeration (Active)

dnsenum example.com -f subdomains.txt

dnsenum --dnsserver <nameserver> --enum -p 0 -s 0 -o

---

# Virtual Host Enumeration

gobuster vhost -u http://192.0.2.1 -w hostnames.txt

### Tactical Notes
- Required when multiple domains share same IP
- Critical for internal web servers

---

# Web Enumeration – FFUF

## Help

ffuf -h

---

## Directory Fuzzing

ffuf -w wordlist.txt:FUZZ -u http://SERVER_IP:PORT/FUZZ

ffuf -w wordlist.txt:FUZZ -u http://SERVER_IP:PORT/indexFUZZ

ffuf -w wordlist.txt:FUZZ -u http://SERVER_IP:PORT/blog/FUZZ.php

---

## Recursive Fuzzing

ffuf -w wordlist.txt:FUZZ -u http://SERVER_IP:PORT/FUZZ -recursion -recursion-depth 1 -e .php -v

---

## Subdomain Fuzzing

ffuf -w wordlist.txt:FUZZ -u https://FUZZ.hackthebox.eu/

---

## Virtual Host Fuzzing

ffuf -w wordlist.txt:FUZZ -u http://academy.htb:PORT/ -H 'Host: FUZZ.academy.htb' -fs xxx

---

## GET Parameter Fuzzing

ffuf -w wordlist.txt:FUZZ -u http://admin.academy.htb:PORT/admin/admin.php?FUZZ=key -fs xxx

---

## POST Parameter Fuzzing

ffuf -w wordlist.txt:FUZZ -u http://admin.academy.htb:PORT/admin/admin.php -X POST -d 'FUZZ=key' -H 'Content-Type: application/x-www-form-urlencoded' -fs xxx

---

## Value Fuzzing

ffuf -w ids.txt:FUZZ -u http://admin.academy.htb:PORT/admin/admin.php -X POST -d 'id=FUZZ' -H 'Content-Type: application/x-www-form-urlencoded' -fs xxx

---

# Wordlists Used

/opt/useful/seclists/Discovery/Web-Content/directory-list-2.3-small.txt

/opt/useful/seclists/Discovery/Web-Content/web-extensions.txt

/opt/useful/seclists/Discovery/DNS/subdomains-top1million-5000.txt

/opt/useful/seclists/Discovery/Web-Content/burp-parameter-names.txt

---

# Hosts File Modification

sudo sh -c 'echo "SERVER_IP academy.htb" >> /etc/hosts'

---

# Generate Numeric Wordlist

for i in $(seq 1 1000); do echo $i >> ids.txt; done

---

# Manual POST Request

curl http://admin.academy.htb:PORT/admin/admin.php -X POST -d 'id=key' -H 'Content-Type: application/x-www-form-urlencoded'

---

# Active Recon Workflow

1. Identify network interfaces
2. Discover live hosts
3. Scan open ports
4. Identify services & versions
5. Enumerate DNS actively
6. Discover VHosts
7. Fuzz directories
8. Fuzz parameters
9. Identify hidden endpoints

Goal: Build full attack surface map.
