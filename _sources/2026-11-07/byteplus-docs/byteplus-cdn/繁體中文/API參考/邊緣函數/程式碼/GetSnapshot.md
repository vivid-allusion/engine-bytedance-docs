---
title: "GetSnapshot"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-GetsnapShot-zh-tw"
---

查看指定版本的程式碼。

<span id="使用說明"></span>
## 使用說明

請求限制：每秒最多可傳送 20 個請求。

<span id="請求說明"></span>
## 請求說明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=GetSnapshot&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |是否必選 |描述 |
|---|---|---|---|
|Action |String |是 |介面名稱。目前 API 的名稱為 `GetSnapshot`。 |
|Version |String |是 |介面版本。目前 API 的版本為 `2021-03-01`。 |
|FunctionId |String |是 |函數 ID。您可以呼叫[ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-zh-tw)取得函數 ID。 |
|VersionTag |String |是 |版本號。您可以透過呼叫介面[ListVersions](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListVersions-zh-tw)取得版本號。 |


<span id="返回參數"></span>
## 返回參數


|參數 |類型 |描述 |範例值 |
|---|---|---|---|
|SourceCode |String |函數程式碼。 | |
|script_type |String |腳本類型。 |`js` |
|source |String |程式碼內容。程式碼轉換為 Base64 編碼格式。 |`LyoqCiAqIEFkZCB0aGUgbmVjZXNzYXJ5IGV2ZW5******B7CiAgcmV0dXJuIG5ldyBSZXNwb25zZSgnSGVsbG8gV29ybGQhJywgeyBzdGF0dXM6IDIwMCB9KTsKfQ==` |
|Config |String |函數設定。 | |
|config |JSONMap |函數設定。 | |


<span id="範例"></span>
## 範例

<span id="請求範例"></span>
### 請求範例

```HTTP
GET  https://cdn.byteplusapi.com?Action=GetSnapshot&Version=2021-03-01&FunctionId=3gyz993****&VersionTag=1.0.1
```


<span id="返回範例"></span>
### 返回範例

```json

{
    "ResponseMetadata": {
        "RequestId": "2022021014244901022524313903*****",
        "Action": "GetSnapshot",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "SourceCode": "{\"script_type\":\"js\",\"source\":\"LyoqCiAqIEFkZCB0aGUgbmVjZXNzYXJ5IGV2ZW50IGxpc3RlbmVyCiAqIEBwYXJhbSB7RXZlbnR9IGZldGNoIGV2ZW50LCB7RnVuY3Rpb259IGFzeW5jIGZ1bmN0aW9uCiAqLwphZGRFdmVudExpc3RlbmVyKCdmZXRjaCcsIGV2ZW50ID0+IHsKICBldmVudC5yZXNwb25kV2l0aChoYW5kbGVSZXF1ZXN0KGV2ZW50LnJlcXVlc3QpKTsKfSkKCi8qKgogKiBNYWtlIGEgcmVzcG9uc2UgdG8gY2xpZW50CiAqIEBwYXJhbSB7UmVxdWVzdH0gcmVxdWVzdAogKi8KYXN5bmMgZnVuY3Rpb24gaGFuZGxlUmVxdWVzdChyZXF1ZXN0KSB7CiAgcmV0dXJuIG5ldyBSZXNwb25zZSgnSGVsbG8gV29ybGQhJywgeyBzdGF0dXM6IDIwMCB9KTsKfQ==\"}",
        "Config": "{\"config\":{},\"env\":{\"js\":{\"default\":{\"wer\":\"wer\"}}}}"
    }
}
```


&nbsp;
