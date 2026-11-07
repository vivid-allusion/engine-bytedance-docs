---
title: "UpdateTimeShiftPresetV2"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatetimeshiftpresetv2-2023"
---

Call the `UpdateTimeShiftPresetV2` API to update an already created time\-shift configuration.

<span id="requirements"></span>
## Requirements


* Effective description: For adding, updating, and deleting time\-shift configurations, you need to re\-push and pull the stream after the adding, updating, and deleting operations (3\-5 minutes) to use the changed configuration.

* Rate limit: 1 query per second per account.


<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=UpdateTimeShiftPresetV2&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="headers"></span>
### Headers


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Content\-Type |String |Yes |`application/json` |The MIME type of the request body. |


<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`UpdateTimeShiftPresetV2` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Vhost |String |Yes |`push.example.com` |The domain name space. You can call the [ListTimeShiftPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listtimeshiftpresetv2-2023) API to obtain the domain name space of configuration. |
|App |String |Yes |`live` |The AppnName field. You can call the [ListTimeShiftPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listtimeshiftpresetv2-2023) API to obtain the AppName of configuration. |
|Preset |String |Yes |`preset-test` |The name of configuration. You can call the [ListTimeShiftPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listtimeshiftpresetv2-2023) API to obtain the name of configuration. |
|MaxShiftTime |Integer |Yes |`3000` |Shift time, which moves the live stream's availability by a set amount. For example, if you set `MaxShiftTime` to `86400`, then the live stream will be available as late as one day from its initial broadcast. Unit: second. The default value is `86400`. Valid range: 300–1296000. |
|Type |String |Yes |`tos` |Storage type. Always set it to `tos`. |


<span id="response-parameters"></span>
## Response parameters

This API only returns [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/request-response) in the response.

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=UpdateTimeShiftPresetV2&Version=2023-01-01
Content-Type: application/json
{
    "Vhost": "push.example.com",
    "App": "live",
    "MaxShiftTime": 86400,
    "Preset": "preset-test",
    "Type": "tos"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1",
        "Action": "UpdateTimeShiftPresetV2",
        "RequestId": "202306041104200100100232280022D31"
    }
}
```


<span id="error-codes"></span>
## Error codes

The following are the error codes related to the current operation. For other error codes, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|200 |CommonErr |\- |Uncategorized error. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/27458#request-parameters) description for inspection. |
|400 |InvalidParam.BindError |Request parameter error, please check input data |The parameter failed validation. Please check if the data type is correct. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.AccountIDNotAllowed |this AccountID does not have permission to access the corresponding resource, please check the request parameters |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |The video live streaming service has not been enabled or the account is in arrears, resulting in an unavailable bill. Please check the service activation status and account arrears status. |
|404 |ResourceNotFound |\- |The resource (including domain name space, domain name, app name, configuration, and certificate) was not found. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|404 |ResourceNotFound.VhostNotExist |vhost not found |The domain name space (Vhost) was not found. Please check if the passed\-in domain name space is consistent with the actual domain name space in use. |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError.DB |an internal error related to database occurred, please contact the administrator. |An internal error related to the database occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError.VhostOrDomain |an internal error related to vhost or domain occurred, please contact the administrator. |An internal error related to the domain name space (Vhost) or domain name (Domain) occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |Internal Service is timeout. Please [contact support](https://console.byteplus.com/workorder/create). |


&nbsp;
