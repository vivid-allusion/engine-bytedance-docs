---
title: "ListStorageSpaceDetail"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-liststoragespacedetail"
---

Call the `ListStorageSpaceDetail` API to query the details of the specified storage spaces under an account.

<span id="requirements"></span>
## Requirements

Rate limit: 100 queries per second per account.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=ListStorageSpaceDetail&Version=2020\-08\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ListStorageSpaceDetail` |The API operation. |
|Version |String |Yes |`2020-08-01` |The version of this API operation. Current version: 2020\-08\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|StorageSpaceList |Array of String |No |`["bucket112233"]` |A list of the storage spaces you want to query. If unspecified, all the storage spaces under the account will be queried. |


<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|StorageSpaceListDetail |Array of [StorageSpaceListDetail](https://docs.byteplus.com/en/docs/24/7814#storagespacelistdetail) |`-` |Details of each storage space you query. |


<span id="storagespacelistdetail"></span>
### StorageSpaceListDetail


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|AccountID |String |`3000000285` |Your account ID. |
|Name |String |`fcdn-boe` |Name of the storage space. |
|PublicDomain |String |```Plain Text```<br>```This parameter is deprecated.```<br> |Public domain name of the storage space. |
|CnameDomain |String |`ccama.test.example.com` |Canonical name that the public domain name points to. |
|TTL |Integer |`-` |This parameter is deprecated. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=ListStorageSpaceDetail&Version=2020-08-01
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202204060959170101742350380764F506",
        "Action": "ListStorageSpace",
        "Version": "2020-08-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "StorageSpaceListDetail": [
            {
                "AccountID": "3000000285",
                "Name": "fcdn-boe",
                "PublicDomain": "test.example.com",
                "CnameDomain": "cname.test.example.com"
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
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/7814#request-parameters) description for inspection. |
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
