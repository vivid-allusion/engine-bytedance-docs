---
title: "GetAwardItemList"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/getawarditemlist"
---

Call the `GetAwardItemList` API to retrieve the list of prizes in the current account’s prize library, including prize name, stock, images, and other information.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When calling this API with an IAM user, you can only get information of prizes that the IAM user can access or edit. For more information on how to configure the user range and classification range of IAM users, see <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles">Managing users, organizations, and roles</a>.</div>


<span id="requirements"></span>
## Requirements


* Rate limit: 10 requests per second per account

* Prerequisite: A BytePlus account or an IAM user with **Media library** \> **Prize library** \> **Edit** or **View only** permission. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).


<span id="http-request"></span>
## HTTP request


* Method: GET

* Endpoint: https://livesaas.byteplusapi.com/?Action=GetAwardItemList&Version=2023\-08\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

Not all common request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`GetAwardItemList` |API operation. |
|Version |String |Yes |`2023-08-01` |The version of this API operation. Current version: `2023-08-01`. |
|Name |String |No |`Prize A` |Prize name. Fuzzy search is supported and is case\-insensitive.<br><br>For example, if the parameter is set to **A**, prizes such as **Prize A** and **Prize abc** will be returned. |
|PageNumber |Integer |No |`1` |The number of the page to return. Default value: `1`. The value must be greater than or equal to 1. |
|PageSize |Integer |No |`200` |The number of results to return on each page. Default value: `200`. The value range is [1,1000]. |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|AwardItemList |Array of [AwardItemList](https://docs.byteplus.com/en/docs/11/75355#awarditemlist) |`-` |Prize list in the prize library. |
|TotalCount |Long |`1` |Total number of query results. |


<span id="awarditemlist"></span>
### AwardItemList


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|AwardItemIcon |String |`https://www.example.com/test.png` |URL of the prize image, including the protocol. |
|AwardItemType |Integer |`1` |Prize type. Valid values are:<br><br><br>* `1`: Physical prize<br><br>* `2`: Virtual prize<br><br>* `3`: Custom prize<br><br>* `4`: Voucher prize |
|AwardItemName |String |`Prize A` |Name of the prize. |
|Id |Long |`1715****1256` |Prize ID. After obtaining the prize ID, you can call the [UpdateAwardItem](https://docs.byteplus.com/en/docs/byteplus-livesaas/updateawarditem) API to update the prize information, or the [DeleteAwardItem](https://docs.byteplus.com/en/docs/byteplus-livesaas/deleteawarditem) API to delete the prize. |
|AwardLotteryTicketAddr |String |`https://example.com` |Claim URL for lottery ticket prizes. |
|AwardItemStock |Long |`200` |Prize stock. A value of `-1` indicates unlimited stock. |
|AwardItemNum |String |`48151841` |Batch number for points prizes. You can use this batch number to identify company points and distribute them to viewers. |
|AwardItemAmounts |Long |`1` |Number of points each winning viewer receives. Only valid when `DeliveryMethod` is 2. |
|DeliveryMethod |Integer |`1` |Category of a custom prize. Only valid when `AwardItemType` is 3. Values:<br><br><br>* `1`: Coupon<br><br>* `2`: Points |
|WinnerInfoType |Array of Integer |`[1,2,3]` |Information types that winners of physical or virtual prizes need to provide. Values:<br><br><br>* `1`: Shipping address<br><br>* `2`: Phone number<br><br>* `3`: Recipient name |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
GET https://livesaas.byteplusapi.com/?Action=GetAwardItemList&Version=2023-08-01&Name=Prize A&PageNumber=1&PageSize=200
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetAwardItemList",
        "Version": "2023-08-01",
        "Service": "livesaas",
        "Region": "cn-north-1",
        "SystemTime": 1697446406
    },
    "Result": {
        "AwardItemList": [
            {
                "AwardItemIcon": "https://www.example.com/test.png",
                "AwardItemType": 1,
                "AwardItemName": "Prize A",
                "Id": 1715****1256,
                "AwardLotteryTicketAddr": "https://example.com",
                "AwardItemStock": 200,
                "AwardItemNum": "48151841",
                "AwardItemAmounts": 1,
                "DeliveryMethod": 1,
                "WinnerInfoType": [
                    1,
                    2,
                    3
                ]
            }
        ],
        "TotalCount": 1
    }
}
```


<span id="error-codes"></span>
## Error codes

For a list of common error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).

&nbsp;
