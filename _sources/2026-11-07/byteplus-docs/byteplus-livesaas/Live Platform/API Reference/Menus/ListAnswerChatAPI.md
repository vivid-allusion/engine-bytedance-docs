---
title: "ListAnswerChatAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/listanswerchatapi"
---

Call this API to get a list of answers and sort them by the number of likes or by sent time, returning the most popular or recent replies first.

<span id="b82ccfd8"></span>
## Requirements


* Quota: 120 queries per minute per account

* Prerequisites:

   * Call [ListQuestionChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/listquestionchatapi) to get the question ID.

   * You must have a BytePlus account or an IAM user with `Live control > Edit` permission. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).


<span id="6825fb68"></span>
## HTTP request


* URL: `https://livesaas.byteplusapi.com/?Action=ListAnswerChatAPI&Version=2020-06-01`

* Method: GET


<span id="d85f0706"></span>
## Request parameters

Not all shared request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="e1a6bb09"></span>
### Query


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ListAnswerChatAPI` |API operation. |
|Version |String |Yes |`2020-06-01` |The version of this API operation. Current version: `2020-06-01`. |
|ActivityId |Long |Yes |`17218312****` |The activity ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |
|QuestionMsgIds |Array of Long |Yes |`[5941305,5941306]` |The IDs of the questions for which you want to retrieve replies. You can get the ID by calling [ListQuestionChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/listquestionchatapi).<br><br>The array can contain at most 100 question IDs. |
|PageNumber |Long |No |`1` |The page number to return. Default value: `1`. |
|PageSize |Long |No |`100` |The number of results to return on each page. Default value: `100`.<br><br>Value range: [1,1000]. |
|OrderType |Integer |No |`1` |Specifies whether to sort replies by the number of likes or by creation time.<br><br>Default value: `0`.<br><br>Valid values:<br><br><br>* `0`: Replies are sorted by creation time in reverse chronological order. The most recent replies will be returned first for each question.<br><br>* `1`: Replies are sorted by the number of likes. The most popular replies will be returned first for each question. |
|FilterPin |Integer |No |`0` |Specifies the type of replies to return.<br><br>Default value: `0`.<br><br>Valid values:<br><br><br>* `0`: All replies.<br><br>* `1`: Returns only the reply pinned to the top of the question in the Q&A menu.<br><br>* `2`: Returns only replies that are not pinned to the top of the question in the Q&A menu. |


<span id="2eac1c31"></span>
## Response parameters


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|PageNumber |Long |`1` |The returned page number. |
|PageSize |Long |`100` |The number of results returned on each page. |
|TotalCount |Long |`3` |The total number of returned replies. |
|AnswerMsgMap |JSON Map |`-` |A map where each key is a question ID and the corresponding value is a list of its replies.<br><br><br>* `"Key"`: Long. The question ID.<br><br>* `"Value"`: Array of [AnswerMsg](https://docs.byteplus.com/docs/byteplus-livesaas/listanswerchatapi#82034406). The list of replies. |


<span id="82034406"></span>
### AnswerMsg


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|AnswerMsgId |Long |`5941311` |The reply ID. |
|UserNickName |String |`Viewer A` |The nickname of the user who replied to the question. |
|UserExternalId |String |`12387404123****` |The user's unique identifier from a third\-party platform. This ID is present only if the viewer logs in using one of the supported methods. You can use this ID to identify the viewer within your organization for user insights and data analysis.<br><br>The ID varies based on how the viewer logs in to the live room.<br><br><br>* Custom account: The value passed in the `UserId` parameter during a custom login. For more information, see [Custom authentication login](https://docs.byteplus.com/docs/byteplus-livesaas/docs-applying-advanced-viewing-restrictions).<br><br>* Phone number: The `passport_id` generated when the viewer registers for BytePlus Live using a phone number.<br><br>* OAuth 2.0: The field corresponding to the user ID in your own account system.<br><br>* Allowlist: The allowlist verification information entered by the viewer. |
|CreateTime |Long |`1717148059` |The time the reply was sent, in Unix timestamp format (seconds). |
|Content |String |`Reply A` |The content of the reply. |
|LikeCount |Long |`20` |The number of likes for the reply. |
|IsPined |Integer |`0` |Indicates whether the reply is pinned to the top of the question under the menu for Q&A.<br><br><br>* `0`: Not pinned to the top.<br><br>* `1`: Pinned to the top. |


<span id="e861fb28"></span>
## Samples

<span id="8057a437"></span>
### Sample request

```JSON
GET https://livesaas.byteplusapi.com/?Action=ListAnswerChatAPI&Version=2020-06-01&ActivityId=17218312****&QuestionMsgIds=5941305&QuestionMsgIds=5941306&PageNumber=1&PageSize=100&OrderType=1&FilterPin=0
```


<span id="3d8f9cde"></span>
### Sample response

```JSON
{
  "ResponseMetadata": {
    "RequestId": "201806041104200100100232280022D30",
    "Action": "ListAnswerChatAPI",
    "Version": "2020-06-01",
    "Service": "livesaas",
    "Region": "ap-singapore-1",
    "SystemTime": 1717593301
  },
    "Result": {
        "PageNumber": 1,
        "PageSize": 100,
        "TotalCount": 3,
        "AnswerMsgMap": {
            "5941305": [
                {
                    "AnswerMsgId": 5941311,
                    "UserNickName": "Viewer A",
                    "UserExternalId": "",
                    "CreateTime": 1717148059,
                    "Content": "Reply A",
                    "LikeCount": 20,
                    "IsPined": 0
                },
                {
                    "AnswerMsgId": 5941309,
                    "UserNickName": "Viewer B",
                    "UserExternalId": "",
                    "CreateTime": 1717145103,
                    "Content": "Reply B",
                    "LikeCount": 10,
                    "IsPined": 1
                }
            ],
            "5941306": [
                {
                    "AnswerMsgId": 5941308,
                    "UserNickName": "Viewer C",
                    "UserExternalId": "",
                    "CreateTime": 1717145064,
                    "Content": "Reply C",
                    "LikeCount": 15,
                    "IsPined": 0
                }
            ]
        }
    }
}
```


<span id="6ccfa3f6"></span>
## Error codes

For a list of shared error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).
