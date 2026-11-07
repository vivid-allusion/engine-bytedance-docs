---
title: "SearchSpeechTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/SearchSpeechTask"
---

Call the `SearchSpeechTask` API to search for AI Dubbing tasks that match specific conditions.

<span id="requirements"></span>
## Requirements

**Rate limit**: 10 requests per second per account.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=SearchSpeechTask&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`SearchSpeechTask` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|TaskStatus |Array of String |No |`["running", "init"]` |The task status. By default, tasks in all statuses are returned. Valid values:<br><br><br>* `running`: Running.<br><br>* `done`: Ended.<br><br>* `prestop`: Stopping.<br><br>* `init`: Preparing.<br><br>* `prepare`: Starting. |
|Name |String |No |`TaskA` |The task name. By default, all tasks are returned. The name must be 1 to 20 characters in length. Fuzzy search is not supported, and English letters are case\-sensitive. The name can contain the following characters:<br><br><br>* Digits (0\-9)<br><br>* Uppercase letters (A\-Z)<br><br>* Lowercase letters (a\-z)<br><br>* Chinese characters<br><br>* Underscores (_)<br><br>* Hyphens (\-) |
|CreateTimeSt |String |No |`2025-11-13 17:01:06` |Returns tasks created at or after this time. The time is in RFC3339 format, uses UTC+8, and is accurate to seconds. By default, all tasks are returned. |
|CreateTimeEd |String |No |`2025-11-14 15:34:43` |Returns tasks created at or before this time. The time is in RFC3339 format, uses UTC+8, and is accurate to seconds. By default, all tasks are returned. |
|Page |Integer |Yes |`1` |The page number to return. The value must be a positive integer. |
|PageSize |Integer |Yes |`10` |The number of results to return on each page. The value must be greater than `0`. |


<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Code |Integer |`0` |The status code. |
|Message |String |`success` |The status message. |
|Data |Object of [Data](https://docs.byteplus.com/en/docs/24/117619#data) |`-` |The task information. |


<span id="data"></span>
### Data


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Count |Integer |`1` |The total number of returned tasks. |
|Tasks |Array of [Tasks](https://docs.byteplus.com/en/docs/24/117619#tasks) |`-` |The task information. |


<span id="tasks"></span>
### Tasks


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Name |String |`TaskA` |The task name. |
|Status |String |`done` |The task status. Valid values:<br><br><br>* `running`: Running.<br><br>* `done`: Ended.<br><br>* `prestop`: Stopping.<br><br>* `init`: Preparing.<br><br>* `prepare`: Starting. |
|TaskID |String |`b71c61****24ae4f` |The task ID. |
|CreatedAt |String |`2025-11-14T15:34:43+08:00` |The time when the task started. The time is in RFC3339 format, uses UTC+8, and is accurate to seconds. |
|UpdatedAt |String |`2025-11-14T16:50:53+08:00` |The time when the task was updated. The time is in RFC3339 format, uses UTC+8, and is accurate to seconds. |
|StoppedAt |String |`2025-11-14T16:50:49+08:00` |The actual time when the task ended. The time is in RFC3339 format, uses UTC+8, and is accurate to seconds. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=SearchSpeechTask&Version=2023-01-01
{
    "TaskStatus": [
        "running",
        "init"
    ],
    "Name": "TaskA",
    "CreateTimeSt": "2025-11-13 17:01:06",
    "CreateTimeEd": "2025-11-14 15:34:43",
    "Page": 1,
    "PageSize": 10
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestID": "2025111417350416C47E772ECEBC01847B",
        "RequestId": "20230604110420****100232280022D31",
        "Action": "SearchSpeechTask",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Code": 0,
        "Message": "success",
        "Data": {
            "Count": 1,
            "Tasks": [
                {
                    "Name": "TaskA",
                    "Status": "done",
                    "TaskID": "b71c61****24ae4f",
                    "CreatedAt": "2025-11-14T15:34:43+08:00",
                    "UpdatedAt": "2025-11-14T16:50:53+08:00",
                    "StoppedAt": "2025-11-14T16:50:49+08:00"
                }
            ]
        }
    }
}
```


<span id="error-codes"></span>
## Error codes

For more information about error codes, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).

&nbsp;
