---
title: "DelActivityAntidirtAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-delactivityantidirtapi-zh-TW"
---

此 API 用於從指定的直播間刪除敏感詞。

<span id="9a06e2dd"></span>
## 需求

配額：每個帳戶每分鐘最多 120 次查詢

<span id="3dda4933"></span>
## HTTP 請求


* URL：`https://livesaas.byteplusapi.com/?Action=DelActivityAntidirtAPI&Version=2020-06-01`

* 方法：POST


<span id="44d1b454"></span>
## 請求參數

以下表格未包含所有共用的請求參數。完整列表請參見 [共用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/gong-yong-can-shu-zh-TW#f1706967)。

<span id="19f7773f"></span>
### 查詢


|名稱 |資料型別 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Action |String |是 |`DelActivityAntidirtAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。目前版本：`2020-06-01`。 |


<span id="e8b5e6dd"></span>
### Body


|名稱 |資料型別 |必填 |範例值 |說明 |
|---|---|---|---|---|
|ActivityId |Long |是 |`178398113630****` |直播間的活動 ID。可透過呼叫 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi) 取得 ID。 |
|WordList |Array of String |是 |`["a","b"]` |要刪除的敏感詞。<br><br>敏感詞不可包含逗號（,），因為逗號用於在列表中分隔詞語。 |
|DeleteAll |Boolean |否 |`true` |指定是否要刪除直播間中的所有敏感詞。<br><br>預設值：`false`。<br><br>有效值：<br><br><br>* `true`：刪除所有敏感詞。<br><br>* `false`：不刪除所有敏感詞。 |


<span id="c86c0d63"></span>
## 回應參數


|名稱 |資料型別 |範例值 |說明 |
|---|---|---|---|
|Status |Boolean |`true` |表示操作是否成功。<br><br><br>* `true`：成功。<br><br>* `false`：失敗。 |


<span id="cae97f6d"></span>
## 範例

<span id="691dfa76"></span>
### 範例請求

```JSON
POST https://livesaas.byteplusapi.com/?Action=DelActivityAntidirtAPI&Version=2020-06-01
{
    "ActivityId": 178398113630****,
    "WordList": ["a","b"]
}
```


<span id="31e7c378"></span>
### 範例回應

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "DelActivityAntidirtAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1681971407
    },
    "Result": {
        "Status": true
    }
}
```


<span id="bd73d2c5"></span>
## 錯誤碼

共用錯誤碼列表請參見 [常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/chang-jian-cuo-wu-yu-zhuang-tai-ma-zh-TW)。
