---
title: "UpdateFloatingAdvertisementAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/UpdateFloatingAdvertisement-zh-TW"
---

呼叫 `UpdateFloatingAdvertisementAPI`，以更新指定直播間中的浮動廣告的狀態、連結及其他配置細節。

<span id="Requirements"></span>
## 需求


* 配額：每個帳戶每秒最多 10 次查詢。

* 先決條件：需有 BytePlus 帳戶，或具備 **Marketing toolkits** \> **Edit** 權限的 IAM 使用者。如需瞭解如何新增 IAM 使用者，請參閱 [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://livesaas.byteplusapi.com/?Action=UpdateFloatingAdvertisementAPI&Version=2023\-08\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

下表未包含所有通用請求參數。完整列表請參閱 [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`UpdateFloatingAdvertisementAPI` |API 操作。 |
|Version |String |是 |`2023-08-01` |此 API 操作的版本。目前版本：`2023-08-01`。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|ActivityId |Long |是 |1798615803\*\*\*\* |直播間的活動 ID。可透過呼叫 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi) 取得 ID。 |
|IsEnable |Integer |否 |`1` |指定是否啟用浮動廣告。支援以下值，預設值為 `0`。<br><br><br>* `0`：停用<br><br>* `1`：啟用 |
|ImageUrl |String |否 |https://p.example.org/6ed59yyum2\-z75.png |浮動廣告圖片 URL。地址必須包含 https 協議標頭。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">首次使用此 API 配置浮動廣告時，此參數為必填。</div><br> |
|HomeUrl |String |否 |`https://example.com` |浮動廣告的嵌入連結必須包含 https 協議標頭。 |
|IsCloseEnable |Integer |否 |`1` |指定觀眾是否可關閉浮動廣告。支援以下值，預設值為 `0`。<br><br><br>* `0`：廣告可關閉<br><br>* `1`：廣告不可關閉 |
|EnableFloating |Boolean |否 |true |指定是否啟用浮動顯示。支援以下值，預設值為 `false`。<br><br><br>* `true`：設為 `true` 時，點擊浮動廣告會在當前直播頁面展開，觀眾可在觀看直播的同時瀏覽廣告。此選項僅於行動端觀看頁面生效。<br><br>* `false`：設為 `false` 時，點擊浮動廣告會開啟新的瀏覽器分頁顯示廣告。因此，觀眾無法同時觀看直播與廣告。 |


<span id="Response parameters"></span>
## 回應參數


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Status |Boolean |`true` |若配置成功更新，則回傳 `true`。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```JSON
POST https://livesaas.byteplusapi.com/?Action=UpdateFloatingAdvertisementAPI&Version=2023-08-01
{
    "ActivityId": 1798615803****,
    "ImageUrl": "https://p.example.org/6ed59yyum2-z75.png",
    "HomeUrl": "https://example.com",
    "IsCloseEnable": 1,
    "IsEnable": 1,
    "EnableFloating": true
}
```


<span id="Sample response"></span>
### 範例回應

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UpdateFloatingAdvertisementAPI",
        "Version": "2023-08-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1697446406
    },
    "Result": {
        "Status": true
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

常見錯誤碼請參閱 [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
