
#portswigger #solution #file_upload

- **Category:** [[File upload vulnerabilities]]
- **Difficulty:** [[PRACTITIONER]]
- **URL Lab:** https://portswigger.net/web-security/learning-paths/file-upload-vulnerabilities
- **Date Solved:** 2026-08-04

---

## 🎯 1. Lab Objective
> Upload a basic PHP web shell and use it to exfiltrate the contents of the file `/home/carlos/secret`. Submit this secret using the button provided in the lab banner.

---

## 🔍 2. Reconnaissance & Vulnerability Analysis
>This lab contains a vulnerable image upload function. Certain file extensions are blacklisted, but this defense can be bypassed due to a fundamental flaw in the configuration of this blacklist.

---
## 🚀 3. Exploitation

First, I tried to upload the [[Webshell script]] directly and this is the result:
 ![[Pasted image 20260803120810.png]]
 
 The server blacklisted .php extension. But the key is, I'm allowed to upload .htaccess file to configure the setting of this Apache server. So that, I added a new file exstension named .bachphan and declare its MIME type to an executable one:
 ```htaccess
 AddType application/x-httpd-php .bachphan
 ```
 
 I modified my script extension to `script.bachphan` after uploading the `.htaccess` configuration file and it worked !
![[Pasted image 20260803121546.png]]


![[Pasted image 20260803121751.png]]

---

## ⚡ 4. PoC / Final Payload

Configuration file: 
 ```htaccess
 AddType application/x-httpd-php .bachphan
 ```
Script name: `script.bachphan`
[[Webshell script]]
---
## 💡 5. Key Takeaways & Remediation

- **Key Concept:** Upload a malicious PHP script into the 'Avatar Upload' section to gain the system's control
- **Remediation:** [[Preventing File Upload Vulnerabilities]]