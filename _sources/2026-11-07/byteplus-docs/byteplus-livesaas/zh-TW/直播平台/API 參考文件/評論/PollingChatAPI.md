---
title: "PollingChatAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-pollingchatapi-zh-TW"
---

呼叫此 API 以獲取直播間的評論。透過指定評論 ID 及輪詢方向，您可以定期獲取新評論或載入歷史聊天訊息。

<span id="bae63780"></span>
## 需求

配額：每個帳戶每分鐘 120 次查詢

<span id="35ca73aa"></span>
## HTTP 請求


* URL：`https://livesaas.byteplusapi.com/?Action=PollingChatAPI&Version=2020-06-01`

* 方法：GET


<span id="f3f5b32b"></span>
## 請求參數

下表並未包含所有共用請求參數。完整列表請參見 [共用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/gong-yong-can-shu-zh-TW#f1706967)。

<span id="ca18801e"></span>
### 查詢


|名稱 |資料型別 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Action |String |是 |`PollingChatAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。目前版本：`2020-06-01`。 |
|ActivityId |Long |是 |`17218346****` |直播間的活動 ID。您可以透過呼叫 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi) 取得此 ID。 |
|ChatId |Long |是 |`0` |評論的 ID，作為分頁游標。API 會回傳在此 ID 之前或之後發送的評論，但不包含此 ID 的評論。<br><br><br>* 若值為 `0`，API 會回傳請求時間之前發送的評論。<br><br>* 若您將此參數設為先前回應中的 `ChatId` 值，API 會根據 `PollingType` 的值，取得該評論之前或之後發送的評論。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">您也可以將此參數設為 <code>1</code>，並將 <code>PollingType</code> 設為 <code>0</code>，以取得目前直播間最早發送的評論。</div><br> |
|Count |Integer |否 |`0` |要回傳的評論最大數量。<br><br>預設值：`0`。<br><br>若值為 `0`，API 會根據 `ChatId` 和 `PollingType` 的條件回傳所有符合條件的評論。 |
|PollingType |Integer |否 |`0` |指定是否回傳在 `ChatId` 所指定評論之前或之後發送的評論。<br><br>預設值：`0`。<br><br>有效值：<br><br><br>* `0`：回傳在指定 `ChatId` 之後發送的評論。<br><br>* `1`：回傳在指定 `ChatId` 之前發送的評論。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若 <code>ChatId</code> 為 <code>0</code>，此參數將被忽略，API 會回傳請求時間之前發送的評論。</div><br> |


<span id="34e67e49"></span>
## 回應參數


|名稱 |資料型別 |範例值 |說明 |
|---|---|---|---|
|Data |Array of[聊天](https://docs.byteplus.com/docs/byteplus-livesaas/docs-pollingchatapi-zh-TW#d762709f) |`-` |評論列表。 |


<span id="d762709f"></span>
### 聊天


|名稱 |資料型別 |範例值 |說明 |
|---|---|---|---|
|ChatId |Integer |`1672920235409489` |評論 ID。 |
|CreateTime |Long |`1714658888` |評論發送時間，Unix 時間戳格式。單位：秒。 |
|TextContent |String |`Hello` |評論內容。 |
|User |Array of[用戶](https://docs.byteplus.com/docs/byteplus-livesaas/docs-pollingchatapi-zh-TW#60fb2ff7) |`-` |發送評論用戶的資訊。 |
|IsDelete |Boolean |`false` |表示評論是否已被刪除。<br><br><br>* `true`：已刪除。<br><br>* `false`：未刪除。 |
|LikeCount |Integer |`10` |評論的按讚數。 |
|IsPresenter |Boolean |`true` |表示評論是否由主持人發送。<br><br><br>* `true`：由主持人發送。<br><br>* `false`：由其他人發送。 |
|reviewStatus |Integer |`0` |評論的審核狀態。<br><br><br>* `0`：無需審核。<br><br>* `1`：審核中。<br><br>* `2`：已通過。<br><br>* `3`：已拒絕。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">如果 <code>IsPresenter</code> 的值為 <code>true</code>，則參數值始終為 <code>2</code>。</div><br> |
|IsTipOff |Integer |`0` |表示評論是否被檢舉。<br><br><br>* `0`：未檢舉。<br><br>* `1`：已檢舉。 |


<span id="60fb2ff7"></span>
#### 用戶


|名稱 |資料型別 |範例值 |說明 |
|---|---|---|---|
|UserId |Long |`17975829****` |用戶的 ID。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">主機的 ID 始終為 <code>0</code>。</div><br> |
|Nickname |String |`Viewer A` |用戶暱稱。 |


<span id="90d4a741"></span>
## 範例

<span id="c9d65ee4"></span>
### 範例請求

```JSON
GET https://livesaas.byteplusapi.com/?Action=PollingChatAPI&Version=2020-06-01&ActivityId=17218346****&ChatId=0&Count=0&PollingType=0
```


<span id="Response"></span>
### 範例回應

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "PollingChatAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1714662740
    },
    "Result": {
        "Data": [
            {
                "ChatId": 1672920235409489,
                "CreateTime": 1714658888,
                "TextContent": "Hello",
                "User": {
                    "Nickname": "Viewer A",
                    "UserId": 17975829****
                },
                "IsDelete": false,
                "LikeCount": 10,
                "IsPresenter": false,
                "reviewStatus": 0,
                "IsTipOff": 0
            },
            {
                "ChatId": 1672920235409492,
                "CreateTime": 1714660078,
                "TextContent": "Hello",
                "User": {
                    "Nickname": "Host",
                    "UserId": 0
                },
                "IsDelete": false,
                "LikeCount": 0,
                "IsPresenter": true,
                "reviewStatus": 2,
                "IsTipOff": 0
            }
        ]
    }
}
```


<span id="f9940149"></span>
## 錯誤碼

共用錯誤碼列表請參見 [常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/chang-jian-cuo-wu-yu-zhuang-tai-ma-zh-TW)。
