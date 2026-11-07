---
title: "CancelDirectEditTask"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-canceldirectedittask"
---

Call `CancelDirectEditTask` to cancel the asynchronous video editing task via `ReqId` parameter.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://vod.byteplusapi.com?Action=CancelDirectEditTask&Version=2025\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`CancelDirectEditTask` |The API action. For the current API, the value is `CancelDirectEditTask`. |
|Version |String |Yes |`2025-01-01` |The API version. For the current API, the value is `2025-01-01`. |


#{.custom\-md\-table\-5}#

<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|ReqId |String |Yes |`e070c***********5657debe7d6547` |Task ID. You can obtain it by calling the [SubmitDirectEditTaskAsync](https://docs.byteplus.com/en/docs/byteplus-vod/reference-submitdirectedittaskasync). |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Message |String |`success` |The successful canceling of the video editing task. |


#{.custom\-md\-table\-4}#

<span id="samples"></span>
## Samples

<span id="Sample request"></span>
### Sample request 1

```json
POST https://vod.byteplusapi.com?Action=CancelDirectEditTask&Version=2025-01-01
{
    "ReqId": "e070c***********5657debe7d6547"
}
```


<span id="Sample response"></span>
### Sample response 1

```json
{
    "ResponseMetadata": {
        "RequestId": "20251104110420****100232280022D31",
        "Action": "CancelDirectEditTask",
        "Version": "2025-01-01",
        "Service": "vod",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Message": "success"
    }
}
```


<span id="Sample-request-2"></span>
### Sample request 2

```json
POST https://vod.byteplusapi.com?Action=CancelDirectEditTask&Version=2025-01-01
{
    "ReqId": "e070c***********5657debe7d6547"
}
```


<span id="Sample-request-2"></span>
### Sample response 2

```json
{
    "ResponseMetadata": {
        "RequestId": "202511******************CC6CE95E",
        "Action": "CancelDirectEditTask",
        "Version": "2025-01-01",
        "Service": "vod",
        "Region": "ap-southeast-1",
        "Error": {
            "Code": "InvalidParameter.InvalidParam",
            "CodeN": 1010,
            "Message": "status error: task has been canceled"
        }
    }
}
```


<span id="error-codes"></span>
## Error codes

This operation does not have specific error codes. For more information, see the [shared error codes of BytePlus VOD](https://docs.byteplus.com/en/docs/byteplus-vod/reference-common-error-codes).

&nbsp;
