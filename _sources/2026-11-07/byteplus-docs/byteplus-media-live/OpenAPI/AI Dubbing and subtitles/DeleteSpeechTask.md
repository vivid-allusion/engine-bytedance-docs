---
title: "DeleteSpeechTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/DeleteSpeechTask"
---

Call the `DeleteSpeechTask` API to delete an AI Dubbing task that is no longer needed. If the task is running, MediaLive stops the task before deleting the task.

<span id="requirements"></span>
## Requirements

**Rate limit**: 10 requests per second per account.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=DeleteSpeechTask&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DeleteSpeechTask` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|TaskID |String |Yes |`497430****75c378` |The task ID. You can get the ID by calling [CreateSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateSpeechTask?lang=en) or [SearchSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/SearchSpeechTask). |
|WithRecord |Boolean |No |`true` |Whether to also delete the task record. Default value: `false`. Valid values:<br><br><br>* `true`: Deletes the record. After the record is deleted, the task can no longer be found by calling [SearchSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/SearchSpeechTask).<br><br>* `false`: Retains the record. |


<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Code |Integer |`0` |The status code. |
|Message |String |`success` |The status message. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=DeleteSpeechTask&Version=2023-01-01
{
    "TaskID": "497430****75c378",
    "WithRecord": true
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestID": "2025111417343916C47E772ECEBC0183DC",
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DeleteSpeechTask",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Code": 0,
        "Message": "success"
    }
}
```


<span id="error-codes"></span>
## Error codes

For more information about error codes, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).

&nbsp;
