---
title: "DescribeCDNTrafficData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecdntrafficdata"
---

Call the `DescribeCDNTrafficData` API to query CDN traffic used when accessing live\-stream recordings and snapshots from within a specified time range.

<span id="requirements"></span>
## Requirements


* Rate limit: 1 query per second per account.

* Data delay: 4 minutes.


<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=DescribeCDNTrafficData&Version=2020\-08\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DescribeCDNTrafficData` |The API operation. |
|Version |String |Yes |`2020-08-01` |The version of this API operation. Current version: 2020\-08\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|StartTime |String |Yes |`2022-04-08T00:00:00Z` |The start time of your query's range in RFC 3339 format with second precision. |
|EndTime |String |Yes |`2022-04-08T00:00:00Z` |The end time of your query's range in RFC 3339 format with second precision. |
|DomainList |Array of String |No |`["push.example.com"]` |A list of the domain names you want to query. If unspecified, all the domain names under your account will be queried. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or visit the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to obtain the domain name. |
|Interval |Integer |Yes |`300` |Data granularity. Unit: seconds. You can only set the value as 300. |
|RegionList |Array of [RegionList](https://docs.byteplus.com/en/docs/24/7775#regionlist) |Yes |`-` |A list of regions. |


<span id="regionlist"></span>
### RegionList


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Area |String |Yes |`Global` |Supported values:<br><br><br>* `AsiaPacific-1`<br><br>* `AsiaPacific-2`<br><br>* `AsiaPacific-3`<br><br>* `NorthAmerica`<br><br>* `SouthAmerica`<br><br>* `Europe`<br><br>* `MiddleEast`<br><br>* `Global`: Non\-Chinese mainland |
|Country |String |No |`-` |Reserved for future use. |
|Province |String |No |`-` |Reserved for future use. |


<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|DomainList |Array of String |`["push.example.com"` |The list of the domain names you want to query. |
|Interval |Integer |`300` |Data granularity. |
|StartTime |String |`2022-04-08T00:00:00Z` |The start time of your query's range in RFC 3339 format with second precision. |
|EndTime |String |`2022-04-08T00:00:00Z` |The end time of your query's range in RFC 3339 format with second precision. |
|TrafficTotalData |Array of [CDNTrafficData](https://docs.byteplus.com/en/docs/24/7775#cdntrafficdata) |`-` |Aggregated data based on time interval. |
|TrafficDetailDataList |Array of [TrafficDetailDataList](https://docs.byteplus.com/en/docs/24/7775#trafficdetaildatalist) |`-` |Aggregated data based on time interval and domain name. |


<span id="cdntrafficdata"></span>
### CDNTrafficData


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|TimeStamp |String |`2022-04-08T00:00:00Z` |The start time of each interval (UTC time in RFC 3339 format). |
|Traffic |Float |`22` |CDN traffic data, in GB. |


<span id="trafficdetaildatalist"></span>
### TrafficDetailDataList


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Domain |String |`push.example.com` |Domain name. |
|TrafficDataList |Array of [CDNTrafficData](https://docs.byteplus.com/en/docs/24/7775#cdntrafficdata) |`-` |Aggregated data based on time interval. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=DescribeCDNTrafficData&Version=2020-08-01
{
    "StartTime": "2022-04-08T00:00:00Z",
    "EndTime": "2022-04-08T00:00:00Z",
    "DomainList": [
        "push.example.com",
        "push.example2.com"
    ],
    "Interval": 300
}
```


<span id="sample-response"></span>
### Sample response

```json
{
  "ResponseMetadata":{
    "RequestId":"202207130928130102511970410745B8DC",
    "Action":"DescribeCDNTrafficData",
    "Version":"2020-08-01",
    "Service":"live",
    "Region":"ap-singapore-1"
  },
  "Result":{
    "StartTime": "2022-04-08T00:00:00Z",
    "EndTime": "2022-04-08T00:00:00Z",
    "DomainList": [
        "push.example.com",
        "push.example2.com"
    ],
    "Interval": 300,
    "TrafficTotalData": [
        {
            "Timestamp": "2022-04-08T00:00:00Z",
            "Traffic": 276.00
        },
        {
            "Timestamp": "2022-04-08T01:00:00Z",
            "Traffic": 276.00
        }
    ],
    "TrafficDetailDataList": [
        {
            "Domain": "push.example.com",
            "TrafficDataList": [
                {
                    "TimeStamp": "2022-04-08T00:00:00Z",
                    "Traffic": 138.00
                },
                {
                    "TimeStamp": "2022-04-08T01:00:00Z",
                    "Traffic": 138.00
                }
            ]
        },
        {
            "Domain": "push.example2.com",
            "TrafficDataList": [
                {
                    "TimeStamp": "2022-04-08T00:00:00Z",
                    "Traffic": 138.00
                },
               {
                    "TimeStamp": "2022-04-08T01:00:00Z",
                    "Traffic": 138.00
                }
            ]
        }
    ]
}
```


<span id="error-codes"></span>
## Error codes

The following are the error codes related to the current operation. For other error codes, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|200 |CommonErr |\- |Uncategorized error. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/7775#request-parameters) description for inspection. |
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
