---
title: "DeleteTranscodePresetBatch"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/DeleteTranscodePresetBatch-2023"
---

Call the `DeleteTranscodePresetBatch` API to batch delete the transcoding configurations of ABR sub\-streams.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=DeleteTranscodePresetBatch&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DeleteTranscodePresetBatch` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Type |String |Yes |`hls-abr` |Select the protocol type of the ABR configurations to delete. Valid values:<br><br><br>* `hls-abr`: HLS\-ABR<br><br>* `dash-abr`: DASH\-ABR<br><br>* `rtm-abr`: RTM\-ABR<br><br>* `abr`: HLS\-ABR and DASH\-ABR<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When deleting ABR configurations that were created with multiple protocol types enabled, use the following <code>Type</code> values:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Use <code>hls-abr</code> for configurations with HLS\-ABR and RTM\-ABR enabled.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Use <code>dash-abr</code> for configurations with DASH\-ABR and RTM\-ABR enabled.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Use <code>abr</code> for configurations with HLS\-ABR, DASH\-ABR, and RTM\-ABR enabled.</div><br> |
|PresetList |Array of [PresetList](https://docs.byteplus.com/en/docs/24/35784#presetlist) |Yes |`-` |To delete the ABR sub\-stream transcoding configuration information, you can call [ListVhostTransCodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhosttranscodepreset_1) to view the transcoding configurations of the ABR type that need to be deleted. |


<span id="presetlist"></span>
### PresetList


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Preset |String |Yes |`asdq12ed` |Delete the Preset value in the configuration. |
|Vhost |String |Yes |`push.example.com` |The Vhost value in the configuration to be deleted. |
|App |String |Yes |`live` |Delete the value of App in the configuration. |


<span id="response-parameters"></span>
## Response parameters

This API only returns [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/request-response) in the response.

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=DeleteTranscodePresetBatch&Version=2023-01-01
{
    "Type": "hls-abr",
    "PresetList": [
        {
            "Vhost": "push.example.com",
            "App": "live",
            "Preset": "asdq12ed"
        },
        {
            "Vhost": "push.example.com",
            "App": "live",
            "Preset": "d2asda2e"
        }
    ]
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DeleteTranscodePresetBatch",
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
|200 |CommonErr |\- |Uncategorized error. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980). |
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/35784#request-parameters)) description for inspection. |
|400 |InvalidParam.BindError |Request parameter error, please check input data |The parameter failed validation. Please check if the data type is correct. |
|400 |InvalidParam.StillUsing |%s is still in use, can't delete |The parameter exceeds the allowable range. Please check if the value of the specified parameter in the error message exceeds the value range. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.AccountIDNotAllow |this AccountID does not have permission to access the corresponding resource, please check the request parameters |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |The video live streaming service has not been enabled or the account is in arrears, resulting in an unavailable bill. Please check the service activation status and account arrears status. |
|404 |ResourceNotFound |\- |The resource (including domain name space, domain name, app name, configuration, and certificate) was not found. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980). |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980). |
|500 |InternalError.Preset |an internal error related to preset occurred, please contact the administrator. |An internal error related to the service or bill occurred. Please [contact support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980). |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980). |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980). |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |Internal Service is timeout. Please [contact support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980). |


&nbsp;
