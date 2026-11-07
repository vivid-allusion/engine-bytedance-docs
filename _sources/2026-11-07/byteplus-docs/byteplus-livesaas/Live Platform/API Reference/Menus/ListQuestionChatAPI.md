---
title: "ListQuestionChatAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/listquestionchatapi"
---

Call this API to get questions from the Q&A menu in a live room. The results can be sorted by the number of likes or by sent time, allowing you to retrieve the most popular or recent questions first. To get replies for a specific question, you can then use the question ID from the response to call the [ListAnswerChatAPI](https://docs.byteplus.com/ihay5kb0/7mknjxub)

<span id="fdea8512"></span>
## Requirements


* Quota: 120 queries per minute per account

* Prerequisite: A BytePlus account or an IAM user with Live control \> Edit permission. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).


<span id="79719cd3"></span>
## HTTP request


* URL: `https://livesaas.byteplusapi.com/?Action=ListQuestionChatAPI&Version=2020-06-01`

* Method: GET


<span id="c0f49424"></span>
## Request parameters

Not all shared request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="32f3e185"></span>
### Query


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ListQuestionChatAPI` |API operation. |
|Version |String |Yes |`2020-06-01` |The version of this API operation. Current version: `2020-06-01`. |
|ActivityId |Long |Yes |`17218312****` |The activity ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |
|PageNumber |Long |No |`1` |The number of the page to return. Default value: `1`. |
|PageSize |Long |No |`100` |The number of results to return on each page. Default value: `100`.<br><br>Value range: [1,1000]. |
|OrderType |Integer |No |`0` |Specifies whether the returned questions are sorted by the number of likes or by submission time.<br><br>Default value: `0`.<br><br>Valid values:<br><br><br>* `0`: Questions are sorted by sent time in reverse chronological order. The most recent questions will be returned first.<br><br>* `1`: Questions are sorted by the number of likes. The most popular questions will be returned first. |
|FilterPin |Integer |No |`0` |Specifies which questions to return.<br><br>Default value: `0`.<br><br>Valid values:<br><br><br>* `0`: All questions.<br><br>* `1`: The question pinned to the top of the menu for Q&A.<br><br>* `2`: Questions not pinned to the top of the menu for Q&A. |


<span id="78eacc9f"></span>
## Response parameters


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|PageNumber |Long |`1` |The page number of the returned page. |
|PageSize |Long |`100` |The number of results returned on each page. |
|TotalCount |Long |`1` |The total number of returned questions. |
|QuestionMsgs |Array of [QuestionMsg](https://docs.byteplus.com/docs/byteplus-livesaas/listquestionchatapi#e2930158) |`-` |The list of returned questions. |


<span id="e2930158"></span>
### QuestionMsg


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|QuestionMsgId |Long |`5941305` |The question ID. |
|UserNickName |String |`Viewer A` |The nickname of the user who sent the question. |
|UserExternalId |String |`12387404123****` |The unique identifier on third\-party platforms of the user who sent the question. Only a viewer who logs in to the live room using the following methods has such an ID. You can use this ID to identify the viewer within your organization for user insights and data analysis.<br><br>The ID varies based on how the viewer logs in to the live room.<br><br><br>* Custom account: The value passed through the `UserId` parameter during custom login. For more information, see [Custom authentication login](https://docs.byteplus.com/docs/byteplus-livesaas/docs-applying-advanced-viewing-restrictions).<br><br>* Phone number: The `passport_id` generated when the viewer registers BytePlus Live using a phone number.<br><br>* OAuth 2.0: The field corresponding to the user ID in your own account system.<br><br>* Allowlist: The allowlist verification information entered by the viewer. |
|CreateTime |Long |`1717145029` |The time when the question was sent in Unix timestamp format. Unit: seconds. |
|Content |String |`Question A` |The content of the question. |
|LikeCount |Long |`20` |The number of likes for the question. |
|IsPined |Integer |`0` |Indicates whether the question is pinned to the top of the Q&A menu.<br><br><br>* `0`: Not pinned to the top.<br><br>* `1`: Pinned to the top. |


<span id="8c70f7da"></span>
## Samples

<span id="bf1a2f5e"></span>
### Sample request

```JSON
GET https://livesaas.byteplusapi.com/?Action=ListQuestionChatAPI&Version=2020-06-01&ActivityId=17218312****&PageNumber=1&PageSize=100&OrderType=0&FilterPin=0
```


<span id="34c8cb31"></span>
### Sample response

```JSON
{
  "ResponseMetadata": {
    "RequestId": "201806041104200100100232280022D30",
    "Action": "ListQuestionChatAPI",
    "Version": "2020-06-01",
    "Service": "livesaas",
    "Region": "ap-singapore-1",
    "SystemTime": 1717593301
  },
    "Result": {
        "PageNumber": 1,
        "PageSize": 100,
        "TotalCount": 1,
        "QuestionMsgs": [
            {
                "QuestionMsgId": 5941305,
                "UserNickName": "Viewer A",
                "UserExternalId": "",
                "CreateTime": 1717145029,
                "Content": "Question A",
                "LikeCount": 20,
                "IsPined": 0
            }
        ]
    }
}
```


<span id="2b1e6a6a"></span>
## Error codes

For a list of shared error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).
