---
title: "CreateCert"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createcert-2023"
---

Call the `CreateCert` API to add or update your certificate to MediaLive so that it can later be bound to a domain name and start HTTPS.

<span id="requirements"></span>
## Requirements

Rate limit: 1 query per second per account.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=CreateCert&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`CreateCert` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|ProjectName |String |No |`default` |The name of the project. Set the project attribution for the certificate. Default value is `Default`. After setting the project, sub\-accounts with project permissions are supported to use the certificate. |
|CertName |String |No |`pushCertName` |Name of the certificate. |
|ChainID |String |No |`9*********a982edf6e84bba1f` |The certificate chain ID. Used to identify the entire certificate chain, including the end\-entity certificate (server certificate), intermediate certificates (intermediate CA certificates), and root certificate (root CA certificate).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When using the current API to update the certificate information, <code>ChainID</code> must be passed in.</div><br> |
|Rsa |Object of [Rsa](https://docs.byteplus.com/en/docs/24/27351#rsa) |Yes |`-` |Certificate information, which contains the contents of both the certificate and the certificate's private key. |
|UseWay |String |Yes |`https` |Usage of the certificate. Always set it to `https`, which means HTTPS encryption. |


<span id="rsa"></span>
### Rsa


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Pubkey |String |Yes |`*******` |The contents of the certificate. You need to open the certificate on a computer using a text editor and copy and paste all the contents as the argument.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The system supports auto\-retrieval of certificate chains. You only need to upload the certificate issued for your domain, and the system will automatically retrieve the complete certificate chain.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you choose to upload a certificate chain, be sure to include the server certificate, intermediate certificate and root certificate, and arrange them in the correct order: the server certificate comes first, followed by the intermediate certificate, and then the root certificate. Incorrect orders will invalidate the certificate chain.</div><br> |
|Prikey |String |Yes |`*******` |The contents of the certificate's private key. You need to open the certificate's private key on a computer using a text editor and copy and paste all the contents as the argument.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Please make sure that the certificate's private key is not password protected.</div><br> |


<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|ChainID |String |`9*********a982edf6e84bba1f` |The certificate chain ID. |
|Domain |String |`live.example.com` |The domain name that uses the current certificate. |
|UseWay |String |`https` |Usage of the certificate. Always set it to `https`, which means HTTPS encryption. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=CreateCert&Version=2023-01-01
{
    "UseWay": "https",
    "Rsa": {
        "PubKey": "******",
        "PriKey": "******"
    }
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestID": "2020091618492801022706705734830",
        "Action": "CreateCert",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "cn-north-1"
    },
    "Result": {
        "ChainID": "9**47c0151394d93a982edf6e84bba1f",
        "Domain": "push.example.com",
        "UseWay": "https"
    }
}
```


<span id="error-codes"></span>
## Error codes

The following are the error codes related to the current operation. For other error codes, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|200 |CommonErr |\- |Uncategorized error. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/27351#request-parameters) description for inspection. |
|400 |InvalidParam.BindError |Request parameter error, please check input data |The parameter failed validation. Please check if the data type is correct. |
|400 |InvalidParam.OutOfRange |%s should be one of {[%s]}%s should be between %d and %d |The parameter exceeds the allowable range. Please check if the value of the specified parameter in the error message exceeds the value range. |
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
