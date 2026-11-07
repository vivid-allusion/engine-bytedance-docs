---
title: "GetSilenceUserListAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getsilenceuserlistapi-zh-TW"
---

調用此 API 以獲取在特定直播活動中被禁止發送聊天訊息的用戶清單。

<span id="Request"></span>
## 請求

<span id="Details"></span>
### 詳細資訊


* API 操作：`GetSilenceUserListAPI`

* 請求方法：GET

* 請求 URI：`http://livesaas.byteplusapi.com/?Action=GetSilenceUserListAPI&Version=2020-06-01`

* 配額：每個帳戶每分鐘 120 次查詢


<span id="Query string parameters"></span>
### 查詢字串參數

下表未包含所有共用請求參數。完整清單請參見[共用請求參數](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**參數名稱** |**是否必填** |**資料型別** |**說明** |
|---|---|---|---|
|Action |是 |字串 |API 操作。 |
|Version |是 |字串 |此 API 操作的版本。目前版本：`2020-06-01`。 |
|ActivityId |是 |整數 |直播活動的 ID。 |


<span id="Sample request"></span>
### 請求範例

```JSON
Get http://livesaas.byteplusapi.com/?Action=GetSilenceUserListAPI&Version=2020-06-01&ActivityId=1231231231
```


<span id="Response"></span>
## 回應

<span id="Response schema"></span>
### 回應結構


|**參數名稱** |**資料型別** |**說明** |
|---|---|---|
|UserList |陣列 |被禁言用戶的清單。 |


<span id="UserInfo"></span>
#### UserInfo


|**參數名稱** |**資料型別** |**說明** |
|---|---|---|
|UserId |整數 |用戶 ID。 |
|Nickname |字串 |用戶暱稱。 |


<span id="Sample response"></span>
### 回應範例

以下為成功請求的回應範例：

```JSON
{
    "ResponseMetadata":{
        "RequestId":"202201201826170101501312091D1C09D2",
        "Action":"GetSilenceUserListAPI",
        "Version":"2020-06-01",
        "Service":"livesaas",
        "Region":"ap-singapore-1"
    },
    "Result":{
         "UserList": [
             {
                 "Nickname": "user1",
                 "UserId": 1670265947464959
             }
         ]
     }
}
```
