---
title: "GetVoteListAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/GetVoteListAPI"
---

Call `GetVoteListAPI` to obtain the vote configuration information for a specified live room.

<span id="Requirements"></span>
## Requirements


* Quota: 120 queries per minute per account.

* Prerequisite: A BytePlus account or an IAM user with **Insights** \> **View only** or **Edit** permission. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).


<span id="HTTP request"></span>
## HTTP request


* Method：GET

* Endpoint：https://livesaas.byteplusapi.com/?Action=GetVoteListAPI&Version=2020\-06\-01


<span id="Request parameters"></span>
## Request parameters

<span id="Common parameters"></span>
### Common parameters

Not all common request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="Query"></span>
### Query


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`GetVoteListAPI` |API operation. |
|Version |String |Yes |`2020-06-01` |The version of this API operation. Current version: `2020-06-01`. |
|ActivityId |Long |Yes |17218346\*\*\*\* |The activity ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |
|PageNo |Integer |No |`1` |The number of the page to return. Default value: `1`. |
|PageCount |Integer |No |`10` |The number of results to return on each page. Default value: `10`. |


<span id="Response parameters"></span>
## Response parameters


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|PageNo |Integer |`1` |The number of the page to return. |
|PageCount |Integer |`10` |The number of results to return on each page. |
|VoteList |Array of [VoteList](https://docs.byteplus.com/docs/byteplus-livesaas/GetVoteListAPI#votelist) |`-` |A list of vote configurations for the live room. |


<span id="votelist"></span>
### VoteList


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|VoteId |String |`vote1779514244272189` |Vote ID. |
|Title |String |Vote |Vote title. |
|TotalCount |Integer |`1` |Number of participants. |
|ChoiceType |String |`Single` |Vote type. Values are as follows:<br><br><br>* `Single`: Single choice<br><br>* `Multiple`: Multiple choice |
|Deadline |Integer |`1697166317` |Vote deadline. Unix timestamp, in seconds. |
|Status |String |`Export` |Vote status. Values are as follows:<br><br><br>* `Init`: Created<br><br>* `Export`: Sent<br><br>* `Deadline`: Ended<br><br>* `Delete`: Deleted |
|ActivityId |Long |17218346\*\*\*\* |The activity ID of the live room. |


<span id="Samples"></span>
## Samples

<span id="Sample request"></span>
### Sample request

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetVoteListAPI&Version=2020-06-01&ActivityId=17218346****&PageNo=1&PageCount=10
```


<span id="Sample response"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetVoteListAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1697446406
    },
    "Result": {
        "PageNo": 1,
        "PageCount": 10,
        "VoteList": [
            {
                "VoteId": "vote1779514244272189",
                "Title": "Vote",
                "TotalCount": 1,
                "ChoiceType": "Single",
                "Deadline": 1697166317,
                "Status": "Export",
                "ActivityId": 17218346****
            }
        ]
    }
}
```


<span id="Error codes"></span>
## Error codes

For a list of common error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).
