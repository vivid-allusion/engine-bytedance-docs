---
title: "SnapshotPublish"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-SnapshotPublish-zh-tw"
---

將函數程式碼回滾到指定版本。

<span id="使用說明"></span>
## 使用說明

請求限制：每秒最多可傳送 20 個請求。另外，對於每個函數，每秒最多可傳送 1 個請求。

<span id="請求說明"></span>
## 請求說明


* Request Method：POST

* Request URL： https://cdn.byteplusapi.com?Action=SnapshotPublish&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |是否必選 |描述 |
|---|---|---|---|
|Action |String |是 |介面名稱。目前 API 的名稱為 `SnapshotPublish`。 |
|Version |String |是 |介面版本。目前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |是否必選 |描述 |範例值 |
|---|---|---|---|---|
|FunctionId |String |是 |函數 ID。您可以呼叫[ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-zh-tw)取得函數 ID。 |`3gyz993****` |
|VersionTag |String |是 |版本號。您可以透過呼叫介面[ListVersions](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListVersions-cn)取得版本號。 |`1.0.1` |
|PublishType |Integer |是 |發佈類型：<br><br><br>* 200：全量發佈<br><br>* 100：金絲雀發佈 |`200` |
|Description |String |否 |填寫此次發佈的描述資訊。 |`test publish` |


<span id="返回參數"></span>
## 返回參數


|參數 |類型 |描述 |範例值 |
|---|---|---|---|
|TicketId |String |發佈記錄的 ID。 |`278335600748419****` |


<span id="範例"></span>
## 範例

<span id="請求範例"></span>
### 請求範例

```json
POST https://cdn.byteplusapi.com/?Action=SnapshotPublish&Version=2021-03-01
{
    "FunctionId": "3gyz993****",
    "PublishType": 200,
    "VersionTag": "1.0.1"
}
```


<span id="返回範例"></span>
### 返回範例

```json

{
    "ResponseMetadata": {
        "RequestId": "202112072116030102251331430*****",
        "Action": "SnapshotPublish",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "TicketId": "278335600748419****"
    }
}
```


&nbsp;
