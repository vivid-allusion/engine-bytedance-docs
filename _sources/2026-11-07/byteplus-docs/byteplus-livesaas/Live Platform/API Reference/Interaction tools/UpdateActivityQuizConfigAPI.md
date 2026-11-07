---
title: "UpdateActivityQuizConfigAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/UpdateActivityQuizConfig"
---

Call `UpdateActivityQuizConfigAPI` to update the configuration information for unsent quizzes in a specified live room.

<span id="Requirements"></span>
## Requirements


* Rate limit: 10 requests per second per account

* Prerequisites:

   * The quiz has not been sent. You can call [ListActivityQuizConfigsAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/ListActivityQuizConfigs?lang=en). If `QuizStatus` is set to `0`, it means the quiz has not been sent.

   * A BytePlus account or an IAM user with **Live control** \> **Edit** permission. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).


<span id="HTTP request"></span>
## HTTP request


* Method：POST

* Endpoint：https://livesaas.byteplusapi.com/?Action=UpdateActivityQuizConfigAPI&Version=2023\-08\-01


<span id="Request parameters"></span>
## Request parameters

<span id="Common parameters"></span>
### Common parameters

Not all common request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="Query"></span>
### Query


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`UpdateActivityQuizConfigAPI` |API operation. |
|Version |String |Yes |`2023-08-01` |The version of this API operation. Current version: `2023-08-01`. |


<span id="Body parameters"></span>
### Body parameters


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Id |Long |Yes |`1808481235212316` |Quiz ID. You can obtain the ID by calling the ListActivityQuizConfigs API. |
|ActivityId |Long |Yes |17218346\*\*\*\* |The activity ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |
|QuizTitle |String |No |Quiz 1 |Quiz title. Default is empty. |
|QuizResultType |Integer |Yes |`1` |Controls when answers are revealed. Valid values are as follows:<br><br><br>* `0`: Automatically reveal answers after submission<br><br>* `1`: Automatically reveal answers when the quiz time ends<br><br>* `2`: Reveal answers manually |
|QuizOptions |Array of [QuizOptions](https://docs.byteplus.com/docs/byteplus-livesaas/UpdateActivityQuizConfig#quizoptions) |Yes |*  |Option information. The maximum number of array elements is 8. |
|RightOptions |Array of String |Yes |`["A"]` |The correct answer. Ensure that the value matches the value of one of the `OptionSite` in this call. |
|Deadline |Long |Yes |`30` |The time limit for the quiz, in seconds. The minimum value is `10`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is valid only when <code>QuizResultType</code> is set to <code>0</code> or <code>1</code>.</div><br> |
|QuizTitleType |Integer |Yes |`0` |Question type. Valid values are as follows:<br><br><br>* `0`: Single choice<br><br>* `1`: Multiple choice |
|QuizAnalysis |String |No |The reciprocal of 1 is 1 |Answer analysis. Default is empty. |


<span id="quizoptions"></span>
### QuizOptions


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|OptionSite |String |Yes |`A` |The option identifier. |
|OptionName |String |No |1 |Option content. The default is empty. |


<span id="Response parameters"></span>
## Response parameters


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Status |Boolean |`true` |Returns `true` if the configuration was updated successfully. |
|Id |Long |`1808481235212316` |Quiz ID. |


<span id="Samples"></span>
## Samples

<span id="Sample request"></span>
### Sample request

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
### Sample response

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
## Error codes

The following table lists error codes specific to this API operation. For a list of common error codes, see [Common error and status codes](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-shared-error-and-status-codes).


|**Status Code** |**Error Code** |**Error Message** |**Description** |
|---|---|---|---|
|403 |OperationDenied.QuizStatusNotMatchExpectedStatus |QuizStatus does not match the expected status |This operation only supports updating configuration information for unsent quizzes. You can call the ListActivityQuizConfigs API. If `QuizStatus` is set to `0`, it means the quiz has not been sent. |
