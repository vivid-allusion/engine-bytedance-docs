---
title: "DescribeLiveSnapshotData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describelivesnapshotdata-zh-CN"
---

调用 `DescribeLiveSnapshotData` API，获取指定直播域名在指定时间范围内由截图功能生成的快照数量。

<span id="Requirements"></span>
## 要求


* 计费情况：有关截图价格，请参阅 [Screenshot capturing](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-screenshot-capturing)。

* 限制：支持查询指定域名（包括已删除域名）下所有直播截图任务生成的截图数量。

* 请求频率限制：每个账号每秒最多可查询 30 次。

* 数据延迟：15 分钟。


<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DescribeLiveSnapshotData&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用时，除了 API 专属参数外，还必须包含 [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### Query


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveSnapshotData` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|DomainList |Array of String |否 |`["push.example.com","push2.example.com"]` |域名列表。默认情况下为空，表示将查询你在 BytePlus MediaLive 下所有域名的快照用量数据。你可以调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail) API 或前往 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 页面获取待查询的域名。 |
|StartTime |String |是 |`2021-04-13T00:00:00Z` |查询范围的起始时间，采用 RFC 3339 格式，精确到秒。 |
|EndTime |String |是 |`2021-04-14T00:00:00Z` |查询范围的结束时间，采用 RFC 3339 格式，精确到秒。 |
|Aggregation |Integer |否 |`86400` |数据聚合的颗粒度，单位为秒，支持以下选项：<br><br><br>* `300`：5 分钟。以 5 分钟为颗粒度聚合时，单次查询的最大时间跨度为 31 天，历史查询的最大时间范围为 366 天。<br><br>* `3600`：1 小时。以 1 小时为颗粒度聚合时，单次查询的最大时间跨度为 93 天，历史查询的最大时间范围为 366 天。<br><br>* `86400`（默认）：1 天。以 1 天为颗粒度聚合时，单次查询的最大时间跨度为 93 天，历史查询的最大时间范围为 366 天。 |
|DetailField |Array of String |否 |`["Domain"]` |数据分割的维度默认为空，表示不进行数据分割。目前仅支持按 `Domain` 维度进行数据分割。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">仅当 <code>DetailField</code> 参数设置为 <code>Domain</code> 且 <code>DomainList</code> 参数包含多个值时，才会按 <code>Domain</code> 维度进行数据分割。</div><br> |
|App |String |否 |`live` |直播流 URL 中的 AppName 字段。可包含大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和点（.），长度为 1 到 30 个字符。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">查询流颗粒度数据时，需同时填写 <code>App</code> 和 <code>Stream</code> 参数。</div><br> |
|Stream |String |否 |`example_stream` |直播流 URL 中的 StreamName 字段。可以包含大写和小写字母（A\-Z，a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和句点（.），长度范围为1到100个字符。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">查询流颗粒度数据时，必须同时提供<code>应用</code>和<code>流</code>参数。</div><br> |


<span id="Response parameters"></span>
## 返回调用结果参数

有关唯一的 API 专属返回调用结果参数，请参见下表。更多详情请参阅 [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|DomainList |字符串数组 |`["push.example.com","push.example.com"]` |域名列表。 |
|StartTime |字符串 |`2021-04-13T00:00:00Z` |查询范围的起始时间，采用RFC 3339格式，精确到秒。 |
|EndTime |字符串 |`2021-04-14T00:00:00Z` |查询范围的结束时间，采用RFC 3339格式，精确到秒。 |
|Aggregation |整数 |`300` |数据颗粒度，单位为秒。 |
|DetailField |字符串数组 |`["Domain"]` |数据分割维度目前仅限于`Domain`，表示域名。 |
|Total |整数 |`19503380` |当前查询条件下的截图总数。 |
|SnapshotDataList |[SnapshotDataList](https://docs.byteplus.com/en/docs/24/107031#snapshotdatalist)数组 |`-` |所有时间颗粒度的数据。 |
|SnapshotDetailData |[SnapshotDetailData](https://docs.byteplus.com/en/docs/24/107031#snapshotdetaildata)数组 |`-` |已按维度分割的数据。 |
|应用 |字符串 |`live` |查询流颗粒度数据时的流的AppName字段。 |
|流 |字符串 |`example_stream` |查询流颗粒度数据时的流的StreamName字段。 |


<span id="snapshotdatalist"></span>
### SnapshotDataList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|TimeStamp |字符串 |`2022-04-13T00:00:00Z` |按时间颗粒度聚合数据时，每个时间颗粒度的起始时间，采用RFC3339 UTC时间格式，精确到秒。 |
|Value |整数 |`9503380` |当前数据聚合时间颗粒度内的截图总数。 |


<span id="snapshotdetaildata"></span>
### SnapshotDetailData


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Domain |字符串 |`push.example.com` |按域名维度分割数据时的域名信息。 |
|Total |整数 |`19503380` |按维度分割数据后当前维度的截图总数。 |
|SnapshotDataList |[SnapshotDataList](https://docs.byteplus.com/en/docs/24/107031#snapshotdatalist)数组 |`-` |按维度分割数据后当前维度下所有颗粒度的数据。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveSnapshotData&Version=2023-01-01
{
    "DomainList": [
        "push.example.com",
        "push2.example.com"
    ],
    "StartTime": "2022-03-07T00:00:00Z",
    "EndTime": "2022-03-08T00:00:00Z",
    "Aggregation": 86400,
    "DetailField": [
        "Domain"
    ]
}
```


<span id="Sample response"></span>
### 返回调用结果示例

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "DescribeLiveSnapshotData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "cn-north-1"
    },
    "Result": {
        "DomainList": [
            "push.example.com",
            "push2.example.com"
        ],
        "StartTime": "2022-03-07T00:00:00Z",
        "EndTime": "2022-03-08T00:00:00Z",
        "Aggregation": 86400,
        "DetailField": [
            "Domain"
        ],
        "Total": 19503380,
        "SnapshotDataList": [
            {
                "TimeStamp": "2022-03-07T00:00:00Z",
                "Value": 9503380
            },
            {
                "TimeStamp": "2022-03-08T00:00:00Z",
                "Value": 9507820
            }
        ],
        "SnapshotDetailData": [
            {
                "Domain": "push.example.com",
                "Total": 19503380,
                "SnapshotDataList": [
                    {
                        "TimeStamp": "2022-03-07T00:00:00Z",
                        "Value": 9503380
                    },
                    {
                        "TimeStamp": "2022-03-08T00:00:00Z",
                        "Value": 9507820
                    }
                ]
            },
            {
                "Domain": "push2.example.com",
                "Total": 19503380,
                "SnapshotDataList": [
                    {
                        "TimeStamp": "2022-03-07T00:00:00Z",
                        "Value": 9503380
                    },
                    {
                        "TimeStamp": "2022-03-08T00:00:00Z",
                        "Value": 9507820
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
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/107031#request-parameters)的接口行为进行检查。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
