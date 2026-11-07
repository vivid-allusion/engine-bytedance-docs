---
title: "DescribeClusterRateLimit"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeclusterratelimit-zh-CN"
---

调用 `DescribeClusterRateLimit` API 查询拉流请求的频率限制。

## 要求

频率限制：每个账号每秒 1 次查询。

## HTTP 请求

* 方法：POST

* 接入点：https://open.byteplusapi.com/?Action=DescribeClusterRateLimit&Version=2023\-01\-01

## 请求参数

### 公共参数

调用所有 API 时，除 API 特定参数外，还必须携带[公共参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

### Query

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Action |String |是 |`DescribeClusterRateLimit` |API 操作。 |
|Version |String |是 |`2023-01-01` |该 API 操作的版本。当前版本：2023\-01\-01。 |

### Body 参数

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |域名空间。您可以调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或访问 BytePlus MediaLive 控制台中的[域名](https://console.byteplus.com/live/main/domain/list)页面，获取域名空间。 |
|Domain |String |否 |`pull.example.com` |拉流域名。您可以调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或访问 BytePlus MediaLive 控制台中的[域名](https://console.byteplus.com/live/main/domain/list)页面，获取域名。 |

## 响应参数

API 特有的响应参数见下表。更多信息，请参见[请求响应](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|ClusterRateLimitItemList |[ClusterRateLimitItemList](https://docs.byteplus.com/en/docs/24/106928#clusterratelimititemlist) 数组 |`-` |限频配置。 |

### ClusterRateLimitItemList

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|Vhost |String |`push.example.com` |域名空间。 |
|Domain |String |`pull.example.com` |域名。 |
|Status |Integer |`0` |是否启用限频。<br><br><br>* `0`：已启用。<br><br>* `2`：已禁用。 |
|Type |String |`ipToAll` |限频类型：<br><br><br>* `ipToAll`：限制单个 IP 地址发出的请求频率。<br><br>* `url`：限制发送到单个 URL 的请求频率。<br><br>* `queryParam`：限制发送到包含指定查询参数的 URL 的请求频率。<br><br>* `ipToUrl`：限制单个 IP 地址向同一 URL 发出的请求频率。 |
|Param |String |`param1` |要应用限频的查询参数。 |
|RejectDuration |Integer |`60` |超出频率限制后拒绝所有传入请求的拒绝时长，单位为秒。 |
|RejectCode |Integer |`429` |请求被拒绝时客户端收到的状态码。 |
|AggregationPeriod |Integer |`1` |统计周期，单位为秒。在此周期内计算请求频率。例如，如果将 `AggregationPeriod` 设置为 `10`，则每 10 秒计算一次请求频率。 |
|Limit |Integer |`101` |在 `AggregationPeriod` 内允许的最大请求数。 |

## 示例

### 示例请求

```json
POST https://open.byteplusapi.com/?Action=DescribeClusterRateLimit&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "Domain": "pull.example.com"
}
```

### 示例响应

```json
{
    "ResponseMetadata": {
        "Action": "DescribeClusterRateLimit",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "ClusterRateLimitItemList": [
            {
                "AggregationPeriod": 1,
                "Domain": "pull.example.com",
                "Limit": 101,
                "Param": "param1",
                "RejectCode": 429,
                "RejectDuration": 60,
                "Status": 0,
                "Type": "queryParam",
                "Vhost": "push.example.com"
            }
        ]
    }
}
```

## 错误码

以下是与当前操作相关的错误码。其他错误码，请参见 [BytePlus OpenAPI 公共错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|状态码 |错误码 |错误消息 |描述 |
|---|---|---|---|
|200 |CommonErr |\- |未分类错误。建议重试。如果仍然返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |\- |输入参数无效或不符合要求。请参见[请求参数](https://docs.byteplus.com/en/docs/24/106928#request-parameters)说明进行检查。 |
|400 |InvalidParam.BindError |Request parameter error, please check input data |参数校验失败。请检查数据类型是否正确。 |
|403 |RequestForbidden |\- |请求被拒绝，因为当前账号下没有请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllow |this AccountID does not have permission to access the corresponding resource, please check the request parameters |请求被拒绝，因为当前账号下没有请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |视频直播服务未开通或账号欠费，导致账单不可用。请检查服务开通状态和账号欠费状态。 |
|404 |ResourceNotFound |\- |未找到资源（包括域名空间、域名、应用名称、配置和证书）。建议重试。如果仍然返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |an internal error occurred, please contact the administrator. |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |an internal error related to database occurred, please contact the administrator. |发生数据库相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
