---
title: "DeleteWatermarkPreset"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletewatermarkpreset-2023"
---

Call the `DeleteWatermarkPreset` API to delete an existing watermark configuration.

<span id="requirements"></span>
## Requirements


* Rate limit: 1 query per second per account.

* Effective time: After you add, update, or delete a watermark configuration, the change takes effect in 3 to 5 minutes. Transcoded streams or ABR (adaptive bitrate) substreams generated after the change takes effect use the latest watermark configuration. Existing transcoded streams or ABR substreams generated before the change takes effect do not automatically apply the update. If no transcoded stream or ABR substream exists before the change, wait for the configuration to take effect. If a transcoded stream or ABR substream already exists before the change and you need to use the updated configuration, wait 3 to 5 minutes after the configuration is added, updated, or deleted, and then push the stream again.


<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=DeleteWatermarkPreset&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DeleteWatermarkPreset` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Vhost |String |Yes |`push.example.com` |The domain name space. You can call the [ListVhostWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostwatermarkpreset-2023) API to get the domain name space of the configuration with the `Vhost` parameter value. |
|App |String |Yes |`live` |The `AppName` field in the live stream URL. You can call the [ListVhostWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostwatermarkpreset-2023) API to get the `AppName` of the configuration with the `App` parameter value. |
|Stream |String |No |`example_stream` |The `StreamName` field in the live stream URL. You can call the [ListVhostWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostwatermarkpreset-2023) API to get the `StreamName` of the configuration with the `Stream` parameter value. |


<span id="response-parameters"></span>
## Response parameters

This API only returns [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/request-response) in the response.

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=DeleteWatermarkPreset&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "App": "live"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "DeleteWatermarkPreset",
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
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/27462#request-parameters) description for inspection. |
|400 |InvalidParam.BindError |Request parameter error, please check input data |The parameter failed validation. Please check if the data type is correct. |
|400 |InvalidParam.StillUsing |%s is still in use, can't delete |The resource specified in the error message is in use, which causes it to not be deleted. Please release the resource and try again. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.AccountIDNotAllowed |this AccountID does not have permission to access the corresponding resource, please check the request parameters |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |The video live streaming service has not been enabled or the account is in arrears, resulting in an unavailable bill. Please check the service activation status and account arrears status. |
|404 |ResourceNotFound |\- |The resource (including domain name space, domain name, app name, configuration, and certificate) was not found. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|404 |ResourceNotFound.PresetNotExist |preset not found |The configuration was not found. Please check if the passed\-in configuration is consistent with the created configuration. |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError.Preset |an internal error related to preset occurred, please contact the administrator. |An internal error related to the preset occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |Internal Service is timeout. Please [contact support](https://console.byteplus.com/workorder/create). |
