---
title: "GetScriptSourceCode"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/GetScriptSourceCode"
---

该接口用于基于函数ID获取函数中所有脚本文件的代码。

<span id="使用说明"></span>
## 使用说明

请求限流：每秒最多可发送20个请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=GetScriptSourceCode&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `GetScriptSourceCode`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |
|FunctionId |String |是 |函数id |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|ScriptSourceCode |JSONMap |函数代码 |`See the explanation below.` |
|_key |String |脚本文件的名称。 |`See the explanation below.` |
|_value |String |脚本文件的代码内容。代码转换为Base64编码格式。 |`See the explanation below.` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
GET  https://cdn.byteplusapi.com?Action=GetScriptSourceCode&Version=2021-03-01&FunctionId=3gyz993****
```


<span id="返回示例"></span>
### 返回示例

```json

{
    "ResponseMetadata": {
        "RequestId": "2022021014244901022524313903*****",
        "Action": "GetScriptSourceCode",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "ScriptSourceCode": {
            "test": "LyoqCiAqIEFkZCB0aGUgbmVjZXNzYXJ5IGV2ZW50IGxpc3RlbmVyCiAqIEBwYXJhbSB7RXZlbnR9IGZldGNoIGV2ZW50LCB7RnVuY3Rpb259IGFzeW5jIGZ1bmN0aW9uCiAqLwphZGRFdmVudExpc3RlbmVyKCdmZXRjaCcsIGV2ZW50ID0+IHsKICBldmVudC5yZXNwb25kV2l0aChoYW5kbGVSZXF1ZXN0KGV2ZW50LnJlcXVlc3QpKTsKfSkKCi8qKgogKiBNYWtlIGEgcmVzcG9uc2UgdG8gY2xpZW50CiAqIEBwYXJhbSB7UmVxdWVzdH0gcmVxdWVzdAoKQHJldHVybiAqLwphc3luYyBmdW5jdGlvbiBoYW5kbGVSZXF1ZXN0KHJlcXVlc3QpIHsKICByZXR1cm4gbmV3IFJlc3BvbnNlKCdIZWxsbyBXb3JsZCEnLCB7IHN0YXR1czogMjAwIH0pOwp9Cg=="
        }
    }
}
```


&nbsp;
