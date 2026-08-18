
#portswigger #solution #xss

- **Category:** [[Cross-site scriping (XSS)]]
- **Difficulty:** [[PRACTITIONER]]
- **URL Lab:** https://portswigger.net/web-security/cross-site-scripting/contexts/lab-html-context-with-most-tags-and-attributes-blocked
- **Date Solved:** 2026-08-18

![[Pasted image 20260818231359.png]]

![[Pasted image 20260818231343.png]]



![[Pasted image 20260818231456.png]]


![[Pasted image 20260818231508.png]]


![[Pasted image 20260818231534.png]]

=> Work



Only ``<body>`` tag works


![[Pasted image 20260818231326.png]]


![[Pasted image 20260818232102.png]]

![[Pasted image 20260818233806.png]]

I put some effort to find a way to exploit using ``<body>``, I found this payload:
```html
<body oncontentvisibilityautostatechange=print() style=display:block;content-visibility:auto>
```

it worked and i sent to my victim:
![[Pasted image 20260818235654.png]]