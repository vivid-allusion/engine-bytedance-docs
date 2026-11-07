---
title: "ListQuizStatisticsAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/ListQuizStatisticsAPI"
---

Call `ListQuizStatisticsAPI` to retrieve a paginated list of quizzes and their engagement statistics. The data includes the number of participants, the count of correct answers, and other relevant details for a specified live room.

<span id="Requirements"></span>
## Requirements


* Quota: 120 queries per minute per account.

* Prerequisite: A BytePlus account or an IAM user with **Insights** \> **View only** or **Edit** permission. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).


<span id="HTTP request"></span>
## HTTP request


* Method：GET

* Endpoint：https://livesaas.byteplusapi.com/?Action=ListQuizStatisticsAPI&Version=2020\-06\-01


<span id="Request parameters"></span>
## Request parameters

<span id="Common parameters"></span>
### Common parameters

Not all common request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="Query"></span>
### Query


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`ListQuizStatisticsAPI` |API operation. |
|Version |String |Yes |`2020-06-01` |The version of this API operation. Current version: `2020-06-01`. |
|ActivityId |Long |Yes |17218346\*\*\*\* |The activity ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |
|PageNo |Integer |No |1 |The number of the page to return. Default value: `1`. |
|PageItemCount |Integer |No |10 |The number of results to return on each page. Default value: `10`. |


<span id="Response parameters"></span>
## Response parameters


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|PageNo |Integer |1 |The number of the page to return. |
|PageItemCount |Integer |10 |The number of results to return on each page. |
|PageTotalCount |Integer |`1` |Total number of query results. |
|QuizStatisticsList |Array of [QuizStatisticsList](https://docs.byteplus.com/docs/byteplus-livesaas/ListQuizStatisticsAPI#quizstatisticslist) |`-` |Quiz list. |


<span id="quizstatisticslist"></span>
### QuizStatisticsList


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|TotalCount |Integer |`1` |Number of participants. |
|QuizTitle |String |Quiz 1 |Quiz title. |
|QuizTitleType |Integer |`0` |Question type. Valid values are as follows:<br><br><br>* `0`: Single choice<br><br>* `1`: Multiple choice |
|SendTime |Integer |`1673348926` |Send time. Unix timestamp, measured in seconds. |
|Deadline |Integer |30 |Quiz time limit. Unit: seconds. |
|RightCount |Integer |1 |The number of participants who answered correctly. |
|QuizID |Integer |`1754628061265087` |Quiz ID. |
|IsDelete |Boolean |`false` |Whether the quiz has been deleted. Valid values are as follows:<br><br><br>* `false`: Not deleted<br><br>* `true`: Deleted |


<span id="Samples"></span>
## Samples

<span id="Sample request"></span>
### Sample request

```JSON
GET https://livesaas.byteplusapi.com/?Action=ListQuizStatisticsAPI&Version=2020-06-01&ActivityId=17791682****&PageNo=1&PageItemCount=10
```


<span id="Sample response"></span>
### Sample response

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
## Error codes

For a list of common error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).
