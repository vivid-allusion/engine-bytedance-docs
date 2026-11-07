---
title: "ListQuizStatisticsAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/ListQuizStatisticsAPI-zh-TW"
---

呼叫 `ListQuizStatisticsAPI` 以取得分頁的測驗清單及其互動統計資料。資料包含參與人數、答對次數，以及指定直播間的其他相關細節。

<span id="Requirements"></span>
## 需求


* 配額：每個帳戶每分鐘最多 120 次查詢。

* 前置條件：需有 BytePlus 帳戶，或擁有 **Insights** \> **View only** 或 **Edit** 權限的 IAM 使用者。如需瞭解如何新增 IAM 使用者，請參閱 [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：GET

* 端點：https://livesaas.byteplusapi.com/?Action=ListQuizStatisticsAPI&Version=2020\-06\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

下表未包含所有通用請求參數。完整列表請參閱 [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`ListQuizStatisticsAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。目前版本：`2020-06-01`。 |
|ActivityId |Long |是 |17218346\*\*\*\* |直播間的活動 ID。可透過呼叫 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi) 取得此 ID。 |
|PageNo |Integer |否 |1 |要返回的頁碼。預設值：`1`。 |
|PageItemCount |Integer |否 |10 |每頁返回的結果數量。預設值：`10`。 |


<span id="Response parameters"></span>
## 回應參數


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|PageNo |Integer |1 |要返回的頁碼。 |
|PageItemCount |Integer |10 |每頁返回的結果數量。 |
|PageTotalCount |Integer |`1` |查詢結果總數。 |
|QuizStatisticsList |Array of[QuizStatisticsList](https://docs.byteplus.com/docs/byteplus-livesaas/ListQuizStatisticsAPI-zh-TW#quizstatisticslist) |`-` |測驗清單。 |


<span id="quizstatisticslist"></span>
### QuizStatisticsList


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|TotalCount |Integer |`1` |參與人數。 |
|QuizTitle |String |Quiz 1 |測驗標題。 |
|QuizTitleType |Integer |`0` |題目類型。有效值如下：<br><br><br>* `0`：單選題<br><br>* `1`：多選題 |
|SendTime |Integer |`1673348926` |發送時間。Unix 時間戳，單位為秒。 |
|Deadline |Integer |30 |測驗時限。單位：秒。 |
|RightCount |Integer |1 |答對人數。 |
|QuizID |Integer |`1754628061265087` |測驗 ID。 |
|IsDelete |Boolean |`false` |測驗是否已刪除。有效值如下：<br><br><br>* `false`：未刪除<br><br>* `true`：已刪除 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```JSON
GET https://livesaas.byteplusapi.com/?Action=ListQuizStatisticsAPI&Version=2020-06-01&ActivityId=17791682****&PageNo=1&PageItemCount=10
```


<span id="Sample response"></span>
### 範例回應

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListQuizStatisticsAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1697446406
    },
    "Result": {
        "PageNo": 1,
        "PageItemCount": 10,
        "PageTotalCount": 1,
        "QuizStatisticsList": [
            {
                "TotalCount": 1,
                "QuizTitle": "Quiz 1",
                "QuizTitleType": 0,
                "SendTime": 1673348926,
                "Deadline": 30,
                "RightCount": 1,
                "QuizID": 1754628061265087,
                "IsDelete": false
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

常見錯誤碼列表請參閱 [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
