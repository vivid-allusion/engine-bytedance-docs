---
title: "GetCheckInListAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/GetCheckInListAPI"
---

Call the `GetCheckInListAPI` API to obtain all check\-in or specified check\-in information for the designated live room, including check\-in ID, number of participants, check\-in duration, and more.

<span id="Requirements"></span>
## Requirements


* Quota: 120 queries per minute per account.

* Prerequisite: A BytePlus account or an IAM user with **Insights** \> **View only** or **Edit** permission. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).


<span id="HTTP request"></span>
## HTTP request


* Method：GET

* Endpoint：https://livesaas.byteplusapi.com/?Action=GetCheckInListAPI&Version=2020\-06\-01


<span id="Request parameters"></span>
## Request parameters

<span id="Common parameters"></span>
### Common parameters

Not all common request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="Query"></span>
### Query


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`GetCheckInListAPI` |API operation. |
|Version |String |Yes |`2020-06-01` |The version of this API operation. Current version: `2020-06-01`. |
|ActivityId |Long |Yes |17218346\*\*\*\* |The activity ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |
|PageNo |Integer |No |1 |The number of the page to return. Default value: `1`. |
|PageCount |Integer |No |10 |The number of results to return on each page. Default value: `10`. |
|CheckInId |String |No |checkIn1754478641140736 |Check\-in ID. |


<span id="Response parameters"></span>
## Response parameters


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|CheckInList |Array of [CheckInList](https://docs.byteplus.com/docs/byteplus-livesaas/GetCheckInListAPI#checkinlist) |`-` |Check\-in information list. |
|PageNo |Integer |`1` |The page number of the returned results. |
|PageCount |Integer |`10` |The number of results to return on each page. |


<span id="checkinlist"></span>
### CheckInList


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|CheckInId |String |`checkIn1754478641140736` |Check\-in ID. |
|CheckInName |String |Start check\-in |Check\-in title. |
|CheckInCount |Integer |`0` |The number of participants in the check\-in. |
|Deadline |Long |`1` |The check\-in duration in minutes. |
|Status |String |`Deadline` |Check\-in status. Valid values are as follows:<br><br><br>* `Init`: Created<br><br>* `Export`: Sent<br><br>* `Deadline`: Ended<br><br>* `Delete`: Deleted<br><br>* `Retract`: Withdrawn |
|ActivityId |Long |`175450930238536` |Live room ID. |
|NeedPersonInfo |Integer |`0` |Indicates whether check\-in information is required. Valid values are as follows:<br><br><br>* `0`: Not required<br><br>* `1`: Required |
|OpenCheckTime |Integer |`1673202771` |The time when the check\-in ends (the deadline). This is a Unix timestamp measured in seconds. |
|CheckInInfo |String |Check in |Check\-in prompt text |
|StartTime |String |`1673202711` |Check\-in start time. Unix timestamp, measured in seconds. |
|IsSendComment |Integer |`1` |Indicates whether to send a comment after check\-in. Valid values are as follows:<br><br><br>* `0`: Do not send<br><br>* `1`: Send |
|CommentContent |String |#User nickname# has checked in |The content of the comment sent after check\-in.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter takes effect only when <code>IsSendComment</code> is set to <code>1</code></div><br> |
|DeadlineSecond |Integer |31 |The seconds component of the check\-in duration. |
|CannotWathcLiveWhenNotCheckIn |Integer |1 |Indicates whether an audience member who does not check in on time is removed from the live room. Valid values are as follows:<br><br><br>* `0`: Not removed.<br><br>* `1`: Removed. |
|SendType |Integer |1 |The check\-in sending method. Valid values are as follows:<br><br><br>* `0`: Send manually<br><br>* `1`: Send on schedule |
|AutoSendTime |Long |1723455354 |The time for scheduled sending. Unix timestamp, measured in seconds.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is valid only when <code>SendType</code> is set to <code>1</code>.</div><br> |
|CannotWatchLivePrompt |String |Viewing has been suspended due to prolonged failure to check in |The notification message sent to a user who is removed.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter takes effect only when <code>CannotWathcLiveWhenNotCheckIn</code> is set to <code>1</code>.</div><br> |


<span id="Samples"></span>
## Samples

<span id="Sample request"></span>
### Sample request

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetCheckInListAPI&Version=2020-06-01&ActivityId=17218346****&PageNo=1&PageCount=10&CheckInId=checkIn1754478641140736
```


<span id="Sample response"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetCheckInListAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1697446406
    },
    "Result": {
        "CheckInList": [
            {
                "CheckInId": "checkIn1754478641140736",
                "CheckInName": "Start check-in",
                "CheckInCount": 0,
                "Deadline": 1,
                "Status": "Deadline",
                "ActivityId": 175450930238****,
                "NeedPersonInfo": 0,
                "OpenCheckTime": 1673202771,
                "CheckInInfo": "Check in",
                "StartTime": "1673202711",
                "CommentContent": "#User nickname# has checked in",
                "IsSendComment": 1,
                "AutoSendTime": 1723455354,
                "CannotWathcLiveWhenNotCheckIn": 1,
                "DeadlineSecond": 31,
                "SendType": 1,
                "CannotWatchLivePrompt": "Viewing has been suspended due to prolonged failure to check in"
            }
        ],
        "PageNo": 1,
        "PageCount": 10
    }
}
```


<span id="Error codes"></span>
## Error codes

For a list of common error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).
