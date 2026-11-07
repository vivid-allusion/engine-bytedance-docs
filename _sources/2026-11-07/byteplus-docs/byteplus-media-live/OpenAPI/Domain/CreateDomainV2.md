---
title: "CreateDomainV2"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-dj3h3u96xn"
---

Call the `CreateDomainV2` API to add one or more domain names for push streaming or pull streaming.

<span id="requirements"></span>
## Requirements

Rate limit: 10 queries per second per account.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=CreateDomainV2&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`CreateDomainV2` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Domains |Array of [Domains](https://docs.byteplus.com/en/docs/24/7641#domains) |Yes |`-` |An array of domain names.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">A domain name space can contain up to 10 domain names.</div><br> |
|Vhost |String |Yes |`vhost` |Domain name space is a collection of associated domains, consisting of letters (A\-Z, a\-z), numbers (0\-9), and hyphens (\-). You can customize a new domain namespace or call the ListDomainDetail interface to obtain the domain name space used by existing domains. |
|ProjectName |String |No |`default` |The project associated with the domain name space. By default, it is empty, indicating it belongs to the 'default 'project.<br><br>After the domain name space is associated with a project, you can manage your resource usage and billing by project. You cannot change the project setting once the domain name space is created. To manage projects, visit the [Project](https://console.byteplus.com/iam/resourcemanage/project) page on the BytePlus console. |


<span id="domains"></span>
### Domains


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|DomainName |String |Yes |`push.example.com` |A domain name consists of letters (A\-Z, a\-z), numbers (0\-9), and hyphens (\-), and is 1 to 60 characters long. |
|ChainID |String |No |`93cb8cf3*******ece5600142` |The SSL certificate chain ID. The default is empty, indicating that no SSL certificate is bound to the domain. You can call the [ListCertV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listcertv2) interface or go to the [Certificate Management](https://console.byteplus.com/live/main/certificate) page in the live video console to obtain the certificate chain ID to be bound. |
|Type |String |Yes |`push` |The type of the domain name:<br><br><br>* `push`: Domain name for push streaming.<br><br>* `pull-flv`: Domain name for pull streaming. |
|Region |String |Yes |`cn` |The accelerated region. Valid values include:<br><br><br>* `oversea`: Outside the Chinese mainland.<br><br>* `cn`: The Chinese mainland.<br><br>* `global`: Global. |


<span id="response-parameters"></span>
## Response parameters

This API only returns [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/request-response) in the response.

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=CreateDomainV2&Version=2023-01-01
{
    "Vhost": "vhost",
    "Domains": [
        {
            "DomainName": "push.example.com",
            "Type": "push",
            "Region": "cn",
            "ChainID": "93cb8cf3*******ece5600142"
        },
        {
            "DomainName": "pull.example.com",
            "Type": "pull-flv",
            "Region": "cn",
            "ChainID": "93c56cf3*******ece522142"
        }
    ],
    "ProjectName": "default"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202306041104200100100232280022D31",
        "Action": "CreateDomainV2",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "cn-north-1"
    }
}
```


<span id="error-codes"></span>
## Error codes

The following are the error codes related to the current operation. For other error codes, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|200 |CommonErr |\- |Uncategorized error. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/7641#request-parameters) description for inspection. |
|400 |InvalidParam.BindError |Request parameter error, please check input data |The parameter failed validation. Please check if the data type is correct. |
|400 |InvalidParam.Format |%s format error |The parameter format is incorrect. Please check if there are illegal characters or URL format errors in the specified parameter in the error message. |
|400 |InvalidParam.OutOfRange |%s should be one of {[%s]}%s should be between %d and %d |The parameter exceeds the allowable range. Please check if the value of the specified parameter in the error message exceeds the value range. |
|400 |InvalidParameter.Tags.Key |The specified parameter Tags.Key is invalid. |The parameter `Tags.Key` fails the validation. Please check if the parameter is correct. |
|400 |InvalidParameter.Tags.Value |The specified parameter Tags.Value is invalid. |The parameter `Tags.Value` fails the validation. Please check if the parameter is correct. |
|400 |InvalidParameter.Tags |The specified parameter Tags is invalid. |The parameter `Tags` fails the validation. Please check if the parameter is correct. |
|400 |Duplicate.Tags.Key |The specified object of tags contains duplicate keys. |The value of the parameter `Tags.Key` is duplicated. Please check if the parameter is correct. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.AccountIDNotAllowed |this AccountID does not have permission to access the corresponding resource, please check the request parameters |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |The video live streaming service has not been enabled or the account is in arrears, resulting in an unavailable bill. Please check the service activation status and account arrears status. |
|404 |ResourceNotFound |\- |The resource (including domain name space, domain name, app name, configuration, and certificate) was not found. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError.DB |an internal error related to database occurred, please contact the administrator. |An internal error related to the database occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |Internal Service is timeout. Please [contact support](https://console.byteplus.com/workorder/create). |


&nbsp;
