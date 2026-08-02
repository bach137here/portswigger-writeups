
#portswigger #solution #file_upload

- **Category:** [[File upload vulnerabilities]]
- **Difficulty:** [[PRACTITIONER]]
- **URL Lab:** https://portswigger.net/web-security/learning-paths/file-upload-vulnerabilities
- **Date Solved:** 2026-08-02

---

## 🎯 1. Lab Objective
> Upload a basic PHP web shell and use it to exfiltrate the contents of the file `/home/carlos/secret`. Submit this secret using the button provided in the lab banner.

---

## 🔍 2. Reconnaissance & Vulnerability Analysis
>This lab contains a vulnerable image upload function. The server is configured to prevent execution of user-supplied files, but this restriction can be bypassed by exploiting a secondary vulnerability.

 I tried to upload the [[Webshell script]] directly and this is the result:
 ![[Pasted image 20260802164442.png]]
 ![[Pasted image 20260802164512.png]]
 
 The problem is, the server treats my script as a text file and this is unexecutable.
 ![[Pasted image 20260802164646.png]]

 After playing around for a while I realized that there is an "Upload Avatar" functionality below each post, which is really weird and my remaining work is easy now

---

## ⚡ 4. PoC / Final Payload

[[Webshell script]]
---
## 💡 5. Key Takeaways & Remediation

- **Key Concept:** Upload a malicious PHP script into the 'Avatar Upload' section to gain the system's control
- **Remediation:** [[Preventing File Upload Vulnerabilities]]