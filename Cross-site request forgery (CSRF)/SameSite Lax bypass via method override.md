
#portswigger #solution #csrf

- **Category:** [[Cross-site request forgery (CSRF)]]
- **Difficulty:** [[PRACTITIONER]]
- **URL Lab:** https://portswigger.net/web-security/learning-paths/csrf
- **Date Solved:** 2026-08-15


The theme of this LAB is the same as other ones. The key difference here is that there's no more other kind of cookies except the session one:
![[Pasted image 20260815223943.png]]
(Default mode for the session cookie is Lax)

Changing email request:
```http
POST /my-account/change-email HTTP/2
Host: 0acf00f4047d26ca80f0449100a7006c.web-security-academy.net
Cookie: session=lR3ExNZJU27JhExuuA1qFlSc4lW2r2pr
Content-Length: 29
Cache-Control: max-age=0
Sec-Ch-Ua: "Not;A=Brand";v="8", "Chromium";v="150"
Sec-Ch-Ua-Mobile: ?0
Sec-Ch-Ua-Platform: "Windows"
Accept-Language: en-US,en;q=0.9
Upgrade-Insecure-Requests: 1
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/150.0.0.0 Safari/537.36
Origin: https://0acf00f4047d26ca80f0449100a7006c.web-security-academy.net
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Referer: https://0acf00f4047d26ca80f0449100a7006c.web-security-academy.net/my-account?id=wiener
Accept-Encoding: gzip, deflate, br
Priority: u=0, i

email=wiener%40crazy-user.net

```
We don't need other parameters over