---
title: "AddActivityAntidirtAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-addactivityantidirtapi-zh-TW"
---

呼叫此 API 以將敏感詞列表新增至指定的直播間。這有助於管理聊天內容，維護安全的互動環境。

<span id="6ca3ae9b"></span>
## 需求

配額：每個帳戶每分鐘最多 120 次查詢

<span id="3e5e18b2"></span>
## HTTP 請求


* URL：`https://livesaas.byteplusapi.com/?Action=AddActivityAntidirtAPI&Version=2020-06-01`

* 方法：POST


<span id="a7e0438d"></span>
## 請求參數

下表未包含所有共用請求參數。完整列表請參見 [共用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/gong-yong-can-shu-zh-TW#f1706967)。

<span id="dc691b28"></span>
### 查詢


|名稱 |資料型別 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Action |String |是 |`AddActivityAntidirtAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。目前版本：`2020-06-01`。 |


<span id="e9034e45"></span>
### 主體


|名稱 |資料型別 |必填 |範例值 |說明 |
|---|---|---|---|---|
|ActivityId |Long |是 |`178398113630****` |直播間的活動 ID。可透過呼叫 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi) 取得 ID。 |
|WordList |字串陣列 |是 |`["a","b"]` |要新增的敏感詞陣列。可新增的詞數量無限制。<br><br>注意：詞語不可包含逗號（,），因為逗號用作分隔符。 |


<span id="eceb3e71"></span>
## 回應參數


|名稱 |資料型別 |範例值 |說明 |
|---|---|---|---|
|Status |布林值 |`true` |表示敏感詞是否成功新增。<br><br><br>* `true`：成功。<br><br>* `false`：失敗。 |


<span id="4cf59303"></span>
## 範例

<span id="45d8e74f"></span>
### 範例請求

```JSON
POST https://livesaas.byteplusapi.com/?Action=AddActivityAntidirtAPI&Version=2020-06-01
{
    "ActivityId": 178398113630****,
    "WordList": ["a","b"]
}
```


<span id="8e3de267"></span>
### 範例回應

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "AddActivityAntidirtAPI",
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


<span id="2c603933"></span>
## 錯誤碼

共用錯誤碼列表請參見 [常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/chang-jian-cuo-wu-yu-zhuang-tai-ma-zh-TW)。
