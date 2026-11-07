---
title: "ListLivePromotionsAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-listlivepromotionsapi-zh-TW"
---

調用此 API 以獲取已新增至特定直播活動的第三方直播推廣平台列表。

<span id="ac70d9a3"></span>
## 請求

<span id="8f3ec89a"></span>
### 詳細資訊


* API 操作：`ListLivePromotionsAPI`

* 請求方法：GET

* 請求 URI：`https://livesaas.byteplusapi.com/?Action=ListLivePromotionsAPI&Version=2020-06-01`

* 配額：每個帳戶每分鐘 120 次查詢


<span id="2fdeadeb"></span>
### 查詢字串參數

下表未包含所有通用請求參數。完整列表請參見[通用請求參數](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**參數名稱** |**資料型別** |**是否必填** |**說明** |
|---|---|---|---|
|Action |String |是 |API 操作。 |
|Version |String |是 |此 API 操作的版本。當前版本：`2020-06-01`。 |
|ActivityId |Integer |是 |直播活動的 ID。可通過調用[ListActivityAPI](https://docs.byteplus.com/en/byteplus-livesaas/docs/listactivityapi)操作獲取該 ID。 |


<span id="63c837a9"></span>
### 請求範例

```JSON
Get https://livesaas.byteplusapi.com/?Action=ListLivePromotionsAPI&Version=2020-06-01&ActivityId=1231231231
```


<span id="33f74cf8"></span>
## 回應

<span id="55db58b6"></span>
### 回應結構


|**參數名稱** |**資料型別** |**說明** |
|---|---|---|
|LivePromotionsInfos |Array of[LivePromotionsInfos](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listlivepromotionsapi-zh-TW#LivePromotionsInfos) |直播推廣平台列表。 |


<span id="13a56d96"></span>
#### **LivePromotionsInfos**


|**參數名稱** |**資料型別** |**說明** |
|---|---|---|
|Id |Integer |平台 ID。 |
|Name |String |平台名稱。 |
|PushUrl |String |推流地址。 |
|Status |Integer |指定該平台是否啟用直播推廣功能。<br><br>有效值：<br><br><br>* `1`：啟用。<br><br>* `2`：停用。 |


<span id="b6394dd7"></span>
### 回應範例

```JSON
{ 
    "ResponseMetadata": { 
        "RequestId": "202201201826170101501312091D1C09D2", 
        "Action": "ListLivePromotionsAPI", 
        "Version": "2020-06-01", 
        "Service": "livesaas", 
        "Region": "ap-singapore-1", 
        "SystemTime": 1656419846 
    }, 
    "Result": {
            "LivePromotionsInfos":[ 
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


<span id="b117450f"></span>
## 錯誤碼

常見錯誤碼請參見[通用錯誤與狀態碼](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-error-and-status-codes)。
