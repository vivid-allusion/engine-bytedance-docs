---
title: "UpdatePresenterAwardConfigAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/UpdateAwardConfig-zh-TW"
---

調用`UpdatePresenterAwardConfigAPI`以新增、更新或刪除直播間的即時抽獎。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">更新抽獎時，必須傳入所有自訂參數的值，以避免參數被重設為預設值。</div>


<span id="Requirements"></span>
## 需求


* 速率限制：每個帳號每秒 10 次請求

* 前置條件：需有 BytePlus 帳號，或具備**直播控制** \> **編輯**權限的 IAM 使用者。如需瞭解如何新增 IAM 使用者，請參見[管理使用者、組織與角色](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://livesaas.byteplusapi.com/?Action=UpdatePresenterAwardConfigAPI&Version=2023\-08\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

下列表格未包含所有通用請求參數。完整列表請參見[通用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`UpdatePresenterAwardConfigAPI` |API 操作。 |
|Version |String |是 |`2023-08-01` |本 API 操作的版本。當前版本：`2023-08-01`。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|ActivityId |Long |是 |17218346\*\*\*\* |直播間的活動 ID。可透過調用[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi)獲取 ID。 |
|AccountId |Long |是 |3000\*\*\*\* |您的帳號 ID，可於[我的帳號](https://console.byteplus.com/user/basics/)頁面查詢。 |
|Id |Long |是 |`36576` |即時抽獎 ID。值說明如下：<br><br><br>* 若要建立即時抽獎，請傳入`0`。<br><br>* 若要更新或刪除抽獎配置，請傳入抽獎 ID。可透過[ListAwardConfigs](https://docs.byteplus.com/docs/byteplus-livesaas/ListAwardConfigs) API 獲取 ID。 |
|Name |String |否 |抽獎活動 |抽獎名稱。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">建立或更新即時抽獎時必填此參數。</div><br> |
|AwardType |Integer |否 |1 |抽獎方式。值說明如下：<br><br><br>* `1`：自動抽獎<br><br>* `2`：手動抽獎<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">建立或更新抽獎時必填此參數。</div><br> |
|DeadLine |Long |否 |30 |抽獎倒數計時長度（分鐘）。預設值為`0`。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">僅當<code>AwardType</code>的值為<code>1</code>時，此參數才有效。</div><br> |
|BarragePwd |String |否 |彈幕密碼 |抽獎彈幕密碼。預設值為空。 |
|WinnerInfoType |String |否 |1 |中獎者需提供的個人資訊。支援的值包括：<br><br><br>* 1：收件地址<br><br>* 2：電話號碼<br><br>* 3：收件人姓名 |
|AwardNum |Integer |否 |1000 |獎品數量。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">建立或更新即時抽獎時必填此參數。</div><br> |
|RangeStatus |Integer |否 |0 |抽獎規則。預設值為`0`。值說明如下：<br><br><br>* `0`：所有觀眾中獎機率相同。<br><br>* `1`：未中獎觀眾優先。 |
|ShowPeopleNumber |Integer |否 |0 |是否在觀看頁面顯示實際參與抽獎的人數。預設值為`0`。值說明如下：<br><br><br>* `0`：顯示<br><br>* `1`：不顯示 |
|Status |Integer |是 |`1` |指定對即時抽獎執行的操作。值說明如下：<br><br><br>* `1`：建立或更新即時抽獎<br><br>* `5`：刪除即時抽獎 |
|AwardCondition |Object of[AwardCondition](https://docs.byteplus.com/docs/byteplus-livesaas/UpdateAwardConfig-zh-TW#awardcondition) |否 |*  |參與抽獎的條件。 |
|ShowWinnerComment |Integer |否 |0 |是否顯示中獎者詳情。預設值為`0`。值說明如下：<br><br><br>* `0`：不顯示<br><br>* `1`：顯示 |
|AwardId |Long |否 |1621615169 |獎品 ID。可透過調用[GetAwardItemList](https://docs.byteplus.com/en/docs/byteplus-livesaas/getawarditemlist?lang=en)獲取 ID。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">建立或更新即時抽獎時必填此參數。</div><br> |


<span id="awardcondition"></span>
### AwardCondition


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|答題 |字串 |否 |all |設定用戶參與問答以符合抽獎資格的條件。若未設定此參數（預設），則不啟用此條件。<br><br><br>* `"all"`：用戶必須在抽獎前，於直播期間回答**所有**發送的問題。<br><br>* `1`\-`999`：用戶必須提交**至少**此數量的答案才符合資格。例如，值為`3`時，表示用戶需至少回答三個問題。 |
|正確答題 |字串 |否 |`1` |用戶必須正確回答的最少題數。 |
|問卷 |字串 |否 |1 |用戶必須提交的最少問卷數量。 |
|簽到 |字串 |否 |all |用戶必須完成的最少簽到次數。 |
|投票 |字串 |否 |1 |用戶必須提交的最少投票數。 |


<span id="awarditemconfigs"></span>
### 回應參數


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|狀態 |布林值 |`true` |若設定成功，則回傳`true`。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```JSON
POST https://livesaas.byteplusapi.com/?Action=UpdatePresenterAwardConfigAPI&Version=2023-08-01
{
    "ActivityId": 172183461234****,
    "AccountId": 3000****,
    "Id": 0,
    "Status": 1,
    "Name": "Prize A",
    "AwardType": 1,
    "DeadLine": 1,
    "AwardId": 1001,
    "AwardNum": 100,
    "RangeStatus": 1,
    "WinnerInfoType": "1",
    "AwardCondition": {
        "CheckIn": "1"
    }
}
```


<span id="Sample response"></span>
### 回應範例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UpdatePresenterAwardConfigAPI",
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

常見錯誤碼請參見[常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
