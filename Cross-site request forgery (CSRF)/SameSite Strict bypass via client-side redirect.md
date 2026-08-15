
#portswigger #solution #csrf

- **Category:** [[Cross-site request forgery (CSRF)]]
- **Difficulty:** [[PRACTITIONER]]
- **URL Lab:** https://portswigger.net/web-security/learning-paths/csrf
- **Date Solved:** 2026-08-15

The mode's changed to strict now ;(
![[Pasted image 20260815230407.png]]

The email changing request:
```http
POST /my-account/change-email HTTP/2
Host: 0a9300b104bf35f4803ebcf5005b00ee.web-security-academy.net
Cookie: session=uWotWHOm3ZQ4f1YUyg4wPJSeZt5Gm2yB
Content-Length: 40


email=wiener2%40normal-user.net&submit=1
```
There's a new 'submit' parameter

Tried to change the submit=0:

![[Pasted image 20260815230637.png]]

The 'submit' must be 1? So what's the point of it here?
![[Pasted image 20260815230741.png]]

I'll put that 'submit' into my consideration. 
My task now is to find an endpoint that helps me construct a gadget that results in a secondary request within the same site.

![[Pasted image 20260815231449.png]]

There's a comment section, I tried to comment something to this post:
![[Pasted image 20260815232019.png]]
![[Pasted image 20260815231643.png]]
I see, the browser automatically redirects me to home page after I post a comment.

I tried to use the path traversal to manipulate the "Location" header in the response:
![[Pasted image 20260815232154.png]]

It seems favorable, but didn't work