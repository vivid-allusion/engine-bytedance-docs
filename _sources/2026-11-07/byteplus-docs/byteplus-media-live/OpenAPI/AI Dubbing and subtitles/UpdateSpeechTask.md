---
title: "UpdateSpeechTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/UpdateSpeechTask"
---

Call the `UpdateSpeechTask` API to update the feature switch status of an AI Dubbing task. This API is commonly used to turn translation on or off as needed during a live stream.

<span id="requirements"></span>
## Requirements


* **Rate limit**: 10 requests per second per account.

* **Billing**: AI Dubbing tasks are billed based on the **actual stream push duration** of the task. For more information, see [AI Dubbing billing](https://docs.byteplus.com/en/docs/byteplus-media-live/ai_dubbing).


<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=UpdateSpeechTask&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`UpdateSpeechTask` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|TaskID |String |Yes |`497430****75c378` |The task ID. You can get the ID by calling [CreateSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateSpeechTask?lang=en) or [SearchSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/SearchSpeechTask). |
|Switch |String |Yes |`AllDisable` |The switch status. Valid values:<br><br><br>* `AllDisable`: Disables all features in the current mode.<br><br>* `AllEnable`: Enables all features that were enabled in the current mode when the AI Dubbing task was created by calling [CreateSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateSpeechTask).<br><br>   For example, in a live stream for English speakers, you can set this parameter to `AllEnable` only when a non\-English speaker is speaking, so translated content is output. At other times, set this parameter to `AllDisable` so the original content is output without AI Dubbing processing.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Changing this parameter value does not interrupt the task. The task continues to be billed.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When this parameter is set to <code>AllDisable</code>, the original sound volume configuration also becomes ineffective.</div><br> |


<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Code |Integer |`0` |The status code. |
|Message |String |`success` |The status message. |
|Data |Object of [Data](https://docs.byteplus.com/en/docs/24/117621#data) |`-` |The task information. |


<span id="data"></span>
### Data


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|OptID |Integer |`2` |The task update sequence number. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=UpdateSpeechTask&Version=2023-01-01
{
    "TaskID": "497430****75c378",
    "Switch": "AllDisable"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestID": "20251117142336C37E6DC6C26C2529018E",
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UpdateSpeechTask",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Code": 0,
        "Message": "success",
        "Data": {
            "OptID": 2
        }
    }
}
```


<span id="error-codes"></span>
## Error codes

For more information about error codes, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).

&nbsp;
