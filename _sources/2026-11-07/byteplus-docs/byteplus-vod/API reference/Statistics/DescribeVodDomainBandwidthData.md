---
title: "DescribeVodDomainBandwidthData"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-describevoddomainbandwidthdata"
---

This interface is used to view the bandwidth usage within a certain time range in a designated space.

<span id="requirements"></span>
## Requirements


* Billing: For bandwidth billing prices, please refer to [Pay-As-You-Go pricing](https://docs.byteplus.com/en/docs/byteplus-vod/docs-pay-as-you-go-pricing).

* Rate limit: The request frequency limit for a single user is **10 times/second**.

* Data Latency: **1 day**.

* Time Range: The time span for queries should not exceed **93 days**.

* Permission Description: When using a sub\-account to request an interface, the interface will perform permission verification based on the sub\-account and only return the data that the sub\-account has permission to access. For more details, see [Creating a sub-account](https://docs.byteplus.com/en/docs/byteplus-vod/docs-creating-iam-users).


<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=DescribeVodDomainBandwidthData&Version=2024\-01\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DescribeVodDomainBandwidthData` |The API action. For the current API, the value is `DescribeVodDomainBandwidthData`. |
|Version |String |Yes |`2024-01-01` |The API version. For the current API, the value is `2024-01-01`. |
|DomainList |String |No |`www.test.com` |Domain list. Separate multiple domains with `,`. You can obtain them through the [ListDomain](https://docs.byteplus.com/en/docs/byteplus-vod/reference-listdomain) API.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If it is a POST request, the parameter type is Array of String.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You can select either the <code>DomainList</code> or <code>DomainInSpaceList</code> parameters and cannot set them at the same time.</div><br> |
|DomainInSpaceList |String |No |`vod-player-test:vod-player-test.volcvod.com` |List of VOD space names and domain names. Multiple domain names are separated by `,`. The format is `space name:domain name`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">If it is a POST request, this parameter type is Array of String.</div><br> |
|StartTime |String |Yes |`2022-04-18T20:00:00Z` |The start time of the query. The UTC time follows the RFC3339 format, with an accuracy of seconds and the format is: yyyy\-MM\-ddTHH:mm:ssZ. |
|EndTime |String |Yes |`2022-04-18T22:00:00Z` |The end time of the query. It follows the RFC3339 format in UTC time, with a precision to the second, formatted as: yyyy\-MM\-ddTHH:mm:ssZ.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">The time span of a single query cannot be less than 5 minutes and cannot exceed 93 days.</div><br> |
|Aggregation |Integer |No |`300` |Aggregation time granularity. The unit is seconds. The values are as follows:<br><br><br>* `300`: (Default) 5 minutes<br><br>* `1800`: 30 minutes<br><br>* `3600`: 1 hour<br><br>* `86400`: 1 day |
|BandwidthType |String |No |`CDN` |Bandwidth type. The values are as follows:<br><br><br>* (Default) `CDN`<br><br>* `All` |
|Area |String |No |`CHN` |Billing region. By default, data for all regions is returned. The values are as follows:<br><br><br>* `CHN`: Mainland China<br><br>* `EU`: Europe<br><br>* `NA`: North America<br><br>* `SA`: South America<br><br>* `ME`: Middle East<br><br>* `AP1`: Asia Pacific 1<br><br>* `AP2`: Asia Pacific 2<br><br>* `AP3`: Asia Pacific 3<br><br>* `All`: All Regions<br><br>* `OverSeas`: Regions outside Mainland China<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">For detailed coverage of each billing region, see <a href="https://docs.byteplus.com/en/docs/byteplus-vod/docs-resource-packs">Prepaid resource packages</a>.</div><br> |
|TimeZone |String |No |`Etc/GMT+12` |The time zone ID, see [Time zones](https://docs.byteplus.com/en/docs/byteplus-vod/reference-time-zones). |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|DomainList |Array of String |`["www.test.com"]` |The domain name list. |
|DomainInSpaceList |Array of String |`["vod-player-test:vod-player-test.volcvod.com"]` |The domain name space list. |
|StartTime |String |`2022-04-18T20:00:00Z` |The start time for the query. It follows the RFC3339 format for UTC time with second precision, formatted as: yyyy\-MM\-ddTHH:mm:ssZ. |
|EndTime |String |`2022-04-18T22:00:00Z` |The query end time. It follows the RFC3339 format for UTC time with second precision, formatted as: yyyy\-MM\-ddTHH:mm:ssZ. |
|Aggregation |Integer |`300` |The aggregation time granularity. The unit is seconds. The values are as follows:<br><br><br>* `300`: 5 minutes<br><br>* `1800`: 30 minutes<br><br>* `3600`: 1 hour<br><br>* `86400`: 1 day |
|BandwidthType |String |`CDN` |Bandwidth Type. The values are as follows:<br><br><br>* `CDN`<br><br>* `ALL` |
|Area |String |`CHN` |The billing regions. The values are as follows:<br><br><br>* `CHN`: Mainland China<br><br>* `EU`: Europe<br><br>* `NA`: North America<br><br>* `SA`: South America<br><br>* `ME`: Middle East<br><br>* `AP1`: Asia Pacific Zone 1<br><br>* `AP2`: Asia Pacific Zone 2<br><br>* `AP3`: Asia Pacific Zone 3<br><br>* `All`: All regions<br><br>* `OverSeas`: Regions outside Mainland China<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">For detailed coverage of each billing region, see <a href="https://docs.byteplus.com/en/docs/byteplus-vod/docs-pay-as-you-go-pricing">Pay\-As\-You\-Go pricing</a>.</div><br> |
|PeakBandwidth |Double |`1.1` |The peak bandwidth of the selected time period. The unit is bps. |
|PeakBandwidthTime |String |`2022-04-18T20:00:00Z` |The time when the peak bandwidth occurs. It follows the RFC3339 format in UTC time with second precision, formatted as: yyyy\-MM\-ddTHH:mm:ssZ. |
|Peak95Bandwidth |Double |`1.1` |The bandwidth 95th percentile for the selected time period, measured in bps. |
|Peak95BandwidthTime |String |`2022-04-18T20:00:00Z` |The time when the bandwidth peak of 95 occurs. It follows the RFC3339 format for UTC time with second precision, formatted as: yyyy\-MM\-ddTHH:mm:ssZ. |
|BandwidthDataList |Array of [BandwidthDataList](https://docs.byteplus.com/en/docs/25/8053#bandwidthdatalist) |`-` |The detailed data of bandwidth usage. |


#{.custom\-md\-table\-4}#

<span id="bandwidthdatalist"></span>
### BandwidthDataList


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Time |String |`2022-04-18T20:00:00Z` |The start time of the data's time interval. It follows the RFC3339 format in UTC time, with a precision of seconds, formatted as: yyyy\-MM\-ddTHH:mm:ssZ. |
|Bandwidth |Double |`1.1` |The bandwidth, measured in bps. |


#{.custom\-md\-table\-4}#

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=DescribeVodDomainBandwidthData&Version=2024-01-01&DomainList=www.test.com&DomainInSpaceList=vod-player-test:vod-player-test.volcvod.com&StartTime=2022-04-18T20:00:00Z&EndTime=2022-04-18T22:00:00Z&Aggregation=300&BandwidthType=CDN&Area=CHN&RegionList=cn-north-1
{
    "DomainList": "www.test.com",
    "DomainInSpaceList": "vod-player-test:vod-player-test.volcvod.com",
    "StartTime": "2022-04-18T20:00:00Z",
    "EndTime": "2022-04-18T22:00:00Z",
    "Aggregation": 300,
    "BandwidthType": "CDN",
    "Area": "CHN"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202507070242290AF3138D94F33B03D067",
        "Action": "DescribeVodDomainTrafficData",
        "Version": "2024-01-01",
        "Service": "vod",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "DomainList": [
            "www.test.com"
        ],
        "StartTime": "2025-06-18T20:00:00Z",
        "EndTime": "2025-06-20T20:00:00Z",
        "Aggregation": 86400,
        "TotalTraffic": 7802739499,
        "TrafficDataList": [
            {
                "Time": "2025-06-19T09:00:00Z",
                "Traffic": 5659775499
            },
            {
                "Time": "2025-06-20T09:00:00Z",
                "Traffic": 2142964000
            }
        ]
    }
}
```


<span id="error-codes"></span>
## Error codes

This operation does not have specific error codes. For more information, see the [shared error codes of BytePlus VOD](https://docs.byteplus.com/en/docs/byteplus-vod/reference-common-error-codes).

&nbsp;
