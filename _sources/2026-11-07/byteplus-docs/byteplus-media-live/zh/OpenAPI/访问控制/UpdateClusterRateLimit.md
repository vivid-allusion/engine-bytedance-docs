---
title: "UpdateClusterRateLimit"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateclusterratelimit-zh-CN"
---

调用 `UpdateClusterRateLimit` API，添加或修改拉流请求的频率限制。

## 使用场景

您可以使用此操作执行以下任一操作：

* 限制来自单个 IP 地址的请求频率。

* 限制来自单个 IP 地址且发送到同一 URL 的请求频率。

* 限制发送到单个 URL 的请求频率。

* 限制发送到包含指定查询参数的 URL 的请求频率。

> **说明**

> 频率限制按边缘集群维度生效，而非在整个网络范围内生效。举例来说，假设将来自某个 IP 地址的请求频率限制设置为每秒 50 次。如果集群 A 和集群 B 在 1 秒内均收到来自某个 IP 地址的 50 个请求，则不会发生错误。但是，如果集群 A 在同一秒内收到 101 个请求，而集群 B 仍收到 50 个请求，则在拒绝期间，来自该 IP 地址且由集群 A 接收的后续请求将被阻止。另一方面，集群 B 不受影响。

## 要求

速率限制：每个账号每秒 1 次查询。

## HTTP 请求

* 方法：POST

* 端点：https://open.byteplusapi.com/?Action=UpdateClusterRateLimit&Version=2023\-01\-01

## 请求参数

### 公共参数

除 API 特定参数外，调用所有 API 时还必须携带[公共参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

### 查询参数

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Action |String |是 |`UpdateClusterRateLimit` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。当前版本：2023\-01\-01。 |

### 请求体参数

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |域名空间。您可以调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或访问 BytePlus MediaLive 控制台中的[域名](https://console.byteplus.com/live/main/domain/list)页面，获取域名空间。 |
|Domain |String |是 |`pull.example.com` |用于拉流的域名。您可以调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或访问 BytePlus MediaLive 控制台中的[域名](https://console.byteplus.com/live/main/domain/list)页面，获取域名。 |
|Status |Integer |否 |`0` |是否启用速率限制。<br><br><br>* `0`：启用速率限制。<br><br>* `2`：禁用速率限制。 |
|Type |String |是 |`ipToAll` |要配置的速率限制类型：<br><br><br>* `ipToAll`：限制来自单个 IP 地址的请求频率。<br><br>* `url`：限制发送到单个 URL 的请求频率。<br><br>* `queryParam`：限制发送到包含指定查询参数的 URL 的请求频率。<br><br>* `ipToUrl`：限制来自单个 IP 地址且发送到同一 URL 的请求频率。 |
|Param |String |否 |`param1` |要对其应用速率限制的查询参数。<br><br>> **说明**<br><br><br>> 仅当同时满足以下两个条件时，此参数为必填并生效：<br><br><br><br>* > `Type` 设置为 `queryParam`。<br><br><br>* > [技术支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)已为您的账号启用查询参数速率限制。<br> |
|RejectDuration |Integer |否 |`1` |拒绝时长，单位为秒。当超出速率限制时，所有传入请求将在该期间被拒绝。取值范围为 [1, 10080]。默认值为 `1`。 |
|RejectCode |Integer |否 |`429` |请求被拒绝时客户端收到的状态码。默认值为 `429`。 |
|AggregationPeriod |Integer |否 |`1` |统计周期，单位为秒，用于计算请求频率。例如，如果将 `AggregationPeriod` 设置为 `10`，则每 10 秒计算一次请求频率。取值范围为 [1, 3600]。默认值为 `1`。 |
|Limit |Integer |是 |`101` |在 `AggregationPeriod` 内允许的最大请求数。取值范围为 [0, 100,000]。 |

## 响应参数

此 API 仅在响应中返回[公共参数](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

## 示例

### 请求示例

```json
POST https://open.byteplusapi.com/?Action=UpdateClusterRateLimit&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "Domain": "pull.example.com",
    "Type": "ipToAll",
    "Limit": 101
}
```

### 响应示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UpdateClusterRateLimit",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```

## 错误码

以下是与当前操作相关的错误码。有关其他错误码，请参见 [BytePlus OpenAPI 公共错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|状态码 |错误码 |错误信息 |描述 |
|---|---|---|---|
|200 |CommonErr |\- |未分类错误。建议重试。如果仍返回此错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |\- |输入参数无效或不符合要求。请参照[请求参数](https://docs.byteplus.com/en/docs/24/106894#request-parameters)说明进行检查。 |
|400 |InvalidParam.BindError |Request parameter error, please check input data |参数校验失败。请检查数据类型是否正确。 |
|403 |RequestForbidden |\- |由于当前账号下没有请求的资源，请求被拒绝。资源包括域名空间、域名、应用名称、配置和证书。 |
|403 |RequestForbidden.AccountIDNotAllow |this AccountID does not have permission to access the corresponding resource, please check the request parameters |由于当前账号下没有请求的资源，请求被拒绝。资源包括域名空间、域名、应用名称、配置和证书。 |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |视频直播服务未开通，或账号欠费，导致账单不可用。请检查服务开通状态和账号欠费状态。 |
|404 |ResourceNotFound |\- |未找到资源，包括域名空间、域名、应用名称、配置和证书。建议重试。如果仍返回此错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |an internal error occurred, please contact the administrator. |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |an internal error related to database occurred, please contact the administrator. |发生与数据库相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
