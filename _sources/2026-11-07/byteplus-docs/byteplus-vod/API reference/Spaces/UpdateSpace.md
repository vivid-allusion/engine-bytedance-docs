---
title: "UpdateSpace"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-updatespace"
---

This interface is used to update the space description.

<span id="requirements"></span>
## Requirements

Prerequisite: [CreateSpace](https://docs.byteplus.com/en/docs/byteplus-vod/reference-createspace) has been completed.

<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=UpdateSpace&Version=2023\-01\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`UpdateSpace` |The API action. For the current API, the value is `UpdateSpace`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|SpaceName |String |Yes |`doc-test` |The VOD space name. You can call the [ListSpace](https://docs.byteplus.com/en/docs/byteplus-vod/reference-listspace) interface to obtain the names of all spaces under the current account. |
|Description |String |No |`example` |The updated description of the space. The length requirement is 0 to 140 characters. |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

This API only returns [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) in the response.

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=UpdateSpace&Version=2023-01-01&SpaceName=doc-test&Description=example
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "Action": "UpdateSpace",
        "Region": "ap-singapore-1",
        "Service": "vod",
        "Version": "2023-01-01",
        "RequestId": "20230604110420****100232280022D31"
    }
}
```


<span id="error-codes"></span>
## Error codes

The following are the error codes related to the current operation. For other error codes, see the [shared errors of BytePlus VOD](https://docs.byteplus.com/en/docs/byteplus-vod/reference-common-error-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|400 |InvalidParameter.InvalidSpaceName |\- |Invalid `SpaceName`. |


#{.custom\-md\-table\-4}#

&nbsp;
