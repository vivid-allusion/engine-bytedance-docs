---
title: "DescribeLiveStreamSessionData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describelivestreamsessiondata"
---

Call the `DescribeLiveStreamSessionData` API to query the request count and maximum online audience number of all live streams or specified live streams under the specified domain within the specified time range.

<span id="requirements"></span>
## Requirements


* Limitations: Supports querying the number of requests and maximum concurrent viewers for specific live domains (including deleted domains).

* Rate limit: 30 queries per second per account

* Data latency:

   * When the aggregation granularity is 60 seconds, the data latency is 5 minutes;

   * For other time granularities, the data latency is 15 minutes.


<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=DescribeLiveStreamSessionData&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DescribeLiveStreamSessionData` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|DomainList |Array of String |No |`["pull.example.com"]` |List of pull stream domains. By default, it is empty, indicating that request counts and online viewership data for all domains will be queried. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or visit the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to obtain the pull stream domains to be queried.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Either <code>DomainList</code> or <code>Domain</code> should be provided, not both.</div><br> |
|Domain |String |No |`pull.example.com` |The pull streaming domain is required when querying data at stream granularity, and both the `App` and `Stream` parameters must be provided. You can obtain the pull streaming domains to be queried by calling the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) interface or visiting the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When querying data for the number of requests and online users at stream granularity, the <code>Domain</code>, <code>App</code>, and <code>Stream</code> parameters must be specified simultaneously to specify the live stream.</div><br> |
|App |String |No |`example_app` |The AppName field in the live stream URL. It can include uppercase letters (A\-Z), lowercase letters (a\-z), numbers (0\-9), underscores (_), hyphens (\-), and periods (.), with a length ranging from 1 to 30 characters.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When querying the origin traffic monitoring data at the stream granularity, you must specify <code>Domain</code>, <code>App</code>, and <code>Stream</code> to identify the specific origin stream.</div><br> |
|Stream |String |No |`example_stream` |The StreamName field in the live stream URL. It can include uppercase letters (A\-Z), lowercase letters (a\-z), numbers (0\-9), underscores (_), hyphens (\-), and periods (.), with a length ranging from 1 to 100 characters.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When querying for the origin traffic monitoring data at the stream granularity, you must specify <code>Domain</code>, <code>App</code>, and <code>Stream</code> to identify the origin stream.</div><br> |
|ProtocolList |Array of String |No |`["HTTP-FLV", "RTMP"]` |Push\-pull streaming protocol. By default, all protocol types are indicated. Supported protocols are as follows.<br><br><br>* `HTTP-FLV`: A push\-pull streaming protocol based on the HTTP protocol, using the FLV format for video transmission.<br><br>* `HTTP-HLS`: A push\-pull streaming protocol based on the HTTP protocol, using the TS format for video transmission.<br><br>* `RTMP`: Real\-Time Messaging Protocol for real\-time message transmission.<br><br>* `RTM`: Real\-Time Media protocol for ultra\-low latency live streaming.<br><br>* `SRT`: Secure Reliable Transport protocol for secure and reliable streaming.<br><br>* `QUIC`: Quick UDP Internet Connections, a new low\-latency internet transmission protocol based on UDP.<br><br>* `CMAF`: Common Media Application Format, a versatile streaming protocol.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If querying the QUIC protocol, other protocols cannot be queried simultaneously.</div><br> |
|ISPList |Array of String |No |`["telecom"]` |Identifiers of operators providing network access services. By default, all operators are indicated. Supported operators are as follows.<br><br><br>* `unicom`: China Unicom;<br><br>* `railcom`: China Railway Telecom;<br><br>* `telecom`: China Telecom;<br><br>* `mobile`: China Mobile;<br><br>* `cernet`: China Education and Research Network (CERNET);<br><br>* `tianwei`: China Tianwei;<br><br>* `alibaba`: Alibaba Group;<br><br>* `tencent`: Tencent Holdings;<br><br>* `drpeng`: Dr. Peng Telecom & Media Group;<br><br>* `btvn`: China Broadcasting Network;<br><br>* `huashu`: Huashu Media.<br><br>   If you need to obtain the identifiers of various operators, you can call the [DescribeLiveISPData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveispdata). |
|RegionList |Array of [RegionList](https://docs.byteplus.com/en/docs/24/25098#regionlist) |No |`-` |List of regions to which CDN node IPs belong, by default indicating all regions. |
|Aggregation |Integer |No | |The granularity of data aggregation, measured in seconds, with the following supported options:<br><br><br>* `60`: 1 minute.<br><br>* `300`: (default) 5 minutes.<br><br>* `3600`: 1 hour. |
|DetailField |Array of String |No |`["Domain"]` |The dimensions for data breakdown are not split by default. The supported dimensions are as follows:<br><br><br>* `Domain`: The domain name;<br><br>* `ISP`: The Internet Service Provider;<br><br>* `Protocol`: The push\-pull streaming protocol.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Data segmentation by dimensions will only occur in the response if the <code>DetailField</code> parameter specifies the dimensions for breakdown and at least one of the following parameters is provided with multiple values: <code>DomainList</code>, <code>ProtocolList</code>, or <code>ISPList</code>.</div><br> |
|StartTime |String |Yes |`2021-04-13T00:00:00Z` |The start time of your query's range in RFC 3339 format with second precision.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The historical query time range is 366 days, and the maximum time span for a single query depends on DetailField and Aggregation. The relationships are described as follows.</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When no dimension splitting is performed or only one dimension is used to split the data:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">When the data is aggregated every 60 seconds, the maximum time span for a single query is 24 hours.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">When the data is aggregated every 300 seconds, the maximum time span for a single query is 31 days.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">When the data is aggregated every 3600 seconds, the maximum time span for a single query is 31 days.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When two or more dimensions are used to split the data:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">When the data is aggregated every 60 seconds, the maximum time span for a single query is 3 hours.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">When the data is aggregated every 300 seconds, the maximum time span for a single query is 24 hours.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">When the data is aggregated every 3600 seconds, the maximum time span for a single query is 7 days.</div><br> |
|EndTime |String |Yes |`2021-04-14T00:00:00Z` |The end time of your query's range in RFC 3339 format with second precision. |


<span id="regionlist"></span>
### RegionList


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Area |String |No |`CN` |The identifier for the major region in the regional information can be obtained by calling [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata). |
|Country |String |No |`CN` |The country identifier in the regional information can be obtained by calling [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata). When filtering by country, both 'Area' and 'Country' need to be passed in simultaneously. |
|Province |String |No |`beijing` |The province identifier in the regional information is currently not supported for countries or regions outside mainland China, Hong Kong, Macao, and Taiwan. You can obtain the identifier information by calling [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata). When filtering by province, you need to simultaneously pass in `Area`, `Country`, and `Province`. |


<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|DomainList |Array of String |`["push.example.com"]` |List of domains. |
|Domain |String |`pull.example.com` |Pull stream domain. |
|App |String |`live` |The AppName field in the live stream URL. |
|Stream |String |`example_stream` |The StreamName field in the live stream URL. |
|ProtocolList |Array of String |`["HTTP-FLV", "RTMP"]` |Push\-pull streaming protocol. By default, indicating all protocol types. Supported protocols are as follows.<br><br><br>* `HTTP-FLV`: A push\-pull streaming protocol based on the HTTP protocol, using the FLV format for video transmission.<br><br>* `HTTP-HLS`: A push\-pull streaming protocol based on the HTTP protocol, using the TS format for video transmission.<br><br>* `RTMP`: Real\-Time Messaging Protocol for real\-time message transmission.<br><br>* `RTM`: Real\-Time Media protocol for ultra\-low latency live streaming.<br><br>* `SRT`: Secure Reliable Transport protocol for secure and reliable streaming.<br><br>* `QUIC`: Quick UDP Internet Connections, a new low\-latency internet transmission protocol based on UDP.<br><br>* `CMAF`: Common Media Application Format, a versatile streaming protocol. |
|ISPList |Array of String |`["telecom", "unicom"]` |Identifiers of operators providing network access services. By default, all operators are included. Supported operators are as follows.<br><br><br>* `unicom`: China Unicom;<br><br>* `railcom`: China Railway Telecom;<br><br>* `telecom`: China Telecom;<br><br>* `mobile`: China Mobile;<br><br>* `cernet`: China Broadcasting Network;<br><br>* `tianwei`: China Tianwei;<br><br>* `alibaba`: Alibaba Group;<br><br>* `tencent`: Tencent Holdings;<br><br>* `drpeng`: Dr. Peng Telecom & Media Group;<br><br>* `btvn`: Broadcasting Television Network (BTVN);<br><br>* `huashu`: Huashu Media. |
|RegionList |Array of [RegionList](https://docs.byteplus.com/en/docs/24/25098#regionlist-response) |`-` |List of regions to which CDN node IPs belong. |
|StartTime |String |`2021-04-13T00:00:00Z` |The start time of your query's range in RFC 3339 format with second precision. |
|EndTime |String |`2021-04-14T00:00:00Z` |The end time of your query's range in RFC 3339 format with second precision. |
|Aggregation |Integer |`300` |Data granularity, measured in seconds. |
|DetailField |Array of String |`["Domain"]` |Data segmentation dimensions:<br><br><br>* `Domain`: The domain name.<br><br>* `ISP`: The Internet Service Provider.<br><br>* `Protocol`: The push\-pull streaming protocol. |
|TotalRequest |Integer |`20` |The total number of requests within the specified query time range. |
|PeakOnlineUser |Integer |`20` |The peak number of concurrent users within the specified query time range. |
|TotalHitRate |Double |`13.45` |The overall edge request hit rate across all domains and protocols during the specified time range. This is used to evaluate the effectiveness of the edge request caching mechanism in reducing the load on the origin servers. |
|SessionDataList |Array of [SessionDataList](https://docs.byteplus.com/en/docs/24/25098#sessiondatalist) |`-` |Data for all time granularities. |
|SessionDetailDataList |Array of [SessionDetailDataList](https://docs.byteplus.com/en/docs/24/25098#sessiondetaildatalist) |`-` |Data segmented by specific dimensions. |


<span id="regionlist-response"></span>
### RegionList


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Area |String |`CN` |The regional identifier in regional information. |
|Country |String |`CN` |The country identifier in the regional information. |
|Province |String |`beijing` |The province identifier in the regional information. |


<span id="sessiondatalist"></span>
### SessionDataList


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|TimeStamp |String |`2022-04-13T00:00:00Z` |The start time of each time granularity when data is aggregated by time granularity, formatted in RFC3339 UTC time with second precision. |
|Request |Integer |`10` |The number of requests within the current data aggregation time granularity. |
|OnlineUser |Integer |`20` |The peak number of online users within the current data aggregation time granularity. |
|HitRate |Double |`13.45` |Edge request hit rate at specified granularity (e.g., every 60 seconds or every 5 minutes). |


<span id="sessiondetaildatalist"></span>
### SessionDetailDataList


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Domain |String |`pull.example.com` |Domain information when data is split by domain dimension. |
|Protocol |String |`HTTP-FLV` |Protocol information for data segmentation by streaming protocol. |
|ISP |String |`telecom` |ISP information when data is split by ISP dimension. |
|TotalRequest |Integer |`20` |Number of requests for the current dimension after data segmentation. |
|PeakOnlineUser |Integer |`20` |Peak number of online users for the current dimension after data segmentation. |
|TotalHitRate |Float |`13.45` |After the data is split by specific dimensions (such as `Domain`), the overall edge request hit rate for each dimension within the specified query time range. This metric is used to assess the caching efficiency across different data segments. |
|SessionDataList |Array of [SessionDataList](https://docs.byteplus.com/en/docs/24/25098#sessiondatalist) |`-` |All time granularity data for the current dimension after data segmentation. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveStreamSessionData&Version=2023-01-01
{
    "Domain": "pull.example.com",
    "App": "example_app",
    "Stream": "example_stream",
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
    "DetailField": [
        "Domain"
    ]
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeLiveStreamSessionData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Domain": "pull.example.com",
        "App": "live",
        "Stream": "example_stream",
        "ProtocolList": [
            "HTTP-FLV",
            "RTMP"
        ],
        "ISPList": [
            "telecom",
            "unicom"
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
            "Domain"
        ],
        "TotalRequest": 20,
        "PeakOnlineUser": 20,
        "TotalHitRate": 13.41,
        "SessionDataList": [
            {
                "TimeStamp": "2022-04-13T00:00:00Z",
                "Request": 10,
                "OnlineUser": 20,
                "HitRate": 13.41
            }
        ],
        "SessionDetailDataList": [
            {
                "Protocol": "HTTP-FLV",
                "Domain": "pull.example.com",
                "ISP": "telecom",
                "TotalRequest": 20,
                "PeakOnlineUser": 20,
                "SessionDataList": [
                    {
                        "TimeStamp": "2022-04-13T00:00:00Z",
                        "Request": 20,
                        "OnlineUser": 20,
                        "HitRate": 13.41
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
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/25098#request-parameters) description for inspection. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |


&nbsp;
