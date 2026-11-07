---
title: "CanaryPublish"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-CanaryPublish-zh-tw"
---

對函數進行金絲雀發佈。

<span id="使用說明"></span>
## 使用說明

請求限制：每秒最多可傳送 20 個請求。另外，對於每個函數，每秒最多可傳送 1 個請求。

<span id="請求說明"></span>
## 請求說明


* Request Method：POST

* Request URL： https://cdn.byteplusapi.com?Action=CanaryPublish&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |是否必選 |描述 |
|---|---|---|---|
|Action |String |是 |介面名稱。目前 API 的名稱為 `CanaryPublish`。 |
|Version |String |是 |介面版本。目前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |是否必選 |描述 |範例值 |
|---|---|---|---|---|
|FunctionId |String |是 |函數 ID。您可以呼叫[ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-zh-tw)取得函數 ID。 |`3gyz993****` |
|Description |String |否 |填寫此次發佈的描述資訊。 |`test publish` |


<span id="返回參數"></span>
## 返回參數


|參數 |類型 |描述 |範例值 |
|---|---|---|---|
|TicketId |Long |發佈記錄的 ID。 |`261285442399182****` |


<span id="範例"></span>
## 範例

<span id="請求範例"></span>
### 請求範例

```json
POST https://cdn.byteplusapi.com/?Action=CanaryPublish&Version=2021-03-01
{
    "FunctionId": "3gyz993****",
    "Description": "test publish"
}
```


<span id="返回範例"></span>
### 返回範例

```json

{
    "ResponseMetadata": {
        "RequestId": "202112072116030102251331430*****",
        "Action": "CanaryPublish",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "TicketId": "261285442399182****"
    }
}
```


&nbsp;
