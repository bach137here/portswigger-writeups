
#portswigger #solution #csrf

- **Category:** [[Cross-site request forgery (CSRF)]]
- **Difficulty:** [[PRACTITIONER]]
- **URL Lab:** https://portswigger.net/web-security/learning-paths/csrf
- **Date Solved:** 2026-08-13


![[Pasted image 20260813160608.png]]

Email changing request:

```http
POST /my-account/change-email HTTP/2
Host: 0a0f004d03056387802c0d87008f00fa.web-security-academy.net
Cookie: session=XRCEr4xdKE3dRlJDgmixiQVKBG71R7dA
...

email=random%40random.com&csrf=jMA1oRozOWtViq2zhbHfpOnP6ZhCUo8Y
```

In second attempt:
```http
POST /my-account/change-email HTTP/2
Host: 0a0f004d03056387802c0d87008f00fa.web-security-academy.net
Cookie: session=XRCEr4xdKE3dRlJDgmixiQVKBG71R7dA
...

email=random2%40random.com&csrf=xTlrFfVd3bPfxSsqVm0MilYTiW1mKbGN
```

We observe that the csrf token change everytime we submit changing our emails.

