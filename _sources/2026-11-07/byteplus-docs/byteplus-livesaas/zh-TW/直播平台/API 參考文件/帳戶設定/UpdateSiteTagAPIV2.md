---
title: "UpdateSiteTagAPIV2"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-updatesitetagapiv2-zh-TW"
---

呼叫此 API 以更新您的 BytePlus 帳戶下直播活動標籤的資訊。

<span id="8baab3a6"></span>
## 請求

<span id="dc5f59cd"></span>
### 詳細資訊


* API 操作：`UpdateSiteTagAPIV2`

* 請求方法：POST

* 請求 URI：`https://livesaas.byteplusapi.com/?Action=UpdateSiteTagAPIV2&Version=2020-06-01`

* 配額：每個帳戶每分鐘 120 次查詢


<span id="6e979a4a"></span>
### 查詢字串參數

下表未包含所有共用請求參數。完整列表請參見[共用請求參數](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**參數名稱** |**資料型態** |**是否必填** |**描述** |
|---|---|---|---|
|Action |String |是 |API 操作。 |
|Version |String |是 |此 API 操作的版本。目前版本：`2020-06-01`。 |


<span id="b23059ea"></span>
### Body 參數


|**參數名稱** |**資料型態** |**是否必填** |**描述** |
|---|---|---|---|
|SiteTags |Array of[Tag](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updatesitetagapiv2-zh-TW#Tag) |是 |所有分類標籤的列表。<br><br>若要更新標籤，請先呼叫[ListSiteTagAPIV2](https://docs.byteplus.com/byteplus-livesaas/docs/listsitetagapiv2)取得目前列表，根據需求修改值，然後在您的請求中包含完整且已更新的列表。 |
|TextSiteTags |Array of[TextTag](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updatesitetagapiv2-zh-TW#TextTag) |是 |所有文字標籤的列表。<br><br>若要更新標籤，請先呼叫[ListSiteTagAPIV2](https://docs.byteplus.com/byteplus-livesaas/docs/listsitetagapiv2)取得目前列表，根據需求修改值，然後在您的請求中包含完整且已更新的列表。 |


<span id="7c2f115d"></span>
#### **Tag**


|**參數名稱** |**資料型態** |**是否必填** |**描述** |
|---|---|---|---|
|Name |String |是 |分類標籤的名稱。名稱不得超過 50 個字元，且不得與其他分類標籤名稱重複。 |
|Value |Array of String |是 |標籤的值陣列。每個標籤值不得超過 50 個字元，且在同一分類標籤下必須唯一。 |
|Show |Integer |是 |已棄用。 |
|Index |Integer |是 |分類標籤的索引，決定在 BytePlus Live 控制台上的顯示順序。<br><br>值範圍：[0,19]。 |


<span id="b07ec8d0"></span>
#### **TextTag**


|**參數名稱** |**資料型態** |**是否必填** |**描述** |
|---|---|---|---|
|Name |String |是 |文字標籤的名稱。名稱不得超過 50 個字元，且不得與其他文字標籤名稱重複。 |
|Index |Integer |是 |文字標籤的索引，用於識別在[BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)上的顯示順序。<br><br>值範圍：[0,4]。 |


<span id="b52be3c9"></span>
### 範例請求

```JSON
Post https://livesaas.byteplusapi.com/?Action=UpdateSiteTagAPIV2&Version=2020-06-01
{ 
      "SiteTags":   [ 
            { 
                  "Name": "Label 1", 
                  "Value": [ 
                        "A", 
                        "B" 
                  ], 
                  "Show": 0, 
                  "Index": 0 
            }, 
           { 
                  "Name": "Label 2", 
                  "Value": [ 
                        "C", 
                        "D" 
                  ], 
                  "Show": 0, 
                  "Index": 1 
            } 
      ], 
      "TextSiteTags":   [ 
            { 
                  "Name": "Label 3", 
                  "Index": 0 
            }, 
            { 
                  "Name": "Label 4", 
                  "Index": 1 
            } 
      ] 
} 
```


<span id="be0e1229"></span>
## 回應

<span id="3e7e53c1"></span>
### 回應結構


|**參數名稱** |**資料型態** |**描述** |
|---|---|---|
|Status |Boolean |表示更新是否成功。<br><br><br>* `true`：成功。<br><br>* `false`：失敗。 |


<span id="7f2c5f49"></span>
### 範例回應

```JSON
{ 
    "ResponseMetadata": { 
        "RequestId": "202201201826170101501312091D1C09D2", 
        "Action": "UpdateSiteTagAPIV2", 
        "Version": "2020-06-01", 
        "Service": "livesaas", 
        "Region": "ap-singapore-1", 
        "SystemTime": 1656419846 
    }, 
    "Result": { 
        "Status": true 
    } 
} 
```


<span id="22d08a72"></span>
## 錯誤碼

常見錯誤碼列表請參見[共用錯誤與狀態碼](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-error-and-status-codes)。
