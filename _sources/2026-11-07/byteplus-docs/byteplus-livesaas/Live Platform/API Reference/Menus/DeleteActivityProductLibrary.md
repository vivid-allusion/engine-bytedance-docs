---
title: "DeleteActivityProductLibrary"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/deleteactivityproductlibrary"
---

Deletes one or more product libraries in a specific live room.

<span id="requirements"></span>
## Requirements

Quota: 120 queries per minute per account

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://livesaas.byteplusapi.com/?Action=DeleteActivityProductLibrary&Version=2024\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

Not all common request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DeleteActivityProductLibrary` |API operation. |
|Version |String |Yes |`2024-01-01` |The version of this API operation. Current version: `2024-01-01`. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|ActivityId |Long |Yes |`1783981136301234` |The activity ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |
|ProductLibraryIds |Array of Long |Yes |`[789, 790]` |The IDs of the product libraries to be deleted. You can get the ID by calling [GetActivityProductCommonConfig](https://docs.byteplus.com/en/docs/byteplus-livesaas/getactivityproductcommonconfig). |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Status |Boolean |`true` |Indicates whether all of the specified product libraries are deleted. Returns `true` if they are. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://livesaas.byteplusapi.com/?Action=DeleteActivityProductLibrary&Version=2024-01-01
{
    "ActivityId": 1783981136301234,
    "ProductLibraryIds": [
        789,
        790
    ]
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DeleteActivityProductLibrary",
        "Version": "2024-01-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1656067132
    },
    "Result": {
        "Status": true
    }
}
```


<span id="error-codes"></span>
## Error codes

The following table lists error codes specific to this API operation. For a list of common error codes, see [Common error and status codes](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-shared-error-and-status-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|400 |InvalidParameter.ProductLibraryIdNotFound |The value of the ProductLibraryId parameter does not exist. |Make sure the ID belongs to an existing product library in the live room. |


&nbsp;
