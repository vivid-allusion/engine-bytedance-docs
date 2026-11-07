---
title: "UpdateAwardItem"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/updateawarditem"
---

Call the `UpdateAwardItem` API to add a new prize to the prize library or update the name, stock, and other information of an existing prize.

<span id="usage-scenario"></span>
## Usage scenario

Using the `Id` parameter of this API, you can add new prizes to the prize library or update existing ones.


* **Add a new prize:**  Do not provide the `Id` in the request parameters, or set `Id` to 0. This will create a new prize.

* **Update an existing prize:**  Provide the prize ID of the item to be updated as the value of the `Id` parameter. You can obtain the prize ID by calling the `GetAwardItemList` API.


<span id="requirements"></span>
## Requirements


* Rate limit: 10 requests per second per account

* Prerequisite: A BytePlus account or an IAM user with **Media library** \> **Prize library** \> **Edit** permission. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).


<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://livesaas.byteplusapi.com/?Action=UpdateAwardItem&Version=2023\-08\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

Not all common request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`UpdateAwardItem` |API operation. |
|Version |String |Yes |`2023-08-01` |The version of this API operation. Current version: `2023-08-01`. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|AwardItem |Object of [AwardItem](https://docs.byteplus.com/en/docs/11/75356#awarditem) |Yes |`-` |Prize list in the prize library. |


<span id="awarditem"></span>
### AwardItem


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|AwardItemIcon |String |No |`https://www.example.com/test.png` |URL of the prize image, including the protocol. |
|AwardItemType |Integer |No |`1` |Prize type. Valid values are:<br><br><br>* `1`: Physical prize<br><br>* `2`: Virtual prize<br><br>* `3`: Custom prize<br><br>* `4`: Voucher prize<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is required when adding a new prize.</div><br> |
|AwardItemName |String |No |`Prize A` |Name of the prize.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is required when adding a new prize.</div><br> |
|Id |Long |No |`1715****1256` |Prize ID.<br><br><br>* **Add a new prize:**  Do not include this parameter, or set its value to `0`. The maximum number of prizes allowed in the prize library is 10,000.<br><br>* **Update prize information:**  Provide the prize ID of the item to be updated. You can obtain the ID by calling the [GetAwardItemList](https://docs.byteplus.com/en/docs/byteplus-livesaas/getawarditemlist) API. |
|AwardLotteryTicketAddr |String |No |`https://example.com` |Claim URL for voucher prizes. The length ranges from 1 to 256 characters.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is required and takes effect only when <code>AwardItemType</code> is set to 4.</div><br> |
|AwardItemStock |Long |No |`200` |Prize stock. The value range is [1, 100000]. A value of `-1` indicates unlimited stock.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is required when adding a new prize.</div><br> |
|AwardItemNum |String |No |`48151841` |Batch number for points prizes. The length ranges from 1 to 256 characters. You can use this batch number to identify company points and distribute them to viewers. |
|AwardItemAmounts |Long |No |`1` |Number of points each winning viewer receives. The value range is [0,99999].<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is required and takes effect only when <code>AwardItemType</code> is set to 3 and <code>DeliveryMethod</code> is set to 2.</div><br> |
|DeliveryMethod |Integer |No |`1` |Category of a custom prize. Values:<br><br><br>* `1`: Coupon<br><br>* `2`: Points<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is required and takes effect when <code>AwardItemType</code> is set to 3.</div><br> |
|WinnerInfoType |Array of Integer |No |`[1,2,3]` |Information types that winners of physical or virtual prizes need to provide. Values:<br><br><br>* `1`: Shipping address<br><br>* `2`: Phone number<br><br>* `3`: Recipient name<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is required and takes effect only when <code>AwardItemType</code> is set to <code>1</code> or <code>2</code>.</div><br><br><br><div data-tips="true" data-tips-type="tip">When <code>AwardItemType</code> is set to <code>2</code>, this parameter only supports the value <code>2</code>.</div><br> |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Status |Boolean |`true` |Whether the prize was successfully added or updated. Returns `true` if successful. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://livesaas.byteplusapi.com/?Action=UpdateAwardItem&Version=2023-08-01
{
    "AwardItem": {
        "AwardItemIcon": "https://www.example.com/test.png",
        "AwardItemType": 1,
        "AwardItemName": "Prize",
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
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UpdateAwardItem",
        "Version": "2023-08-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1697446406
    },
    "Result": {
        "Status": true
    }
}
```


<span id="error-codes"></span>
## Error codes

For a list of common error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).

&nbsp;
