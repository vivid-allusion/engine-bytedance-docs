---
title: "ListCertV2"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listcertv2"
---

Call the `ListCertV2` API to view the list of certificates under the current account.

## Requirements

Rate limit: 10 queries per second per account.

## HTTP request

* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=ListCertV2&Version=2023\-01\-01

## Request parameters

### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

### Query

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ListCertV2` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |

### Body parameters

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Available |Boolean |No |`true` |Whether to retrieve enabled or disabled certificates.<br><br><br>* `true`: (Default) Retrieves enabled certificates.<br><br>* `false`: Retrieves disabled certificates. |
|Domain |String |No |`push.example.com` |The domain name secured by the certificates. Exact search is supported. |
|Expiring |Boolean |No |`false` |Whether to retrieve valid or expired certificates.<br><br><br>* `false`: (Default) Retrieves certificates that are still valid.<br><br>* `true`: Retrieves expired certificates.<br><br><br>> **说明**<br><br><br>> This parameter takes effect only if `Available` is specified.<br> |
|CertName |String |No |`domaincert` |The certificate name. Fuzzy search is supported. |
|PageSize |Integer |No |`10` |The number of query results per page. Valid values: [1,1000].<br><br>> **说明**<br><br><br>> `PageNum` and `PageSize` must be specified together. If either parameter is not specified, all results are returned.<br> |
|PageNum |Integer |No |`1` |The page number. Valid values: [1,1000].<br><br>> **说明**<br><br><br>> `PageNum` and `PageSize` must be specified together. If either parameter is not specified, all results are returned.<br> |
|ProjectName |String |No |`MyProject` |The name of the project associated with the certificate. This field is optional and can be used to filter certificates by project name. |

## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|CertList |Array of [CertList](https://docs.byteplus.com/en/docs/24/7688#certlist) |`-` |A list of certificates. |
|Total |Integer |`20` |The total number of certificates in the current query result. |
|ExpirationInfo |Object of [ExpirationInfo](https://docs.byteplus.com/en/docs/24/7688#expirationinfo) |`-` |Expiration information of all certificates in the current query. |

### CertList

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|ProjectName |String |`default` |The certificate's project. |
|CertDomainList |Array of String |`["push.example.com"]` |A list of domain names secured by the certificate. |
|CertName |String |`push.example.com` |The certificate name. |
|ChainID |String |`4060e26538a149e2a87b42*******11` |The certificate chain ID. |
|CertID |String |`812******1` |The certificate ID. |
|NotAfter |String |`2024-08-18T07:19:00Z` |The effective time of the certificate (UTC time in RFC 3339 format with timestamp precision to the second). |
|NotBefore |String |`2020-08-19T07:19:00Z` |The expiration time of the certificate (UTC time in RFC 3339 format with timestamp precision to the second). |
|Status |String |`OK` |The certificate status. Valid values include:<br><br><br>* `OK`: Normal.<br><br>* `Expire`: Expired.<br><br>* `30days`: Expires in 30 days.<br><br>* `15days`: Expires in 15 days.<br><br>* `7days`: Expires in 7 days.<br><br>* `1days`: Expires in 1 day. |
|CreateTime |String |`2020-08-19T07:19:00Z` |The timestamp when the certificate was created, in RFC3339 format with UTC timezone and second precision. |

### ExpirationInfo

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|ActiveNum |Integer |`10` |The number of active certificates that are currently valid and not expired. |
|ExpireNum |Integer |`5` |The number of expired certificates in the current query result. |
|ClosingExpireNum |Integer |`5` |The number of certificates that are about to expire within one month. |

## Samples

### Sample request

```json
POST https://open.byteplusapi.com/?Action=ListCertV2&Version=2023-01-01
{
    "AccountID": "1000000001"
}
```

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestID":  "2020091618453101022706705762997",
        "Action": "ListCert",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "CertList": [
            {
                "CertID": "cert-94552b4a4b0a4b8fbe3d*****",
                "CertName": "*.example.com",
                "CertDomainList": ["*.example.com"],
                "ChainID": "4060e26538a149e2a87b42deba979011",
                "NotBefore": "2020-08-19T07:19:00Z",
                "NotAfter": "2024-08-18T07:19:00Z",
                "Status": "OK"
            }
            {
                "CertID": "cert-94552b4a4b0a4b8******e5152",
                "CertName": "*.test.com.cn",
                "CertDomainList": ["*.test.com.cn"],
                "ChainID": "d7134cbff1dd4425847f329cba0245e4",
                "NotBefore": "2020-08-11T05:42:54Z",
                "NotAfter": "2020-09-18T05:42:54Z",
                "Status": "Expire"
            }
        ]
    }
}
```

## Error codes

The following are the error codes related to the current operation. For other error codes, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes).

|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|200 |CommonErr |\- |Uncategorized error. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/7688#request-parameters) description for inspection. |
|400 |InvalidParam.BindError |Request parameter error, please check input data |The parameter failed validation. Please check if the data type is correct. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.AccountIDNotAllowed |this AccountID does not have permission to access the corresponding resource, please check the request parameters |The request is rejected. There are no requested resources (domain namespace, domain name, application, configuration template, certificate) under the current account. |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |The video live streaming service has not been enabled or the account is in arrears, resulting in an unavailable bill. Please check the service activation status and account arrears status. |
|403 |AccessDenied |User is not authorized to perform: %s on resource: %s |The request is rejected. There are no requested resources (domain namespace, domain name, application, configuration template, certificate) or interface permissions under the current account. |
|404 |ResourceNotFound |\- |The resource (including domain name space, domain name, app name, configuration, and certificate) was not found. It is recommended to retry. If the error code is still returned, please [contact support](https://docs.byteplus.com/en/docs/24/%5B++https://console.byteplus.com/workorder/create++%5D(https://console.byteplus.com/workorder/create)). |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError.DB |an internal error related to database occurred, please contact the administrator. |An internal error related to the database occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |Internal Service is timeout. Please [contact support](https://console.byteplus.com/workorder/create). |
