---
title: "GetCheckInRecordStatisticsAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/GetCheckInRecordStatisticsAPI"
---

Call `GetCheckInRecordStatisticsAPI` to obtain the check\-in records for a specific live room.

<span id="Requirements"></span>
## Requirements


* Quota: 120 queries per minute per account.

* Prerequisite: A BytePlus account or an IAM user with **Insights** \> **View only** or **Edit** permission. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).


<span id="HTTP request"></span>
## HTTP request


* Method：GET

* Endpoint：https://livesaas.byteplusapi.com/?Action=GetCheckInRecordStatisticsAPI&Version=2020\-06\-01


<span id="Request parameters"></span>
## Request parameters

<span id="Common parameters"></span>
### Common parameters

Not all common request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="Query"></span>
### Query


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`GetCheckInRecordStatisticsAPI` |API operation. |
|Version |String |Yes |`2020-06-01` |The version of this API operation. Current version: `2020-06-01`. |
|ActivityId |Long |Yes |17218346\*\*\*\* |The activity ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |
|PageNo |Integer |No |1 |The number of the page to return. Default value: `1`. |
|PageItemCount |Integer |No |`10` |The number of results to return on each page. Default value: `10`. |
|CheckInId |String |Yes |`checkIn1754478641140752` |The check\-in ID of the live room. You can get the ID by calling GetCheckInListAPI. |


<span id="Response parameters"></span>
## Response parameters


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|CheckInStatisticsList |Array of [CheckInStatisticsList](https://docs.byteplus.com/docs/byteplus-livesaas/GetCheckInRecordStatisticsAPI#checkinstatisticslist) |`-` |A list of information for checked\-in audience members. |
|PageNo |Integer |1 |The number of the page to return. |
|PageItemCount |Integer |10 |The number of results to return on each page. |
|PageTotalCount |Integer |1 |Total number of query results. |


<span id="checkinstatisticslist"></span>
### CheckInStatisticsList


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|ActivityId |Long |17218346\*\*\*\* |The activity ID of the live room. |
|CheckInID |String |`checkIn1754478641140752` |Check\-in ID. |
|UserID |Long |173868673758\*\*\*\* |Audience ID. |
|UserName |String |`aa` |Audience nickname. |
|LoginTel |String |`158xxxx66` |The mobile number used by the audience to log in. |
|Email |String |zhibo@xxx.com |The email of the audience. |
|CheckInTime |Integer |`1673202796` |The check\-in time of the audience, Unix timestamp in seconds. |
|PersonInfo |String |`aa` |Audience check\-in information. |
|Extra |String |abc |An additional parameter synchronized to BytePlus Live that can be associated with a viewer. For example, you can synchronize the viewer's department from your own account system to BytePlus Live. |
|UserAgent |String |Intel Mac OS X 10_15_7 |The user agent string of the viewer's device. |
|Ip |String |192.0.2.1 |The IP address of the audience who checked in to the live room. |
|ExternalId |String |160575648853\*\*\*\* |The viewer's unique identifier on a third\-party platform. Fuzzy search is supported.<br><br>The ID varies based on how the viewer logs in to the live room. For more information, see [Viewer behavior data](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-data-statistics#viewer-behavior-data). You can use this ID to identify the viewer within your organization, enabling user insights and data analysis. |


<span id="Samples"></span>
## Samples

<span id="Sample request"></span>
### Sample request

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetCheckInRecordStatisticsAPI&Version=2020-06-01&ActivityId=17218346****&PageNo=1&PageItemCount=10&CheckInId=checkIn1754478641140752
```


<span id="Sample response"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetCheckInRecordStatisticsAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1697446406
    },
    "Result": {
        "CheckInStatisticsList": [
            {
                "ActivityId": 17218346****,
                "CheckInID": "checkIn1754478641140752",
                "UserID": 173868673758****,
                "UserName": "aa",
                "LoginTel": "158xxxx66",
                "Email": "zhibo@xxx.com",
                "CheckInTime": 1673202796,
                "PersonInfo": "aa",
                "Extra": "abc",
                "UserAgent": "Intel Mac OS X 10_15_7",
                "Ip": "192.0.2.1",
                "ExternalId": "160575648853****"
            }
        ],
        "PageNo": 1,
        "PageItemCount": 10,
        "PageTotalCount": 1
    }
}
```


<span id="Error codes"></span>
## Error codes

The following table lists error codes specific to this API operation. For a list of common error codes, see [Common error and status codes](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-shared-error-and-status-codes).


|**Status Code** |**Error Code** |**Error Message** |**Description** |
|---|---|---|---|
|400 |InvalidParameter.ActivityIDInvalid |The specified parameter ActivityID is invalid. |Invalid Live Room ID. Please enter a valid ID and try again. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |
|500 |InternalError |The request has failed due to an unknown error. |An unknown error occurred while processing the request. Contact technical support for assistance. |
