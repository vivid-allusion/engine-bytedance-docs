---
title: "DescribeLivePullToPushData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describelivepulltopushdata-zh-CN"
---

调用`DescribeLivePullToPushData` API，在指定时间范围内查询该分组下所有拉流转推任务的时长用量。

<span id="Requirements"></span>
## 要求


* 计费情况：关于拉流转推的计费，请参见[Relay](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-relay-1)。

* 频率限制：每个账号每秒最多查询 30 次

* 数据延迟：

   * 当聚合颗粒度为 60 秒时，数据延迟为 5 分钟；

   * 其他时间颗粒度下，数据延迟为 15 分钟。


<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DescribeLivePullToPushData&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用除需传入各自的 API 专属参数外，还必须携带[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLivePullToPushData` |API 操作名。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本号。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|GroupList |Array of String |否 |`["group001"]` |拉流转推任务分组列表。默认值为空，表示查询所有拉流转推任务的时长用量。 |
|StartTime |String |是 |`2022-03-07T00:00:00Z` |查询范围的起始时间，RFC 3339 格式，精确到秒。 |
|EndTime |String |是 |`2021-04-14T00:00:00Z` |查询范围的结束时间，RFC 3339 格式，精确到秒。 |
|Aggregation |Integer |否 |`3600` |数据聚合颗粒度，单位为秒，支持以下选项：<br><br><br>* `60`：1 分钟。以 1 分钟为颗粒度聚合时，单次查询的最大时间跨度为 24 小时，历史查询时间范围为 366 天；<br><br>* `3600`：1 小时。以 1 小时为颗粒度聚合时，单次查询的最大时间跨度为 93 天，历史查询的最大时间范围为 366 天。<br><br>* `86400`：（默认）1 天。以 1 天为颗粒度聚合时，单次查询的最大时间跨度为 93 天，历史查询的最大时间范围为 366 天。 |
|DetailField |Array of String |否 |`["Group"]` |数据分割维度默认为空，表示不进行数据分割。当前仅支持按`Group`维度进行数据分割。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">仅当<code>DetailField</code>参数设置为<code>Group</code>，且<code>GroupList</code>参数包含多个值时，才会按<code>Group</code>维度进行数据分割。</div><br> |
|应用 |String |否 |`live` |直播流 URL 中的 AppName 字段。可包含大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和点（.），长度为 1~30 个字符。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">查询流颗粒度数据时，<code>应用</code>和<code>流</code>参数均为必填。</div><br> |
|流 |String |否 |`example_stream` |直播流 URL 中的 StreamName 字段。可包含大写和小写字母（A\-Z，a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和点（.），长度为 1~100 个字符。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">在查询流颗粒度数据时，必须同时提供<code>应用</code>和<code>流</code>参数。</div><br> |


<span id="Response parameters"></span>
## 返回参数

关于 API 专属的唯一返回参数，请参见下表。更多详情请参见[请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|StartTime |String |`2021-04-13T00:00:00Z` |查询的起始时间，采用UTC时间，格式为RFC3339，精确到秒。 |
|EndTime |String |`2021-04-14T00:00:00Z` |查询的结束时间，采用UTC时间，格式为RFC3339，精确到秒。 |
|Aggregation |Integer |`300` |数据颗粒度，单位为秒。 |
|DetailField |Array of String |`["Group"]` |数据拆分维度目前仅支持`Group`，表示分组名称。 |
|TotalDuration |Float |`6` |当前查询条件下拉流和推流的总时长，单位为分钟。 |
|PullToPushDataList |Array of [PullToPushDataList](https://docs.byteplus.com/en/docs/24/107017#pulltopushdatalist) |`-` |所有颗粒度的数据。 |
|PullToPushDetailDataList |Array of [PullToPushDetailDataList](https://docs.byteplus.com/en/docs/24/107017#pulltopushdetaildatalist) |`-` |按维度拆分的数据。 |
|应用 |String |`live` |查询流颗粒度数据时的流名称对应的AppName。 |
|流 |String |`example_stream` |查询流颗粒度数据时的流名称对应的StreamName。 |
|GroupList |Array of String |`["group001"]` |分组名称列表。 |


<span id="pulltopushdatalist"></span>
### PullToPushDataList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|TimeStamp |String |`2022-04-13T00:00:00Z` |按时间颗粒度聚合数据时，每个时间颗粒度的起始时间，采用RFC3339 UTC时间格式，精确到秒。 |
|Value |Float |`99` |当前数据聚合时间颗粒度内拉流和推流的总时长，单位为分钟。 |


<span id="pulltopushdetaildatalist"></span>
### PullToPushDetailDataList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Group |String |`group001` |按分组维度拆分数据时的分组信息。 |
|TotalDuration |Float |`99` |按维度拆分数据后，当前维度下拉流和推流的总时长，单位为分钟。 |
|PullToPushDataList |Array of [PullToPushDataList](https://docs.byteplus.com/en/docs/24/107017#pulltopushdatalist) |`-` |按维度拆分数据后，当前维度下所有颗粒度的数据。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=DescribeLivePullToPushData&Version=2023-01-01
{
    "GroupList": [
        "group001"
    ],
    "StartTime": "2022-03-07T00:00:00Z",
    "EndTime": "2022-03-08T00:00:00Z",
    "Aggregation": 86400,
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
        "RequestId": "201806041104200100****",
        "Action": "DescribeLivePullToPushData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "GroupList": [
            "group001"
        ],
        "StartTime": "2022-03-07T00:00:00Z",
        "EndTime": "2022-03-08T00:00:00Z",
        "Aggregation": 86400,
        "DetailField": [
            "Group"
        ],
        "TotalDuration": 6,
        "PullToPushDataList": [
            {
                "TimeStamp": "2022-03-07T00:00:00Z",
                "Value": 99
            }
        ],
        "PullToPushDetailDataList": [
            {
                "Group": "group001",
                "TotalDuration": 6,
                "PullToPushDataList": [
                    {
                        "TimeStamp": "2022-03-07T00:00:00Z",
                        "Value": 99
                    }
                ]
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为与当前操作相关的错误码。其他错误码请参见[BytePlus OpenAPI 通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/107017#request-parameters)接口行为进行检查。 |
|403 |RequestForbidden |*  |请求被拒绝，因为当前账号下没有请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
