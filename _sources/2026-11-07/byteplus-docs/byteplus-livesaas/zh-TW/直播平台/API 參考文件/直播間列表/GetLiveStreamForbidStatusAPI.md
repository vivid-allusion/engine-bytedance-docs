---
title: "GetLiveStreamForbidStatusAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getlivestreamforbidstatusapi-zh-TW"
---

調用此 API 以檢查直播間中特定直播來源的串流是否被禁播。

<span id="708ec574"></span>
## 需求

配額：每個帳戶每分鐘 120 次查詢

<span id="ed67113c"></span>
## HTTP 請求


* URL：`https://livesaas.byteplusapi.com/?Action=GetLiveStreamForbidStatusAPI&Version=2020-06-01`

* 方法：POST


<span id="Request"></span>
## 請求參數

下列表格未包含所有共用請求參數。如需完整列表，請參見[共用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/gong-yong-can-shu-zh-TW#f1706967)。

<span id="19a94c8d"></span>
### 查詢


|名稱 |資料型別 |是否必填 |範例值 |說明 |
|---|---|---|---|---|
|Action |字串 |是 |`GetLiveStreamForbidStatusAPI` |API 操作。 |
|Version |字串 |是 |`2020-06-01` |此 API 操作的版本。當前版本：`2020-06-01`。 |


<span id="840d0fd2"></span>
### 主體


|名稱 |資料型別 |是否必填 |範例值 |說明 |
|---|---|---|---|---|
|ActivityId |整數 |是 |`17218312****` |直播間的活動 ID。可透過調用[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-TW)取得該 ID。 |
|LineId |整數陣列 |否 |`[356218,356219]` |直播來源的 ID。若省略此參數，API 將返回該直播間所有來源的串流狀態。<br><br>一個直播間可包含多個直播來源，每個來源有其專屬串流。可透過調用[GetStreamsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getstreamsapi-zh-TW)取得直播間的來源 ID。 |


<span id="52182519"></span>
## 回應參數


|名稱 |資料型別 |範例值 |說明 |
|---|---|---|---|
|StreamForbidStatus |陣列[ForbidStatus](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getlivestreamforbidstatusapi-zh-TW#ecdad8ed) |`-` |指定來源的串流狀態。 |


<span id="ecdad8ed"></span>
### ForbidStatus


|名稱 |資料型別 |範例值 |說明 |
|---|---|---|---|
|StreamStatus |整數 |`0` |串流的狀態。<br><br><br>* `0`：未禁播。<br><br>* `1`：已禁播。 |
|ForbidTime |字串 |`2024-07-13T02:59:50Z` |串流被禁播至的時間（UTC+0）。<br><br>值為`"0"`表示該串流未被禁播。 |
|LineId |整數 |`356218` |直播來源 ID。 |


<span id="d14b27e8"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```JSON
POST https://livesaas.byteplusapi.com/?Action=GetLiveStreamForbidStatusAPI&Version=2020-06-01
{
    "ActivityId": 17218312****,
    "LineId": [356218,356219]
}
```


<span id="Sample response"></span>
### 範例回應

```JSON
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "GetLiveStreamForbidStatusAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1718161649
    },
    "Result": {
        "StreamForbidStatus": [
            {
                "StreamStatus": 0,
                "ForbidTime": "0",
                "LineId": 356218
            },
            {
                "StreamStatus": 1,
                "ForbidTime": "2024-07-13T02:59:50Z",
                "LineId": 356219
            }
        ]
    }
}
```
