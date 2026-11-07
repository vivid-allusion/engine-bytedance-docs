---
title: "Data masking"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/data_masking"
---

Torch Log Service (TLS) Domain Specific Language (DSL) supports a regular replacement function. You can use this function to hide sensitive data in logs and reduce the risk of sensitive data leakage.

<span id="手机号脱敏"></span>
### Mobile phone number masking

To mask a mobile phone number, use the regular replacement function to replace the middle digits of a mobile phone number with specified characters. For example, use the regex_replace function to replace the middle 4 digits of an 11\-digit mobile phone number. This way, incomplete mobile phone number information is displayed.

<span id="原始日志"></span>
#### Logs

```json
[
    {
        "phone":"15199997654"
    }
]
```


<span id="dsl-加工规则"></span>
#### Domain Specification Language (DSL) transformation rules

```python
# Use the regular replacement function.
f_set("phone", regex_replace(v("phone"), "(\\d{0,3})\\d{4}(\\d{4})", replace="$1****$2"))
```


<span id="加工结果"></span>
#### Transformation results

```json
[
    {
        "phone":"151****7654"
    }
]
```


<span id="ip地址脱敏"></span>
### IP address masking

To mask an IP address, use the regular replacement function to replace the middle digits of an IP address with specified characters. For example, the following log contains an IP address. You can use the regex_replace function to mask the IP address after capturing it.

<span id="原始日志"></span>
#### Logs

```json
[
    {
        "ip":"111.222.111.222"
    }
]
```


<span id="dsl-加工规则"></span>
#### Domain Specification Language (DSL) transformation rules

```python
# Use the regular replacement function.
f_set("ip", regex_replace(v("ip"), "(\\d+).(\\d+).(\\d+).(\\d+)", replace="$1.*.*.$4"))
```


<span id="加工结果"></span>
#### Transformation results

```json
[
    {
        "ip":"111.*.*.222"
    }
]
```


<span id="邮箱地址脱敏"></span>
### Email address masking

To mask an **email address**, use the regular replacement function to replace the **prefix of the address** with specified characters. For example, the following log contains a complete email address. You can replace the prefix of the email address except the first character with asterisks( \* ). This way, an incomplete email address is displayed.

<span id="原始日志"></span>
#### Logs

```json
[
    {
        "mail":"seo1893@dev.com"
    }
]
```


<span id="dsl-加工规则"></span>
#### Domain Specification Language (DSL) transformation rules

```python
# Use the regular replacement function.
f_set("mail", regex_replace(v("mail"), "([A-Za-z\d])[A-Za-z\d]+(@.*)", replace="$1***$2"))
```


<span id="加工结果"></span>
#### Transformation results

```json
[
    {
        "mail":"s***@dev.com"
    }
]
```
