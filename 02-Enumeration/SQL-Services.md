# SQL Services Enumeration

Goal: Identify accessible database services, weak credentials, misconfigurations,
and potential OS-level execution vectors.

---

# MySQL

## Login

mysql -u root -h docker.hackthebox.eu -P 3306 -p

mysql -u julio -pPassword123 -h 10.129.20.13

---

## Database Enumeration

SHOW DATABASES

USE users

SHOW TABLES

DESCRIBE logins

SELECT * FROM table_name

SELECT column1, column2 FROM table_name

SELECT * FROM table_name WHERE <condition>

SELECT * FROM logins WHERE username LIKE 'admin%'

SELECT * FROM logins ORDER BY column_1

SELECT * FROM logins ORDER BY column_1 DESC

SELECT * FROM logins ORDER BY column_1 DESC, id ASC

SELECT * FROM logins LIMIT 2

SELECT * FROM logins LIMIT 1, 2

---

## Table Manipulation

CREATE TABLE logins (id INT, ...)

INSERT INTO table_name VALUES (value_1,..)

INSERT INTO table_name(column2, ...) VALUES (column2_value, ..)

UPDATE table_name SET column1=newvalue1 WHERE <condition>

ALTER TABLE logins ADD newColumn INT

ALTER TABLE logins RENAME COLUMN newColumn TO oldColumn

ALTER TABLE logins MODIFY oldColumn DATE

ALTER TABLE logins DROP oldColumn

DROP TABLE logins

---

# MSSQL

sqlcmd -S SRVMSSQL\SQLEXPRESS -U julio -P 'MyPassword!' -y 30 -Y 30

sqsh -S 10.129...

mssqlclient.py sql_dev@10.129.43.30 -windows-auth

---

## xp_cmdshell Abuse

enable_xp_cmdshell

xp_cmdshell whoami

---

# Tactical Notes

- Always attempt weak credentials first.
- Check if SQL runs as SYSTEM (MSSQL).
- Attempt xp_cmdshell.
- Check for file read/write privileges.
- Look for database service accounts.
