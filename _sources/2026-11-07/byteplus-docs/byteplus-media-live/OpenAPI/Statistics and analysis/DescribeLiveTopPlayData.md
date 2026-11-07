---
title: "DescribeLiveTopPlayData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivetopplaydata-2023"
---

Call the `DescribeLiveTopPlayData` API to query traffic and bandwidth details for the top live streams or top domains within a specified time range.

## Requirements

* Rate limit: 30 queries per second per account

* Data latency: Data from the previous day can be queried after 07:00 on the current day.

* Data metric:

   * Bandwidth data is calculated in base 1000, for example, 1 Mbps = 1000 Kbps.

   * Traffic data is calculated in base 1000, for example, 1 GB = 1000 MB.

## HTTP request

* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=DescribeLiveTopPlayData&Version=2023\-01\-01

## Request parameters

### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

### Query

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DescribeLiveTopPlayData` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |

### Body parameters

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|StartTime |String |Yes |`2024-11-16T00:00:00Z` |The start time of the query in UTC time, formatted according to RFC3339, with precision to the second.<br><br>> **说明**<br><br><br><br>* > The maximum period for a single query is 31 days.<br><br><br>* > The maximum historical query range is 366 days.<br><br><br>* > Bandwidth and traffic data are aggregated hourly. We recommend that the query start and end times cover full\-hour intervals for the period you wish to query.<br> |
|EndTime |String |Yes |`2024-11-20T00:00:00Z` |The end time of the query in UTC time, formatted according to RFC3339, with precision to the second. |
|QueryType |String |No |`Stream` |Query type, enumerated values:<br><br><br>* `Domain`: query traffic and bandwidth details for the top domains.<br><br>* `Stream` (default): query traffic and bandwidth details for the top live streams. |
|SortBy |String |No |`PeakBandwidth` |Sorting criteria, enumerated values:<br><br><br>* `PeakBandwidth` (default): query in descending order of peak bandwidth.<br><br>* `AvgBandwidth`: query in descending order of average bandwidth.<br><br>* `TotalTraffic`: query in descending order of total traffic.<br><br><br>> **说明**<br><br><br>> This API sorts the results in descending order by the specified metric and returns the corresponding ranking range based on `PageNum` and `PageSize`.<br> |
|VhostList |Array of String |No |`["push.example.com"]` |Domain name space list. The default is null, indicating to query all name spaces. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or navigate to the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus console to retrieve the domain name space information. |
|DomainList |Array of String |No |`["push.example.com"]` |Domain list. The default value is null, indicating to query all domains.<br><br>You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or navigate to the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus console to retrieve the domain information. |
|PageSize |Integer |No |`10` |The number of query results per page. Valid values: [1,1000]. Default value: `10`.<br><br>> **说明**<br><br><br>> If you set this parameter to `0`, the default value is used.<br> |
|PageNum |Integer |No |`1` |The page number. The value must be greater than or equal to `1`. Default value: `1`. |

## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|StartTime |String |`2024-11-16T00:00:00Z` |The start time of the query in UTC time, formatted according to RFC3339, with precision to the second. |
|EndTime |String |`2024-11-20T00:00:00Z` |The end time of the query in UTC time, formatted according to RFC3339, with precision to the second. |
|QueryType |String |`Stream` |Query type, enumeration values:<br><br><br>* `Domain`: query traffic and bandwidth details for the top domains.<br><br>* `Stream` (default): query traffic and bandwidth details for the top live streams. |
|SortBy |String |`PeakBandwidth` |Sorting criteria, enumerated values：<br><br><br>* `PeakBandwidth` (default): query in descending order of peak bandwidth.<br><br>* `AvgBandwidth`: query in descending order of average bandwidth.<br><br>* `TotalTraffic`: query in descending order of total traffic. |
|VhostList |Array of String |`["push.example.com"]` |Domain name space list. |
|DomainList |Array of String |`["push.example.com"]` |Domain list. |
|DataItemList |Array of [DataItemList](https://docs.byteplus.com/en/docs/24/36022#dataitemlist) |`-` |Detailed data on bandwidth and traffic. |
|Pagination |Object of [Pagination](https://docs.byteplus.com/en/docs/24/36022#pagination) |`-` |Pagination information for the query results. |

### DataItemList

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Domain |String |`push.example.com` |Domain name. |
|App |String |`live` |The AppName field in the live stream URL. Leave this field empty when querying by Domain. |
|Stream |String |`example_stream` |The StreamName field in the live stream URL. Leave this field empty when querying by Domain. |
|PeakBandwidth |Float |`1000` |Peak bandwidth, measured in bps. |
|AvgBandwidth |Float |`1000` |Average bandwidth, measured in bps. |
|TotalTraffic |Float |`1000` |Total traffic, measured in Bytes. |

### Pagination

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|PageSize |Integer |`10` |Number of data entries displayed per page. |
|PageNum |Integer |`1` |Current page number in pagination. |
|TotalCount |String |`20` |Total number of data entries in the query results. |

## Samples

### Sample request

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveTopPlayData&Version=2023-01-01
{
    "StartTime": "2024-11-16T00:00:00Z",
    "EndTime": "2024-11-20T00:00:00Z",
    "QueryType": "Stream",
    "SortBy": "PeakBandwidth",
    "VhostList": [
        "push.example.com"
    ],
    "DomainList": [
        "push.example.com"
    ],
    "PageSize": 10,
    "PageNum": 1
}
```

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeLiveTopPlayData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "StartTime": "2024-11-16T00:00:00Z",
        "EndTime": "2024-11-20T00:00:00Z",
        "QueryType": "Stream",
        "SortBy": "PeakBandwidth",
        "VhostList": [
            "push.example.com"
        ],
        "DomainList": [
            "push.example.com"
        ],
        "DataItemList": [
            {
                "Domain": "push.example.com",
                "App": "live",
                "Stream": "example_stream",
                "PeakBandwidth": 1000,
                "AvgBandwidth": 1000,
                "TotalTraffic": 1000
            }
        ],
        "Pagination": {
            "PageSize": 10,
            "PageNum": 1,
            "TotalCount": "20"
        }
    }
}
```

## Error codes

The following are the error codes related to the current operation. For other error codes, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes).

|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/36022#request-parameters) description for inspection. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980). |
