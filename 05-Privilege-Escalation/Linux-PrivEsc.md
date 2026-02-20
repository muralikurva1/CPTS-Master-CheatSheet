# Linux Privilege Escalation

Goal: Escalate from low-privileged user to root.

---

# Basic Enumeration

whoami

id

hostname

uname -a

cat /etc/issue

cat /etc/os-release

env

set

---

# Process Enumeration

ps aux

ps aux | grep root

---

# Sudo Permissions

sudo -l

---

# SUID Binaries

find / -perm -4000 2>/dev/null

---

# Writable Directories

find / -writable -type d 2>/dev/null

---

# Cron Jobs

ls -la /etc/cron.daily

cat /etc/crontab

---

# PATH Abuse

echo $PATH

---

# Network

netstat -tulpn

ss -tulpn

---

# Installed Packages

dpkg -l

rpm -qa

---

# Kernel Exploit Checks

uname -a

---

# Tactical Notes

- Check sudo -l first.
- Look for writable cron scripts.
- Exploit SUID binaries.
- Check for outdated kernel.
- Inspect PATH for writable directories.
