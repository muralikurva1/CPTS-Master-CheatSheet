# NFS Enumeration

Goal: Identify exposed NFS shares and potential privilege escalation vectors.

---

# Show Exports

showmount -e <FQDN/IP>

---

# Mount Share

mount -t nfs <FQDN/IP>:/<share> ./target-NFS/ -o nolock

---

# Unmount Share

umount ./target-NFS

---

# Tactical Notes

- Check for no_root_squash.
- Look for SSH keys.
- Look for sensitive backups.
- Look for writable directories.
