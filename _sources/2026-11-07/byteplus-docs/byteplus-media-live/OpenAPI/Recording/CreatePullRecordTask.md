---
title: "CreatePullRecordTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/CreatePullRecordTask"
---

Call the `CreatePullRecordTask` API to create a live pull stream recording task that starts and ends at a specified time. After successful creation, a single live stream of any duration can be recorded during the live broadcast and saved as a video file.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If calling this API to create a recording task fails and you have confirmed that the request parameters are valid, check whether the recording configuration for the current <code>AppName</code> (the value of the <code>App</code> request parameter) was created before the end of December 2025. If so, you can call <a href="https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deleterecordpreset-2023">DeleteRecordPreset</a> to delete the recording configuration for this <code>AppName</code>, and then call <a href="https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createrecordpresetv2-2023">CreateRecordPresetV2</a> to recreate the recording configuration for the same <code>AppName</code>. Alternatively, contact <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980">technical support</a> for help.</div>


<span id="usage-scenario"></span>
## Usage scenario

By calling this API, you can record the specified pull stream address `StreamURL` according to the configured recording start time `StartTime` and end time `EndTime`. The recording rules of this task are consistent with the associated recording configuration. The recording task and the recording configuration are associated through the `Domain` and `App` parameters. Therefore, the `Vhost`, `Domain`, and `App` of the live recording task need to be within the effective range of the recording configuration. For example, if you need to create a recording task with `"Vhost":"live.example.com"`, `"Domain":"live.example.push.com"`, and `"App":"live"`; then when calling [CreateRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createrecordpresetv2-2023) to add a recording configuration, the value of `Vhost` should be `live.example.com`, and the value of `App` should be `live` or `*`.

<span id="requirements"></span>
## Requirements


* Usage Limitations: For the same stream, you can only create a new recording task after the previous one has ended.

* Stream Interruption Policy: If the stream is interrupted for more than 120 seconds, the recording task will stop immediately. If the interruption lasts 120 seconds or less, recording will continue based on the rules defined in the [recording configuration](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createrecordpresetv2-2023).

* Rate limit: 50 queries per second per account.

* Prerequisites: Before starting a recording task, you must configure the recording settings for the corresponding `Vhost`, `Domain`, and `App`. See [CreateRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createrecordpresetv2-2023) for details.


<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=CreatePullRecordTask&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`CreatePullRecordTask` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Vhost |String |No |`push.example.com` |Domain space. You can call the [ListVhostRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023) API to view the `Vhost` value of the recording configuration to be used. |
|Domain |String |Yes |`push.example.com` |The push domain name or pull domain name used by the live stream. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or visit the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to obtain the domain name. |
|App |String |Yes |`Live` |The application name, that is, the value of the `AppName` field of the live stream address, supports a combination of uppercase and lowercase letters (A\-Z, a\-z), numbers (0\-9), underscores (_), hyphens (\-), and periods (.), with a length of 1 to 30 characters. |
|Stream |String |Yes |`example_stream` |The stream name, that is, the value of the `StreamName` field in the live stream address, supports being composed of uppercase and lowercase letters (A \- Z, a \- z), digits (0 \- 9), letters, underscores (_), hyphens (\-), and periods (.), with a length of 1 to 100 characters. |
|StreamURL |String |Yes |`http://example.push.com/Live/example_stream.flv` |The pull stream address of the live stream to be recorded.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Currently, only the pull stream address in FLV format is supported.</div><br> |
|StartTime |String |No |`2023-06-30T15:04:05Z` |Specify the start time of the recording task. The timestamp is in RFC3339 format with a precision of seconds. The default is empty, indicating immediate start. |
|EndTime |String |No |`2023-06-30T15:05:05Z` |Specify the end time of the recording task, a timestamp in RFC3339 format with a precision of seconds. The default value is empty, indicating that the recording will continue until the end of the live stream. |


<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|TaskId |String |`f831f3b0********1aa4dcf7621` |Task ID, the unique identifier of the recording task. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=CreatePullRecordTask&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "Domain": "push.example.com",
    "App": "Live",
    "Stream": "example_stream",
    "StreamURL": "http://example.push.com/Live/example_stream.flv",
    "StartTime": "2023-06-30T15:04:05Z",
    "EndTime": "2023-06-30T15:05:05Z"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreatePullRecordTask",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "TaskId": "f831f3b0123412341aa4dcf7621"
    }
}
```


<span id="error-codes"></span>
## Error codes

The following are the error codes related to the current operation. For other error codes, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|200 |CommonErr |\- |Unclassified error. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](#Request Parameters) description for inspection. |
|400 |InvalidParam.BindError |Request parameter error, please check input data |The parameters failed to pass the verification. Please check whether the parameter types are correct. |
|403 |RequestForbidden |\- |The request is rejected. There are no requested resources (domain name space, domain name, application, configuration template, certificate) under the current account. |
|403 |RequestForbidden.AccountIDNotAllow |this AccountID does not have permission to access the corresponding resource, please check the request parameters |The request is rejected. There are no requested resources (domain name space, domain name, application, configuration template, certificate) under the current account. |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |The video live broadcast service is not activated or the account is in arrears, resulting in the unavailability of the bill. Please check the service activation status and the account arrears status. |
|404 |ResourceNotFound |\- |The resource (domain space, domain name, application, configuration template, certificate) was not found. It is recommended to retry. If this error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|429 |RequestLimitExceeded |\- |The resources (domain namespace, domain name, application, configuration template, certificate) created by the request exceed the limit. |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error has occurred, please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |There is an error between services, please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |An error occurred between services, please [contact support](https://console.byteplus.com/workorder/create). |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |Internal service timeout, please [contact support](https://console.byteplus.com/workorder/create). |


&nbsp;
