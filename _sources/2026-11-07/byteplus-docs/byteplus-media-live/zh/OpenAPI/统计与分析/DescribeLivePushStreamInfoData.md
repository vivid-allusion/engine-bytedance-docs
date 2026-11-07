---
title: "DescribeLivePushStreamInfoData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describelivepushstreaminfodata-zh-CN"
---

调用 `DescribeLivePushStreamInfoData` API 查询推流信息及断流原因

## 要求

* 速率限制：每个账号每秒 100 次查询

## HTTP 请求

* 方法：POST

* 端点：https://open.byteplusapi.com/?Action=DescribeLivePushStreamInfoData&Version=2023\-01\-01

## 请求参数

### 公共参数

调用所有 API 时，除 API 特定参数外，还必须携带[公共参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

### 查询参数

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Action |String |是 |`DescribeLivePushStreamInfoData` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。当前版本：2023\-01\-01。 |

### Body 参数

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|DomainList |String 数组 |否 |`["push.example.com","push2.example.com"]` |要查询的域名列表。 |
|App |String |否 |`live` |直播流 URL 中的 AppName 字段。可包含大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和句点（.），长度范围为 1 到 30 个字符。 |
|Stream |String |否 |`example_stream` |直播流 URL 中的 StreamName 字段。可包含大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和句点（.），长度范围为 1 到 100 个字符。 |
|StartTime |String |是 |`2023-05-29T00:00:00Z` |查询范围的开始时间，采用 RFC 3339 格式，精确到秒。可查询过去 93 天内开始的数据。 |
|EndTime |String |是 |`2023-05-29T00:00:00Z` |查询范围的结束时间，采用 RFC 3339 格式，精确到秒。 |
|PageNum |Integer |否 |`1` |页码。取值必须大于或等于 `1`。默认值：`1`。 |
|PageSize |Integer |否 |`20` |每页查询结果数量。有效值：[1,1000]。默认值：`20`。<br><br>> **说明**<br><br><br>> 如果将此参数设置为 `0`，则使用默认值。<br> |

## 响应参数

有关唯一的 API 特定响应参数，请参见下表。有关更多详情，请参阅[请求响应](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|DomainList |String 数组 |`["push.example.com"]` |推流域名。 |
|App |String |`example_app` |直播流 URL 中的 AppName 字段。 |
|Stream |String |`exampel_stream` |直播流 URL 中的 StreamName 字段。 |
|StartTime |String |`2024-03-16T00:00:00Z` |查询范围的开始时间，采用 RFC 3339 格式，精确到秒。 |
|EndTime |String |`2024-03-16T00:01:59Z` |查询范围的结束时间，采用 RFC 3339 格式，精确到秒。 |
|PushStreamInfoDataList |[PushStreamInfoDataList](https://docs.byteplus.com/en/docs/24/107008#pushstreaminfodatalist) 数组 |`-` |推流详情。 |
|Pagination |[Pagination](https://docs.byteplus.com/en/docs/24/107008#pagination) 对象 |`-` |分页信息。 |

### PushStreamInfoDataList

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|App |String |`example_app` |直播流 URL 中的 AppName 字段。 |
|Stream |String |`example_stream` |直播流 URL 中的 StreamName 字段。 |
|StartTime |String |`2024-03-16T00:00:00Z` |每个时间间隔的开始时间。采用 RFC 3339 格式的 UTC 时间。 |
|EndTime |String |`2024-03-16T00:00:30Z` |每个时间间隔的结束时间。采用 RFC 3339 格式的 UTC 时间。 |
|Duration |Integer |`122345` |推流时长。 |
|IP |String |`xx.xx.xx.xx` |推流的 IP 地址。 |
|StreamBreakReason |String |`Duplicate stream push with the same stream ID` |结束推流的原因。 |

### Pagination

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|PageCur |Integer |`1` |当前页码。 |
|PageSize |Integer |`20` |日志文件大小，单位为字节。 |
|TotalCount |Integer |`2` |结果总数。 |

## 示例

### 示例请求

```json
POST https://open.byteplusapi.com/?Action=DescribeLivePushStreamInfoData&Version=2023-01-01
{
    "Domain": "example.com",
    "App": "example_app",
    "Stream": "example_stream",
    "StartTime": "2021-08-16T00:00:00Z",
    "EndTime": "2021-08-16T00:01:59Z"
}
```

### 示例响应

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "DescribeLivePushStreamInfoData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "DomainList": [
            "push.example.com"
        ],
        "App": "example_app",
        "Stream": "exampel_stream",
        "StartTime": "2024-03-16T00:00:00Z",
        "EndTime": "2024-03-16T00:01:59Z",
        "PushStreamInfoDataList": [
            {
                "App": "example_app",
                "Stream": "example_stream",
                "StartTime": "2024-03-16T00:00:00Z",
                "EndTime": "2024-03-16T00:00:30Z",
                "Duration": 122345,
                "IP": "xx.xx.xx.xx",
                "StreamBreakReason": "Duplicate stream push with the same stream ID"
            }
        ],
        "Pagination": {
            "PageCur": 1,
            "PageSize": 20,
            "TotalCount": 2
        }
    }
}
```

## 错误码

以下是与当前操作相关的错误码。有关其他错误码，请参见 [BytePlus OpenAPI 公共错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|状态码 |错误码 |错误信息 |描述 |
|---|---|---|---|
|400 |InvalidParam |\- |输入参数无效或不符合要求。请参阅 [请求参数](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveispdata#request-parameters) 说明进行检查。 |
|500 |InternalError |an internal error occurred, please contact the administrator. |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
