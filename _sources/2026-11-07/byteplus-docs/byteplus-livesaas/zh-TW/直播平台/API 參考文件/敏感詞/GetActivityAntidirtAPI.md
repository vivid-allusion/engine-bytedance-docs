---
title: "GetActivityAntidirtAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getactivityantidirtapi-zh-TW"
---

為了管理你的直播間內容審核，你可以呼叫此 API 以獲取已設定的敏感詞列表。此 API 可讓你取得所有敏感詞，或僅取得包含特定關鍵字的敏感詞。

<span id="6012f85b"></span>
## 需求

配額：每個帳戶每分鐘最多 120 次查詢

<span id="9ee8c1eb"></span>
## HTTP 請求


* URL：`https://livesaas.byteplusapi.com/?Action=GetActivityAntidirtAPI&Version=2020-06-01`

* 方法：GET


<span id="7ad60001"></span>
## 請求參數

下表並未包含所有共用請求參數。完整列表請參見 [共用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/gong-yong-can-shu-zh-TW#f1706967)。

<span id="7ccae2e4"></span>
### 查詢


|名稱 |資料型別 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Action |String |是 |`GetActivityAntidirtAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。目前版本：`2020-06-01`。 |
|ActivityId |Long |是 |`178398113630****` |直播間的活動 ID。你可以透過呼叫 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi) 取得此 ID。 |
|PageNo |Integer |是 |`1` |要返回的頁碼。 |
|PageItemCount |Integer |是 |`10` |每頁返回的結果數量。 |
|Content |String |否 |`a` |關鍵字。API 僅返回包含此關鍵字的敏感詞。 |


<span id="c45a43ea"></span>
## 回應參數


|名稱 |資料型別 |範例值 |說明 |
|---|---|---|---|
|EnablePhoneNumberFilter |Integer |`1` |指定是否封鎖包含電話號碼的評論與暱稱。<br><br><br>* `1`：啟用。包含電話號碼的評論僅對發送者可見。<br><br>* 其他值：停用。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">目前此功能支援新加坡、日本、韓國、印尼、泰國及中國大陸的電話號碼。</div><br> |
|EnableSensitiveForLetter |Integer |`1` |表示是否啟用大小寫敏感。<br><br><br>* `1`：啟用。<br><br>* 其他值：停用。 |
|TotalItemCount |Integer |`2` |返回的敏感詞總數。 |
|WordList |String 陣列 |`["a","ab"]` |返回的敏感詞列表。 |


<span id="cd1e512b"></span>
## 範例

<span id="af8ea841"></span>
### 範例請求

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetActivityAntidirtAPI&Version=2020-06-01&ActivityId=178398113630****&PageNo=1&PageItemCount=10&Content=a
```


<span id="2ea02c1c"></span>
### 範例回應

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "GetActivityAntidirtAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1656419846
    },
    "Result": {
        "WordList": ["a","ab"],
        "TotalItemCount": 2,
        "EnablePhoneNumberFilter": 1,
        "EnableSensitiveForLetter": 1
    }
}
```


<span id="21a1266f"></span>
## 錯誤碼

共用錯誤碼列表請參見 [常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/chang-jian-cuo-wu-yu-zhuang-tai-ma-zh-TW)。
