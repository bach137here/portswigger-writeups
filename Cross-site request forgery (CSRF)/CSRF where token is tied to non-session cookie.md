

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

![[Pasted image 20260813170813.png]]
somehow they threw the Set-Cookie for csrfKey away and I think my main goal here is to figure it out.
And I realise that we need a different Set-Cookie Header for the csrfKey. So that I tried this payload:

Second trial:
![[Pasted image 20260813171543.png]]
Of course it didn't work ;(

![[Pasted image 20260813171700.png]]

After a few more attempts, I asked AI for help:

![[Pasted image 20260813172025.png]]

