---
title: "GetTicket"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-GetTicket-zh-tw"
---

取得發佈記錄。

<span id="使用說明"></span>
## 使用說明

請求限流：每秒最多可發送20個請求。

<span id="請求說明"></span>
## 請求說明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=GetTicket&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |是否必選 |描述 |
|---|---|---|---|
|Action |String |是 |介面名稱。目前 API 的名稱為 `GetTicket`。 |
|Version |String |是 |介面版本。目前 API 的版本為 `2021-03-01`。 |
|FunctionId |String |是 |函數 ID。您可以呼叫[ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-zh-tw)取得函數 ID。 |
|TicketId |Long |是 |發佈記錄 ID。 |


<span id="返回參數"></span>
## 返回參數


|參數 |類型 |描述 |範例值 |
|---|---|---|---|
|Ticket |Object |發佈記錄詳情。 | |
|Id |Long |發佈記錄 ID。 |`1` |
|FunctionId |String |函數 ID。 |`23455331245` |
|Content |String |發佈記錄的內容。 |`{&quot;current_traffics&quot;:[{&quot;version_tag&quot;:&quot;1.0.1&quot;}],&quot;origin_traffics&quot;:[]}` |
|Status |Integer |發佈狀態。<br><br><br>* 100：金絲雀發佈成功。<br><br>* 200：全量發佈成功。 |`100` |
|Description |String |發佈記錄的描述。 |`this is a release` |
|Creator |String |發佈記錄的建立者。 |`test_user` |
|CreateTime |Long |發佈記錄的建立時間。格式為 Unix 時間標記（秒）。 |`1638326159` |
|UpdateTime |Long |發佈記錄的更新時間。格式為 Unix 時間標記（秒）。 |`1638326159` |


<span id="範例"></span>
## 範例

<span id="請求範例"></span>
### 請求範例

```json
GET  https://cdn.byteplusapi.com?Action=GetTicket&Version=2021-03-01&FunctionId=3gyz993****&TicketId=28
```


<span id="返回範例"></span>
### 返回範例

```json
{
    "ResponseMetadata": {
        "RequestId": "2022011310531001022511001100*****",
        "Action": "GetTicket",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Ticket":
         {
            "Id": 133,
            "FunctionId": "3gyz993****",
            "Content": "{\"current_traffics\":[{\"version_tag\":\"1.0.1\"}],\"origin_traffics\":[]}",
            "Description": "test publish",
            "Creator": "****",
            "CreateTime": 1640077698,
            "UpdateTime": 1640077759
        }
    }
}
```


&nbsp;
