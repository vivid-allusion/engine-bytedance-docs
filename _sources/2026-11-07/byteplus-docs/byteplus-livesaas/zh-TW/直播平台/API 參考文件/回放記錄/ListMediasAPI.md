---
title: "ListMediasAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-listmediasapi-zh-TW"
---

呼叫此 API 以取得特定直播活動播放列表中影片的資訊。此 API 支援分頁，並允許您取得如影片 ID、名稱、時長及線上狀態等詳細資訊。

<span id="Request"></span>
## 請求

<span id="Details"></span>
### 詳細資訊


* API 操作：`ListMediasAPI`

* 請求方法：GET

* 請求 URI：`http://livesaas.byteplusapi.com/?Action=ListMediasAPI&Version=2020-06-01`

* 配額：每個帳戶每分鐘 120 次查詢


<span id="Query string parameters"></span>
### 查詢字串參數

下表未包含所有共用請求參數。完整列表請參見[共用請求參數](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**參數名稱** |**必填** |**資料型態** |**說明** |
|---|---|---|---|
|Action |是 |字串 |API 操作。 |
|Version |是 |字串 |此 API 操作的版本。目前版本：`2020-06-01`。 |
|ActivityId |是 |整數 |直播活動的 ID。 |
|IsNeedTotalCount |否 |布林值 |是否回傳播放列表中影片的總數。 |
|PageNo |是 |整數 |要回傳結果的頁碼。當您指定此參數時，結果將以分頁方式呈現。 |
|PageItemCount |是 |整數 |每頁要回傳的結果數量。 |
|Name |否 |字串 |若您指定此欄位，BytePlus Live 會回傳所有名稱包含指定字串的影片。 |
|Vid |否 |字串 |若您指定此參數，BytePlus Live 會回傳具有指定 Vid 的影片。 |


<span id="Sample request"></span>
### 請求範例

```JSON
Get http://livesaas.byteplusapi.com/?Action=ListMediasAPI&Version=2020-06-01&ActivityId=1231231231&PageNo=1&PageItemCount=10
```


<span id="Response"></span>
## 回應

<span id="Response schema"></span>
### 回應結構


|**參數名稱** |**資料型態** |**說明** |
|---|---|---|
|PageNo |整數 |頁碼。 |
|PageItemCount |整數 |每頁的結果數量。 |
|TotalItemCount |整數 |播放列表中影片的總數。 |
|Medias |陣列 |影片資訊。 |


<span id="Media"></span>
#### 媒體


|**參數名稱** |**資料型態** |**說明** |
|---|---|---|
|MediaId |字串 |播放列表中影片的 ID。您可在呼叫 UpdateMediaOnlineStatusAPI 時使用此資訊。 |
|Name |字串 |影片名稱。 |
|Duration |整數 |影片時長（秒）。 |
|SourceType |整數 |影片來源：<br><br><br>* 1：上傳的影片檔案<br><br>* 2：錄製的回放 |
|OnlineStatus |整數 |影片狀態：<br><br><br>* 1：線上<br><br>* 2：離線 |
|Vid |字串 |媒體庫中影片的 ID。 |
|CreateTime |整數 |透過呼叫 `UpdateMediaOnlineStatusAPI` 發佈影片時的時間戳。 |
|CoverImage |字串 |播放的封面圖片。 |


<span id="Sample response"></span>
### 回應範例

```JSON
{
    "ResponseMetadata":{
        "RequestId":"202201201826170101501312091D1C09D2",
        "Action":"ListMediasAPI",
        "Version":"2020-06-01",
        "Service":"livesaas",
        "Region":"ap-singapore-1"
    },
    "Result":{
        "Medias":[
            {
                "MediaId":1,
                "Name":"example",
                "Duration":111,
                "SourceType":1,
                "OnlineStatus":0,
                "vid":"idexample",
                "CreateTime":1541154433671,
                "CoverImage": "//p-example.e.org/example.img"
            }
        ],
        "TotalItemCount":1,
        "PageNo":1,
        "PageItemCount":10           
    }
}
```
