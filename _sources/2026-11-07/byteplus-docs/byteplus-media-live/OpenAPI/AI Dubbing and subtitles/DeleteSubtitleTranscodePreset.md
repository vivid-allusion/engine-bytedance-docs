---
title: "DeleteSubtitleTranscodePreset"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletesubtitletranscodepreset-2023"
---

Call the `DeleteSubtitleTranscodePreset` API to delete the added subtitle configuration.

<span id="requirements"></span>
## Requirements


* **Rate limit**: 10 requests per second per account.

* **Activation time**: After you add, edit, or delete a subtitle configuration, you must wait 3 to 5 minutes and restart stream pushing for the change to take effect.


<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=DeleteSubtitleTranscodePreset&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DeleteSubtitleTranscodePreset` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Vhost |String |Yes |`push.example.com` |The domain name space. You can call the [ListVhostSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostsubtitletranscodepreset-2023) API to obtain the `Vhost` value of the subtitle configuration to delete. |
|App |String |Yes |`live` |The `AppName`. You can call the [ListVhostSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostsubtitletranscodepreset-2023) API to obtain the `App` value of the subtitle configuration to delete. |
|PresetName |String |Yes |`OriginPreset` |The name of the subtitle configuration. You can call the [ListVhostSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostsubtitletranscodepreset-2023) API to get the `PresetName` value of the subtitle configuration to delete. |


<span id="response-parameters"></span>
## Response parameters

This API only returns [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/request-response) in the response.

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=DeleteSubtitleTranscodePreset&Version=2023-01-01
{
    "App": "live",
    "Vhost": "push.example.com",
    "PresetName": "OriginPreset"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DeleteSubtitleTranscodePreset",
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
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/28043#request-parameters) description for inspection. |
|400 |InvalidParam.BindError |Request parameter error, please check input data |The parameter failed validation. Please check if the data type is correct. |
|400 |InvalidParam.StillUsing |%s is still in use, can't delete |The resource specified in the error message is in use, which causes it to not be deleted. Please release the resource and try again. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.AccountIDNotAllow |this AccountID does not have permission to access the corresponding resource, please check the request parameters |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |The video live streaming service has not been enabled or the account is in arrears, resulting in an unavailable bill. Please check the service activation status and account arrears status. |
|404 |ResourceNotFound |\- |The resource (including domain name space, domain name, app name, configuration, and certificate) was not found. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError.Preset |an internal error related to preset occurred, please contact the administrator. |An internal error related to the preset occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |Internal service timed out. Please [contact support](https://console.byteplus.com/workorder/create). |


&nbsp;
