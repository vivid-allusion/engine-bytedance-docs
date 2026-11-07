---
title: "CreateSnapshotPreset"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createsnapshotpreset-2023"
---

Call the `CreateSnapshotPreset` API to create a screenshot configuration. The system will take screenshots of live streams that meet the conditions based on your screenshot configuration.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This API is no longer maintained. We recommend that you call <a href="https://docs.byteplus.com/en/docs/byteplus-media-live/createsnapshotpresetv2">CreateSnapshotPresetV2</a> to add the screenshot configuration.</div>


<span id="requirements"></span>
## Requirements


* Billing: For screenshot pricing, please refer to [Screenshot capturing](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-screenshot-capturing).

* Rate limit: 1 queries per second per account.

* Effective description: For adding, updating, and deleting screenshot configurations, you need to re\-push and pull the stream to apply the changes. The configuration will take effect within 3 to 5 minutes.


<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=CreateSnapshotPreset&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`CreateSnapshotPreset` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Vhost |String |Yes |`push.example.com` |The domain name space. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or visit the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to obtain the domain name space which the domain belongs. |
|App |String |Yes |`live` |The AppName field in the live stream URL. It can include uppercase letters (A\-Z), lowercase letters (a\-z), numbers (0\-9), underscores (_), hyphens (\-), and periods (.), with a length ranging from 1 to 30 characters. |
|Status |Integer |No |`1` |The effective status of the screenshot configuration, the values and their meanings are as follows.<br><br><br>* `1`: (default value) effective;<br><br>* `0`: not effective. |
|Interval |Integer |Yes |`300` |The interval time between screenshots, in seconds. The default value is `10`, and the valid range is positive integers. |
|Bucket |String |No |`live-test-tos-example` |The bucket of BytePlus TOS. |
|StorageDir |String |No |`live/liveapp` |Storage directory of the screenshots in the bucket. |
|SnapshotFormat |String |No |`jpeg` |Screenshot format, currently only jpeg is supported. |
|SnapshotObject |String |No |`{Domain}/{App}/{Stream}/{UnixTimestamp}` |Storage path. The default value is `{Domain}/{App}/{Stream}/{StartTime}_{EndTime}`.<br><br>You can delete fixed segments in the path, such as `{App}/{Stream}`. |
|CallbackDetailList |Array of [CallbackDetailList](https://docs.byteplus.com/en/docs/24/27437#callbackdetaillist) |No |`-` |Callback configuration.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can update the screenshot callback configuration by calling <a href="https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatecallback-2023">UpdateCallback</a> and this API. When calling these two interfaces repeatedly to update the screenshot callback address configuration, the address configuration of the last call will take effect.</div><br> |


<span id="callbackdetaillist"></span>
### CallbackDetailList


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|CallbackType |String |No |`http` |The type of the callback address. You can only set it as `"http"`, which means both HTTP and HTTPS are supported. |
|URL |String |No |`https://example.com/api/callback` |Callback address. |


<span id="response-parameters"></span>
## Response parameters

This API only returns [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/request-response) in the response.

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=CreateSnapshotPreset&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "App": "live",
    "Interval": 300,
    "Bucket": "bucket1",
    "StorageDir": "live/liveapp"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "CreateSnapshotPreset",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```


<span id="error-codes"></span>
## Error codes

The following are the error codes related to the current operation. For other error codes, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|200 |CommonErr |\- |Uncategorized error. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/27437#request-parameters) description for inspection. |
|400 |InvalidParam.BindError |Request parameter error, please check input data |The parameter failed validation. Please check if the data type is correct. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.AccountIDNotAllowed |this AccountID does not have permission to access the corresponding resource, please check the request parameters |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |The video live streaming service has not been enabled or the account is in arrears, resulting in an unavailable bill. Please check the service activation status and account arrears status. |
|404 |ResourceNotFound |\- |The resource (including domain name space, domain name, app name, configuration, and certificate) was not found. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|429 |RequestLimitExceeded.Exist |%s already exist |The resource (including domain name space, domain name, app name, configuration, certificate) requested to be created already exists. |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError.Preset |an internal error related to preset occurred, please contact the administrator. |An internal error related to the preset occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |Internal Service is timeout. Please [contact support](https://console.byteplus.com/workorder/create). |


&nbsp;
