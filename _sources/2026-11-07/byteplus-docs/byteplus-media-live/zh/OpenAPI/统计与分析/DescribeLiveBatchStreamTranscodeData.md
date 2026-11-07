---
title: "DescribeLiveBatchStreamTranscodeData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivebatchstreamtranscodedata-2023-zh-CN"
---

调用`DescribeLiveBatchStreamTranscodeData` API，查询指定时间范围内域名下所有转码流的转码时长、分辨率档位和编码方式等转码数据。

## 要求

* 限制：支持查询指定域名下的流量数据，包括已删除的域名。

* 速率限制：每个账号每秒 30 次查询。

* 数据延迟：数据延迟为 15 分钟。

## HTTP 请求

* 方法：POST

* 端点：[https://open.byteplusapi.com/?Action=DescribeLiveBatchStreamTranscodeData&Version=2023-01-01](https://open.byteplusapi.com/?Action=DescribeLiveBatchStreamTranscodeData&Version=2023-01-01)

## 请求参数

### 公共参数

调用所有 API 时，除 API 特定参数外，还必须携带[公共参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

### 查询参数

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DescribeLiveBatchStreamTranscodeData` |API 操作。 |
|Version |String |Yes |`2023-01-01` |该 API 操作的版本。当前版本：2023\-01\-01。 |

### 请求体参数

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|DomainList |Array of String |No |`["push.example.com", "push2.example.com"]` |拉流域名列表。默认值为空，表示查询所有域名。您可以调用[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或前往 BytePlus MediaLive 控制台的[域名](https://console.byteplus.com/live/main/domain/list)页面，获取需要查询的拉流域名。 |
|StartTime |String |Yes |`2022-11-10T00:00:00Z` |查询时间范围的开始时间（UTC 时间，RFC 3339 格式，精确到秒）。<br><br>> **说明**<br><br><br>> 历史查询时间范围的最大跨度为 366 天。<br> |
|EndTime |String |Yes |`2022-11-11T00:00:00Z` |查询时间范围的结束时间（UTC 时间，RFC 3339 格式，精确到秒）。 |
|PageSize |Integer |No |`1000` |每页查询结果数量。取值范围：[100,1000]。默认值：`1000`。<br><br>> **说明**<br><br><br>> 如果将该参数设置为`0`，则使用默认值。<br> |
|PageNum |Integer |No |`1` |页码。取值必须大于等于`1`。默认值：`1`。 |

## 响应参数

下表列出了该 API 特有的响应参数。更多信息，请参见[请求响应](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)。

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|DomainList |Array of String |`["push.example.com", "push2.example.com"]` |域名列表。 |
|StartTime |String |`2022-11-10T00:00:00Z` |查询的开始时间，为 UTC 时间，按 RFC3339 格式化，精确到秒。 |
|EndTime |String |`2022-11-11T00:00:00Z` |查询的结束时间，为 UTC 时间，按 RFC3339 格式化，精确到秒。 |
|TotalDuration |Float |`40.1` |当前查询条件下所有流的总转码时长，单位为分钟。 |
|StreamInfoList |Array of [StreamInfoList](https://docs.byteplus.com/en/docs/24/107034#streaminfolist) |`-` |按流维度划分的数据。 |
|Pagination |Object of [Pagination](https://docs.byteplus.com/en/docs/24/107034#pagination) |`-` |分页信息。 |

### StreamInfoList

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Domain |String |`push.example.com` |域名。 |
|App |String |`live` |流地址中的 AppName 字段。 |
|Stream |String |`example_stream` |流地址中的 StreamName 字段。 |
|Resolution |String |`720P` |转码分辨率档位为可选项，默认不指定具体分辨率档位。例如，选择`720P`表示转码配置将作用于面积（长边乘以短边）大于`480P`分辨率（640x480）且小于等于`720P`分辨率（1280x720）的视频。支持的取值及含义如下：<br><br><br>* `480P`：640 × 480；<br><br>* `720P`：1280 × 720；<br><br>* `1080P`：1920 × 1080；<br><br>* `2K`：2560 × 1440；<br><br>* `4K`：4096 × 2160；<br><br>* `8K`：大于 4096 x 2160；<br><br>* `0P`：纯音频转码，表示无视频内容。 |
|Duration |Float |`20.1` |当前流在查询时间内的总转码时长，单位为分钟。 |
|VCodec |String |`Normal_H264` |视频编码格式：如果留空，则表示不指定编码格式。支持的取值及含义如下：<br><br><br>* `Normal_H264`：H.264。<br><br>* `Normal_H265`：H.265。<br><br>* `Normal_H266`：H.266。<br><br>* `ByteHD_H264`：低码率高清模式下的 H.264。<br><br>* `ByteHD_H265`：低码率高清模式下的 H.265。<br><br>* `ByteHD_H266`：低码率高清模式下的 H.266。<br><br>* `ByteQE`：视频画质增强。<br><br>* `Audio`：纯音频流。 |
|Coderate |Integer |`2000` |当前流的转码码率。 |

### Pagination

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|PageNum |Integer |`1` |当前页码。 |
|PageSize |Integer |`1000` |每页结果数量。 |
|TotalCount |Integer |`2` |结果总数。 |

## 示例

### 示例请求

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveBatchStreamTranscodeData&Version=2023-01-01
{
  "StartTime": "2022-11-10T00:00:00Z",
  "EndTime": "2022-11-11T00:00:00Z"
}
```

### 示例响应

```json
{
  "ResponseMetadata":{
    "RequestId": "201806041104200100100232280022D30",
    "Action": "DescribeLiveBatchStreamTranscodeData",
    "Version": "2023-01-01",
    "Service": "live",
    "Region": "ap-singapore-1"
  },
  "Result":{
    "StartTime": "2022-11-10T00:00:00Z",
    "EndTime": "2022-11-11T00:00:00Z",
    "TotalDuration": 40,
    "StreamInfoList": [
      {
        "Domain": "pull.example.com"
        "Stream": "example_stream001",
        "App": "live",
        "Resolution": "720P",
        "Duration": 20,
        "VCodec": "Normal_H264"
      },
      {
        "Domain": "pull.example.com"
        "Stream": "example_stream002",
        "App": "live",
        "Resolution": "720P",
        "Duration": 20,
        "VCodec": "Normal_H264"
      }
    ],
    "Pagination": {
        "PageNum":    1,
        "PageSize":   1000,
        "TotalCount": 2,
    }
}
```

## 错误码

以下是与当前操作相关的错误码。其他错误码请参见 [BytePlus OpenAPI 公共错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|200 |CommonErr |\- |未分类错误。建议重试。如果仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|400 |InvalidParam |\- |输入参数无效或不符合要求。请参照[请求参数](https://docs.byteplus.com/en/docs/24/107034#request-parameters)说明进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验失败。请检查数据类型是否正确。 |
|403 |RequestForbidden |\- |请求被拒绝，因为当前账号下没有请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|404 |ResourceNotFound |\- |未找到资源（包括域名空间、域名、应用名称、配置和证书）。建议重试。如果仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
