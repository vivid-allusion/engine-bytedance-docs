---
title: "GetSourceCode"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-GetSourceCode-cn"
---

获取函数最新版本的代码。本 API 会返回 default 代码文件的代码。

<span id="使用说明"></span>
## 使用说明

请求限流：每秒最多可发送20个请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=GetSourceCode&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `GetSourceCode`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |
|FunctionId |String |是 |函数 ID。您可以调用[ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-cn)获取函数 ID。 |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|SourceCode |String |代码内容。Base64编码格式。 |`"LyoqCiAqIEFkZCB0a******uIG5ldyBSZXNwb25zZSgnSGVsbG8gV29ybGQhJywgeyBzdGF0dXM6IDIwMCB9KTsKfQ=="` |
|WasmSourceCode |String |.wasm 文件的内容。Base64编码格式。仅 OPA 类型的函数才会返回该参数。 |`"AGFzbQEAAAABBwFgAn9/AX8DAgEABAUBcAEBAQUDAQAQBhkDfwFBgIDAAAt/AEGAgMAAC38AQYCAwAALBysEBm1lbW9yeQIAA2FkZAAACl9fZGF0YV9lbmQDAQtfX2hlYXBfYmFzZQMCCgkBBwAgASAAagsALwRuYW1lAAw*****3JlZmVyZW5jZS10eXBlcysIc2lnbi1leHQ="` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```HTTP
GET  https://cdn.byteplusapi.com?Action=GetSourceCode&Version=2021-03-01&FunctionId=3gyz993****
```


<span id="返回示例"></span>
### 返回示例

```json

{
    "ResponseMetadata": {
        "RequestId": "202112072138180102251100110****",
        "Action": "GetSourceCode",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "SourceCode": "LyoqCiAqIEFkZCB0aGUgbmVjZXNzYXJ5IGV2ZW50IGxpc3RlbmVyCiAqIEBwYXJhbSB7RXZlbnR9IGZldGNoIGV2ZW50LCB7RnVuY3Rpb259IGFzeW5jIGZ1bmN0aW9uCiAqLwphZGRFdmVudExpc3RlbmVyKCdmZXRjaCcsIGV2ZW50ID0+IHsKICBldmVudC5yZXNwb25kV2l0aChoYW5kbGVSZXF1ZXN0KGV2ZW50LnJlcXVlc3QpKTsKfSkKCi8qKgogKiBNYWtlIGEgcmVzcG9uc2UgdG8gY2xpZW50CiAqIEBwYXJhbSB7UmVxdWVzdH0gcmVxdWVzdAogKi8KYXN5bmMgZnVuY3Rpb24gaGFuZGxlUmVxdWVzdChyZXF1ZXN0KSB7CiAgcmV0dXJuIG5ldyBSZXNwb25zZSgnSGVsbG8gV29ybGQhJywgeyBzdGF0dXM6IDIwMCB9KTsKfQ=="
    }
}
```


&nbsp;
