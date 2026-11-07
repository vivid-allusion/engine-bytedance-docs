---
title: "SendAward"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/SendAward-zh-TW"
---

呼叫`SendAward`以在直播間啟動即時抽獎。

<span id="Requirements"></span>
## 需求


* 速率限制：每個帳戶每秒 10 次請求

* 前置條件：需具備 BytePlus 帳戶或擁有**直播控制** \> **編輯**權限的 IAM 使用者。如需瞭解如何新增 IAM 使用者，請參閱[管理使用者、組織與角色](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://livesaas.byteplusapi.com/?Action=SendAward&Version=2023\-08\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

下列表格未涵蓋所有通用請求參數。完整列表請參閱[通用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |字串 |是 |`SendAward` |API 操作。 |
|Version |字串 |是 |`2023-08-01` |此 API 操作的版本。目前版本：`2023-08-01`。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|ActivityId |整數 |是 |17218346\*\*\*\* |直播間的活動 ID。可透過呼叫[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi)取得該 ID。 |
|Id |整數 |是 |`36***` |即時抽獎 ID。可透過呼叫`ListAwardConfigs` API 取得該 ID。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">啟動即時抽獎時，請確保尚未啟動該抽獎。若<code>ListAwardConfigs</code> API 回傳的<code>Status</code>參數值為<code>1</code>，即可呼叫本 API 啟動即時抽獎。</div><br> |


<span id="Response parameters"></span>
## 回應參數


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Status |布林值 |`true` |表示是否成功啟動抽獎。若成功，則回傳`true`。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```JSON
POST https://livesaas.byteplusapi.com/?Action=SendAward&Version=2023-08-01
{
    "ActivityId": 17218346****,
    "Id": 36***
}
```


<span id="Sample response"></span>
### 回應範例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "SendAward",
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

如需常見錯誤碼列表，請參閱[常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
