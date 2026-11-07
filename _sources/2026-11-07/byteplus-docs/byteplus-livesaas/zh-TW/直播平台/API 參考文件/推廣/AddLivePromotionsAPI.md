---
title: "AddLivePromotionsAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-addlivepromotionsapi-zh-TW"
---

調用此 API 可將多個第三方平台新增至直播活動，以進行同步直播。平台新增後，當活動串流開始時，BytePlus Live 會自動將串流推送至該平台，協助你擴大觀眾覆蓋範圍。

<span id="f6dba5d6"></span>
## 請求

<span id="46fe124d"></span>
### 詳細資訊


* API 操作：`AddLivePromotionsAPI`

* 請求方法：POST

* 請求 URI：`https://livesaas.byteplusapi.com/?Action=AddLivePromotionsAPI&Version=2020-06-01`

* 配額：每個帳戶每分鐘 120 次查詢


<span id="4136eabc"></span>
### 查詢字串參數

下表未包含所有共用請求參數。完整列表請參見[共用請求參數](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**參數名稱** |**資料型別** |**是否必填** |**說明** |
|---|---|---|---|
|Action |String |是 |API 操作。 |
|Version |String |是 |此 API 操作的版本。目前版本：`2020-06-01`。 |


<span id="d4b8acb3"></span>
### Body 參數


|**參數名稱** |**資料型別** |**是否必填** |**說明** |
|---|---|---|---|
|ActivityId |Integer |是 |直播活動的 ID。你可以透過調用[ListActivityAPI](https://docs.byteplus.com/en/byteplus-livesaas/docs/listactivityapi)取得 ID。 |
|AddLivePromotionsInfos |Array of[AddLivePromotionsInfos](https://docs.byteplus.com/docs/byteplus-livesaas/docs-addlivepromotionsapi-zh-TW#AddLivePromotionsInfos) |是 |要新增用於直播推廣的第三方平台清單。 |


<span id="0b56e510"></span>
#### **AddLivePromotionsInfos**


|**參數名稱** |**資料型別** |**是否必填** |**說明** |
|---|---|---|---|
|Name |String |是 |平台名稱。最大長度為 100 個字元。 |
|PushUrl |String |是 |推流地址。 |


<span id="19bbf454"></span>
### 請求範例

```JSON
POST https://livesaas.byteplusapi.com/?Action=AddLivePromotionsAPI&Version=2020-06-01
{ 
    "ActivityId": 1231231231, 
    "AddLivePromotionsInfos":[ 
        { 
             "Name": "Platform A", 
             "PushUrl": "rtmp://example" 
        } 
    ] 
} 
```


<span id="19cab44c"></span>
## 回應

<span id="d13b0166"></span>
### 回應結構


|**參數名稱** |**資料型別** |**說明** |
|---|---|---|
|LivePromotionsInfos |Array of[LivePromotionsInfos](https://docs.byteplus.com/docs/byteplus-livesaas/docs-addlivepromotionsapi-zh-TW#LivePromotionsInfos) |已新增平台的詳細資訊。 |


<span id="46024ed2"></span>
#### **LivePromotionsInfos**


|**參數名稱** |**資料型別** |**說明** |
|---|---|---|
|Id |Integer |平台 ID。 |
|Name |String |平台名稱。 |
|PushUrl |String |推流地址。 |
|Status |Integer |表示該平台是否啟用直播推廣。<br><br>有效值：<br><br><br>* `1`：已啟用。<br><br>* `2`：已停用。 |


<span id="96d00acd"></span>
### 回應範例

```JSON
{ 
    "ResponseMetadata": { 
        "RequestId": "202201201826170101501312091D1C09D2", 
        "Action": "AddLivePromotionsAPI", 
        "Version": "2020-06-01", 
        "Service": "livesaas", 
        "Region": "ap-singapore-1", 
        "SystemTime": 1656419846 
    }, 
    "Result": {
        "LivePromotionsInfos": [ 
              { 
                 "Id": 123, 
                 "Name": "Platform A", 
                 "PushUrl": "rtmp://example", 
                 "Status": 1 
              } 
          ] 
      } 
} 
```


<span id="a499fffb"></span>
## 錯誤碼

常見錯誤碼請參見[共用錯誤與狀態碼](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-error-and-status-codes)。
