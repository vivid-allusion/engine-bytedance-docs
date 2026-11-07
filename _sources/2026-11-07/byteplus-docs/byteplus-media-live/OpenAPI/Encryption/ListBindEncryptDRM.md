---
title: "ListBindEncryptDRM"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecertdrm_4"
---

Invoke the `ListBindEncryptDRM` interface to query the encryption configuration for a specified domain namespace and application name, or to view all encryption configurations under a specified domain namespace.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=ListBindEncryptDRM&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ListBindEncryptDRM` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Vhost |String |Yes |`push.example.com` |The domain name space. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or visit the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to obtain the domain name space which the domain belongs. |
|App |String |No |`live` |The AppName field in the live stream URL. It can include uppercase letters (A\-Z), lowercase letters (a\-z), numbers (0\-9), underscores (_), hyphens (\-), and periods (.), with a length ranging from 1 to 30 characters. If unspecified, it means to query all configuration in all domain name spaces. |


<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|DRMBindingList |Array of [DRMBindingList](https://docs.byteplus.com/en/docs/24/7697#drmbindinglist) |`-` |DRM Encryption Configuration List. |


<span id="drmbindinglist"></span>
### DRMBindingList


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Vhost |String |`push.example.com` |The domain name space. |
|App |String |`live` |The AppName field. |
|DRMSystems |Array of String |`["FairPlay","Widevine"]` |Encryption Type, the supported values and their meanings are as follows.<br><br><br>* `FairPlay`: Commercial DRM encryption using FairPlay technology;<br><br>* `Widevine`: Commercial DRM encryption using Widevine technology;<br><br>* `PlayReady`: Commercial DRM encryption using PlayReady technology;<br><br>* `ClearKey`: HLS standard encryption.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">DRM encryption and HLS standard encryption cannot be configured at the same time.</div><br> |
|EncryptOriginStream |Boolean |`true` |Whether to enable source streaming encryption, the values and their meanings are as follows.<br><br><br>* `true`: Enabled;<br><br>* `false`: Not enabled. |
|EncryptTranscodeStream |Boolean |`true` |Whether to enable transcoding stream encryption, the values and their meanings are as follows.<br><br><br>* `true`: Enabled;<br><br>* `false`: Not enabled. |
|EncryptTranscodeSuffix |Array of String |`["_hd"]` |When enabling transcoding stream encryption, configure the suffix of the transcoding stream to be encrypted. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=ListBindEncryptDRM&Version=2023-01-01
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
        "RequestId": "202306041104200100100232280022D31",
        "Action": "ListBindEncryptDRM",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "cn-north-1"
    },
    "Result": {
        "DRMBindingList": [
            {
                "Vhost": "push.example.com",
                "App": "live",
                "AccountID": "1000000002",
                "Enable": true,
                "EncryptTranscodeSuffix": [
                    "_hd"
                ]
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
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/7697#request-parameters) description for inspection. |
|400 |InvalidParam.BindError |Request parameter error, please check input data |The parameter failed validation. Please check if the data type is correct. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.AccountIDNotAllow |this AccountID does not have permission to access the corresponding resource, please check the request parameters |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |The video live streaming service has not been enabled or the account is in arrears, resulting in an unavailable bill. Please check the service activation status and account arrears status. |
|404 |ResourceNotFound |\- |The resource (including domain name space, domain name, app name, configuration, and certificate) was not found. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError.DB |an internal error related to database occurred, please contact the administrator. |An internal error related to the database occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |Internal Service is timeout. Please [contact support](https://console.byteplus.com/workorder/create). |


&nbsp;
