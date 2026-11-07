---
title: "DescribeLiveBatchStreamTrafficData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivebatchstreamtrafficdata-2023"
---

Call the `DescribeLiveBatchStreamTrafficData` API to query the upstream and downstream traffic data and its detailed data within the specified time range.

## Requirements

* Limitations:

   * Support querying traffic data under a specified domain name or protocol.

   * Support querying traffic data generated under deleted domain names.

* Rate limit: 30 queries per second per account.

* Data latency: the data latency is 15 minutes.

* Data metric: Traffic data is calculated in base 1000, for example, 1 GB = 1000 MB.

## HTTP request

* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=DescribeLiveBatchStreamTrafficData&Version=2023\-01\-01

## Request parameters

### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

### Query

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DescribeLiveBatchStreamTrafficData` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |

### Body parameters

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|DomainList |Array of String |No |`["push.example.com", "push2.example.com"]` |List of pull stream domains. By default, it is empty, indicating all domains will be queried. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or go to the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to obtain the pull stream domains to be queried. |
|ProtocolList |Array of String |No |`["HTTP-FLV", "RTMP"]` |Push\-Pull Streaming Protocol, the protocol is described as follows:<br><br><br>* `HTTP-FLV`: HTTP\-based push\-pull streaming protocol, transmitting video format in FLV format.<br><br>* `HTTP-HLS`: HTTP\-based push\-pull streaming protocol, transmitting video format in TS format.<br><br>* `RTMP`: Real Time Message Protocol.<br><br>* `RTM`: Real Time Media, ultra\-low latency live streaming protocol.<br><br>* `SRT`: Secure Reliable Transport protocol.<br><br>* `QUIC`: Quick UDP Internet Connections, a new low\-latency Internet transmission protocol based on UDP.<br><br>* `CMAF`: A protocol for efficient, adaptive video streaming over HTTP.<br><br><br>> **说明**<br><br><br><br>* > If querying the QUIC protocol, other protocols cannot be queried simultaneously.<br><br><br>* > By default, the total traffic data queried is the actual generated upstream and downstream traffic.<br><br><br>* > If a single protocol is passed in for query and the traffic of each protocol is summed up, the result will be greater than the actual total traffic.<br> |
|ISPList |Array of String |No |`["telecom"]` |Identifiers of operators providing network access services. By default, all operators are indicated. Supported operators are as follows.<br><br><br>* `unicom`: China Unicom;<br><br>* `railcom`: China Railway Telecom;<br><br>* `telecom`: China Telecom;<br><br>* `mobile`: China Mobile;<br><br>* `cernet`: China Education and Research Network (CERNET);<br><br>* `tianwei`: China Tianwei;<br><br>* `alibaba`: Alibaba Group;<br><br>* `tencent`: Tencent Holdings;<br><br>* `drpeng`: Dr. Peng Telecom & Media Group;<br><br>* `btvn`: China Broadcasting Network;<br><br>* `huashu`: Huashu Media.<br><br>   If you need to obtain the identifiers of various operators, you can call the [DescribeLiveISPData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveispdata). |
|RegionList |Array of [RegionList](https://docs.byteplus.com/en/docs/24/36093#regionlist) |No |`-` |List of regions to which CDN node IPs belong, by default indicating all regions.<br><br>> **说明**<br><br><br>> Parameters RegionList and UserRegionList are not supported simultaneously.<br> |
|UserRegionList |Array of [RegionList](https://docs.byteplus.com/en/docs/24/36093#regionlist) |No |`-` |List of regions to which client IPs belong, by default indicating all regions.<br><br>> **说明**<br><br><br>> Parameters RegionList and UserRegionList are not supported simultaneously.<br> |
|StartTime |String |Yes |`2021-04-13T00:00:00Z` |The start time of your query's range (UTC time in RFC 3339 format with second precision).<br><br>> **说明**<br><br><br>> The maximum time span for a single query is 24 hours, and the historical query time range is 366 days.<br> |
|EndTime |String |Yes |`2021-04-14T00:00:00Z` |The end time of your query's range (UTC time in RFC 3339 format with second precision). |
|PageNum |Integer |No |`1` |The page number. The value must be greater than or equal to `1`. Default value: `1`. |
|PageSize |Integer |No |`1000` |The number of query results per page. Valid values: [100,1000]. Default value: `1000`.<br><br>> **说明**<br><br><br>> If you set this parameter to `0`, the default value is used.<br> |

### RegionList

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Area |String |No |`CN` |The identifier for the major region in the regional information can be obtained by calling [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata). |
|Country |String |No |`CN` |The country identifier in the regional information can be obtained by calling [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata). When filtering by country, both 'Area' and 'Country' need to be passed in simultaneously. |
|Province |String |No |`beijing` |The province identifier in the regional information is currently not supported for countries or regions outside mainland China, Hong Kong, Macao, and Taiwan. You can obtain the identifier information by calling [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata). When filtering by province, you need to simultaneously pass in `Area`, `Country`, and `Province` |

## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|DomainList |Array of String |`["push.example.com", "push2.example.com"]` |List of domains. |
|ProtocolList |Array of String |`["RTMP"]` |Push\-Pull Streaming Protocol, the protocol is described as follows:<br><br><br>* `HTTP-FLV`: HTTP\-based push\-pull streaming protocol, transmitting video format in FLV format.<br><br>* `HTTP-HLS`: HTTP\-based push\-pull streaming protocol, transmitting video format in TS format.<br><br>* `RTMP`: Real Time Message Protocol.<br><br>* `RTM`: Real Time Media, ultra\-low latency live streaming protocol.<br><br>* `SRT`: Secure Reliable Transport protocol.<br><br>* `QUIC`: Quick UDP Internet Connections, a new low\-latency Internet transmission protocol based on UDP.<br><br>* `CMAF`: A protocol for efficient, adaptive video streaming over HTTP. |
|ISPList |Array of String |`["telecom"]` |Identifiers of operators providing network access services. |
|RegionList |Array of [RegionList](https://docs.byteplus.com/en/docs/24/36093#regionlist-response) |`-` |List of regions to which CDN node IPs belong. |
|UserRegionList |Array of [RegionList](https://docs.byteplus.com/en/docs/24/36093#regionlist-response) |`-` |List of regions to which client IPs belong. |
|StartTime |String |`2022-11-10T00:00:00Z` |The start time of the query in UTC time, formatted according to RFC3339, with precision to the second. |
|EndTime |String |`2022-11-11T00:00:00Z` |The end time of the query in UTC time, formatted according to RFC3339, with precision to the second. |
|TotalUpTraffic |Float |`40` |The total upstream traffic within the query time range, measured in gigabytes (GB). |
|TotalDownTraffic |Float |`40` |The total downstream traffic within the query time range, measured in gigabytes (GB). |
|StreamInfoList |Array of [StreamInfoList](https://docs.byteplus.com/en/docs/24/36093#streaminfolist) |`-` |Data segmented by stream. |
|Pagination |Object of [Pagination](https://docs.byteplus.com/en/docs/24/36093#pagination) |`-` |Page information. |

### RegionList

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Area |String |`CN` |The regional identifier in regional information. |
|Country |String |`CN` |The country identifier in the regional information. |
|Province |String |`beijing` |The province identifier in the regional information. |

### StreamInfoList

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Domain |String |`push.example.com` |Domain name. |
|App |String |`example_app` |The AppName field of a stream address. |
|Stream |String |`example_stream` |The StreamName field of a stream address. |
|UpTraffic |Float |`20` |The upstream traffic of the current stream, with the unit of GB. |
|DownTraffic |Float |`20` |The downstream traffic of the current stream, with the unit of GB. |

### Pagination

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|PageNum |Integer |`1` |The current page number. |
|PageSize |Integer |`1000` |The number of results on each page. |
|TotalCount |Integer |`2` |The total number of results. |

## Samples

### Sample request

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveBatchStreamTrafficData&Version=2023-01-01
{
    "StartTime": "2022-11-10T00:00:00Z",
    "EndTime": "2022-11-11T00:00:00Z"
}
```

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "DescribeLiveBatchStreamTrafficData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singpore-1"
    },
    "Result": {
        "StartTime": "2022-11-10T00:00:00Z",
        "EndTime": "2022-11-11T00:00:00Z",
        "TotalUpTraffic": 40,
        "TotalDownTraffic": 40,
        "StreamInfoList": [
            {
                "Domain": "push.example.com",
                "Stream": "example_stream",
                "App": "live",
                "UpTraffic": 20,
                "DownTraffic": 20
            },
            {
                "Domain": "push2.example.com",
                "Stream": "example_stream",
                "App": "live",
                "UpTraffic": 20,
                "DownTraffic": 20
            }
        ],
        "Pagination": {
            "PageNum": 1,
            "PageSize": 1000,
            "TotalCount": 2
        }
    }
}
```

## Error codes

The following are the error codes related to the current operation. For other error codes, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes).

|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|200 |CommonErr |\- |Uncategorized error. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980). |
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/36093#request-parameters) description for inspection. |
|400 |InvalidParam.BindError |Request parameter error, please check input data |The parameter failed validation. Please check if the data type is correct. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|404 |ResourceNotFound |\- |The resource (including domain name space, domain name, app name, configuration, and certificate) was not found. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980). |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980). |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980). |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980). |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |Internal Service is timeout. Please [contact support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980). |
