---
title: "ListCarouselTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listcarouseltask"
---

Call the `ListCarouselTask` API to obtain the list of all current carousel tasks, including task IDs, statuses, and creation times, which can be used for task management and batch queries.

<span id="requirements"></span>
## Requirements

Rate limit: 10 queries per second per account.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=ListCarouselTask&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ListCarouselTask` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Page |Integer |Yes |`1` |The page number of the queried data. |
|PageSize |Integer |Yes |`30` |The number of data items displayed per page, with a maximum value of 1000. |


<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Data |Object of [Data](https://docs.byteplus.com/en/docs/24/47074#data) |`-` |Carousel task data object. |


<span id="data"></span>
### Data


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Count |Integer |`29` |The total number of carousel tasks that meet the query conditions. |
|Result |Array of [Result](https://docs.byteplus.com/en/docs/24/47074#result) |`-` |The array of carousel tasks, where each element represents the detailed information of a task. |


<span id="result"></span>
### Result


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|CreatedAt |Object of [CreatedAt](https://docs.byteplus.com/en/docs/24/47074#createdat) |`{"Time":"2023-03-15T08:00:00+08:00"}` |The creation time of the task, a timestamp in RFC3339 format with a precision of seconds. |
|Name |String |`Carousel test` |Carousel task name. |
|Status |String |`running` |The current status of the carousel task. The values and meanings are as follows:<br><br><br>* `pending`: The task is waiting to be scheduled;<br><br>* `prepare`: The task is being initialized;<br><br>* `running`: The task is running;<br><br>* `prestop`: The task is being stopped;<br><br>* `done`: The task has been stopped. |
|StoppedAt |Object of [StoppedAt](https://docs.byteplus.com/en/docs/24/47074#stoppedat) |`{"Time":"2023-03-16T08:00:00+08:00"}` |The end time of the task, a timestamp in RFC3339 format with a precision of seconds. |
|TaskID |String |`e1fb009334fc5b16` |The unique identifier of the carousel task. |
|UpdatedAt |Object of [UpdatedAt](https://docs.byteplus.com/en/docs/24/47074#updatedat) |`{"Time":"2023-03-15T10:00:00+08:00"}` |The update time of the task, a timestamp in RFC3339 format, with a precision of seconds. |


<span id="createdat"></span>
### CreatedAt


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Time |String |`2024-10-30T15:25:07+08:00` |The creation time of the task, a timestamp in RFC3339 format with a precision of seconds. |


<span id="stoppedat"></span>
### StoppedAt


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Time |String |`0001-01-01T00:00:00Z` |The end time of the task, a timestamp in RFC3339 format with a precision of seconds. |


<span id="updatedat"></span>
### UpdatedAt


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Time |String |`2024-10-30T15:25:08+08:00` |The update time of the task, a timestamp in RFC3339 format with a precision of seconds. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=ListCarouselTask&Version=2023-01-01
{
    "Page": 1,
    "PageSize": 30
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestID": "202410301540353C34785110C816119A9E",
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListCarouselTask",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Data": {
            "Count": 29,
            "Result": [
                {
                    "CreatedAt": {
                        "Time": "2024-10-30T15:25:07+08:00"
                    },
                    "Name": "Carousel test",
                    "Status": "running",
                    "StoppedAt": {
                        "Time": "0001-01-01T00:00:00Z"
                    },
                    "TaskID": "e1fb009334fc5b16",
                    "UpdatedAt": {
                        "Time": "2024-10-30T15:25:08+08:00"
                    }
                }
            ]
        }
    }
}
```


<span id="error-codes"></span>
## Error codes

The following are the error codes related to the current operation. For other error codes, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](#Request Parameters) description for inspection. |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |


&nbsp;
