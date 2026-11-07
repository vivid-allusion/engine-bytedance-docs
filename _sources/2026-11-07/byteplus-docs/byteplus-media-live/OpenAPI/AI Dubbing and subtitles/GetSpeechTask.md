---
title: "GetSpeechTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/GetSpeechTask"
---

Call the `GetSpeechTask` API to query information about a specific AI Dubbing task.

<span id="requirements"></span>
## Requirements

**Rate limit**: 10 requests per second per account.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=GetSpeechTask&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`GetSpeechTask` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|TaskID |String |Yes |`497430****75c378` |The task ID. You can get the ID by calling [CreateSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateSpeechTask?lang=en) or [SearchSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/SearchSpeechTask). |


<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Code |Integer |`0` |The status code. |
|Message |String |`success` |The status message. |
|Data |Object of [Data](https://docs.byteplus.com/en/docs/24/117620#data) |`-` |The task information. |


<span id="data"></span>
### Data


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Name |String |`TaskA` |The task name. |
|Status |String |`done` |The task status. Valid values:<br><br><br>* `running`: Running.<br><br>* `done`: Ended.<br><br>* `prestop`: Stopping.<br><br>* `init`: Preparing.<br><br>* `prepare`: Starting. |
|TaskID |String |`497430****75c378` |The task ID. |
|CreatedAt |String |`2025-11-14T15:34:43+08:00` |The time when the task was created. The time is in RFC3339 format, uses UTC+8, and is accurate to seconds. |
|UpdatedAt |String |`2025-11-14T16:50:53+08:00` |The time when the task was updated. The time is in RFC3339 format, uses UTC+8, and is accurate to seconds. |
|StoppedAt |String |`2025-11-14T16:50:49+08:00` |The actual time when the task ended. The time is in RFC3339 format, uses UTC+8, and is accurate to seconds. |
|Rule |String |`{"Pipe":"mix","Delay":15,"Source":{"Url":"https://pull.example.com/live/cloud.flv"},"Output":{"Url":["rtmp://push.example.com/live/cloud?auth_key=1779891783-0-0-e1f5a2a****4b5fe21cb3efdc89af901"]},"Subtitle":{"Original":{"Border":{"W":1,"Color":"black@0.5"},"Font":"arial","FontColor":"white","Language":"zh"},"Translation":[{"Border":{"W":1,"Color":"black@0.5"},"Font":"arial","FontColor":"white","Language":"en"}]}}` |The task rule configuration. The value is a JSON string that contains the task type, pull stream URL, push stream URL, subtitle configuration, and other information. For details about the fields, see [CreateSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateSpeechTask). |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=GetSpeechTask&Version=2023-01-01
{
    "TaskID": "497430****75c378"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestID": "20251114171722145C604658CB14014261",
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetSpeechTask",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Code": 0,
        "Message": "success",
        "Data": {
            "Name": "TaskA",
            "Status": "done",
            "TaskID": "497430****75c378",
            "CreatedAt": "2025-11-14T15:34:43+08:00",
            "UpdatedAt": "2025-11-14T16:50:53+08:00",
            "StoppedAt": "2025-11-14T16:50:49+08:00",
            "Rule": "{\"Pipe\":\"mix\",\"Delay\":15,\"Source\":{\"Url\":\"https://pull.example.com/live/cloud.flv\"},\"Output\":{\"Url\":[\"rtmp://push.example.com/live/cloud?auth_key=1779891783-0-0-e1f5a2a****4b5fe21cb3efdc89af901\"]},\"Subtitle\":{\"Original\":{\"Border\":{\"W\":1,\"Color\":\"black@0.5\"},\"Font\":\"arial\",\"FontColor\":\"white\",\"Language\":\"zh\"},\"Translation\":[{\"Border\":{\"W\":1,\"Color\":\"black@0.5\"},\"Font\":\"arial\",\"FontColor\":\"white\",\"Language\":\"en\"}]}}"
        }
    }
}
```


<span id="error-codes"></span>
## Error codes

For more information about error codes, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).

&nbsp;
