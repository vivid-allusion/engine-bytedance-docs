---
title: "DescribeVodDomainTrafficData"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-describevoddomaintrafficdata-deprecated"
---

This interface is used to query the traffic usage within a specified time range in the specified space.

<span id="requirements"></span>
## Requirements


* Billing: For traffic billing prices, please refer to [Pay-As-You-Go pricing](https://docs.byteplus.com/en/docs/byteplus-vod/docs-pay-as-you-go-pricing).

* Data Latency: **1 day**.

* Time Range: The time span for queries should not exceed **93 days**.

* Permission Description: When using a sub\-account to request an interface, the interface will perform permission verification based on the sub\-account and only return the data that the sub\-account has permission to access. For more details, see [Creating a sub-account](https://docs.byteplus.com/en/docs/byteplus-vod/docs-creating-iam-users).


<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=DescribeVodDomainTrafficData&Version=2023\-01\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DescribeVodDomainTrafficData` |The API action. For the current API, the value is `DescribeVodDomainTrafficData`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|DomainList |String |No |`www.test.com` |The domain list. Multiple domains should be separated by commas `,`. You can obtain the domain list via the [ListDomain](https://docs.byteplus.com/en/docs/byteplus-vod/reference-listdomain) API.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If it is a POST request, the parameter type is Array of String.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You can select either the <code>DomainList</code> or <code>DomainInSpaceList</code> parameters and cannot set them at the same time.</div><br> |
|StartTime |String |No |`2022-04-18T20:00:00Z` |The query start time. It follows the RFC3339 format for UTC time with second precision, formatted as: yyyy\-MM\-ddTHH:mm:ssZ. |
|EndTime |String |No |`2022-04-19T20:00:00Z` |The end time of the query. It follows the RFC3339 format in UTC time, with a precision of seconds, formatted as: yyyy\-MM\-ddTHH:mm:ssZ.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">The time span of a single query should not exceed 93 days.</div><br> |
|Aggregation |Integer |No |`300` |The aggregation time granularity. The unit is seconds. The values are as follows:<br><br><br>* `300`: (default) 5 minutes<br><br>* `1800`: 30 minutes<br><br>* `3600`: 1 hour<br><br>* `86400`: 1 day |
|TrafficType |String |No |`CDN` |The traffic type. The default is `CDN`. Possible values are as follows:<br><br><br>* `CDN`<br><br>* `ALL` |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|DomainList |Array of String |`["www.test.com"]` |The domain name list. |
|StartTime |String |`2022-04-18T20:00:00Z` |The start time for the query. It follows the RFC3339 format for UTC time with precision to the second, in the format: yyyy\-MM\-ddTHH:mm:ssZ. |
|EndTime |String |`2022-04-18T22:00:00Z` |The query end time. It follows the RFC3339 format in UTC time with a precision of seconds, formatted as: yyyy\-MM\-ddTHH:mm:ssZ. |
|Aggregation |Integer |`300` |The aggregation time granularity. The unit is seconds. The values are as follows:<br><br><br>* `300`: 5 minutes<br><br>* `1800`: 30 minutes<br><br>* `3600`: 1 hour<br><br>* `86400`: 1 day |
|TrafficType |String |`CDN` |Traffic Type. The values are as follows:<br><br><br>* `CDN`<br><br>* `ALL` |
|TotalTraffic |Double |`1.1` |The total traffic of the selected time period, in bytes. |
|TrafficDataList |Array of [TrafficDataList](https://docs.byteplus.com/en/docs/25/54483#trafficdatalist) |`-` |The traffic detailed data. |


#{.custom\-md\-table\-4}#

<span id="trafficdatalist"></span>
### TrafficDataList


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Time |String |`2022-04-18T20:00:00Z` |The start time of the data's time range. It follows the RFC3339 format for UTC time, with a precision to the second, and the format is: yyyy\-MM\-ddTHH:mm:ssZ. |
|Traffic |Double |`1.1` |The traffic, in units of B. |


#{.custom\-md\-table\-4}#

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=DescribeVodDomainTrafficData&Version=2023-01-01&DomainList=www.test.com&DomainInSpaceList=vod-player-test:vod-player-test.volcvod.co&StartTime=2022-04-18T20:00:00Z&EndTime=2022-04-19T20:00:00Z&Aggregation=300&TrafficType=CDN&Area=CHN
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104***00100232280022D30",
        "Action": "DescribeVodDomainTrafficData",
        "Version": "2023-01-01",
        "Service": "vod"
    },
    "Result": {
        "DomainList": [
            "www.test.com"
        ],
        "DomainInSpaceList": [
            "test:www.test.com"
        ],
        "StartTime": "2022-04-18T20:00:00Z",
        "EndTime": "2022-04-18T22:00:00Z",
        "Aggregation": 300,
        "Area": "AP1",
        "TrafficType": "CDN",
        "TotalTraffic": 1.1,
        "TrafficDataList": [
            {
                "Time": "2022-04-18T20:00:00Z",
                "Traffic": 1.1
            }
        ]
    }
}
```


<span id="error-codes"></span>
## Error codes

This operation does not have specific error codes. For more information, see the [shared error codes of BytePlus VOD](https://docs.byteplus.com/en/docs/byteplus-vod/reference-common-error-codes).

&nbsp;
