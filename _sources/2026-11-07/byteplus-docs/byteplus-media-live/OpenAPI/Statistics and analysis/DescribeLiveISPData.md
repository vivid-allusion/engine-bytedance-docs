---
title: "DescribeLiveISPData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveispdata"
---

Call the `DescribeLiveISPData` API to retrieve the identifiers of Internet Service Providers (ISPs) that provide network access services for BytePlus MediaLive. Once you obtain the ISP identifiers, you can use them to query dimensional data for specific ISPs in APIs that support ISP\-based querying.

<span id="requirements"></span>
## Requirements

Rate limit：30 queries per second per account.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=DescribeLiveISPData&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DescribeLiveISPData` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|ISPList |Array of [ISPList](https://docs.byteplus.com/en/docs/24/20942#isplist) |`-` |An array indicating Internet Service Provider (ISP) identifiers. |


<span id="isplist"></span>
### ISPList


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Code |String |`unicom` |Internet Service Provider (ISP) identifiers.<br><br><br>* `unicom`: China Unicom;<br><br>* `railcom`: China Railway Telecom;<br><br>* `telecom`: China Telecom;<br><br>* `mobile`: China Mobile;<br><br>* `cernet`: China Education and Research Network (CERNET);<br><br>* `tianwei`: China Tianwei;<br><br>* `alibaba`: Alibaba Group;<br><br>* `tencent`: Tencent Holdings;<br><br>* `drpeng`: Dr. Peng Telecom & Media Group;<br><br>* `btvn`: Broadcasting Television Network (BTVN);<br><br>* `huashu`: Huashu Media. |
|Name |String |`unicom` |Internet Service Provider (ISP) names. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveISPData&Version=2023-01-01
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202309042019116E825EC4FC63CD166C91",
        "Action": "DescribeLiveISPData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "cn-north-1"
    },
    "Result": {
        "ISPList": [
            {
                "Code": "unicom",
                "Name": "unicom"
            },
            {
                "Code": "railcom",
                "Name": "railcom"
            },
            {
                "Code": "telecom",
                "Name": "telecom"
            },
            {
                "Code": "mobile",
                "Name": "mobile"
            },
            {
                "Code": "cernet",
                "Name": "cernet"
            },
            {
                "Code": "tianwei",
                "Name": "tianwei"
            },
            {
                "Code": "alibaba",
                "Name": "alibaba"
            },
            {
                "Code": "tencent",
                "Name": "tencent"
            },
            {
                "Code": "drpeng",
                "Name": "drpeng"
            },
            {
                "Code": "btvn",
                "Name": "btvn"
            },
            {
                "Code": "huashu",
                "Name": "huashu"
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
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/20942#request-parameters) description for inspection. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |


&nbsp;
