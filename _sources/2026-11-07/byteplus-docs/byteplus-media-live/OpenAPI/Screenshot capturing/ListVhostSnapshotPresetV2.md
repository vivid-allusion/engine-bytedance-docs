---
title: "ListVhostSnapshotPresetV2"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/listvhostsnapshotpresetv2"
---

Gets all screenshot configuration information under a specific domain namespace.

<span id="requirements"></span>
## Requirements

Rate limit: 10 requests per second per account.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=ListVhostSnapshotPresetV2&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ListVhostSnapshotPresetV2` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Vhost |String |Yes |`push.example.com` |The domain namespace, which is the namespace to which the domain of the live stream address belongs. You can call [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) or visit the **Domains** page of the [BytePlus MediaLive console](https://console.byteplus.com/live/main/domain/list) to check the namespace to which the domain used by the live stream belongs. |
|Type |String |No |`tos` |The storage location of the screenshot files in the screenshot configuration. By default, screenshot configurations are not filtered based on storage location. Currently, you can only set the value to `tos`, indicating storing screenshots in TOS. |


<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|PresetList |Array of [PresetList](https://docs.byteplus.com/en/docs/24/71706#presetlist) |`-` |Screenshot configuration list. |


<span id="presetlist"></span>
### PresetList


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Vhost |String |`push.example.com` |The domain namespace. |
|App |String |`live` |The app name. |
|SlicePresetV2 |Object of [SlicePresetV2](https://docs.byteplus.com/en/docs/24/71706#slicepresetv2) |`-` |The basic information of screenshot configuration. |


<span id="slicepresetv2"></span>
### SlicePresetV2


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|SnapshotPresetConfig |Object of [SnapshotPresetConfig](https://docs.byteplus.com/en/docs/24/71706#snapshotpresetconfig) |`-` |The detailed information of screenshot configuration. |
|Name |String |`preset-123` |The screenshot configuration name. |
|Status |Integer |`1` |Whether the screenshot configuration takes effect. Valid values:<br><br><br>* `1`: Takes effect.<br><br>* `0`: Does not take effect. |


<span id="snapshotpresetconfig"></span>
### SnapshotPresetConfig


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|JpegParam |Object of [JpegParam](https://docs.byteplus.com/en/docs/24/71706#jpegparam) |`-` |Parameters for screenshots in JPEG format. |
|JpgParam |Object of [JpgParam](https://docs.byteplus.com/en/docs/24/71706#jpgparam) |`-` |Parameters for screenshots in JPG format. |
|Interval |Integer |`10` |The interval time for screenshots, in seconds. |


<span id="jpegparam"></span>
### JpegParam


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Enable |Boolean |`true` |Whether screenshots in the current format are enabled. Valid values:<br><br><br>* `true`: Enabled.<br><br>* `false`: Disabled. |
|TOSParam |Object of [TOSParam](https://docs.byteplus.com/en/docs/24/71706#tosparam) |`-` |Configuration for storing screenshots in TOS. |


<span id="jpgparam"></span>
### JpgParam


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Enable |Boolean |`false` |Whether screenshots in the current format are enabled. Valid values:<br><br><br>* `true`: Enabled.<br><br>* `false`: Disabled. |
|TOSParam |Object of [TOSParam](https://docs.byteplus.com/en/docs/24/71706#tosparam) |`-` |Configuration for storing screenshots in TOS. |


<span id="tosparam"></span>
### TOSParam


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Enable |Boolean |`true` |Whether TOS storage is used. Valid values:<br><br><br>* `true`: Used.<br><br>* `false`: Not used. |
|Bucket |String |`live-test-tos-example` |The bucket for TOS storage. For example, if the storage path is `live-test-tos-example/live/liveapp`, the parameter value is `live-test-tos-example`. |
|StorageDir |String |`live/liveapp` |The storage directory under the bucket for TOS storage. For example, if the storage path is `live-test-tos-example/live/liveapp`, the parameter value is `live/liveapp`. |
|ExactObject |String |`{Domain}/{App}/{Stream}/{UnixTimestamp}` |Storage rule when the screenshot type is non\-overwrite. You can configure the rule in the format of {Domain}/{App}/{Stream}/{UnixTimestamp}. Supports the following characters:<br><br><br>* Lowercase letters (a\-z)<br><br>* Uppercase letters (A\-Z)<br><br>* Numbers (0\-9)<br><br>* Hyphen (\-)<br><br>* Exclamation point (!)<br><br>* Underscore (_)<br><br>* Period (.)<br><br>* Asterisk (\*)<br><br>* Placeholder |
|OverwriteObject |String |`{Domain}/{App}/{Stream}` |Storage rule when the screenshot type is overwrite. You can configure the rule in the format of {Domain}/{App}/{Stream}. Supports the following characters:<br><br><br>* Lowercase letters (a\-z)<br><br>* Uppercase letters (A\-Z)<br><br>* Numbers (0\-9)<br><br>* Hyphen (\-)<br><br>* Exclamation point (!)<br><br>* Underscore (_)<br><br>* Period (.)<br><br>* Asterisk (\*)<br><br>* Placeholder |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=ListVhostSnapshotPresetV2&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "Type": "tos"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListVhostSnapshotPresetV2",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "PresetList": [
            {
                "Vhost": "push.example.com",
                "App": "live",
                "SlicePreset": {
                    "SnapshotPresetConfig": {
                        "JpegParam": {
                            "Enable": true,
                            "TOSParam": {
                                "Enable": true,
                                "Bucket": "live-test-tos-example",
                                "StorageDir": "live/liveapp",
                                "ExactObject": "{Domain}/{App}/{Stream}/{UnixTimestamp}"
                            }
                        },
                        "Interval": 10
                    },
                    "Name": "preset-123",
                    "Status": "1"
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
|200 |CommonErr |\- |Uncategorized error. It is recommended to retry. If the error code is still returned, please [contact technical support](https://console.byteplus.com/workorder/create). |
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the request parameters description for inspection. |
|400 |InvalidParam.BindError |Request parameter error, please check input data |The parameter failed validation. Please check if the data type is correct. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain namespace, domain, app, configuration, and certificate). |
|403 |RequestForbidden.AccountIDNotAllowed |this AccountID does not have permission to access the corresponding resource, please check the request parameters |The request is rejected because there are no requested resources under the current account (resources include domain namespace, domain, app, configuration, and certificate). |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |The BytePlus MediaLive service has not been activated or the account is in arrears, resulting in an unavailable bill. Please check the service activation status and account arrears status. |
|404 |ResourceNotFound |\- |The resource (including domain namespace, domain, app, configuration, and certificate) was not found. It is recommended to retry. If the error code is still returned, please [contact technical support](https://console.byteplus.com/workorder/create). |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact technical support](https://console.byteplus.com/workorder/create). |
|500 |InternalError.Preset |an internal error related to preset occurred, please contact the administrator. |An internal error related to feature configuration occurred. Please [contact technical support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact technical support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact technical support](https://console.byteplus.com/workorder/create). |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |Internal service timeout. Please [contact technical support](https://console.byteplus.com/workorder/create). |


&nbsp;
