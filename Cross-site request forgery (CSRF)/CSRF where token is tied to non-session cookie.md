

#portswigger #solution #csrf

- **Category:** [[Cross-site request forgery (CSRF)]]
- **Difficulty:** [[PRACTITIONER]]
- **URL Lab:** https://portswigger.net/web-security/learning-paths/csrf
- **Date Solved:** 2026-08-13

![[Pasted image 20260813165112.png]]

I think this LAB's exploit method is similar to the previous one: [[CSRF where token is not tied to user session]]
The point is, we need to somehow modify victim's cookie to ours.

Notice that there is a addition functionality added: The search bar.
![[Pasted image 20260813165440.png]]

I hadn't known what is its role in this LAB yet.
Until I looked at the /login request:
![[Pasted image 20260813165626.png]]

Surprisingly, the website stored my "LastSearchTerm" for absolutely no reason;) So I figured out a trick that can potentially modify my own cookie (What I can use with my victim too):
I simply send a GET request to attempt for a search like:

```http
GET /?search=a%3B+csrfKey%3Dchanged_csrf_cookie HTTP/2
Host: 0a4f009b0365817b80deae2b00e900e9.web-security-academy.net
```
 and it didn't work, unfortunately ;)

