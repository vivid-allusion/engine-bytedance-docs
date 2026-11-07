---
title: "GetDirectEditProgress"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-getdirecteditprogress"
---

Call `GetDirectEditProgress` to obtain the execution progress of an asynchronous video editing task through `ReqId` (task ID).

<span id="http-request"></span>
## HTTP request


* Method: GET

* Endpoint: https://vod.byteplusapi.com?Action=GetDirectEditProgress&Version=2025\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`GetDirectEditProgress` |The API action. For the current API, the value is `GetDirectEditProgress`. |
|Version |String |Yes |`2025-01-01` |The API version. For the current API, the value is `2025-01-01`. |
|ReqId |String |Yes |`3b5fece1a******0443a6aeea5f47` |The editing task ID. You can obtain it by calling the [SubmitDirectEditTaskAsync](https://docs.byteplus.com/en/docs/byteplus-vod/reference-submitdirectedittaskasync). |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Result |Integer |`1` |The video editing task progress. The value range is from 1 to 100, with the unit being %.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the progress repeatedly jumps between 1 and 100, you can call <a href="https://docs.byteplus.com/en/docs/byteplus-vod/reference-getdirecteditresult">GetDirectEditResult</a> to query the asynchronous editing task details.</div><br> |


#{.custom\-md\-table\-4}#

<span id="samples"></span>
## Samples

<span id="Sample request"></span>
### Sample request

```json
GET https://vod.byteplusapi.com?Action=GetDirectEditProgress&Version=2025-01-01&ReqId=3b5fece1a******0443a6aeea5f47
```


<span id="Sample response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetDirectEditProgress",
        "Version": "2025-01-01",
        "Service": "vod",
        "Region": "ap-southeast-1"
    },
    "Result": 1
}
```


<span id="error-codes"></span>
## Error codes

The following are the error codes related to the current operation. For other error codes, see the [shared errors of BytePlus VOD](https://docs.byteplus.com/en/docs/byteplus-vod/reference-common-error-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|500 |1000 |\- |Internal error. |
|500 |1001 |\- |The database write error. |
|400 |1010 |\- |Parameter error. |
|500 |1014 |\- |The downstream service error. |


#{.custom\-md\-table\-4}#

&nbsp;
