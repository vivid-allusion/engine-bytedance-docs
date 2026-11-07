---
title: "DeleteCarouselTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletecarouseltask"
---

Call the `DeleteCarouselTask` API to delete the specified carousel task. After the task is deleted, the system will stop playing all the carousel content of the task and release the relevant resources.

<span id="requirements"></span>
## Requirements


* Rate limit: 10 queries per second per account.

* Irrecoverable: After calling the `DeleteCarouselTask` interface, the task and its related resources will be released and cannot be recovered. Please operate with caution.

* Immediate stop: After the task is deleted, all ongoing carousel playback will stop immediately without waiting for the current playback to complete.


<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=DeleteCarouselTask&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DeleteCarouselTask` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|TaskID |String |Yes |`44c5da50318440*********2d62c910b8` |The ID of the carousel task to be deleted, which is the unique identifier of the task. It is returned when the `CreateCarouselTask` interface is called to create a carousel task. |


<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Data |String |`kill task [e1fb009334fc5b16] success,mesos id is [live_bff26015_000000000025852],rowsAffect [0]` |The operation result information of the deleted task, returning whether the task is successfully deleted and the relevant Mesos ID and the number of operation impact records. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=DeleteCarouselTask&Version=2023-01-01
{
    "TaskID": "44c5da50318440*********2d62c910b8"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestID": "202410301524025B4509E7E242BD12477C",
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DeleteCarouselTask",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Data": "kill task [e1fb009334fc5b16] success,mesos id is [live_bff26015_000000000025852],rowsAffect [0]"
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
