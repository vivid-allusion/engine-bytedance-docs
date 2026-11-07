---
title: "DescribeCertDetailSecretV2"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecertdetailsecretv2-2023"
---

Call the `DescribeCertDetailSecretV2` API to view the detailed information of the certificate through the certificate ID or certificate chain ID.

<span id="requirements"></span>
## Requirements

Rate limit: 10 queries per second per account.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=DescribeCertDetailSecretV2&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DescribeCertDetailSecretV2` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|CertID |String |No |`812******1` |The certificate ID. You can call the [ListCertV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listcertv2) API to obtain the CertID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Either <code>ChainID</code> or <code>CertID</code> should be provided, not both.</div><br> |
|ChainID |String |No |`188b5c6f6b3c47728418932*******d2` |The ChainID of the certificate. You can call the [ListCertV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listcertv2) API to obtain the ChainID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Either <code>ChainID</code> or <code>CertID</code> should be provided, not both.</div><br> |


<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|CertDomainList |Array of String |`["live.example.com"]` |A list of domain names secured by the certificate. |
|ChainID |String |`188b5c6f6b3c47728418932*******d2` |The certificate chain ID. |
|SSL |Object of [SSL](https://docs.byteplus.com/en/docs/24/27355#ssl) |`-` |Certificate chain information. |
|CertName |String |`live.example.com` |The certificate name. |
|NotBefore |String |`2019-09-05T00:00:00Z` |The effective time of the certificate (UTC time in RFC 3339 format with timestamp precision to the second). |
|NotAfter |String |`2020-09-04T12:00:00Z` |The expiration time of the certificate (UTC time in RFC 3339 format with timestamp precision to the second). |
|Status |String |`OK` |Certificate status, the corresponding relationship between values and meanings is as follows.<br><br><br>* `OK`: Normal;<br><br>* `Expire`: Expired;<br><br>* `30days`: 30 days remaining in the validity period;<br><br>* `15days`: 15 days remaining in the validity period;<br><br>* `7days`: 7 days remaining in the validity period;<br><br>* `1days`: 1 day remaining in the validity period. |


<span id="ssl"></span>
### SSL


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|KeyType |String |`rsa` |The encryption algorithm used by the certificate, currently the default is RSA algorithm. |
|Chain |Array of String |`[ "-----BEGIN CERTIFICATE-----MIIFa**********5S98-----END CERTIFICATE-----", "-----BEGIN CERTIFICATE-----MIIEk**********0UiB-----END CERTIFICATE-----", "-----BEGIN CERTIFICATE-----MIIEN**********B5==-----END CERTIFICATE-----" ]` |Certificate chain, including leaf certificate (server certificate), intermediate certificate (intermediate CA certificate), and root certificate (root CA certificate). The certificates in the certificate chain use PEM encoding format. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=DescribeCertDetailSecretV2&Version=2023-01-01
{
    "ChainID": "188b5c6f6b3c47728418932*******d2"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202306041104200100100232280022D31",
        "Action": "DescribeCertDetailV2",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "CertDomainList": [
        "pull.example.xyz"
        ],
        "CertName": "pull.example.xyz",
        "ChainID": "37a***b22d554a3b8785f111d51a2b88",
        "NotAfter": "2024-08-03T23:59:59Z",
        "NotBefore": "2024-05-06T00:00:00Z",
        "SSL": {
        "Chain": [
            "-----BEGIN CERTIFICATE-----\nMIIF+TCCBOG***UrNyWlJ7\n-----END CERTIFICATE-----\n",
            "-----BEGIN CERTIFICATE-----\nMIIEqjCCA5K***QjJNSg==\n-----END CERTIFICATE-----\n",
            "-----BEGIN CERTIFICATE-----\nMIIDjjCCAna***Zl\nMrY=\n-----END CERTIFICATE-----\n"
        ]
        "KeyType": "rsa",
        },
        "Status": "OK"
    }
    }
```


<span id="error-codes"></span>
## Error codes

The following are the error codes related to the current operation. For other error codes, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|200 |CommonErr |\- |Uncategorized error. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/27355#request-parameters) description for inspection. |
|400 |InvalidParam.BindError |Request parameter error, please check input data |The parameter failed validation. Please check if the data type is correct. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.AccountIDNotAllowed |this AccountID does not have permission to access the corresponding resource, please check the request parameters |The request is rejected. There are no requested resources (domain name space, domain name, application, configuration template, certificate) under the current account. |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |The video live streaming service has not been enabled or the account is in arrears, resulting in an unavailable bill. Please check the service activation status and account arrears status. |
|403 |AccessDenied |User is not authorized to perform: %s on resource: %s |The request is rejected. There are no requested resources (domain name space, domain name, application, configuration template, certificate) or interface permissions under the current account. |
|404 |ResourceNotFound |\- |The resource (including domain name space, domain name, app name, configuration, and certificate) was not found. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError.DB |an internal error related to database occurred, please contact the administrator. |An internal error related to the database occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |Internal Service is timeout. Please [contact support](https://console.byteplus.com/workorder/create). |


&nbsp;
