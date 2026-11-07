---
title: "PresenterChatAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-presenterchatapi-zh-TW"
---

調用此 API 以作為直播間的主播發送評論。

<span id="459d9053"></span>
## 需求

配額：每個帳戶每分鐘 120 次查詢

<span id="b2acb75e"></span>
## HTTP 請求


* URL：`https://livesaas.byteplusapi.com/?Action=PresenterChatAPI&Version=2020-06-01`

* 方法：POST


<span id="5ad3f4d9"></span>
## 請求參數

以下表格未包含所有共用請求參數。如需完整列表，請參見 [共用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/gong-yong-can-shu-zh-TW#f1706967)。

<span id="91ba5468"></span>
### 查詢


|名稱 |資料型別 |是否必填 |範例值 |描述 |
|---|---|---|---|---|
|Action |String |是 |`PresenterChatAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。當前版本：`2020-06-01`。 |


<span id="Body parameters"></span>
### 主體


|名稱 |資料型別 |是否必填 |範例值 |描述 |
|---|---|---|---|---|
|ActivityId |Long |是 |`17218346****` |直播間的活動 ID。可通過調用 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi) 獲取該 ID。 |
|Comment |String |是 |`Hello` |要發送的評論內容。 |


<span id="e21e2025"></span>
## 回應參數


|名稱 |資料型別 |範例值 |描述 |
|---|---|---|---|
|status |Boolean |`true` |表示評論是否發送成功。<br><br><br>* `true`：成功。<br><br>* `false`：失敗。 |


<span id="b574ac21"></span>
## 範例

<span id="3ca901e7"></span>
### 請求範例

```JSON
POST https://livesaas.byteplusapi.com/?Action=PresenterChatAPI&Version=2020-06-01
{
    "ActivityId": 17218346****,
    "Comment": "Hello" 
}
```


<span id="Sample response"></span>
### 回應範例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "PresenterChatAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1656067132
    },
    "Result":{
        "status": true
    }
}
```


<span id="6d8a9dad"></span>
## 錯誤碼

如需共用錯誤碼列表，請參見 [常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/chang-jian-cuo-wu-yu-zhuang-tai-ma-zh-TW)。
