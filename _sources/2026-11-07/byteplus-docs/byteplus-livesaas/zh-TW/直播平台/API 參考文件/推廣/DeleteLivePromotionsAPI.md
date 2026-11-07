---
title: "DeleteLivePromotionsAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-deletelivepromotionsapi-zh-TW"
---

此 API 用於刪除直播活動中的第三方直播推廣平台。

<span id="3bd1cae3"></span>
## 請求

<span id="b4b95ba8"></span>
### 詳細資訊


* API 操作：`DeleteLivePromotionsAPI`

* 請求方法：POST

* 請求 URI：`https://livesaas.byteplusapi.com/?Action=DeleteLivePromotionsAPI&Version=2020-06-01`

* 配額：每個帳戶每分鐘最多 120 次查詢


<span id="15273936"></span>
### 查詢字串參數

下表未包含所有共用請求參數。完整列表請參見[共用請求參數](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**參數名稱** |**資料型別** |**是否必填** |**說明** |
|---|---|---|---|
|Action |String |是 |API 操作。 |
|Version |String |是 |此 API 操作的版本。目前版本：`2020-06-01`。 |


<span id="da228a08"></span>
### Body 參數


|**參數名稱** |**資料型別** |**是否必填** |**說明** |
|---|---|---|---|
|ActivityId |Integer |是 |直播活動的 ID。可透過呼叫[ListActivityAPI](https://docs.byteplus.com/en/byteplus-livesaas/docs/listactivityapi)取得 ID。 |
|Id |Integer |是 |推廣平台的 ID。可透過呼叫[ListLivePromotionsAPI](https://docs.byteplus.com/byteplus-livesaas/docs/listlivepromotionsapi)取得 ID。 |


<span id="6cafa432"></span>
### 請求範例

```JSON
POST https://livesaas.byteplusapi.com/?Action=DeleteLivePromotionsAPI&Version=2020-06-01
{ 
    "ActivityId": 1231231231, 
    "Id": 123 
} 
```


<span id="e05f6486"></span>
## 回應

<span id="696aa8bd"></span>
### 回應結構


|**參數名稱** |**資料型別** |**說明** |
|---|---|---|
|ActivityId |Integer |直播活動的 ID。 |


<span id="fc31d626"></span>
### 回應範例

```JSON
{ 
    "ResponseMetadata": { 
        "RequestId": "202201201826170101501312091D1C09D2", 
        "Action": "DeleteLivePromotionsAPI", 
        "Version": "2020-06-01", 
        "Service": "livesaas", 
        "Region": "ap-singapore-1", 
        "SystemTime": 1656419846 
    }, 
    "Result": {
            "ActivityId": 1231231231 
      } 
} 
```


<span id="fd33babb"></span>
## 錯誤碼

常見錯誤碼列表請參見[共用錯誤與狀態碼](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-error-and-status-codes)。
