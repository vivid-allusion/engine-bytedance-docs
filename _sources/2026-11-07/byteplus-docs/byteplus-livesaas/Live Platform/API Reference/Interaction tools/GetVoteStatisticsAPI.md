---
title: "GetVoteStatisticsAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/GetVoteStatisticsAPI"
---

Call `GetVoteStatisticsAPI` to get the voting data of a live room.

<span id="Requirements"></span>
## Requirements


* Quota: 120 queries per minute per account.

* Prerequisite: A BytePlus account or an IAM user with **Insights** \> **View only** or **Edit** permission. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).


<span id="HTTP request"></span>
## HTTP request


* Method：GET

* Endpoint：https://livesaas.byteplusapi.com/?Action=GetVoteStatisticsAPI&Version=2020\-06\-01


<span id="Request parameters"></span>
## Request parameters

<span id="Common parameters"></span>
### Common parameters

Not all common request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="Query"></span>
### Query


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`GetVoteStatisticsAPI` |API operation. |
|Version |String |Yes |`2020-06-01` |The version of this API operation. Current version: `2020-06-01`. |
|ActivityId |Long |Yes |17218346\*\*\*\* |The activity ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |
|PageNo |Integer |No |1 |The number of the page to return. Default value: `1`. |
|PageCount |Integer |No |10 |The number of results to return on each page. Default value: `10`. |
|VoteId |String |Yes |vote1754472505032763 |Vote ID. You can get the vote ID by calling the [GetVoteListAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/GetVoteListAPI). |


<span id="Response parameters"></span>
## Response parameters


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|PageNo |Integer |1 |The number of the page to return. |
|PageCount |Integer |10 |The number of results to return on each page. |
|TotalCount |Integer |1 |The total number of entries. |
|VoteStatisticsList |Array of [VoteStatisticsList](https://docs.byteplus.com/docs/byteplus-livesaas/GetVoteStatisticsAPI#votestatisticslist) |*  |List of voter information. |


<span id="votestatisticslist"></span>
### VoteStatisticsList


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|UserChose |Array of [UserChose](https://docs.byteplus.com/docs/byteplus-livesaas/GetVoteStatisticsAPI#userchose) |*  |The user's selected options. |
|UserName |String |Audience A |The nickname of the viewer. |
|IP |String |10.5.xx.xx |The IP address of the viewer. |
|VoteTime |Integer |1673169500 |The time of the vote, as a Unix timestamp. |
|Extra |String |abc |An additional parameter synchronized to BytePlus Live, which can be used to associate with the viewer. For example, you can synchronize the viewer's department from your own account system to BytePlus Live. |
|UserID |Long |1738686737584142 |The viewer's unique identifier in BytePlus Live.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If a viewer does not log in to the live room by entering a nickname or by other methods, their user ID is 0.</div><br> |
|UserTel |String |137xxxxx88 |The phone number of the viewer. |
|Email |String |zhibo@xxx.com |The email of the viewer. |
|UserAgent |String |Intel Mac OS X 10_15_7 |The user agent string of the viewer's device. |
|ExternalId |String |1605756488530014 |The viewer's unique identifier on third\-party platforms. Fuzzy search is supported.<br><br>The ID varies based on how the viewer logs in to the live room. For more information, see [Viewer behavior data](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-data-statistics#viewer-behavior-data). You can use this ID to identify the viewer within your organization, enabling user insights and data analysis as needed. |


<span id="userchose"></span>
### UserChose


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|OptionSite |String |D |The identifier of the selected option. |
|OptionName |String |Option content |The text of the selected option. |


<span id="Samples"></span>
## Samples

<span id="Sample request"></span>
### Sample request

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetVoteStatisticsAPI&Version=2020-06-01&ActivityId=17218346****&PageNo=1&PageCount=10&VoteId=vote1754472505032763
```


<span id="Sample response"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetVoteStatisticsAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1697446406
    },
    "Result": {
        "PageNo": 1,
        "PageCount": 10,
        "TotalCount": 1,
        "VoteStatisticsList": [
            {
                "UserChose": [
                    {
                        "OptionSite": "D",
                        "OptionName": "Option content"
                    }
                ],
                "UserName": "Audience A",
                "IP": "10.5.xx.xx",
                "VoteTime": 1673169500,
                "Extra": "abc",
                "UserID": 1738686737584142,
                "UserTel": "137xxxxx88",
                "Email": "zhibo@xxx.com",
                "UserAgent": "Intel Mac OS X 10_15_7",
                "ExternalId": "1605756488530014"
            }
        ]
    }
}
```


<span id="Error codes"></span>
## Error codes

For a list of common error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).
