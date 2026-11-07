---
title: "GetQuizDataAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/GetQuizDataAPI-zh-TW"
---

呼叫 `GetQuizDataAPI` 以取得直播間中指定問答的詳細資訊。這包括參與人數、答對人數，以及每個選項的內容。

<span id="Requirements"></span>
## 需求


* 配額：每個帳戶每分鐘最多可查詢 120 次。

* 前提條件：需有 BytePlus 帳戶，或具備 **Insights** \> **View only** 或 **Edit** 權限的 IAM 使用者。如需新增 IAM 使用者的詳細資訊，請參閱 [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：GET

* 端點：https://livesaas.byteplusapi.com/?Action=GetQuizDataAPI&Version=2020\-06\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

下表並未包含所有通用請求參數。完整列表請參閱 [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`GetQuizDataAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。目前版本：`2020-06-01`。 |
|ActivityId |Long |是 |17218346\*\*\*\* |直播間的活動 ID。可透過呼叫 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi) 取得 ID。 |
|QuizID |Integer |是 |1779512495\*\*\*\* |問答的 ID。可透過呼叫 [ListQuizStatisticsAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/ListQuizStatisticsAPI) 取得 ID。 |


<span id="Response parameters"></span>
## 回應參數


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|TotalCount |Integer |2 |參與人數。 |
|RightCount |Integer |1 |答對人數。 |
|QuizOptions |Array of[QuizOptions](https://docs.byteplus.com/docs/byteplus-livesaas/GetQuizDataAPI-zh-TW#quizoptions) |*  |問答的選項列表。 |


<span id="quizoptions"></span>
### QuizOptions


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|OptionSite |String |A |選項識別碼。 |
|OptionName |String |1 |選項內容。 |
|OptionCount |String |1 |選擇此選項的人數。 |
|OptionPercent |Integer |50 |選擇此選項的人數占總參與人數的百分比。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetQuizDataAPI&Version=2020-06-01&ActivityId=17218346****&QuizID=1779512495345672
```


<span id="Sample response"></span>
### 範例回應

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetQuizDataAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1697446406
    },
    "Result": {
        "TotalCount": 2,
        "RightCount": 1,
        "QuizOptions": [
            {
                "OptionSite": "A",
                "OptionName": "1",
                "OptionCount": "1",
                "OptionPercent": 50
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

常見錯誤碼列表請參閱 [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
