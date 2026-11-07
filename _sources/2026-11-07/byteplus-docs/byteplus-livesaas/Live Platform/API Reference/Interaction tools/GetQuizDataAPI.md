---
title: "GetQuizDataAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/GetQuizDataAPI"
---

Call `GetQuizDataAPI` to obtain detailed information about a specified quiz in a live streaming room. This includes the number of participants, the number of correct answers, and the content of each option.

<span id="Requirements"></span>
## Requirements


* Quota: 120 queries per minute per account.

* Prerequisite: A BytePlus account or an IAM user with **Insights** \> **View only** or **Edit** permission. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).


<span id="HTTP request"></span>
## HTTP request


* Method：GET

* Endpoint：https://livesaas.byteplusapi.com/?Action=GetQuizDataAPI&Version=2020\-06\-01


<span id="Request parameters"></span>
## Request parameters

<span id="Common parameters"></span>
### Common parameters

Not all common request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="Query"></span>
### Query


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`GetQuizDataAPI` |API operation. |
|Version |String |Yes |`2020-06-01` |The version of this API operation. Current version: `2020-06-01`. |
|ActivityId |Long |Yes |17218346\*\*\*\* |The activity ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |
|QuizID |Integer |Yes |1779512495\*\*\*\* |The ID of the quiz. You can obtain the ID by calling [ListQuizStatisticsAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/ListQuizStatisticsAPI). |


<span id="Response parameters"></span>
## Response parameters


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|TotalCount |Integer |2 |Number of participants. |
|RightCount |Integer |1 |The number of people who answered correctly. |
|QuizOptions |Array of [QuizOptions](https://docs.byteplus.com/docs/byteplus-livesaas/GetQuizDataAPI#quizoptions) |*  |A list of the options for the quiz. |


<span id="quizoptions"></span>
### QuizOptions


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|OptionSite |String |A |The option identifier. |
|OptionName |String |1 |Option content. |
|OptionCount |String |1 |The number of people who chose this option. |
|OptionPercent |Integer |50 |The percentage of the number of people who chose this option among the total number of participants. |


<span id="Samples"></span>
## Samples

<span id="Sample request"></span>
### Sample request

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetQuizDataAPI&Version=2020-06-01&ActivityId=17218346****&QuizID=1779512495345672
```


<span id="Sample response"></span>
### Sample response

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
## Error codes

For a list of common error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).
