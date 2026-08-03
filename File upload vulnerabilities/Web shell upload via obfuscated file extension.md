
#portswigger #solution #file_upload

- **Category:** [[File upload vulnerabilities]]
- **Difficulty:** [[PRACTITIONER]]
- **URL Lab:** https://portswigger.net/web-security/learning-paths/file-upload-vulnerabilities
- **Date Solved:** 2026-08-03

---

## 🎯 1. Lab Objective
> Upload a basic PHP web shell and use it to exfiltrate the contents of the file `/home/carlos/secret`. Submit this secret using the button provided in the lab banner.

==CheatSheet==
[[Obfuscating file extensions]]
# File Extension Bypass Cheat Sheet

|  #  | Technique                 | Mechanism                                                            | Example                                                    |
| :-: | :------------------------ | :------------------------------------------------------------------- | :--------------------------------------------------------- |
|  1  | **Multiple Extensions**   | Parsers disagree on which extension takes precedence.                | `exploit.php.jpg`                                          |
|  2  | **Trailing Characters**   | Components automatically strip or ignore trailing spaces or dots.    | `exploit.php.`<br>`exploit.php `                           |
|  3  | **URL Encoding**          | Filename validated pre-decode, then decoded later server-side.       | `exploit%2Ephp`<br>`exploit%252Ephp`                       |
|  4  | **Null Byte / Semicolon** | High-level validator (PHP/Java) vs. low-level C/C++ parser mismatch. | `exploit.asp;.jpg`<br>`exploit.asp%00.jpg`                 |
|  5  | **Multibyte Unicode**     | Unicode normalization converts multibyte characters into dots/nulls. | `xC0 x2E` $\rightarrow$ `.`<br>`xC4 xAE` $\rightarrow$ `.` |
 Some other weird ways to do:
 ![[Pasted image 20260803124937.png]]
 
---

## 🔍 2. Reconnaissance & Vulnerability Analysis
>This lab contains a vulnerable image upload function. Certain file extensions are blacklisted, but this defense can be bypassed using a classic obfuscation technique

---
## 🚀 3. Exploitation

 Typically, the solution is the same as some previous ones, the key difference is changing the PHP script into `script.php%00.png` to trick the server
---

## ⚡ 4. PoC / Final Payload

`script.php%00.png`
[[Webshell script]]
---
## 💡 5. Key Takeaways & Remediation

- **Key Concept:** Upload a malicious PHP script into the 'Avatar Upload' section to gain the system's control
- **Remediation:** [[Preventing File Upload Vulnerabilities]]