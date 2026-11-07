---
title: "DeleteAwardItem"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/deleteawarditem"
---

You can use this API to delete a specified prize from the prize library.

<span id="requirements"></span>
## Requirements


* Rate limit: 10 requests per second per account

* Prerequisite: A BytePlus account or an IAM user with **Media library** \> **Prize library** \> **Edit** permission. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).


<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://livesaas.byteplusapi.com/?Action=DeleteAwardItem&Version=2023\-08\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

Not all common request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DeleteAwardItem` |API operation. |
|Version |String |Yes |`2023-08-01` |The version of this API operation. Current version: `2023-08-01`. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Id |Long |Yes |`1715****1256` |Prize ID. You can obtain the ID by calling the [GetAwardItemList](https://docs.byteplus.com/en/docs/byteplus-livesaas/getawarditemlist) API. |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Status |Boolean |`true` |Whether the prize was successfully deleted. Returns `true` if successful. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://livesaas.byteplusapi.com/?Action=DeleteAwardItem&Version=2023-08-01
{
    "Id": 1715****1256
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DeleteAwardItem",
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
