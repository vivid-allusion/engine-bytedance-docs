---
title: "WithdrawAward"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/WithdrawAward-zh-TW"
---

調用 `WithdrawAward` 以從直播間撤回一個即時抽獎。注意，已撤回的抽獎無法再次發送或更新。

<span id="Requirements"></span>
## 需求


* 頻率限制：每個帳戶每秒 10 次請求

* 前提條件：擁有 BytePlus 帳戶或具備 **Live control** \> **Edit** 權限的 IAM 使用者。如需瞭解如何新增 IAM 使用者，請參見 [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://livesaas.byteplusapi.com/?Action=WithdrawAward&Version=2023\-08\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

下列表格未包含所有通用請求參數。如需完整列表，請參見 [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`WithdrawAward` |API 操作。 |
|Version |String |是 |`2023-08-01` |此 API 操作的版本。當前版本：`2023-08-01`。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|ActivityId |Integer |是 |17218346\*\*\*\* |直播間的活動 ID。可透過調用 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi) 獲取該 ID。 |
|Id |Integer |是 |36576 |要撤回的即時抽獎 ID。可透過調用 ListAwardConfigs API 獲取該 ID。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">撤回即時抽獎時，請確保抽獎狀態為「進行中」或「已結束」。當 <code>ListAwardConfigs</code> API 回傳的 <code>Status</code> 參數值為 <code>2</code> 或 <code>4</code> 時，可調用本 API 撤回即時抽獎。</div><br> |


<span id="Response parameters"></span>
## 回應參數


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Status |Boolean |`true` |抽獎是否成功撤回。若成功則回傳 `true`。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```JSON
POST https://livesaas.byteplusapi.com/?Action=WithdrawAward&Version=2023-08-01
{
    "ActivityId": 17218346****,
    "Id": 36576
}
```


<span id="Sample response"></span>
### 回應範例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "WithdrawAward",
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

如需常見錯誤碼列表，請參見 [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
