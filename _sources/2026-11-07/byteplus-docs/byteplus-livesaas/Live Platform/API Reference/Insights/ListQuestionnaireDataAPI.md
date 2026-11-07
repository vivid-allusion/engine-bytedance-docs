---
title: "ListQuestionnaireDataAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-listquestionnairedataapi"
---

Call this API to retrieve a paginated list of statistical data for questionnaires associated with a specific live\-streaming activity. This includes details such as the questionnaire ID, title, publish time, and the number of submitters.

<span id="64b48720"></span>
## Request

<span id="4ea84dd3"></span>
### Details


* API operation: `ListQuestionnaireDataAPI`

* Request method: GET

* Request URI: `http://livesaas.byteplusapi.com/?Action=ListQuestionnaireDataAPI&Version=2020-06-01`

* Quota: 120 queries per minute per account


<span id="8f085832"></span>
### Query string parameters

Not all shared request parameters are included in the following table. For a complete list, see [Shared request parameters](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967).


|**Parameter Name** |**Data Type** |**Required** |**Description** |
|---|---|---|---|
|Action |String |Yes |API operation. |
|Version |String |Yes |The version of this API operation. Current version: `2020-06-01`. |
|ActivityId |Integer |Yes |The ID of the live\-streaming activity. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/en/byteplus-livesaas/docs/listactivityapi). |
|PageNo |Integer |No |The page number to return. Default value: `1`. |
|PageItemCount |Integer |No |The number of results to return on each page. Default value: `10`. Value range: [1,50] |
|Source |Integer |No |Specifies the source of the data to return. Default value: `0`.<br><br>Valid values:<br><br><br>* `-1`: Returns data from all addresses.<br><br>* `0`: Returns data from the default address only.<br><br>* `1`: Returns data from address A only.<br><br>* `2`: Returns data from address B only.<br><br>* `3`: Returns data from address C only.<br><br>* `4`: Returns data from address D only. |


<span id="afcd3304"></span>
### Sample request

```JSON
Get http://livesaas.byteplusapi.com/?Action=ListQuestionnaireDataAPI&Version=2020-06-01&ActivityId=1231231231&Source=0
```


<span id="ec2412a8"></span>
## Response

<span id="c87420d8"></span>
### Response schema


|**Parameter Name** |**Data Type** |**Description** |
|---|---|---|
|PageItemCount |Integer |The number of results returned on each page. |
|PageNo |Integer |The page number of the returned results. |
|TotalItemCount |Integer |The total number of results returned. |
|StatisticsQuestionnaires |Array of [StatisticsQuestionnaires](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listquestionnairedataapi#StatisticsQuestionnaires) |Data of questionnaires. |


**StatisticsQuestionnaires**


|**Parameter Name** |**Data Type** |**Description** |
|---|---|---|
|QuestionnaireId |Integer |The ID of the questionnaire. |
|Title |String |The title of the questionnaire. |
|PublishTime |Integer |The publication time of the questionnaire, in Unix timestamp format. Unit: seconds. |
|UserCount |Integer |The number of respondents. |


<span id="ef841ad3"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "ListQuestionnaireDataAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1681983419
    },
    "Result": {
        "TotalItemCount": 1,
        "PageNo": 0,
        "PageItemCount": 0,
        "StatisticsQuestionnaires": [
            {
                "QuestionnaireId": 31402,
                "Title": "Title",
                "PublishTime": 1681982646,
                "UserCount": 2
            }
        ]
    }
}
```


<span id="d9fa6e91"></span>
## Error codes

For a list of common error codes, see [Shared error and status codes](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-error-and-status-codes).
