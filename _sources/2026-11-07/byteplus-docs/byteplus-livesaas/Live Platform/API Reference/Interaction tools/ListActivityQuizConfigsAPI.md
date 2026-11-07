---
title: "ListActivityQuizConfigsAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/ListActivityQuizConfigs"
---

Call `ListActivityQuizConfigsAPI` to obtain the quiz configuration information for a specified live room.

<span id="Requirements"></span>
## Requirements


* Rate limit: 10 requests per second per account

* Prerequisite: A BytePlus account or an IAM user with **Live control** \> **Edit** permission. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).


<span id="HTTP request"></span>
## HTTP request


* Method：POST

* Endpoint：https://livesaas.byteplusapi.com/?Action=ListActivityQuizConfigsAPI&Version=2023\-08\-01


<span id="Request parameters"></span>
## Request parameters

<span id="Common parameters"></span>
### Common parameters

Not all common request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="Query"></span>
### Query


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`ListActivityQuizConfigsAPI` |API operation. |
|Version |String |Yes |`2023-08-01` |The version of this API operation. Current version: `2023-08-01`. |


<span id="Body parameters"></span>
### Body parameters


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|ActivityId |Long |Yes |17218346\*\*\*\* |The activity ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |


<span id="Response parameters"></span>
## Response parameters


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|QuizConfigs |Array of [QuizConfigs](https://docs.byteplus.com/docs/byteplus-livesaas/ListActivityQuizConfigs#quizconfigs) |*  |Quiz configuration information. |


<span id="quizconfigs"></span>
### QuizConfigs


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Id |Long |`180848123521****` |Quiz ID. |
|ActivityId |Long |1770637083\*\*\*\* |Live room ID. |
|QuizTitle |String |Quiz 1 |Quiz title. |
|QuizResultType |Integer |`0` |Specifies when to publish the answers. Valid values are as follows:<br><br><br>* `0`: Automatically publish answers after submission<br><br>* `1`: Automatically publish answers when the quiz time ends<br><br>* `2`: Manually publish answers |
|QuizOptions |Array of [QuizOptions](https://docs.byteplus.com/docs/byteplus-livesaas/ListActivityQuizConfigs#quizoptions) |*  |Option information. |
|RightOptions |Array of String |["A"] |Correct answer. |
|Deadline |Long |`30` |Quiz time limit. Unit: seconds. |
|SendTime |Long |1621111109 |Sending time. Unix timestamp, measured in seconds. If not sent, the value is `-1`. |
|QuizStatus |Integer |[0,1,2,3,5] |Quiz status. Valid values are as follows:<br><br><br>* `0`: Initialized, which means created but not sent<br><br>* `1`: Sent<br><br>* `2`: The answer was manually published. This value applies only to historical data<br><br>* `3`: Ended<br><br>* `4`: Deleted<br><br>* `5`: Withdrawn |
|QuizTitleType |Integer |`1` |Question type. Valid values are as follows:<br><br><br>* `0`: Single choice<br><br>* `1`: Multiple choice |
|QuizAnalysis |String |The reciprocal of 1 is 1 |Answer explanation. |


<span id="quizoptions"></span>
### QuizOptions


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|OptionSite |String |`A` |Option. |
|OptionName |String |1 |Option content. |
|OptionCount |Long |`50` |The number of users who selected this option. |
|OptionPercent |String |`100` |The percentage of users who selected this option among all participants. |


<span id="Samples"></span>
## Samples

<span id="Sample request"></span>
### Sample request

```JSON
POST https://livesaas.byteplusapi.com/?Action=ListActivityQuizConfigsAPI&Version=2023-08-01
{
    "ActivityId": 1770637083****
}
```


<span id="Sample response"></span>
### Sample response

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
## Error codes

For a list of common error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).
