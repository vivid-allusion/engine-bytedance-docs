---
title: "UpdateActivityQuizConfigAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/UpdateActivityQuizConfig-zh-TW"
---

呼叫 `UpdateActivityQuizConfigAPI`，以更新指定直播間中未發送問答的配置信息。

<span id="Requirements"></span>
## 需求


* 頻率限制：每個帳戶每秒最多 10 次請求

* 先決條件：

   * 問答尚未發送。可呼叫 [ListActivityQuizConfigsAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/ListActivityQuizConfigs?lang=en)。若 `QuizStatus` 設為 `0`，表示問答尚未發送。

   * 需擁有 BytePlus 帳戶或具備 **Live control** \> **Edit** 權限的 IAM 使用者。如需新增 IAM 使用者的詳細資訊，請參閱 [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://livesaas.byteplusapi.com/?Action=UpdateActivityQuizConfigAPI&Version=2023\-08\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

下表未包含所有通用請求參數。完整列表請參閱 [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`UpdateActivityQuizConfigAPI` |API 操作。 |
|Version |String |是 |`2023-08-01` |此 API 操作的版本。目前版本：`2023-08-01`。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Id |Long |是 |`1808481235212316` |問答 ID。可透過呼叫 ListActivityQuizConfigs API 取得 ID。 |
|ActivityId |Long |是 |17218346\*\*\*\* |直播間的活動 ID。可透過呼叫 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi) 取得 ID。 |
|QuizTitle |String |否 |Quiz 1 |問答標題。預設為空。 |
|QuizResultType |Integer |是 |`1` |控制答案揭示的時機。有效值如下：<br><br><br>* `0`：提交後自動揭示答案<br><br>* `1`：問答時間結束時自動揭示答案<br><br>* `2`：手動揭示答案 |
|QuizOptions |Array of[QuizOptions](https://docs.byteplus.com/docs/byteplus-livesaas/UpdateActivityQuizConfig-zh-TW#quizoptions) |是 |*  |選項資訊。陣列元素最多 8 個。 |
|RightOptions |Array of String |是 |`["A"]` |正確答案。請確保此值與本次呼叫中的 `OptionSite` 其中一個值相符。 |
|Deadline |Long |是 |`30` |問答的時間限制（秒）。最小值為 `10`。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">此參數僅於 <code>QuizResultType</code> 設為 <code>0</code> 或 <code>1</code> 時有效。</div><br> |
|QuizTitleType |Integer |是 |`0` |題型。有效值如下：<br><br><br>* `0`：單選題<br><br>* `1`：多選題 |
|QuizAnalysis |String |否 |1 的倒數是 1 |答案解析。預設為空。 |


<span id="quizoptions"></span>
### QuizOptions


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|OptionSite |String |是 |`A` |選項識別碼。 |
|OptionName |String |否 |1 |選項內容。預設為空。 |


<span id="Response parameters"></span>
## 回應參數


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Status |Boolean |`true` |若配置更新成功則回傳 `true`。 |
|Id |Long |`1808481235212316` |問答 ID。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```JSON
POST https://livesaas.byteplusapi.com/?Action=UpdateActivityQuizConfigAPI&Version=2023-08-01
{
    "Id": 1808481235212316,
    "ActivityId": 17218346,
    "QuizTitle": "Quiz 1",
    "QuizResultType": 1,
    "QuizOptions": [
        {
            "OptionSite": "A",
            "OptionName": "1"
        }
    ],
    "RightOptions": [
        "A"
    ],
    "Deadline": 30,
    "QuizTitleType": 0,
    "QuizAnalysis": "The reciprocal of 1 is 1"
}
```


<span id="Sample response"></span>
### 範例回應

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UpdateActivityQuizConfigAPI",
        "Version": "2023-08-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1697446406
    },
    "Result": {
        "Status": true,
        "Id": 1808481235212316
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

下表列出此 API 操作專屬的錯誤碼。通用錯誤碼請參閱 [Common error and status codes](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|403 |OperationDenied.QuizStatusNotMatchExpectedStatus |QuizStatus 與預期狀態不符 |此操作僅支援更新未發送問答的配置信息。可呼叫 ListActivityQuizConfigs API。若 `QuizStatus` 設為 `0`，表示問答尚未發送。 |
