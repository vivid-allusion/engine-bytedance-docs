---
title: "DescribeLiveTranscodeInfoData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivetranscodeinfodata-2023-zh-CN"
---

调用 `DescribeLiveTranscodeInfoData` API，查询指定时间范围内特定直播域名或直播流的详细数据，例如转码任务 ID、流名称、转码后缀以及转码开始和结束时间。

## 要求

* 频率限制：每个账号每秒 100 次查询

* 数据延迟：20 分钟

## HTTP 请求

* 方法：POST

* 接入点：[https://open.byteplusapi.com/?Action=DescribeLiveTranscodeInfoData&Version=2023-01-01](https://open.byteplusapi.com/?Action=DescribeLiveTranscodeInfoData&Version=2023-01-01)

## 请求参数

### 公共参数

调用所有 API 时，除 API 特有参数外，还必须传入[公共参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

### 查询

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveTranscodeInfoData` |API 操作。 |
|Version |String |是 |`2023-01-01` |该 API 操作的版本。当前版本：2023\-01\-01。 |

### 请求体参数

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|DomainList |String 数组 |否 |`["push.example.com","push.example2.com"]` |域名列表。默认值为空，表示查询您 BytePlus MediaLive 下所有域名的转码数据。您可以调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或访问 BytePlus MediaLive 控制台中的[域名](https://console.byteplus.com/live/main/domain/list)页面，获取要查询的域名。 |
|App |String |否 |`live` |直播流 URL 中的 AppName 字段。可包含大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和英文句点（.），长度为 1 到 30 个字符。<br><br>> **说明**<br><br><br>> 查询流粒度数据时，`App` 和 `Stream` 参数均为必填。<br> |
|Stream |String |否 |`example_stream` |直播流 URL 中的 StreamName 字段。可包含大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和英文句点（.），长度范围为 1 到 100 个字符。<br><br>> **说明**<br><br><br>> 查询流粒度数据时，`App` 和 `Stream` 参数均为必填。<br> |
|StartTime |String |是 |`2021-04-13T00:00:00Z` |查询时间范围的开始时间，采用 RFC 3339 格式，精度为秒。<br><br>> **说明**<br><br><br>> 历史查询的最大时间范围为 366 天。<br> |
|EndTime |String |是 |`2021-04-14T00:00:00Z` |查询时间范围的结束时间，采用 RFC 3339 格式，精度为秒。 |
|TranscodeType |String 数组 |否 |`["Normal_H264","ByteHD_H265"]` |视频编解码器。默认值为空，表示不指定视频编解码器。可取以下值：<br><br><br>* `Normal_H264`：H.264 标准转码；<br><br>* `Normal_H265`：H.265 标准转码；<br><br>* `ByteHD_H264`：H.264 低码率高清；<br><br>* `ByteHD_H265`：H.265 低码率高清；<br><br>* `ByteQE`：视频增强；<br><br>* `Audio`：音频流。 |
|Resolution |String 数组 |否 |`["720P","1080P"]` |转码视频的分辨率。例如，720P 分辨率表示转码视频的总面积大于 480P（640 × 480）且小于或等于 720P（1280 × 720）。<br><br><br>* `480P`：640 × 480；<br><br>* `720P`：1280 × 720；<br><br>* `1080P`：1920 × 1088；<br><br>* `2K`：2560 × 1440；<br><br>* `4K`：4096 × 2160；<br><br>* `8K`：\> 4096 x 2160；<br><br>* `0P`：音频流转码。 |
|PageNum |Integer |否 |`1` |页码。取值必须大于或等于 `1`。默认值：`1`。 |
|PageSize |Integer |否 |`20` |每页查询结果数。有效取值：[1,100000]。默认值：`20`。<br><br>> **说明**<br><br><br>> 如果将此参数设置为 `0`，则使用默认值。<br> |

## 响应参数

有关 API 特有的响应参数，请参见下表。更多详情，请参阅[请求响应](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|DomainList |String 数组 |`["push.example.com","push.example2.com"]` |域名列表。 |
|App |String |`live` |直播流 URL 中用于查询流粒度的 AppName 字段。 |
|Stream |String |`example_stream` |直播流 URL 中用于查询流粒度的 StreamName 字段。 |
|StartTime |String |`2021-04-13T00:00:00Z` |查询时间范围的开始时间，采用 RFC 3339 格式，精度为秒。 |
|EndTime |String |`2021-04-14T00:00:00Z` |查询时间范围的结束时间，采用 RFC 3339 格式，精度为秒。 |
|TranscodeType |String 数组 |`["Normal_H264","ByteHD_H265"]` |视频编解码器。默认值为空，表示不指定视频编解码器。可取以下值：<br><br><br>* `Normal_H264`：H.264 标准转码；<br><br>* `Normal_H265`：H.265 标准转码；<br><br>* `ByteHD_H264`：H.264 低码率高清；<br><br>* `ByteHD_H265`：H.265 低码率高清；<br><br>* `ByteQE`：视频增强；<br><br>* `Audio`：音频流。 |
|Resolution |String 数组 |`["720P","1080P"]` |转码视频的分辨率。例如，720P 分辨率表示转码视频的总面积大于 480P（640 × 480）且小于或等于 720P（1280 × 720）。<br><br><br>* `480P`：640 × 480；<br><br>* `720P`：1280 × 720；<br><br>* `1080P`：1920 × 1088；<br><br>* `2K`：2560 × 1440；<br><br>* `4K`：4096 × 2160；<br><br>* `8K`：\> 4096 x 2160；<br><br>* `0P`：音频流转码。 |
|TranscodeInfoDataList |[TranscodeInfoDataList](https://docs.byteplus.com/en/docs/24/107006#transcodeinfodatalist) 数组 |`-` |所有时间粒度的数据。 |
|Pagination |[Pagination](https://docs.byteplus.com/en/docs/24/107006#pagination) 对象 |`-` |分页信息。 |

### TranscodeInfoDataList

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|TaskID |String |`yvnytvvnigm3456` |转码任务 ID。 |
|Stream |String |`example_stream` |直播流 URL 中的 StreamName 字段。 |
|TranscodeSuffix |String |`hd` |转码后缀。 |
|TranscodeType |String |`Normal_H264` |转码格式。可取以下值：<br><br><br>* `Normal_H264`：H.264 标准转码；<br><br>* `Normal_H265`：H.265 标准转码；<br><br>* `ByteHD_H264`：H.264 低码率高清；<br><br>* `ByteHD_H265`：H.265 低码率高清；<br><br>* `ByteQE`：视频增强；<br><br>* `Audio`：音频流。 |
|Resolution |String |`720P` |转码视频的分辨率。例如，720P 分辨率表示转码视频的总面积大于 480P（640 × 480）且小于或等于 720P（1280 × 720）。<br><br><br>* `480P`：640 × 480；<br><br>* `720P`：1280 × 720；<br><br>* `1080P`：1920 × 1088；<br><br>* `2K`：2560 × 1440；<br><br>* `4K`：4096 × 2160；<br><br>* `8K`：\> 4096 x 2160；<br><br>* `0P`：音频流转码。 |
|StartTime |String |`2022-03-07T00:00:00Z` |查询时间范围的开始时间，采用 RFC 3339 格式，精度为秒。 |
|EndTime |String |`2022-03-08T00:00:00Z` |查询时间范围的结束时间，采用 RFC 3339 格式，精度为秒。 |
|Duration |Float |`1.4475713543666666` |查询时间范围内当前转码任务的转码时长，单位为分钟。 |

### Pagination

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|PageCur |Integer |`1` |当前页码。 |
|PageSize |Integer |`20` |每页结果数。 |
|TotalCount |Integer |`1000` |结果总数。 |

## 示例

### 请求示例

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveTranscodeInfoData&Version=2023-01-01
{
    "DomainList": [
        "push.example.com",
        "push.example2.com"
    ],
    "StartTime": "2021-04-13T00:00:00Z",
    "EndTime": "2021-04-14T00:00:00Z",
    "App": "live",
    "Stream": "example_stream",
    "Resolution": [
        "720P",
        "1080P"
    ],
    "PageNum": 1,
    "PageSize": 20,
    "TranscodeType": [
        "Normal_H264",
        "ByteHD_H265"
    ]
}
```

### 响应示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeLiveTranscodeInfoData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "DomainList": [
            "push.example.com",
            "push.example2.com"
        ],
        "StartTime": "2021-04-13T00:00:00Z",
        "EndTime": "2021-04-14T00:00:00Z",
        "App": "live",
        "Stream": "example_stream",
        "Resolution": [
            "720P",
            "1080P"
        ],
        "TranscodeInfoDataList": [
            {
                "Duration": 1.4475713543666666,
                "Resolution": "720P",
                "TranscodeType": "Normal_H264",
                "Stream": "example_stream",
                "TranscodeSuffix": "hd",
                "StartTime": "2022-03-07T00:00:00Z",
                "EndTime": "2022-03-08T00:00:00Z",
                "TaskID": "yvnytvvnigm3456"
            }
        ],
        "Pagination": {
            "PageCur": 1,
            "PageSize": 20,
            "TotalCount": 1000
        },
        "TranscodeType": [
            "Normal_H264",
            "ByteHD_H265"
        ]
    }
}
```

## 错误码

以下为当前操作相关的错误码。有关其他错误码，请参见 [BytePlus OpenAPI 公共错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|状态码 |错误码 |错误信息 |描述 |
|---|---|---|---|
|400 |InvalidParam |\- |输入参数无效或不符合要求。请参阅[请求参数](https://docs.byteplus.com/en/docs/24/107006#request-parameters)说明进行检查。 |
|500 |InternalError |an internal error occurred, please contact the administrator. |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|403 |RequestForbidden |\- |请求被拒绝，因为当前账号下没有请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
