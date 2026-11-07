---
title: "DescribeLiveLogData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describelivelogdata-zh-CN"
---

调用 `DescribeLiveLogData` API，查询域名生成的日志文件信息。

## 要求

* 限制：

   * 支持查询指定域名（包括已删除域名）下生成的日志文件信息。

   * 支持查询最近 31 天内生成的日志数据。

   * 支持查询日志打包文件信息。有关各种日志格式的说明，请参阅[日志格式](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-managing-logs#log-format)。

* 速率限制：每个账号每秒 100 次查询

* 数据延迟：1 小时

* 延迟日志聚合：日志文件的聚合可能存在延迟，并会持续补充和追加内容。最完整的日志文件最长将在 24 小时内可用。

## HTTP 请求

* 方法：POST

* 接入点：https://open.byteplusapi.com/?Action=DescribeLiveLogData&Version=2023\-01\-01

## 请求参数

### 公共参数

调用所有 API 时，除 API 特定参数外，还必须传入[公共参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

### Query

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveLogData` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。当前版本：2023\-01\-01。 |

### Body 参数

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|StartTime |String |是 |`2022-04-13T10:00:00Z` |查询范围的结束时间，采用 RFC 3339 格式，精确到秒。<br><br>> **说明**<br><br><br><br>* > 当前仅可查询最近 31 天的日志数据。<br><br><br>* > 日志文件按整点小时拆分。请确保查询的开始时间和结束时间包含所查询时段的整点时间。例如，如果需要查询某天 07:30:00 到 08:10:00 的日志数据，则日志查询的开始时间应早于 07:00:00，结束时间应晚于 09:00:00。<br> |
|EndTime |String |是 |`2022-04-13T11:00:00Z` |查询范围的结束时间，采用 RFC 3339 格式，精确到秒。 |
|DomainList |Array of String |否 |`["push.example.com","push2.example.com"]` |域名列表。默认表示当前用户的所有推流和拉流域名。<br><br>> **说明**<br><br><br>> 当日志类型为 relay，即 `'Type': 'relay'` 时，此参数无效。<br> |
|Type |String |是 |`pull` |支持的日志类型包括：<br><br><br>* `pull`：拉流日志；<br><br>* `push`：推流日志；<br><br>* `source`：回源日志；<br><br>* `relay`：拉转推流转换日志。 |
|PageNum |Integer |否 |`1` |页码。取值必须大于或等于 `1`。默认值：`1`。 |
|PageSize |Integer |否 |`20` |每页查询结果数量。取值范围：[1,1000]。默认值：`20`。<br><br>> **说明**<br><br><br>> 如果将此参数设置为 `0`，则使用默认值。<br> |

## 响应参数

有关 API 特定的响应参数，请参见下表。更多详情，请参阅[请求响应](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|StartTime |String |`2022-04-13T10:00:00Z` |查询范围的开始时间（UTC 时间，采用 RFC 3339 格式，精确到秒）。 |
|EndTime |String |`2022-04-13T11:00:00Z` |查询范围的结束时间（UTC 时间，采用 RFC 3339 格式，精确到秒）。 |
|DomainList |Array of String |`["push.example.com", "push2.example.com"]` |域名列表。 |
|Type |String |`pull` |支持的日志类型包括：<br><br><br>* `pull`：拉流日志；<br><br>* `push`：推流日志；<br><br>* `source`：回源日志；<br><br>* `relay`：拉转推流转换日志。 |
|Pagination |Object of [Pagination](https://docs.byteplus.com/en/docs/24/106993#pagination) |`-` |数据分页信息。 |
|LogInfoList |Array of [LogInfoList](https://docs.byteplus.com/en/docs/24/106993#loginfolist) |`-` |日志文件信息列表。 |

### Pagination

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|PageNum |Integer |`1` |当前页码。 |
|PageSize |Integer |`20` |每页显示的数据项数量。 |
|TotalCount |Integer |`123` |查询结果中的数据项总数。 |

### LogInfoList

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|Domain |String |`push.example.com` |域名。<br><br>> **说明**<br><br><br>> 当日志类型为 relay，即 `'Type': 'relay'` 时，此字段为空。<br> |
|LogName |String |`example.com_2023_09_01_000000_010000_0.gz` |日志文件名，遵循如下命名约定。<br><br><br>* 与域名相关时：加速域名_年_月_日_时间开始_时间结束_文件分片序号。例如，`www.example.com_2023_08_11_000000_010000_0.gz`；<br><br>* 与域名无关时：年_月_日_时间开始_时间结束_文件分片序号。例如，`2023_08_11_000000_010000_0.gz`；<br><br>* 如果当前事件在某一小时内生成的日志数量超过 150 万条，则会生成多个日志文件，文件分片序号表示日志文件的顺序，例如，`2023_08_11_000000_010000_0.gz`、`2023_08_11_000000_010000_1.gz`。 |
|LogSize |Integer |`12` |日志文件大小，单位为字节。 |
|DateTime |String |`2022-04-13T00:00:00Z` |日志文件对应的小时间隔，采用 RFC3339 格式的 UTC 时间，精确到秒。 |
|DownloadUrl |String |`http://example.com/download/20230901/example.com_2023_09_01_000000_010000_0.gz?x-expires=1693918129` |日志文件下载链接。 |

## 示例

### 请求示例

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveLogData&Version=2023-01-01
{
    "StartTime": "2023-09-01T00:00:00Z",
    "EndTime": "2023-09-01T23:00:00Z",
    "Type": "pull",
    "DomainList": [
        "example.com"
    ],
    "PageSize": 20,
    "PageNum": 1
}
```

### 响应示例

```json
{
    "ResponseMetadata": {
        "RequestId": "202306041104200100100232280022D31",
        "Action": "DescribeLiveLogData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "cn-north-1"
    },
    "Result": {
        "StartTime": "2023-09-01T00:00:00Z",
        "EndTime": "2023-09-01T23:00:00Z",
        "Type": "pull",
        "LogInfoList": [
            {
                "DateTime": "2023-09-01T22:00:00Z",
                "Domain": "example.com",
                "DownloadUrl": "http://example.com/download/20230901/example.com_2023_09_01_000000_010000_0.gz?x-expires=1693918129",
                "LogName": "example.com_2023_09_01_000000_010000_0.gz",
                "LogSize": 24900
            }
        ],
        "Pagination": {
            "PageNum": 1,
            "PageSize": 1,
            "TotalCount": 1
        }
    }
}
```

## 错误码

以下为与当前操作相关的错误码。有关其他错误码，请参阅 [BytePlus OpenAPI 公共错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|状态码 |错误码 |错误消息 |描述 |
|---|---|---|---|
|400 |InvalidParam |\- |输入参数无效或不符合要求。请参阅[请求参数](https://docs.byteplus.com/en/docs/24/106993#request-parameters)说明进行检查。 |
|403 |RequestForbidden |\- |请求被拒绝，因为当前账号下没有请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|500 |InternalError |an internal error occurred, please contact the administrator. |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
