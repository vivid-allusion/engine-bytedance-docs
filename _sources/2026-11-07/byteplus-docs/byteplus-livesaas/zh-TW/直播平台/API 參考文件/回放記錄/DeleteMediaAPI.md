---
title: "DeleteMediaAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-deletemediaapi-zh-TW"
---

從直播活動的回放列表中刪除一個影片。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">若影片被包含於多個活動的回放列表中，刪除時會從所有這些列表中移除。</div>


* <div data-tips="true" data-tips-type="tip">被刪除的影片將永久從 BytePlus Live 移除，無法復原。</div>


* <div data-tips="true" data-tips-type="tip">若刪除的影片正在作為回放播放，活動狀態將變更為<strong>Over</strong>。但若活動設定為自動播放下一部影片，且回放列表中有其他影片，則會播放下一部影片。</div>



<span id="Request"></span>
## 請求

<span id="Details"></span>
### 詳細資訊


* API 操作：`DeleteMediaAPI`

* 請求方法：POST

* 請求 URI：`http://livesaas.byteplusapi.com/?Action=DeleteMediaAPI&Version=2019-10-10`

* 配額：每個帳戶每分鐘 120 次查詢


<span id="Query string parameters"></span>
### 查詢字串參數

下表並未包含所有共用請求參數。完整列表請參見[共用請求參數](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**參數名稱** |**資料型別** |**必填** |**說明** |
|---|---|---|---|
|Action |String |是 |API 操作。 |
|Version |String |是 |此 API 操作的版本。目前版本：`2019-10-10`。 |


<span id="Body parameter"></span>
### Body 參數


|**參數名稱** |**資料型別** |**必填** |**說明** |
|---|---|---|---|
|Vid |String |是 |要刪除的影片 ID。 |


<span id="Sample request"></span>
### 請求範例

```JSON
POST http://livesaas.byteplusapi.com/?Action=DeleteMediaAPI&Version=2019-10-10
{
    "Vid": "v0c251g7007abc1"
}
```


<span id="Response"></span>
## 回應

<span id="Response schema"></span>
### 回應結構


|**參數名稱** |**資料型別** |**說明** |
|---|---|---|
|Success |Boolean |表示刪除是否成功。<br><br><br>* `true`：影片已刪除。<br><br>* `false`：刪除失敗。 |


<span id="Sample response"></span>
### **回應範例**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20221205033247010251197018041E783F",
        "Action": "DeleteMediaAPI",
        "Version":"2019-10-10",
        "Service":"livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1670211167
    },
    "Result": {
        "Success": true
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

常見錯誤碼列表請參見[共用錯誤與狀態碼](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-error-and-status-codes)。
