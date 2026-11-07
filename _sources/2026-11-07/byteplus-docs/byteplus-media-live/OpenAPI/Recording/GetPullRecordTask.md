---
title: "GetPullRecordTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/GetPullRecordTask"
---

Call the `GetPullRecordTask` API to query the information of a single live recording task.

<span id="requirements"></span>
## Requirements

Rate limit: 50 queries per second per account.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=GetPullRecordTask&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`GetPullRecordTask` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|TaskID |String |Yes |`5b903f78c7f5ae*******01f6fe2eea` |Task ID, the unique identifier of the recording task. You can call [ListPullRecordTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpullrecordtask) API to obtain the task ID. |


<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|TaskDetail |Object of [TaskDetail](https://docs.byteplus.com/en/docs/24/48559#taskdetail) |`-` |Task details. |


<span id="taskdetail"></span>
### TaskDetail


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|TaskId |String |`5b903f78c7f5ae*******01f6fe2eea` |Task ID. |
|StartTime |String |`2023-10-09T15:16:15Z` |The start time of the task, UTC time in RFC3339 format, with a precision of seconds. |
|EndTime |String |`2023-10-09T15:18:28Z` |The end time of the task, in UTC time in RFC3339 format, with a precision of seconds. |
|Vhost |String |`example.com` |The domain namespace passed in when creating a recording task. |
|Domain |String |`pull.example.com` |The domain name passed in when creating a recording task. |
|App |String |`live` |The application name passed in when creating a recording task. |
|Status |String |`未开始` |The status of the recording task. Possible values are as follows.<br><br><br>* `停用`：The recording task has been stopped;<br><br>* `未开始`：The recording task has not started yet;<br><br>* `生效中`：The recording task is in progress;<br><br>* `已结束`：The recording has been completed. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=GetPullRecordTask&Version=2023-01-01
{
    "TaskID": "5b903f78c7f5ae*******01f6fe2eea"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetPullRecordTask",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "TaskDetail": {
            "TaskId": "5b903f78c7f5ae*******01f6fe2eea",
            "StartTime": "2023-10-09T15:16:15Z",
            "EndTime": "2023-10-09T15:18:28Z",
            "Vhost": "example.com",
            "Domain": "pull.example.com",
            "App": "live",
            "Status": "生效中"
        }
    }
}
```


<span id="error-codes"></span>
## Error codes

The following are the error codes related to the current operation. For other error codes, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|200 |CommonErr |\- |Unclassified error. It is recommended to retry. If this error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](#Request Parameters) description for inspection. |
|400 |InvalidParam.BindError |Request parameter error, please check input data |The parameter fails the verification. Please check if the parameter type is correct. |
|403 |RequestForbidden |\- |The request is rejected. There are no requested resources (domain space, domain name, application, configuration template, certificate) under the current account. |
|403 |RequestForbidden.AccountIDNotAllowed |this AccountID does not have permission to access the corresponding resource, please check the request parameters |The request is rejected. There are no requested resources (domain space, domain name, application, configuration template, certificate) under the current account. |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |The video live broadcast service is not activated or the account is in arrears, resulting in the unavailability of the bill. Please check the activation status of the service and the arrears situation of the account. |
|404 |ResourceNotFound |\- |The resource (domain namespace, domain name, application, configuration template, certificate) was not found. It is recommended to retry. If this error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred, please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |An error occurred between services, please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |An error occurred between services, please [contact support](https://console.byteplus.com/workorder/create). |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |Internal service timeout, please [contact support](https://console.byteplus.com/workorder/create). |


&nbsp;
