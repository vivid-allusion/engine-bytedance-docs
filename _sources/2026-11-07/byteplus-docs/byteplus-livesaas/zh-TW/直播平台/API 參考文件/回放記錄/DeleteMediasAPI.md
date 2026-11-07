---
title: "DeleteMediasAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-deletemediasapi-zh-TW"
---

一次最多可從直播活動的播放列表中刪除 100 部影片。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">若某部影片存在於多個活動的播放列表中，刪除後將會從所有這些列表中移除。</div>


* <div data-tips="true" data-tips-type="tip">已刪除的影片會從 BytePlus Live 永久移除，且無法還原。</div>


* <div data-tips="true" data-tips-type="tip">若被刪除的影片為觀看頁面的當前播放內容，刪除後活動狀態將變為 <strong>Over</strong>。但若活動設定為直播結束後自動釋出播放，且該活動的播放列表中有多於一部影片，則刪除後將自動播放列表中的下一部影片。</div>



<span id="Request"></span>
## 請求

<span id="Details"></span>
### 詳細資訊


* API 操作：`DeleteMediasAPI`

* 請求方法：POST

* 請求 URI：`http://livesaas.byteplusapi.com/?Action=DeleteMediasAPI&Version=2019-10-10`

* 配額：每個帳戶每分鐘 120 次查詢


<span id="Query string parameters"></span>
### 查詢字串參數

下表未包含所有共用請求參數。如需完整清單，請參閱[共用請求參數](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**參數名稱** |**資料型別** |**是否必填** |**說明** |
|---|---|---|---|
|Action |String |是 |API 操作。 |
|Version |String |是 |此 API 操作的版本。目前版本：`2019-10-10`。 |


<span id="Body parameter"></span>
### Body 參數


|**參數名稱** |**資料型別** |**是否必填** |**說明** |
|---|---|---|---|
|Vids |Array of String |是 |要刪除的影片 ID。最多可指定 100 個 ID。 |


<span id="Sample request"></span>
### 請求範例

```JSON
POST http://livesaas.byteplusapi.com/?Action=DeleteMediasAPI&Version=2019-10-10
{
    "Vids": [
        "v0c251g7007abc1",
        "v0c251g7007abc2"
    ]
}
```


<span id="Response"></span>
## 回應

<span id="Response schema"></span>
### 回應結構


|**參數名稱** |**資料型別** |**說明** |
|---|---|---|
|Success |Boolean |表示刪除是否成功。<br><br><br>* `true`：所有影片均已刪除。<br><br>* `false`：有一部或多部影片刪除失敗。 |
|FailedList |Array of String |刪除失敗的影片 ID。當`Success`的值為`false`時，會回傳此參數。 |


<span id="Sample response"></span>
### **回應範例**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20221205033247010251197018041E783F",
        "Action": "DeleteMediasAPI",
        "Version":"2019-10-10",
        "Service":"livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1670211167
    },
    "Result": {
        "Success": false,
        "FailedList": ["v0c251g7007abc1"]
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

如需常見錯誤碼清單，請參閱[共用錯誤與狀態碼](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-error-and-status-codes)。
