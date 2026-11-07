---
title: "DescribeEncryptDRM"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecertdrm_2"
---

Call the `DescribeEncryptDRM` API to view the configured DRM certificate management platform access keys and FairPlay certificate information.

<span id="requirements"></span>
## Requirements

Rate limit: 1 query per second per account.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=DescribeEncryptDRM&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DescribeEncryptDRM` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|DRMItem |Object of [DRMItem](https://docs.byteplus.com/en/docs/24/7694#drmitem) |`-` |DRM Encryption Configuration List. |


<span id="drmitem"></span>
### DRMItem


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|APIKey |String |`desnjkfjsedlfndskfnsklnda` |DRM Certificate Management Platform API Access Key. |
|CertificateName |String |`test` |Custom FairPlay Certificate Name. |
|PrivateKeyFileName |String |`private.cer` |The private key file name created when applying for a FairPlay certificate. |
|CertificateFileName |String |`fairplay.pem` |The name of the FairPlay certificate file. |
|ApplicationSecretKey |String |`dandkandkadacdsknkmkmmknk` |The process of applying for a FairPlay certificate involves Apple returning an ASk (Application Secret Key) string. |
|PrivateKey |String |`hufh29893rh2f384hfv82` |The private key file key created when applying for the FairPlay certificate. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=DescribeEncryptDRM&Version=2023-01-01
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104*****100232280022D30",
        "Action": "DescribeEncryptDRM",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "DRMItem": {
            "APIKey": "desnjkfjs*****dskfnsklnda",
            "CertificateName": "test",
            "PrivateKeyFileName": "private.cer",
            "CertificateFileName": "fairplay.pem",
            "ApplicationSecretKey": "dandkan*****sknkmkmmknk",
            "PrivateKey": "hufh298*****84hfv82"
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
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/7694#request-parameters) description for inspection. |
|400 |InvalidParam.BindError |Request parameter error, please check input data |The parameter failed validation. Please check if the data type is correct. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.AccountIDNotAllowed |this AccountID does not have permission to access the corresponding resource, please check the request parameters |The request is rejected. There is no requested resource (domain name space, domain name, application, configuration template, certificate) under the current account. |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |The video live streaming service has not been enabled or the account is in arrears, resulting in an unavailable bill. Please check the service activation status and account arrears status. |
|403 |AccessDenied |User is not authorized to perform: %s on resource: %s |The request is denied. There are no requested resources (domain space, domain name, application, configuration template, certificate) or interface permissions under the current account. |
|404 |ResourceNotFound |\- |The resource (including domain name space, domain name, app name, configuration, and certificate) was not found. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError.DB |an internal error related to database occurred, please contact the administrator. |An internal error related to the database occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |Internal Service is timeout. Please [contact support](https://console.byteplus.com/workorder/create). |


&nbsp;
