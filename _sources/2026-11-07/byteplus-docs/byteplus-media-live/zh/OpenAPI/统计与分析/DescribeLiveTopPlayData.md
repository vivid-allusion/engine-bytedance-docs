---
title: "DescribeLiveTopPlayData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivetopplaydata-2023-zh-CN"
---

调用 `DescribeLiveTopPlayData` API，查询指定时间范围内热门直播流或热门域名的流量和带宽详情。

## 要求

* 速率限制：每个账号每秒 30 次查询

* 数据延迟：前一天的数据可在当天 07:00 后查询。

* 数据指标：

   * 带宽数据按 1000 进制计算，例如，1 Mbps = 1000 Kbps。

   * 流量数据按 1000 进制计算，例如，1 GB = 1000 MB。

## HTTP 请求

* 方法：POST

* 端点：https://open.byteplusapi.com/?Action=DescribeLiveTopPlayData&Version=2023\-01\-01

## 请求参数

### 公共参数

调用所有 API 时，除 API 特定参数外，还必须传入[公共参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

### 查询参数

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveTopPlayData` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。当前版本：2023\-01\-01。 |

### 请求体参数

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|StartTime |String |是 |`2024-11-16T00:00:00Z` |查询的开始时间，采用 UTC 时间，并按 RFC3339 格式表示，精度为秒。<br><br>> **说明**<br><br><br><br>* > 单次查询的最大时间范围为 31 天。<br><br><br>* > 最大历史查询范围为 366 天。<br><br><br>* > 带宽和流量数据按小时聚合。建议查询的开始时间和结束时间覆盖要查询时段的整点区间。<br> |
|EndTime |String |是 |`2024-11-20T00:00:00Z` |查询的结束时间，采用 UTC 时间，并按 RFC3339 格式表示，精度为秒。 |
|QueryType |String |否 |`Stream` |查询类型，取值：<br><br><br>* `Domain`：查询热门域名的流量和带宽详情。<br><br>* `Stream`（默认）：查询热门直播流的流量和带宽详情。 |
|SortBy |String |否 |`PeakBandwidth` |排序条件，取值：<br><br><br>* `PeakBandwidth`（默认）：按峰值带宽降序查询。<br><br>* `AvgBandwidth`：按平均带宽降序查询。<br><br>* `TotalTraffic`：按总流量降序查询。<br><br><br>> **说明**<br><br><br>> 此 API 会按指定指标对结果进行降序排序，并根据 `PageNum` 和 `PageSize` 返回对应的排名范围。<br> |
|VhostList |Array of String |否 |`["push.example.com"]` |域名空间列表。默认值为 null，表示查询所有域名空间。你可以调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或前往 BytePlus 控制台的[域名](https://console.byteplus.com/live/main/domain/list)页面获取域名空间信息。 |
|DomainList |Array of String |否 |`["push.example.com"]` |域名列表。默认值为 null，表示查询所有域名。<br><br>你可以调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或前往 BytePlus 控制台的[域名](https://console.byteplus.com/live/main/domain/list)页面获取域名信息。 |
|PageSize |Integer |否 |`10` |每页的查询结果数量。取值范围：[1,1000]。默认值：`10`。<br><br>> **说明**<br><br><br>> 如果将此参数设置为 `0`，则使用默认值。<br> |
|PageNum |Integer |否 |`1` |页码。取值必须大于或等于 `1`。默认值：`1`。 |

## 响应参数

API 特定的唯一响应参数见下表。更多详情，请参见[请求响应](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|StartTime |String |`2024-11-16T00:00:00Z` |查询的开始时间，采用 UTC 时间，并按 RFC3339 格式表示，精度为秒。 |
|EndTime |String |`2024-11-20T00:00:00Z` |查询的结束时间，采用 UTC 时间，并按 RFC3339 格式表示，精度为秒。 |
|QueryType |String |`Stream` |查询类型，取值：<br><br><br>* `Domain`：查询热门域名的流量和带宽详情。<br><br>* `Stream`（默认）：查询热门直播流的流量和带宽详情。 |
|SortBy |String |`PeakBandwidth` |排序条件，取值：<br><br><br>* `PeakBandwidth`（默认）：按峰值带宽降序查询。<br><br>* `AvgBandwidth`：按平均带宽降序查询。<br><br>* `TotalTraffic`：按总流量降序查询。 |
|VhostList |Array of String |`["push.example.com"]` |域名空间列表。 |
|DomainList |Array of String |`["push.example.com"]` |域名列表。 |
|DataItemList |Array of [DataItemList](https://docs.byteplus.com/en/docs/24/106985#dataitemlist) |`-` |带宽和流量的详细数据。 |
|Pagination |Object of [Pagination](https://docs.byteplus.com/en/docs/24/106985#pagination) |`-` |查询结果的分页信息。 |

### DataItemList

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|Domain |String |`push.example.com` |域名。 |
|App |String |`live` |直播流 URL 中的 AppName 字段。按 Domain 查询时，请将此字段留空。 |
|Stream |String |`example_stream` |直播流 URL 中的 StreamName 字段。按 Domain 查询时，请将此字段留空。 |
|PeakBandwidth |Float |`1000` |峰值带宽，单位为 bps。 |
|AvgBandwidth |Float |`1000` |平均带宽，单位为 bps。 |
|TotalTraffic |Float |`1000` |总流量，单位为 Bytes。 |

### Pagination

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|PageSize |Integer |`10` |每页显示的数据条目数。 |
|PageNum |Integer |`1` |分页中的当前页码。 |
|TotalCount |String |`20` |查询结果中的数据条目总数。 |

## 示例

### 示例请求

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

### 示例响应

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

## 错误码

以下是与当前操作相关的错误码。其他错误码，请参见 [BytePlus OpenAPI 公共错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|状态码 |错误码 |错误信息 |描述 |
|---|---|---|---|
|400 |InvalidParam |\- |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/106985#request-parameters)说明进行检查。 |
|403 |RequestForbidden |\- |请求被拒绝，因为当前账号下没有请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|500 |InternalError |an internal error occurred, please contact the administrator. |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
