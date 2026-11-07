---
title: "DescribeLiveStorageSpaceData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describelivestoragespacedata-zh-CN"
---

调用 `DescribeLiveStorageSpaceData` API，在指定时间范围内按天查询直播时移功能的存储空间使用情况。

<span id="Requirements"></span>
## 要求


* 频率限制：每个账号每秒最多查询100次

* 数据延迟：每日8:00后可查询前一天的数据。

* 数据指标：存储容量数据以二进制1024倍数计量，例如，1 GB = 1024 MB。


<span id="HTTP request"></span>
## HTTP请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DescribeLiveStorageSpaceData&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有API调用时，除API专属参数外，还需包含[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveStorageSpaceData` |API操作。 |
|Version |String |是 |`2023-01-01` |本API操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### 请求体参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Aggregation |Integer |否 |`86400` |时间颗粒度参数，单位为秒，支持配置为86400，表示一天的时间间隔。单次查询的时间跨度为93天，历史查询时间范围为366天。 |
|StartTime |String |是 |`2022-02-11T00:00:00Z` |查询范围的起始时间，采用RFC 3339格式，精确到秒。 |
|EndTime |String |是 |`2022-02-17T23:59:59Z` |查询范围的结束时间，采用RFC 3339格式，精确到秒。 |
|Buckets |Array of String |否 |`["example"]` |Bucket列表，默认情况下，若未指定该参数，则表示查询账号下所有存储Bucket。 |


<span id="Response parameters"></span>
## 返回调用结果参数

关于唯一的API专属返回调用结果参数，请参见下表。更多详情请参考[请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Buckets |Array of String |`["example"]` |Bucket列表。 |
|StartTime |String |`2022-02-16T00:00:00Z` |查询范围的起始时间，采用RFC 3339格式，精确到秒。 |
|EndTime |String |`2022-02-17T23:59:59Z` |查询范围的结束时间，采用RFC 3339格式，精确到秒。 |
|Aggregation |Boolean |`86400` |数据颗粒度，单位为秒。 |
|StorageDataList |Array of [StorageDataList](https://docs.byteplus.com/en/docs/24/107015#storagedatalist) |`-` |时移存储数据。 |


<span id="storagedatalist"></span>
### StorageDataList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|TimeStamp |String |`2022-02-16T00:00:00Z` |时间戳，默认为每日结束时间。例如，返回2022\-02\-16T00:00:00Z表示该时间点的存储用量作为2月16日的计费情况。 |
|Storage |Float |`4503380.1` |直播时移存储用量，单位为GB。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveStorageSpaceData&Version=2023-01-01
{
    "Aggregation": 86400,
    "EndTime": "2022-02-17T23:59:59Z",
    "StartTime": "2022-02-11T00:00:00Z",
    "Buckets": [
        "example"
    ]
}
```


<span id="Sample response"></span>
### 返回调用结果示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20180604110420010010****",
        "Action": "DescribeLiveStorageSpaceData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Buckets": [
            "example"
        ],
        "StartTime": "2022-02-16T00:00:00Z",
        "EndTime": "2022-02-17T23:59:59Z",
        "TimeShiftDataList": [
            {
                "TimeStamp": "2022-02-16T00:00:00Z",
                "Storage": 4503380
            },
            {
                "TimeStamp": "2022-02-16T00:05:00Z",
                "Storage": 4503380
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为当前操作相关的错误码。其他错误码请参见[BytePlus OpenAPI通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/107015#request-parameters)说明进行检查。 |
|403 |RequestForbidden |*  |请求被拒绝，因为当前账号下无所请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
