---
title: "DescribeLivePullToPushBandwidthData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describelivepulltopushbandwidthdata-zh-CN"
---

调用 `DescribeLivePullToPushBandwidthData` API 查询指定时间范围内生成的拉流转推任务的带宽使用情况。

<span id="Requirements"></span>
## 要求


* 计费情况：关于推流至第三方时拉流转推带宽的计费，请参见 [Relay](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-relay-1)。

* 频率限制：每个账号每秒最多查询 30 次

* 数据延迟：15 分钟

* 数据指标：带宽数据以 1000 为基数计算，例如 1 Mbps = 1000 Kbps。


<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DescribeLivePullToPushBandwidthData&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用除了需传入 API 专属参数外，还必须包含 [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### Query


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLivePullToPushBandwidthData` |API 操作名。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本号。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|GroupList |Array of String |否 |`["group001","group002"]` |拉流转推任务组列表。默认值为空，表示查询所有拉流转推任务的带宽使用情况。 |
|StartTime |String |是 |`2021-04-13T00:00:00Z` |查询范围的起始时间，RFC 3339 格式，精确到秒。 |
|EndTime |String |是 |`2021-04-14T00:00:00Z` |查询范围的结束时间，RFC 3339 格式，精确到秒。 |
|Aggregation |Integer |否 |`300` |数据聚合的颗粒度，单位为秒，支持以下选项：<br><br><br>* `300`（默认）：5 分钟。以 5 分钟为聚合间隔时，单次查询的最大时间跨度为 31 天，历史查询最大时间范围为 366 天。<br><br>* `3600`：1 小时。以 1 小时为聚合间隔时，单次查询的最大时间跨度为 93 天，历史查询最大时间范围为 366 天。<br><br>* `86400`：1 天。以 1 天为聚合间隔时，单次查询的最大时间跨度为 93 天，历史查询最大时间范围为 366 天。 |
|DetailField |Array of String |否 |`["Group"]` |数据分组的维度默认为空，表示不进行数据分组。当前仅支持按 `Group` 维度进行数据分组。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">仅当 <code>DetailField</code> 参数设置为 <code>Group</code> 且 <code>GroupList</code> 参数包含多个值时，才会按 <code>Group</code> 维度进行数据分组。</div><br> |


<span id="Response parameters"></span>
## 返回参数

关于 API 专属的唯一返回参数，请参见下表。更多详情请参见 [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|StartTime |String |`2021-04-13T00:00:00Z` |查询范围的起始时间，RFC 3339 格式，精确到秒。 |
|EndTime |String |`2021-04-14T00:00:00Z` |查询范围的结束时间，RFC 3339 格式，精确到秒。 |
|Aggregation |Integer |`300` |数据颗粒度，单位为秒。 |
|DetailField |Array of String |`["Group"]` |数据分组维度目前仅支持 `Group`，表示组名。 |
|PeakUpBandwidth |Float |`12` |当前查询条件下拉流和推流的带宽峰值，单位为 Mbps。 |
|BandwidthDataList |[BandwidthDataList](https://docs.byteplus.com/en/docs/24/107038#bandwidthdatalist) 数组 |`-` |所有时间颗粒度下的数据。 |
|BandwidthDetailDataList |[BandwidthDetailDataList](https://docs.byteplus.com/en/docs/24/107038#bandwidthdetaildatalist) 数组 |`-` |按维度分割后的数据。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">仅当对应维度参数输入多个值时，数据才会按指定维度分割返回。</div><br> |
|GroupList |字符串数组 |`["group001"]` |分组名称列表。 |


<span id="bandwidthdatalist"></span>
### BandwidthDataList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|TimeStamp |字符串 |`2022-04-13T00:00:00Z` |按时间颗粒度聚合数据时，每个时间颗粒度的起始时间，格式为 RFC3339 UTC 时间，精确到秒。 |
|UpBandwidth |浮点型 |`12.0` |当前数据聚合时间颗粒度内拉流和推流的带宽峰值，单位为 Mbps。 |


<span id="bandwidthdetaildatalist"></span>
### BandwidthDetailDataList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Group |字符串 |`group001` |按分组维度分割数据时的分组信息。 |
|PeakUpBandwidth |浮点型 |`12.0` |指定维度时间范围内拉流和推流的带宽峰值，单位为 Mbps。 |
|BandwidthDataList |[BandwidthDataList](https://docs.byteplus.com/en/docs/24/107038#bandwidthdatalist) 数组 |`-` |当前维度分割后每个颗粒度下的全部数据。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=DescribeLivePullToPushBandwidthData&Version=2023-01-01
{
    "GroupList": [
        "group001"
    ],
    "StartTime": "2021-04-13T00:00:00Z",
    "EndTime": "2021-04-14T00:00:00Z",
    "Aggregation": 300,
    "DetailField": [
        "Group"
    ]
}
```


<span id="Sample response"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "DescribeLivePullToPushBandwidthData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "GroupList": [
            "group001"
        ],
        "StartTime": "2021-04-13T00:00:00Z",
        "EndTime": "2021-04-14T00:00:00Z",
        "Aggregation": 300,
        "DetailField": [
            "Group"
        ],
        "PeakUpBandwidth": 12,
        "BandwidthDataList": [
            {
                "TimeStamp": "2022-04-13T00:00:00Z",
                "UpBandwidth": 12
            },
            {
                "TimeStamp": "2022-04-13T00:00:05Z",
                "UpBandwidth": 10
            }
        ],
        "BandwidthDetailDataList": [
            {
                "DstAddrType": "Live",
                "PeakUpBandwidth": 12,
                "BandwidthDataList": [
                    {
                        "TimeStamp": "2022-04-13T00:00:00Z",
                        "UpBandwidth": 12
                    },
                    {
                        "TimeStamp": "2022-04-13T00:00:05Z",
                        "UpBandwidth": 10
                    }
                ]
            },
            {
                "DstAddrType": "Third",
                "PeakUpBandwidth": 12,
                "BandwidthDataList": [
                    {
                        "TimeStamp": "2022-04-13T00:00:00Z",
                        "UpBandwidth": 12
                    },
                    {
                        "TimeStamp": "2022-04-13T00:00:05Z",
                        "UpBandwidth": 10
                    }
                ]
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为当前操作相关的错误码。其他错误码请参见 [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/107038#request-parameters)接口行为进行检查。 |
|403 |RequestForbidden |*  |请求被拒绝，因为当前账号下无请求资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
