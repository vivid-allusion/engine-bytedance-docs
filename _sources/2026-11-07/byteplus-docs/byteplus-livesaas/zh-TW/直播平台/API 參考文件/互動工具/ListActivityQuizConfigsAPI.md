---
title: "ListActivityQuizConfigsAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/ListActivityQuizConfigs-zh-TW"
---

呼叫 `ListActivityQuizConfigsAPI` 以取得指定直播間的測驗配置資訊。

<span id="Requirements"></span>
## 需求


* 頻率限制：每個帳戶每秒最多 10 次請求

* 先決條件：需有 BytePlus 帳戶或具備 **Live control** \> **Edit** 權限的 IAM 使用者。如需更多有關新增 IAM 使用者的資訊，請參閱 [管理使用者、組織與角色](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://livesaas.byteplusapi.com/?Action=ListActivityQuizConfigsAPI&Version=2023\-08\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

下表並未包含所有通用請求參數。完整列表請參閱 [通用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`ListActivityQuizConfigsAPI` |API 操作。 |
|Version |String |是 |`2023-08-01` |此 API 操作的版本。目前版本：`2023-08-01`。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**必填** |**範例值** |**說明** |
|---|---|---|---|---|
|ActivityId |Long |是 |17218346\*\*\*\* |直播間的活動 ID。可透過呼叫 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi) 取得 ID。 |


<span id="Response parameters"></span>
## 回應參數


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|QuizConfigs |Array of[QuizConfigs](https://docs.byteplus.com/docs/byteplus-livesaas/ListActivityQuizConfigs-zh-TW#quizconfigs) |*  |測驗配置資訊。 |


<span id="quizconfigs"></span>
### QuizConfigs


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Id |Long |`180848123521****` |測驗 ID。 |
|ActivityId |Long |1770637083\*\*\*\* |直播間 ID。 |
|QuizTitle |String |Quiz 1 |測驗標題。 |
|QuizResultType |Integer |`0` |指定答案發布時機。有效值如下：<br><br><br>* `0`：提交後自動發布答案<br><br>* `1`：測驗時間結束時自動發布答案<br><br>* `2`：手動發布答案 |
|QuizOptions |Array of[QuizOptions](https://docs.byteplus.com/docs/byteplus-livesaas/ListActivityQuizConfigs-zh-TW#quizoptions) |*  |選項資訊。 |
|RightOptions |Array of String |["A"] |正確答案。 |
|Deadline |Long |`30` |測驗時限。單位：秒。 |
|SendTime |Long |1621111109 |發送時間。Unix 時間戳，單位為秒。若未發送，值為 `-1`。 |
|QuizStatus |Integer |[0,1,2,3,5] |測驗狀態。有效值如下：<br><br><br>* `0`：已初始化，表示已建立但尚未發送<br><br>* `1`：已發送<br><br>* `2`：答案已手動發布。此值僅適用於歷史資料<br><br>* `3`：已結束<br><br>* `4`：已刪除<br><br>* `5`：已撤回 |
|QuizTitleType |Integer |`1` |題型。有效值如下：<br><br><br>* `0`：單選題<br><br>* `1`：多選題 |
|QuizAnalysis |String |1 的倒數是 1 |答案解析。 |


<span id="quizoptions"></span>
### QuizOptions


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|OptionSite |String |`A` |選項。 |
|OptionName |String |1 |選項內容。 |
|OptionCount |Long |`50` |選擇此選項的使用者數。 |
|OptionPercent |String |`100` |在所有參與者中選擇此選項的使用者百分比。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```JSON
POST https://livesaas.byteplusapi.com/?Action=ListActivityQuizConfigsAPI&Version=2023-08-01
{
    "ActivityId": 1770637083****
}
```


<span id="Sample response"></span>
### 回應範例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListActivityQuizConfigsAPI",
        "Version": "2023-08-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1697446406
    },
    "Result": {
        "QuizConfigs": [
            {
                "Id": 180848123521****,
                "ActivityId": 1770637083****,
                "QuizTitle": "Quiz 1",
                "QuizResultType": 0,
                "QuizOptions": [
                    {
                        "OptionSite": "A",
                        "OptionName": "1",
                        "OptionCount": 50,
                        "OptionPercent": "100"
                    }
                ],
                "RightOptions": [
                    "A"
                ],
                "Deadline": 30,
                "SendTime": 1621111109,
                "QuizStatus": 1,
                "QuizTitleType": 1,
                "QuizAnalysis": "The reciprocal of 1 is 1"
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

如需常見錯誤碼列表，請參閱 [常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
