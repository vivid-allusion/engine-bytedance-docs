---
title: "UpdateActivityMenuAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-updateactivitymenuapi-zh-TW"
---

呼叫此 API 以更新直播活動的選單。

<span id="Request"></span>
## 請求

<span id="Details"></span>
### 詳細資訊


* API 操作：`UpdateActivityMenuAPI`

* 請求方法：POST

* 請求 URI：`https://livesaas.byteplusapi.com/?Action=UpdateActivityMenuAPI&Version=2020-06-01`

* 配額：每個帳戶每分鐘 120 次查詢


<span id="Query string parameters"></span>
### 查詢字串參數

下表並未包含所有共用請求參數。完整列表請參見[共用請求參數](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**參數名稱** |**必填** |**資料型別** |**說明** |
|---|---|---|---|
|Action |是 |字串 |API 操作。 |
|Version |是 |字串 |此 API 操作的版本。目前版本：`2020-06-01`。 |


<span id="Body parameters"></span>
### Body 參數


|**參數名稱** |**必填** |**資料型別** |**說明** |
|---|---|---|---|
|ActivityId |是 |整數 |直播活動的 ID。 |
|Menus |是 |陣列 |選單的配置。 |


<span id="Menu"></span>
#### 選單


|**參數名稱** |**必填** |**資料型別** |**說明** |
|---|---|---|---|
|Name |是 |字串 |分頁標籤的名稱。 |
|Type |是 |整數 |分頁標籤類型：<br><br><br>* 1：圖文<br><br>* 2：卡片<br><br>* 3：聊天互動<br><br>* 4：直播內容<br><br>* 5：聚合直播<br><br>* 6：互動問答 |
|Location |是 |整數 |分頁標籤的顯示順序，從左側開始。 |


<span id="Sample request"></span>
### 請求範例

```JSON
POST https://livesaas.byteplusapi.com/?Action=UpdateActivityMenuAPI&Version=2020-06-01
{
     "ActivityId" :732412312,
     "Menus" : [
        {
             "Name" : "Menu name 1" ,
             "Type" : 2,
             "Location" : 1
        },
        {
             "Name" : "Menu name 2" ,
             "Type" : 2,
             "Location" : 2
        }
    ]
}
```


<span id="Response"></span>
## 回應

<span id="Response schema"></span>
### 回應結構


|**參數名稱** |**資料型別** |**說明** |
|---|---|---|
|Status |布林值 |操作結果：<br><br><br>* true：成功<br><br>* false：失敗 |


<span id="Sample response"></span>
### 回應範例

以下為請求成功處理時的回應範例：

```JSON
{
   "ResponseMetadata" :{
     "RequestId" : "201806041104200100100232280022D30" ,
     "Action" : "UpdateActivityMenuAPI" ,
     "Version" : "2020-06-01" ,
     "Service" : "livesaas" ,
     "Region" : "ap-singapore-1" 
  },
   "Result" : {
       "Status" : true
  }
}
```
