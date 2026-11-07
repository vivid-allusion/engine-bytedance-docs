---
title: "DescribeCDNSnapshotHistory"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecdnsnapshothistory-2023-zh-CN"
---

调用 `DescribeCDNSnapshotHistory` API 查询直播流的截图文件信息。

## 要求

限频：每个账号每秒 1 次查询。

## HTTP 请求

* 方法：POST

* 端点：https://open.byteplusapi.com/?Action=DescribeCDNSnapshotHistory&Version=2023\-01\-01

## 请求参数

### 公共参数

除 API 特定参数外，调用所有 API 时还必须携带[公共参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

### 查询参数

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Action |String |是 |`DescribeCDNSnapshotHistory` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。当前版本：2023\-01\-01。 |

### Body 参数

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |域名空间。您可以调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或访问 BytePlus MediaLive 控制台中的 [域名](https://console.byteplus.com/live/main/domain/list) 页面，获取域名所属的域名空间。 |
|App |String |是 |`live` |直播流 URL 中的 AppName 字段。可包含大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和句点（.），长度范围为 1 到 30 个字符。 |
|Stream |String |是 |`stream-123` |直播流 URL 中的 StreamName 字段。可包含大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和句点（.），长度范围为 1 到 100 个字符。 |
|DateFrom |String |是 |`2022-04-01T00:00:00Z` |查询范围的开始时间（本地时间，RFC 3339 格式，精确到秒）。查询指定录制任务的详细信息时，DateFrom 应设置为录制任务开始时间之前的任意时间。 |
|DateTo |String |是 |`2022-04-02T00:00:00Z` |查询范围的结束时间（本地时间，RFC 3339 格式，精确到秒）。DateTo 需晚于 DateFrom，且 DateTo 与 DateFrom 的间隔不应超过 7 天。 |
|PageNum |Integer |否 |`1` |页码。取值必须大于或等于 `1`。默认值：`1`。 |
|PageSize |Integer |否 |`10` |每页查询结果数。有效值：[1,1000]。默认值：`10`。<br><br>> **说明**<br><br><br>> 如果将此参数设置为 `0`，则使用默认值。<br> |
|Type |String |否 |`tos` |存储类型。始终设置为 `tos`。 |

## 响应参数

特有的 API 响应参数见下表。更多信息请参见[请求响应](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)章节。

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|Data |[Data](https://docs.byteplus.com/en/docs/24/106971#data) 数组 |`-` |截图记录列表。 |
|Pagination |[Pagination](https://docs.byteplus.com/en/docs/24/106971#pagination) 对象 |`-` |分页信息。 |

### Data

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|Vhost |String |`push.example.com` |域名空间。 |
|App |String |`live` |AppName 字段。 |
|Stream |String |`stream-123` |StreamName 字段。 |
|Path |String |`20210830135051697.jpeg` |截图文件的保存路径。 |
|TimeStamp |String |`2021-08-30 21:48:25.000` |精确到毫秒的截图时间戳。 |
|Width |Integer |`720` |截图宽度，单位为 px。 |
|Height |Integer |`1280` |截图高度，单位为 px。 |

### Pagination

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|PageCur |Integer |`1` |当前页码。 |
|PageSize |Integer |`10` |每页结果数。 |
|PageTotal |Integer |`231` |总页数。 |
|TotalCount |Integer |`4613` |检索到的录制文件总数。 |

## 示例

### 请求示例

```json
POST https://open.byteplusapi.com/?Action=DescribeCDNSnapshotHistory&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "App": "live",
    "Stream": "stream-123",
    "DateFrom": "2022-04-01T00:00:00Z",
    "DateTo": "2022-04-02T00:00:00Z"
}
```

### 响应示例

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "DescribeCDNSnapshotHistory",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Data": [
            {
                "App": "live",
                "FileSize": 0,
                "Height": 1280,
                "Path": "20210830135051697.jpeg",
                "Stream": "testStream413",
                "TimeStamp": "2021-08-30 21:48:25.000",
                "Vhost": "example.org",
                "Width": 720
            }
        ],
        "Pagination": {
            "PageCur": 1,
            "PageSize": 10,
            "PageTotal": 231,
            "TotalCount": 4613
        }
    }
}
```

## 错误码

以下是当前操作相关的错误码。其他错误码请参见 [BytePlus OpenAPI 的公共错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|状态码 |错误码 |错误信息 |描述 |
|---|---|---|---|
|200 |CommonErr |\- |未分类错误。建议重试。如果仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |\- |输入参数无效或不符合要求。请参见[请求参数](https://docs.byteplus.com/en/docs/24/106971#request-parameters)说明进行检查。 |
|400 |InvalidParam.BindError |Request parameter error, please check input data |参数验证失败。请检查数据类型是否正确。 |
|403 |RequestForbidden |\- |由于当前账号下没有请求的资源（资源包括域名空间、域名、应用名称、配置和证书），请求被拒绝。 |
|403 |RequestForbidden.AccountIDNotAllow |this AccountID does not have permission to access the corresponding resource, please check the request parameters |由于当前账号下没有请求的资源（资源包括域名空间、域名、应用名称、配置和证书），请求被拒绝。 |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |视频直播服务未开通或账号欠费，导致计费不可用。请检查服务开通状态和账号欠费状态。 |
|404 |ResourceNotFound |\- |未找到资源（包括域名空间、域名、应用名称、配置和证书）。建议重试。如果仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |an internal error occurred, please contact the administrator. |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
