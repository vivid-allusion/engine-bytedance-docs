---
title: "DeleteActivityProductLibrary"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/DeleteActivityProductLibrary-zh-TW2"
---

刪除特定直播間中的一個或多個商品庫。

<span id="Requirements"></span>
## 需求

配額：每個帳戶每分鐘最多 120 次查詢

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://livesaas.byteplusapi.com/?Action=DeleteActivityProductLibrary&Version=2024\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

下表未包含所有通用請求參數。完整列表請參見[通用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`DeleteActivityProductLibrary` |API 操作。 |
|Version |String |是 |`2024-01-01` |此 API 操作的版本。目前版本：`2024-01-01`。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|ActivityId |Long |是 |`1783981136301234` |直播間的活動 ID。可透過呼叫[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi)取得 ID。 |
|ProductLibraryIds |Long 陣列 |是 |`[789, 790]` |要刪除的商品庫 ID。可透過呼叫[GetActivityProductCommonConfig](https://docs.byteplus.com/en/docs/byteplus-livesaas/getactivityproductcommonconfig)取得 ID。 |


<span id="Response parameters"></span>
## 回應參數


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Status |Boolean |`true` |表示是否已刪除所有指定的商品庫。若已刪除，則回傳`true`。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://livesaas.byteplusapi.com/?Action=DeleteActivityProductLibrary&Version=2024-01-01
{
    "ActivityId": 1783981136301234,
    "ProductLibraryIds": [
        789,
        790
    ]
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DeleteActivityProductLibrary",
        "Version": "2024-01-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1656067132
    },
    "Result": {
        "Status": true
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

下表列出此 API 操作專屬的錯誤碼。通用錯誤碼請參見[通用錯誤與狀態碼](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|400 |InvalidParameter.ProductLibraryIdNotFound |ProductLibraryId 參數的值不存在。 |請確認該 ID 屬於直播間中現有的商品庫。 |
