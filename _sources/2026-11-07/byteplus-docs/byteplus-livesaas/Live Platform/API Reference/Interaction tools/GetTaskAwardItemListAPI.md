---
title: "GetTaskAwardItemListAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/GetTaskAwardItemListAPI"
---

Get the list of prizes for the watch time\-based lucky draw that has been sent in the live room.

<span id="Requirements"></span>
## Requirements


* Quota: 120 queries per minute per account.

* Prerequisite: A BytePlus account or an IAM user with **Insights** \> **View only** or **Edit** permission. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).


<span id="HTTP request"></span>
## HTTP request


* Method：GET

* Endpoint：https://livesaas.byteplusapi.com/?Action=GetTaskAwardItemListAPI&Version=2020\-06\-01


<span id="Request parameters"></span>
## Request parameters

<span id="Common parameters"></span>
### Common parameters

Not all common request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="Query"></span>
### Query


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`GetTaskAwardItemListAPI` |API operation. |
|Version |String |Yes |`2020-06-01` |The version of this API operation. Current version: `2020-06-01`. |
|ActivityId |Long |Yes |1798615803\*\*\*\* |The activity ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |
|PageNo |Integer |No |1 |The page number of the returned results. Default value: `1`. |
|PageItemCount |Integer |No |10 |The number of results to return on each page. Default value: `10`. |


<span id="Response parameters"></span>
## Response parameters


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|TaskAwardItemList |Array of [TaskAwardItemList](https://docs.byteplus.com/docs/byteplus-livesaas/GetTaskAwardItemListAPI#taskawarditemlist) |None |A list of prize information for the watch time\-based lucky draw. |
|PageNo |Integer |1 |The page number of the returned results. |
|PageItemCount |Integer |10 |The number of results to return on each page. |
|PageTotalCount |Integer |1 |Total number of query results. |


<span id="taskawarditemlist"></span>
### TaskAwardItemList


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|TaskAwardItemId |String |8480 |The prize ID for the watch time\-based lucky draw. |
|AwardItemType |Integer |4 |Prize type. Valid values are as follows:<br><br><br>* `1`: Physical prize<br><br>* `2`: Virtual prize<br><br>* `3`: Custom prize<br><br>* `4`: Voucher prize |
|PeopleCount |Integer |1 |Number of participants. |
|AwardCount |Integer |1 |The number of winners. |
|AwardItemName |String |Physical prizes |Prize name. |
|AwardLotteryTicketAddr |String |https://example.com |Claim URL for voucher prizes. The length ranges from 1 to 256 characters.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is required and takes effect only when <code>AwardItemType</code> is set to 4.</div><br> |
|AwardStartTime |Long |1689570360 |The start time of the watch time\-based lucky draw. A Unix timestamp in seconds. |
|AwardEndTime |Long |1689656640 |The end time of the watch time\-based lucky draw. A Unix timestamp in seconds. |
|AwardItemNum |String |48151841 |Batch number for points prizes. The length ranges from 1 to 256 characters. You can use this batch number to identify company points and distribute them to viewers. |
|AwardItemAmounts |Integer |1 |Number of points each winning viewer receives. The value range is [0,99999].<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is required and takes effect only when <code>AwardItemType</code> is set to 3.</div><br> |
|TaskAwardIcon |String |//example\-image.image |The URL of the prize icon, without the protocol header. |


<span id="Samples"></span>
## Samples

<span id="Sample request"></span>
### Sample request

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetTaskAwardItemListAPI&Version=2020-06-01&ActivityId=1798615803****&PageNo=1&PageItemCount=10
```


<span id="Sample response"></span>
### Sample response

```JSON
{
  "ResponseMetadata": {
    "RequestId": "202301112319419CCB1169F45D1CD7A49F",
    "Action": "GetTaskAwardItemListAPI",
    "Version": "2020-06-01",
    "Service": "livesaas",
    "Region": "cn-north-1",
    "SystemTime": 1673450381
  },
  "Result": {
    "PageNo": 1,
    "PageItemCount": 10,
    "PageTotalCount": 1,
    "TaskAwardItemList": [
      {
        "TaskAwardItemId": "8480",
        "AwardItemType": 1,
        "PeopleCount": 1,
        "AwardCount": 0,
        "AwardItemName": "Prize A",
        "AwardLotteryTicketAddr": "",
        "AwardItemNum": "",
        "AwardItemAmounts": 0,
        "TaskAwardIcon": "//example.com/path/to/image.png",
        "AwardStartTime": 1689570360,
        "AwardEndTime": 1689656640
      }
    ]
  }
}
```


<span id="Error codes"></span>
## Error codes

For a list of common error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).
