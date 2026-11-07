---
title: "ListAwardRecordStatisticsAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/ListAwardRecordStatisticsAPI"
---

Call the `ListAwardRecordStatisticsAPI` API to obtain the list of participating or winning viewers for a specific lucky draw in a live streaming room.

<span id="Requirements"></span>
## Requirements


* Rate limit: 10 requests per second per account

* Prerequisite: A BytePlus account or an IAM user with **Insights** \> **View only** or **Edit** permission. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).


<span id="HTTP request"></span>
## HTTP request


* Method：GET

* Endpoint：https://livesaas.byteplusapi.com/?Action=ListAwardRecordStatisticsAPI&Version=2023\-08\-01


<span id="Request parameters"></span>
## Request parameters

<span id="Common parameters"></span>
### Common parameters

Not all common request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="Query"></span>
### Query


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`ListAwardRecordStatisticsAPI` |API operation. |
|Version |String |Yes |`2023-08-01` |The version of this API operation. Current version: `2023-08-01`. |
|ActivityId |Long |Yes |1798615803\*\*\*\* |The activity ID of the live room. You can get the ID by calling [ListAwardConfigs](https://docs.byteplus.com/docs/byteplus-livesaas/ListAwardConfigs). |
|SearchType |Integer |No |1 |Viewer list type. The following values are supported, and the default value is `0`.<br><br><br>* `0`: Participating viewer list<br><br>* `1`: Winning viewer list |
|AwardId |Long |Yes |1621615169 |Lucky draw ID. You can query the ID by calling [ListAwardConfigs](https://docs.byteplus.com/en/docs/byteplus-livesaas/ListAwardConfigs). |
|PageNo |Integer |No |1 |The number of the page to return. Default value: `1`. |
|PageItemCount |Integer |No |10 |The number of results to return on each page. Default value: `10`. The value range is [1, 500]. |


<span id="Response parameters"></span>
## Response parameters


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|AwardRecords |Array of [AwardRecords](https://docs.byteplus.com/docs/byteplus-livesaas/ListAwardRecordStatisticsAPI#awardrecords) |*  |List of viewer information. |
|PageNo |Integer |1 |The page number of the returned results. |
|PageItemCount |Integer |10 |The number of results to return on each page. |
|PageTotalCount |Integer |1 |Total number of query results. |


<span id="awardrecords"></span>
### AwardRecords


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|ActivityId |Integer |17218346\*\*\*\* |The activity ID of the live room. |
|AwardId |Long |1621615169 |Lucky draw ID. |
|UserId |String |1753988749\*\*\*\* |The user ID. |
|UserName |String |Audience A |The nickname of the user. |
|LoginTel |String |158xxxx66 |The mobile number used by the viewer to log in. |
|AwardAddress |String |Beijing |Recipient's address. |
|AwardResult |Integer |4 |The viewer's lucky draw result. The following values are supported:<br><br><br>* `4`: Won the lucky draw<br><br>* `5`: Did not win the lucky draw |
|NotifyResult |Integer |1 |Indicates whether the viewer has been notified of the lucky draw result. Supported values are as follows:<br><br><br>* `1`: Not notified<br><br>* `2`: Notified |
|ExternalId |String |160575648853\*\*\*\* |The viewer's unique identifier on a third\-party platform. Fuzzy search is supported.<br><br>The ID varies based on how the viewer logs in to the live room. For more information, see [Viewer behavior data](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-data-statistics#viewer-behavior-data). You can use this ID to identify the viewer within your organization, enabling user insights and data analysis. |
|AwardName |String |lucky draw event |Lucky draw name. |
|ReceiverName |String |Li |Recipient's name. |
|ReceiverTel |String |157xxxx66 |Recipient's mobile phone number. |
|Email |String |zhibo@xxx.com |The email address provided by the viewer during account registration. |
|OpenAwardTime |Integer |1673199158 |The time the lucky draw results were announced, as a Unix timestamp measured in seconds. |
|Extra |String |abc |An additional parameter synchronized to BytePlus Live that can be associated with a viewer. For example, you can synchronize the viewer's department from your own account system to BytePlus Live. |
|UserAgent |String |Intel Mac OS X 10_15_7 |The user agent string of the viewer's device. |
|Ip |String |192.0.2.1 |The IP address of the viewer. |
|IsPriorityUser |Integer |1 |Whether the user is prioritized for winning. Valid values are as follows:<br><br><br>* `0`: No<br><br>* `1`: Yes |


<span id="Samples"></span>
## Samples

<span id="Sample request"></span>
### Sample request

```JSON
GET https://livesaas.byteplusapi.com/?Action=ListAwardRecordStatisticsAPI&Version=2023-08-01&ActivityId=1798615803****&SearchType=1&AwardId=1621615169&PageNo=1&PageItemCount=10
```


<span id="Sample response"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListAwardRecordStatisticsAPI",
        "Version": "2023-08-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1697446406
    },
    "Result": {
        "PageNo": 1,
        "PageItemCount": 10,
        "PageTotalCount": 1,
        "AwardRecords": [
            {
                "ActivityId": 17218346,
                "UserName": "Audience A",
                "LoginTel": "158xxxx66",
                "AwardAddress": "Beijing",
                "AwardResult": 4,
                "NotifyResult": 1,
                "ExternalId": "160575648853****",
                "AwardName": "lucky draw event",
                "ReceiverName": "Li",
                "ReceiverTel": "157xxxx66",
                "Email": "zhibo@xxx.com",
                "OpenAwardTime": 1673199158,
                "Extra": "abc",
                "UserAgent": "Intel Mac OS X 10_15_7",
                "Ip": "192.0.2.1",
                "IsPriorityUser": 1,
                "AwardId": 1621615169,
                "UserId": "1753988749****"
            }
        ]
    }
}
```


<span id="Error codes"></span>
## Error codes

For a list of common error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).
