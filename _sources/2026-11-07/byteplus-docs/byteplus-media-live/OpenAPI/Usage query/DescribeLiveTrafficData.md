---
title: "DescribeLiveTrafficData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describelivetrafficdata"
---

Call the `DescribeLiveTrafficData` API to query the traffic usage of specified live streaming domains within the specified time range. Moreover, it includes upstream traffic data for push domains and downstream traffic data for pull domains.

<span id="requirements"></span>
## Requirements


* Billing: For pricing information, please refer to [Live-streaming service fees](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-live-streaming-service-fees).

* Limitations:

   * Supports querying traffic usage data (including for deleted domain names);

   * Traffic usage data is used for billing reconciliation, and its collection method differs from traffic data monitoring. Please use [DescribeLiveEdgeStatData](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeliveedgestatdata-2023) to query live traffic monitoring data.

* Rate limit: 30 queries per second per account.

* Data latency: 15 minutes.

* Data metric: Traffic data is calculated in base 1000, for example, 1 GB = 1000 MB.


<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=DescribeLiveTrafficData&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DescribeLiveTrafficData` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|DomainList |Array of String |No |`["example.com"]` |List of domains. By default, it is empty, indicating that the traffic usage data for all domain names under your BytePlus MediaLive will be queried. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or go to the [Domain Management](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to obtain the domain names to be queried. |
|ProtocolList |Array of String |No |`["HTTP-FLV", "RTMP"]` |Push\-pull streaming protocol. By default, all protocol types are included. Supported protocols are as follows.<br><br><br>* `HTTP-FLV`: HTTP\-based push\-pull streaming protocol, transmitting video format in FLV format.<br><br>* `HTTP-HLS`: HTTP\-based push\-pull streaming protocol, transmitting video format in TS format.<br><br>* `RTMP`: Real Time Message Protocol.<br><br>* `RTM`: Real Time Media, ultra\-low latency live streaming protocol.<br><br>* `SRT`: Secure Reliable Transport protocol.<br><br>* `QUIC`: Quick UDP Internet Connections, a new low\-latency Internet transmission protocol based on UDP.<br><br>* `CMAF`: A protocol for efficient, adaptive video streaming over HTTP.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If querying the <code>QUIC</code> protocol, other protocols cannot be queried simultaneously.</div><br> |
|ISPList |Array of String |No |`["telecom"]` |Identifiers of operators providing network access services. By default, all operators are indicated. Supported operators are as follows.<br><br><br>* `unicom`: China Unicom;<br><br>* `railcom`: China Railway Telecom;<br><br>* `telecom`: China Telecom;<br><br>* `mobile`: China Mobile;<br><br>* `cernet`: China Education and Research Network (CERNET);<br><br>* `tianwei`: China Tianwei;<br><br>* `alibaba`: Alibaba Group;<br><br>* `tencent`: Tencent Holdings;<br><br>* `drpeng`: Dr. Peng Telecom & Media Group;<br><br>* `btvn`: Broadcasting Television Network (BTVN);<br><br>* `huashu`: Huashu Media.<br><br>   If you need to obtain the identifiers of various operators, you can call the [DescribeLiveISPData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveispdata). |
|RegionList |Array of [Region](https://docs.byteplus.com/en/docs/24/20978#region) |No |`-` |List of regions to which CDN node IPs belong, by default indicating all regions.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>RegionList</code> and <code>UserRegionList</code> cannot be used together in a single request.</div><br> |
|UserRegionList |Array of [Region](https://docs.byteplus.com/en/docs/24/20978#region) |No |`-` |List of regions to which client IPs belong, by default indicating all regions.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>RegionList</code> and <code>UserRegionList</code> cannot be used together in a single request.</div><br> |
|StartTime |String |Yes |`2021-04-13T00:00:00Z` |The start time of your query's range in RFC 3339 format with second precision. |
|EndTime |String |Yes |`2021-04-14T00:00:00Z` |The end time of your query's range in RFC 3339 format with second precision. |
|Aggregation |Integer |No |`300` |The granularity of data aggregation, measured in seconds, with the following supported options:<br><br><br>* `300` (default): 5 minutes. When aggregated in 5\-minute intervals, the maximum time span for a single query is 31 days, and for historical queries, the maximum time range is 366 days.<br><br>* `3600`: 1 hour. When aggregated in 1\-hour intervals, the maximum time span for a single query is 93 days, and for historical queries, the maximum time range is 366 days.<br><br>* `86400`: 1 day. When aggregated in 1\-day intervals, the maximum time span for a single query is 93 days, and for historical queries, the maximum time range is 366 days. |
|DetailField |Array of String |No |`["Domain"]` |The dimensions for data segmentation are not segmented by default. The supported dimensions are as follows:<br><br><br>* `Domain`: Domain name;<br><br>* `ISP`: Internet Service Provider;<br><br>* `Protocol`: Push\-pull streaming protocol.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Data segmentation by dimensions will only occur in the response if the <code>DetailField</code> parameter is used to specify dimensions for data segmentation and if at least one of the parameters <code>DomainList</code>, <code>ProtocolList</code>, or <code>ISPList</code> is provided with multiple values.</div><br> |


<span id="region"></span>
### Region


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Area |String |No |`CN` |The identifier for the major region in the regional information can be obtained by calling [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata). |
|Country |String |No |`CN` |The country identifier in the regional information can be obtained by calling [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata). When filtering by country, both `Area` and `Country` need to be passed in simultaneously. |
|Province |String |No |`beijing` |The province identifier in the regional information is currently not supported for countries or regions outside mainland China, Hong Kong, Macao, and Taiwan. You can obtain the identifier information by calling [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata). When filtering by province, you need to simultaneously pass in `Area`, `Country`, and `Province` |


<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|DomainList |Array of String |`["example.com"]` |List of domain names. |
|ProtocolList |Array of String |`["HTTP-FLV", "RTMP"]` |Push\-Pull Streaming Protocol, the protocol is described as follows:<br><br><br>* `HTTP-FLV`: HTTP\-based push\-pull streaming protocol, transmitting video format in FLV format.<br><br>* `HTTP-HLS`: HTTP\-based push\-pull streaming protocol, transmitting video format in TS format.<br><br>* `RTMP`: Real Time Message Protocol.<br><br>* `RTM`: Real Time Media, ultra\-low latency live streaming protocol.<br><br>* `SRT`: Secure Reliable Transport protocol.<br><br>* `QUIC`: Quick UDP Internet Connections, a new low\-latency Internet transmission protocol based on UDP.<br><br>* `CMAF`: A protocol for efficient, adaptive video streaming over HTTP. |
|ISPList |Array of String |`["telecom"]` |An array indicating Internet Service Provider (ISP) identifiers. Valid options include:<br><br><br>* `unicom`: China Unicom;<br><br>* `railcom`: China Railway Telecom;<br><br>* `telecom`: China Telecom;<br><br>* `mobile`: China Mobile;<br><br>* `cernet`: China Education and Research Network (CERNET);<br><br>* `tianwei`: China Tianwei;<br><br>* `alibaba`: Alibaba Group;<br><br>* `tencent`: Tencent Holdings;<br><br>* `drpeng`: Dr. Peng Telecom & Media Group;<br><br>* `btvn`: Broadcasting Television Network (BTVN);<br><br>* `huashu`: Huashu Media. |
|RegionList |Array of [Region](https://docs.byteplus.com/en/docs/24/20978#region-response) |`-` |List of regions to which CDN node IPs belong. |
|UserRegionList |Array of [Region](https://docs.byteplus.com/en/docs/24/20978#region-response) |`-` |List of regions to which client IPs belong. |
|StartTime |String |`2021-04-13T00:00:00Z` |The start time of your query's range in RFC 3339 format with second precision. |
|EndTime |String |`2021-04-14T00:00:00Z` |The end time of your query's range in RFC 3339 format with second precision. |
|Aggregation |Integer |`300` |Data granularity, measured in seconds. |
|DetailField |Array of String |`["Domain"]` |Dimensions for data segmentation, along with their descriptions, are as follows:<br><br><br>* `Domain`: Domain name;<br><br>* `ISP`: Internet Service Provider;<br><br>* `Protocol`: Push\-pull streaming protocol. |
|TotalUpTraffic |Float |`20` |The total upstream traffic within the query time range, measured in gigabytes (GB). |
|TotalDownTraffic |Float |`20` |The total downstream traffic within the query time range, measured in gigabytes (GB). |
|TrafficDataList |Array of [TrafficData](https://docs.byteplus.com/en/docs/24/20978#trafficdata) |`-` |All data for every time granularity. |
|TrafficDetailDataList |Array of [TrafficDetailData](https://docs.byteplus.com/en/docs/24/20978#trafficdetaildata) |`-` |Data segmented by dimensions.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Data segmentation by dimensions will only occur in the response if the <code>DetailField</code> parameter is used to specify dimensions for data segmentation and if at least one of the parameters <code>DomainList</code>, <code>ProtocolList</code>, or <code>ISPList</code> is provided with multiple values.</div><br> |


<span id="region-response"></span>
### Region


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Area |String |`CN` |The regional identifier in regional information. |
|Country |String |`CN` |The country identifier in the regional information. |
|Province |String |`beijing` |The province identifier in the regional information. |


<span id="trafficdata"></span>
### TrafficData


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|TimeStamp |String |`2022-04-13T00:00:00Z` |The start time of each time granularity when data is aggregated by time granularity, formatted in RFC3339 UTC time with second precision. |
|UpTraffic |Float |`20` |The total upstream traffic generated within the current data aggregation time granularity, measured in gigabytes (GB). |
|DownTraffic |Float |`20` |The total downstream traffic generated within the current data aggregation time granularity, measured in gigabytes (GB). |


<span id="trafficdetaildata"></span>
### TrafficDetailData


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Domain |String |`example.com` |Domain information when data is segmented by domain dimension. |
|Protocol |String |`HTTP-FLV` |Protocol information when data is segmented by push\-pull streaming protocol dimension. |
|ISP |String |`telecom` |Operator information when data is segmented by operator dimension. |
|TotalUpTraffic |Float |`0` |Total upstream traffic of the current dimension after data segmentation, measured in GB. |
|TotalDownTraffic |Float |`0` |Total downstream traffic of the current dimension after data segmentation, measured in GB. |
|TrafficDataList |Array of [TrafficData](https://docs.byteplus.com/en/docs/24/20978#trafficdata) |`-` |Data of all time granularities under the current dimension after data segmentation. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveTrafficData&Version=2023-01-01
{
    "DomainList": [
        "example.com"
    ],
    "ProtocolList": [
        "HTTP-FLV",
        "RTMP"
    ],
    "ISPList": [
        "telecom"
    ],
    "RegionList": [
        {
            "Area": "CN",
            "Country": "CN",
            "Province": "beijing"
        }
    ],
    "StartTime": "2021-04-13T00:00:00Z",
    "EndTime": "2021-04-14T00:00:00Z",
    "Aggregation": 300,
    "DetailField": [
        "Protocol"
    ]
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "DescribeLiveTrafficData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "cn-north-1"
    },
    "Result": {
        "DomainList": [
            "example.com"
        ],
        "ProtocolList": [
            "HTTP-FLV",
            "RTMP"
        ],
        "ISPList": [
            "telecom"
        ],
        "RegionList": [
            {
                "Area": "CN",
                "Country": "CN",
                "Province": "beijing"
            }
        ],
        "StartTime": "2021-04-13T00:00:00Z",
        "EndTime": "2021-04-14T00:00:00Z",
        "Aggregation": 300,
        "TotalUpTraffic": 20,
        "TotalDownTraffic": 20,
        "TrafficDataList": [
            {
                "TimeStamp": "2022-04-13T00:00:00Z",
                "UpTraffic": 20,
                "DownTraffic": 20
            },
            {
                "TimeStamp": "2022-04-13T00:05:00Z",
                "UpTraffic": 20,
                "DownTraffic": 20
            }
        ],
        "TrafficDetailDataList": [
            {
                "Protocol": "HTTP-FLV",
                "TotalUpTraffic": 20,
                "TotalDownTraffic": 20,
                "TrafficDataList": [
                    {
                        "TimeStamp": "2022-04-13T00:00:00Z",
                        "UpTraffic": 20,
                        "DownTraffic": 20
                    },
                    {
                        "TimeStamp": "2022-04-13T00:05:00Z",
                        "UpTraffic": 20,
                        "DownTraffic": 20
                    }
                ]
            },
            {
                "Protocol": "RTMP",
                "TotalUpTraffic": 0,
                "TotalDownTraffic": 0,
                "TrafficDataList": [
                    {
                        "TimeStamp": "2022-04-13T00:00:00Z",
                        "UpTraffic": 0,
                        "DownTraffic": 0
                    },
                    {
                        "TimeStamp": "2022-04-13T00:05:00Z",
                        "UpTraffic": 0,
                        "DownTraffic": 0
                    }
                ]
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
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/20978#request-parameters) description for inspection. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |


&nbsp;
