---
title: "ListVhostSnapshotPreset"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostsnapshotpreset-2023"
---

Call the `ListVhostSnapshotPreset` API to query all screenshot configurations under Vhost.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This API is no longer maintained. We recommend that you call <a href="https://docs.byteplus.com/en/docs/byteplus-media-live/listvhostsnapshotpresetv2">ListVhostSnapshotPresetV2</a> to get screenshot configuration information.</div>


<span id="requirements"></span>
## Requirements

Rate limit: 1 query per second per account.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=ListVhostSnapshotPreset&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ListVhostSnapshotPreset` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Vhost |String |Yes |`push.example.com` |The domain name space. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or visit the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to obtain the domain name space. |
|Type |String |No |`tos` |Storage type. Always set it to `tos`. |


<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|PresetList |Array of [PresetList](https://docs.byteplus.com/en/docs/24/27446#presetlist) |`-` |A list of screenshot configurations. |


<span id="presetlist"></span>
### PresetList


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Vhost |String |`push.example.com` |The domain name space. |
|App |String |`live` |The AppName field. |
|SlicePreset |Object of [SlicePreset](https://docs.byteplus.com/en/docs/24/27446#slicepreset) |`-` |The details of screenshot configuration. |


<span id="slicepreset"></span>
### SlicePreset


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Preset |String |`preset-123` |The name of the screenshot configuration. |
|Status |Integer |`1` |The effective status of the screenshot configuration, the values and their meanings are as follows.<br><br><br>* `1`: effective;<br><br>* `0`: not effective. |
|Interval |Integer |`3` |The interval time between screenshots, in seconds. The default value is `10`, and the valid range is positive integers. |
|Bucket |String |`live-test-tos-example` |The bucket of bucket TOS. |
|CallbackDetail |Object of [CallbackDetail](https://docs.byteplus.com/en/docs/24/27446#callbackdetail) | |Callback configuration. |


<span id="callbackdetail"></span>
### CallbackDetail


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|URL |String |`http` |The type of the callback address. You can only set it as "http", which means both HTTP and HTTPS are supported. |
|CallbackType |String |`https://example.com/api/callback` |Callback address. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=ListVhostSnapshotPreset&Version=2023-01-01
{
    "Vhost": "push.example.com"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "ListVhostSnapshotPreset",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "cn-north-1"
    },
    "Result": {
        "PresetList": [
            {
                "Vhost": "push.example.com",
                "App": "live",
                "SlicePreset": {
                    "Preset": "preset-123",
                    "Status": 1,
                    "Interval": 3,
                    "Bucket": "live-test-tos-example",
                    "CallbackDetail": []
                }
            }
        ]
    }
}
```


<span id="error-codes"></span>
## Error codes

The following are the error codes related to the current operation. For other error codes, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|200 |CommonErr |\- |Uncategorized error. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/27446#request-parameters) description for inspection. |
|400 |InvalidParam.BindError |Request parameter error, please check input data |The parameter failed validation. Please check if the data type is correct. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.AccountIDNotAllowed |this AccountID does not have permission to access the corresponding resource, please check the request parameters |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |The video live streaming service has not been enabled or the account is in arrears, resulting in an unavailable bill. Please check the service activation status and account arrears status. |
|404 |ResourceNotFound |\- |The resource (including domain name space, domain name, app name, configuration, and certificate) was not found. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError.Preset |an internal error related to preset occurred, please contact the administrator. |An internal error related to the preset occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |Internal Service is timeout. Please [contact support](https://console.byteplus.com/workorder/create). |


&nbsp;
