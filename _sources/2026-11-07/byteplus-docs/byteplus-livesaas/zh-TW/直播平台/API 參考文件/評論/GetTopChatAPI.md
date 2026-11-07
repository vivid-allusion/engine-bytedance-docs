---
title: "GetTopChatAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-gettopchatapi-zh-TW"
---

呼叫此 API 以取得特定直播活動中目前置頂的聊天訊息列表。

<span id="Request"></span>
## 請求

<span id="Details"></span>
### 詳細資訊


* API 操作：`GetTopChatAPI`

* 請求方法：GET

* 請求 URI：`http://livesaas.byteplusapi.com/?Action=GetTopChatAPI&Version=2020-06-01`

* 配額：每個帳戶每分鐘最多 120 次查詢


<span id="Query string parameters"></span>
### 查詢字串參數

下表未包含所有共用請求參數。完整列表請參見[共用請求參數](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**參數名稱** |**是否必填** |**資料型態** |**說明** |
|---|---|---|---|
|Action |是 |字串 |API 操作。 |
|Version |是 |字串 |此 API 操作的版本。目前版本：`2020-06-01`。 |
|ActivityId |是 |整數 |直播活動的 ID。 |


<span id="Sample request"></span>
### 請求範例

```JSON
Get http://livesaas.byteplusapi.com/?Action=GetTopChatAPI&Version=2020-06-01&ActivityId=1231231231
```


<span id="Response"></span>
## 回應

<span id="Response schema"></span>
### 回應結構


|**參數名稱** |**資料型態** |**說明** |
|---|---|---|
|ActivityId |整數 |直播活動的 ID。 |
|Data |陣列 |聊天訊息物件的陣列。 |


<span id="Chat"></span>
#### Chat


|**參數名稱** |**資料型態** |**說明** |
|---|---|---|
|ChatId |整數 |聊天訊息的 ID。 |
|CreateTime |整數 |訊息發送的時間戳。 |
|TextContent |字串 |聊天訊息內容。 |
|User |UserInfo |發送者資訊。 |
|IsDelete |布林值 |聊天訊息是否已被刪除：<br><br><br>* true：已刪除<br><br>* false：未刪除 |
|LikeCount |整數 |訊息的總按讚數。 |
|IsPresenter |布林值 |訊息是否由主持人發送：<br><br><br>* true：由主持人發送<br><br>* false：由觀眾發送 |
|reviewStatus |整數 |聊天訊息的審核狀態：<br><br><br>* 0：無需審核<br><br>* 1：待審核<br><br>* 2：已通過 |


<span id="UserInfo"></span>
#### UserInfo


|**參數名稱** |**資料型態** |**說明** |
|---|---|---|
|UserId |整數 |發送者的 ID。 |
|Nickname |字串 |發送者暱稱。 |


<span id="Sample response"></span>
### 回應範例

以下為成功請求的回應範例：

```JSON
{
     "ResponseMetadata" :{
         "RequestId" : "202201201826170101501312091D1C09D2" ,
         "Action" : "GetTopChatAPI" ,
         "Version" : "2020-06-01" ,
         "Service" : "livesaas" ,
         "Region" : "ap-singapore-1" 
    },
     "Result" :{
         "Data" :[
            {
                 "ChatId" :31823336, 
                 "CreateTime" :1591860377, 
                 "TextContent" : "Hello!" , 
                 "User" :{
                     "Nickname" : "111" ,             
                     "UserId" :1669024344048647 
                },
                 "IsDelete" :true, 
                 "LikeCount" :3, 
                 "IsPresenter" :false, 
                 "reviewStatus" :0 
            }
        ]
    }
}
```
