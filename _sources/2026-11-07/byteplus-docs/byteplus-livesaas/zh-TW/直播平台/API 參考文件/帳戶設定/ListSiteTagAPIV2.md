---
title: "ListSiteTagAPIV2"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-listsitetagapiv2-zh-TW"
---

呼叫此 API 以取得在您的 BytePlus 帳戶中配置的直播間分類標籤及文字標籤的完整清單。

<span id="cfe8a431"></span>
## 請求

<span id="7160a064"></span>
### 詳細資訊


* API 操作：`ListSiteTagAPIV2`

* 請求方法：GET

* 請求 URI：`https://livesaas.byteplusapi.com/?Action=ListSiteTagAPIV2&Version=2020-06-01`

* 配額：每個帳戶每分鐘最多 120 次查詢


<span id="e3183224"></span>
### 查詢字串參數

下表並未包含所有共用請求參數。完整清單請參見[共用請求參數](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**參數名稱** |**資料型別** |**是否必填** |**說明** |
|---|---|---|---|
|Action |String |是 |API 操作。 |
|Version |String |是 |此 API 操作的版本。目前版本：`2020-06-01`。 |


<span id="db442151"></span>
### 請求範例

```JSON
Get https://livesaas.byteplusapi.com/?Action=ListSiteTagAPIV2&Version=2020-06-01
```


<span id="916b2c22"></span>
## 回應

<span id="426c0334"></span>
### 回應結構


|**參數名稱** |**資料型別** |**說明** |
|---|---|---|
|SiteTags |[Tag](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listsitetagapiv2#539ba0fe) 陣列 |分類標籤清單。 |
|TextSiteTags |[TextTag](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listsitetagapiv2#b066ce5e) 陣列 |文字標籤清單。 |


<span id="539ba0fe"></span>
#### Tag


|**參數名稱** |**資料型別** |**說明** |
|---|---|---|
|Name |String |分類標籤名稱。 |
|Value |String 陣列 |標籤值。 |
|Show |Integer |已淘汰。 |
|Index |Integer |分類標籤在[BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)上的顯示順序索引。 |


<span id="b066ce5e"></span>
#### TextTag


|**參數名稱** |**資料型別** |**說明** |
|---|---|---|
|Name |String |文字標籤名稱。 |
|Index |Integer |文字標籤在[BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)上的顯示順序索引。 |


<span id="d6c5e207"></span>
### 回應範例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "ListSiteTagAPIV2",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1656419846 
    },
    "Result": {
        "SiteTags": [
            {
                "Index": 0,
                "Name": "Label 1",
                "Value": [
                    "A"
                ],
                "Show": 0
            },
            {
                "Index": 1,
                "Name": "Label 2",
                "Value": [
                    "B",
                    "C",
                    "D",
                    "E"
                ],
                "Show": 0
            }
        ],
        "TextSiteTags": [
            {
                "Index": 0,
                "Name": "Label 3"
            },
            {
                "Index": 1,
                "Name": "Label 4"
            }
        ]
    }
}
```


<span id="f43dff76"></span>
## 錯誤碼

常見錯誤碼清單請參見[共用錯誤及狀態碼](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-error-and-status-codes)。
