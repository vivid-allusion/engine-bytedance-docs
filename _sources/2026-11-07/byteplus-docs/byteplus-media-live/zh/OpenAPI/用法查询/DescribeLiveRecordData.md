---
title: "DescribeLiveRecordData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describeliverecorddata-zh-CN"
---

调用 `DescribeLiveRecordData` API，查询指定直播域名在指定时间范围内的录制用量，包括最大并发录制数。

<span id="Requirements"></span>
## 要求


* 计费情况：关于录制计费，请参阅 [Recording Billing](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-transcoding_2)。

* 限制：支持查询已删除域名产生的录制用量数据。

* 请求频率限制：每个账号每秒最多可查询30次。

* 数据延迟：7小时。


<span id="HTTP request"></span>
## HTTP请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DescribeLiveRecordData&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有API调用时，除API专属参数外，还需包含 [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveRecordData` |该API操作。 |
|Version |String |是 |`2023-01-01` |该API操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|DomainList |Array of String |否 |`["push.example.com"]` |域名列表。默认情况下为空，表示将查询你在 BytePlus MediaLive 下所有域名的录制用量数据。你可以调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail) API，或在 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 页面获取待查询的域名。 |
|StartTime |String |是 |`2021-04-13T00:00:00Z` |查询范围的起始时间，需采用RFC 3339格式，精确到秒。 |
|EndTime |String |是 |`2021-04-14T00:00:00Z` |查询范围的结束时间，需采用RFC 3339格式，精确到秒。 |
|Aggregation |Integer |否 |`300` |数据聚合的颗粒度，单位为秒，支持以下选项：<br><br><br>* `300`（默认）：5分钟。以5分钟为颗粒度聚合时，单次查询的最大时间跨度为31天，历史查询的最大时间范围为366天。<br><br>* `3600`：1小时。以1小时为颗粒度聚合时，单次查询的最大时间跨度为93天，历史查询的最大时间范围为366天。<br><br>* `86400`：1天。以1天为颗粒度聚合时，单次查询的最大时间跨度为93天，历史查询的最大时间范围为366天。 |
|DetailField |Array of String |否 |`["Domain"]` |数据分割的维度默认为空，表示不进行数据分割。目前仅支持按 `Domain` 维度进行数据分割。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">仅当 <code>DetailField</code> 参数设置为 <code>Domain</code> 且 <code>DomainList</code> 参数包含多个值时，才会按 <code>Domain</code> 维度进行数据分割。</div><br> |
|App |String |否 |`live` |直播流URL中的AppName字段。可包含大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和点（.），长度为1到30个字符。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">查询流颗粒度数据时，需同时填写 <code>App</code> 和 <code>Stream</code> 参数。</div><br> |
|Stream |String |否 |`example_stream` |直播流URL中的StreamName字段。可以包含大写和小写字母（A\-Z，a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和句点（.），长度范围为1到100个字符。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">查询流颗粒度数据时，必须同时提供<code>App</code>和<code>Stream</code>参数。</div><br> |


<span id="Response parameters"></span>
## 返回调用结果参数

如需了解API专属返回调用结果参数，请参见下表。更多详情请参阅 [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|DomainList |字符串数组 |`["push.example.com"]` |域名列表。 |
|StartTime |字符串 |`2021-04-13T00:00:00Z` |查询范围的起始时间，采用RFC 3339格式，精确到秒。 |
|EndTime |字符串 |`2021-04-14T00:00:00Z` |查询范围的结束时间，采用RFC 3339格式，精确到秒。 |
|Aggregation |整数 |`300` |数据颗粒度，单位为秒。 |
|DetailField |字符串数组 |`["Domain"]` |数据拆分维度目前仅限于`Domain`，表示域名。 |
|RecordPeak |整数 |`2` |当前查询条件下允许的最大并发录制流数量。 |
|RecordDataList |Array of [RecordDataList](https://docs.byteplus.com/en/docs/24/107045#recorddatalist) |`-` |所有时间颗粒度的数据。 |
|RecordDetailDataList |Array of [RecordDetailDataList](https://docs.byteplus.com/en/docs/24/107045#recorddetaildatalist) |`-` |已按特定维度分类的数据。 |
|App |字符串 |`live` |查询流颗粒度数据时的Stream的AppName字段。 |
|Stream |字符串 |`example_stream` |查询流颗粒度数据时的Stream的StreamName字段。 |


<span id="recorddatalist"></span>
### RecordDataList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|TimeStamp |字符串 |`2022-04-13T00:00:00Z` |按时间颗粒度聚合数据时，每个时间颗粒度的起始时间，采用RFC3339 UTC时间格式，精确到秒。 |
|Value |整数 |`1` |当前数据聚合时间颗粒度内的最大并发录制流数量。 |


<span id="recorddetaildatalist"></span>
### RecordDetailDataList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Domain |字符串 |`push.example.com` |按域名维度拆分数据时的域名信息。 |
|RecordPeak |整数 |`2` |按维度拆分数据后，当前维度下的最大并发录制流数量。 |
|RecordDataList |Array of [RecordDataList](https://docs.byteplus.com/en/docs/24/107045#recorddatalist) |`-` |按维度拆分数据后，当前维度下每个颗粒度的所有数据。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveRecordData&Version=2023-01-01
{
    "DomainList": [
        "push.example.com"
    ],
    "StartTime": "2021-04-13T00:00:00Z",
    "EndTime": "2021-04-13T00:10:00Z",
    "Aggregation": 300,
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
        "RequestId": "201806041104200100100***",
        "Action": "DescribeLiveRecordData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "DomainList": [
            "push.example.com"
        ],
        "StartTime": "2021-04-13T00:00:00Z",
        "EndTime": "2021-04-13T00:10:00Z",
        "Aggregation": 300,
        "DetailField": [
            "Domain"
        ],
        "RecordPeak": 2,
        "RecordDataList": [
            {
                "TimeStamp": "2021-04-13T00:00:00Z",
                "Value": 1
            },
            {
                "TimeStamp": "2021-04-13T00:05:00Z",
                "Value": 2
            }
        ],
        "RecordDetailDataList": [
            {
                "Domain": "push.example.com",
                "RecordPeak": 2,
                "RecordDataList": [
                    {
                        "TimeStamp": "2021-04-13T00:00:00Z",
                        "Value": 1
                    },
                    {
                        "TimeStamp": "2021-04-13T00:05:00Z",
                        "Value": 2
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
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/107045#request-parameters)接口行为进行检查。 |
|403 |RequestForbidden |*  |请求被拒绝，因为当前账号下没有请求的资源（资源包括域名空间、域名、App名称、配置和证书）。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
