---
title: "ListWatermarkPreset"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listwatermarkpreset-2023"
---

Call the `ListWatermarkPreset` API to query information about a watermark configuration.

<span id="requirements"></span>
## Requirements

Rate limit: 5 queries per minute per account.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=ListWatermarkPreset&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ListWatermarkPreset` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Vhost |String |Yes |`push.example.com` |The domain name space. You can call the [ListVhostWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostwatermarkpreset-2023) API to get the domain name space of the configuration with the `Vhost` parameter value. |
|App |String |Yes |`live` |The `AppName` field in the live stream URL. You can call the [ListVhostWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostwatermarkpreset-2023) API to get the `AppName` of the configuration with the `App` parameter value. |
|Stream |String |No |`example_stream` |The `StreamName` field in the live stream URL. You can call the [ListVhostWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostwatermarkpreset-2023) API to get the `StreamName` of the configuration with the `Stream` parameter value.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Leave this parameter empty to query configurations for all streams under the specified <code>AppName</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Specify a stream name to query the configuration for that stream under the specified <code>AppName</code>.</div><br> |


<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Preset |Object of [Preset](https://docs.byteplus.com/en/docs/24/27464#preset) |`-` |The watermark configuration. |


<span id="preset"></span>
### Preset


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|ID |Integer |`1****67` |The watermark template ID. |
|AccountID |String |`****1` |The BytePlus account ID. |
|Vhost |String |`push.example.com` |The domain name space. |
|App |String |`example_app` |The `AppName`. |
|Stream |String |`test-stream` |The `StreamName`. |
|Picture |String |`data:image/png;base64,iVBORw0KGg****mCC` |The encoded watermark image string. |
|PictureKey |String |`testtesttest.png` |The watermark image file name. |
|Orientation |String |`vertical` |Orientation of the watermarked video. Valid values:<br><br><br>* `vertical`: Portrait.<br><br>* `horizontal`: Landscape. |
|PosX |Float |`1.0` |Horizontal offset, which indicates the distance between the left edge of the watermark and the left edge of the transcoded stream or ABR (adaptive bitrate) substream image. A relative ratio is used. Valid range: [0,1].<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter has a value only when <code>WatermarkMode</code> is set to <code>static</code>.</div><br> |
|PosY |Float |`1.0` |Vertical offset, which indicates the distance between the top edge of the watermark and the top edge of the transcoded stream or ABR substream image. A relative ratio is used. Valid range: [0,1].<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter has a value only when <code>WatermarkMode</code> is set to <code>static</code>.</div><br> |
|RelativeWidth |Float |`1.0` |The relative watermark width, which is the ratio of the watermark width to the transcoded stream or ABR substream image width. Valid range: [0,1]. The watermark height scales proportionally with the width. |
|WatermarkMode |String |`dynamic` |The watermark type. Valid values:<br><br><br>* `static`: Static watermark. The watermark is fixed at the specified position.<br><br>* `dynamic`: Dynamic watermark. The watermark moves during playback, which increases the difficulty of unauthorized screen recording and misuse. |
|DynamicMode |String |`dynamic_move_curve` |The dynamic watermark effect. Valid values:<br><br><br>* `dynamic_move_curve`: Dynamic curve movement. The watermark moves continuously and changes direction when it reaches the video edges.<br><br>* `dynamic_blink`: Dynamic blinking. The watermark appears at a new random position in the video at the specified frequency.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter has a value only when <code>WatermarkMode</code> is set to <code>dynamic</code>.</div><br> |
|TransSuffixs |String |`_hd,_uhd` |The transcoded stream or ABR substream suffixes to which the watermark configuration applies. Suffixes are separated by commas (,). |
|DynamicSpeedLevel |Integer |`1` |The dynamic speed. Valid values are integers from 1 to 10. A larger value indicates faster changes.<br><br><br>* When `DynamicMode` is set to `dynamic_move_curve`, this speed controls the movement speed of the watermark.<br><br>* When `DynamicMode` is set to `dynamic_blink`, this speed controls the frequency at which the watermark changes position.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter has a value only when <code>WatermarkMode</code> is set to <code>dynamic</code>.</div><br> |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=ListWatermarkPreset&Version=2023-01-01
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
        "Action": "ListWatermarkPreset",
        "Region": "ap-singapore-1",
        "Service": "live",
        "Version": "2023-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Preset": {
            "App": "example_app",
            "Orientation": "vertical",
            "Picture": "data:image/png;base64,iVBORw0KGg****mCC",
            "RelativeWidth": 1.0,
            "AccountID": "****1",
            "PictureKey": "testtesttest.png",
            "ID": 1****67,
            "Vhost": "push.example.com",
            "Stream": "test-stream",
            "WatermarkMode": "dynamic",
            "DynamicMode": "dynamic_move_curve",
            "TransSuffixs": "_hd,_uhd",
            "DynamicSpeedLevel": 1
        }
    }
}
```


<span id="error-codes"></span>
## Error codes

The following are the error codes related to the current operation. For other error codes, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|200 |CommonErr |\- |Uncategorized error. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/27464#request-parameters) description for inspection. |
|400 |InvalidParam.BindError |Request parameter error, please check input data |The parameter failed validation. Please check if the data type is correct. |
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
