---
title: "UpdateLivePromotionsStatusAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-updatelivepromotionsstatusapi-zh-TW"
---

更新直播活動中第三方平台的分發狀態，以指定該平台是否啟用直播推廣功能。

<span id="e3f87cdb"></span>
## 請求

<span id="bfd37204"></span>
### 詳細資訊


* API 操作：`UpdateLivePromotionsStatusAPI`

* 請求方法：POST

* 請求 URI：`https://livesaas.byteplusapi.com/?Action=UpdateLivePromotionsStatusAPI&Version=2020-06-01`

* 配額：每個帳戶每分鐘最多 120 次查詢


<span id="4486e7e1"></span>
### 查詢字串參數

下表未包含所有共用請求參數。完整列表請參見[共用請求參數](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**參數名稱** |**資料型別** |**是否必填** |**說明** |
|---|---|---|---|
|Action |String |是 |API 操作。 |
|Version |String |是 |此 API 操作的版本。目前版本：`2020-06-01`。 |


<span id="5f330622"></span>
### 請求體參數


|**參數名稱** |**資料型別** |**是否必填** |**說明** |
|---|---|---|---|
|ActivityId |Integer |是 |直播活動的 ID。可透過呼叫[ListActivityAPI](https://docs.byteplus.com/en/byteplus-livesaas/docs/listactivityapi)取得 ID。 |
|Id |Integer |是 |平台 ID。可透過呼叫[ListLivePromotionsAPI](https://docs.byteplus.com/byteplus-livesaas/docs/listlivepromotionsapi)取得 ID。 |
|Status |Integer |是 |指定平台是否啟用直播推廣功能。<br><br>有效值：<br><br><br>* `1`：啟用。<br><br>* `2`：停用。 |


<span id="3c33a17e"></span>
### 請求範例

```JSON
POST https://livesaas.byteplusapi.com/?Action=UpdateLivePromotionsStatusAPI&Version=2020-06-01
{ 
    "ActivityId": 1231231231, 
    "Id": 12, 
    "Status": 1 
} 
```


<span id="4713a872"></span>
## 回應

<span id="1d1c8f48"></span>
### 回應結構


|**參數名稱** |**資料型別** |**說明** |
|---|---|---|
|ActivityId |Integer |直播活動的 ID。 |


<span id="104a3dd9"></span>
### 回應範例

```JSON
{ 
    "ResponseMetadata": { 
        "RequestId": "202201201826170101501312091D1C09D2", 
        "Action": "UpdateLivePromotionsStatusAPI", 
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


<span id="d3b604ed"></span>
## 錯誤碼

常見錯誤碼列表請參見[共用錯誤與狀態碼](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-error-and-status-codes)。
