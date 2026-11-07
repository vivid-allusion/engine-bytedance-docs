---
title: "CreateSnapshotPresetV2"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/createsnapshotpresetv2"
---

Adds the screenshot configuration to capture and save screenshots of the live stream when it falls within the effective range of the screenshot configuration.

<span id="usage-scenario"></span>
## Usage scenario

The screenshot configuration specifies the applicable live stream range based on `Vhost` and `App`. When the domain used by the live stream belongs to the configured `Vhost`, and the `AppName` field of the live stream matches the `App` configuration, the live stream will be captured and saved.

<span id="requirements"></span>
## Requirements


* Prerequisite: If you choose to store screenshot files in TOS, you must first activate the TOS service and contact [technical support](https://console.byteplus.com/workorder/create) for authorization.

* Billing: The live stream screenshots feature requires payment. For more information, see [Screenshot capturing](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-screenshot-capturing).

* Rate limit: 10 requests per second per account.

* Effectiveness: To apply changes to the screenshot configuration, whether adding, updating, or deleting, you need to push the stream again 3\-5 minutes after making the modifications.


<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=CreateSnapshotPresetV2&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`CreateSnapshotPresetV2` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Vhost |String |Yes |`push.example.com` |The domain namespace, which is the namespace to which the domain of the live stream address belongs. You can call [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) or visit the **Domains** page of the [BytePlus MediaLive console](https://console.byteplus.com/live/main/domain/list) to check the namespace to which the domain used by the live stream belongs. |
|App |String |Yes |`live` |The app name, which is the same as the value of the `AppName` field in the live stream address. The name must be 1\-30 characters in length, and can contain the following characters:<br><br><br>* Uppercase letters (A\-Z)<br><br>* Lowercase letters (a\-z)<br><br>* Numbers (0\-9)<br><br>* Underscores (_)<br><br>* Hyphens (\-)<br><br>* Periods (.) |
|Status |Integer |No |`1` |Whether the screenshot configuration takes effect. Default value: `1`. Valid values:<br><br><br>* `1`: Takes effect.<br><br>* `0`: Does not take effect. |
|SnapshotPresetConfig |Object of [SnapshotPresetConfig](https://docs.byteplus.com/en/docs/24/71703#snapshotpresetconfig) |Yes |`-` |Detailed parameters of the screenshot configuration. |


<span id="snapshotpresetconfig"></span>
### SnapshotPresetConfig


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|JpegParam |Object of [JpegParam](https://docs.byteplus.com/en/docs/24/71703#jpegparam) |No |`-` |Parameters for screenshots in JPEG format, set when enabling JPEG screenshots.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You must enable either JPEG or JPG screenshots, but not both.</div><br> |
|JpgParam |Object of [JpgParam](https://docs.byteplus.com/en/docs/24/71703#jpgparam) |No |`-` |Parameters for screenshots in JPG format, set when enabling JPG screenshots.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You must enable either JPEG or JPG screenshots, but not both.</div><br> |
|Interval |Integer |No |`10` |The interval time for screenshots, in seconds. Default value: `10`. The value must be a positive integer. |


<span id="jpegparam"></span>
### JpegParam


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Enable |Boolean |No |`true` |Whether to enable screenshots in the current format. Default value: `false`. Valid values:<br><br><br>* `true`: Enable.<br><br>* `false`: Disable. |
|TOSParam |Object of [TOSParam](https://docs.byteplus.com/en/docs/24/71703#tosparam) |No |`-` |Configuration for storing screenshots in TOS. |


<span id="jpgparam"></span>
### JpgParam


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Enable |Boolean |No |`false` |Whether to enable screenshots in the current format. Default value: `false`. Valid values:<br><br><br>* `true`: Enable.<br><br>* `false`: Disable. |
|TOSParam |Object of [TOSParam](https://docs.byteplus.com/en/docs/24/71703#tosparam) |No |`-` |Configuration for storing screenshots in TOS. |


<span id="tosparam"></span>
### TOSParam


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Enable |Boolean |No |`true` |Whether to use TOS for storage. Default value: `false`. Valid values:<br><br><br>* `true`: Use TOS.<br><br>* `false`: Does not use TOS. |
|Bucket |String |No |`live-test-tos-example` |The bucket for TOS storage. For example, if the storage path is `live-test-tos-example/live/liveapp`, the parameter value is `live-test-tos-example`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is required when using TOS storage.</div><br> |
|StorageDir |String |No |`live/liveapp` |The storage directory under the bucket for TOS storage. By default, the value is empty. For example, if the storage path is `live-test-tos-example/live/liveapp`, the parameter value is `live/liveapp`. |
|ExactObject |String |No |`{Domain}/{App}/{Stream}/{UnixTimestamp}` |Storage rule when the screenshot type is non\-overwrite. You can configure the rule in the format of {Domain}/{App}/{Stream}/{UnixTimestamp}. Supports the following characters:<br><br><br>* Lowercase letters (a\-z)<br><br>* Uppercase letters (A\-Z)<br><br>* Numbers (0\-9)<br><br>* Hyphen (\-)<br><br>* Exclamation point (!)<br><br>* Underscore (_)<br><br>* Period (.)<br><br>* Asterisk (\*)<br><br>* Placeholder<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You must pass in either <code>ExactObject</code> or <code>OverwriteObject</code>.</div><br> |
|OverwriteObject |String |No |`{Domain}/{App}/{Stream}` |Storage rule when the screenshot type is overwrite. You can configure the rule in the format of {Domain}/{App}/{Stream}. Supports the following characters:<br><br><br>* Lowercase letters (a\-z)<br><br>* Uppercase letters (A\-Z)<br><br>* Numbers (0\-9)<br><br>* Hyphen (\-)<br><br>* Exclamation point (!)<br><br>* Underscore (_)<br><br>* Period (.)<br><br>* Asterisk (\*)<br><br>* Placeholder<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You must pass in either <code>ExactObject</code> or <code>OverwriteObject</code>.</div><br> |


<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|PresetName |String |`preset-123` |The screenshot configuration name. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=CreateSnapshotPresetV2&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "App": "live",
    "Status": 1,
    "SnapshotPresetConfig": {
        "JpegParam": {
            "Enable": true,
            "TOSParam": {
                "Enable": true,
                "Bucket": "live-test-tos-example",
                "StorageDir": " live/liveapp",
                "ExactObject": "{Domain}/{App}/{Stream}/{UnixTimestamp}"
            }
        },
        "Interval": 10
    }
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateSnapshotPresetV2",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "PresetName": "preset-123"
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
|429 |RequestLimitExceeded.Exist |%s already exist |The resource you are requesting to create (including domain namespace, domain, app, configuration, and certificate) already exists. |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact technical support](https://console.byteplus.com/workorder/create). |
|500 |InternalError.Preset |an internal error related to preset occurred, please contact the administrator. |An internal error related to feature configuration occurred. Please [contact technical support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact technical support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact technical support](https://console.byteplus.com/workorder/create). |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |Internal service timeout. Please [contact technical support](https://console.byteplus.com/workorder/create). |


&nbsp;
