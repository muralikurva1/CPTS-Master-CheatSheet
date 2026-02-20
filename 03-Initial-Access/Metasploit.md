# Metasploit Framework

Goal: Exploit vulnerabilities and gain shell access.

---

# Core Commands

show exploits

show payloads

show auxiliary

search <name>

info

use <name>

use <number>

set <option>

setg <option>

show options

show targets

set target <number>

set payload <payload>

set payload <number>

show advanced

set autorunscript migrate -f

check

exploit

exploit -j

exploit -z

exploit -e <encoder>

exploit -h

---

# Sessions

sessions -l

sessions -l -v

sessions -s <script>

sessions -K

sessions -c <cmd>

sessions -u <sessionID>

---

# Database

db_create <name>

db_connect <name>

db_nmap

db_destroy

db_destroy <user:password@host:port/database>

---

# Modules Used

use exploit/windows/smb/psexec

use auxiliary/scanner/smb/smb_ms17_010

use exploit/windows/smb/ms17_010_psexec

use exploit/linux/http/rconfig_vendors_auth_file_upload_rce

---

# Tactical Notes

- Always run check before exploit.
- Use -j for background jobs.
- Upgrade shells to meterpreter.
- Use db_nmap for target management.
