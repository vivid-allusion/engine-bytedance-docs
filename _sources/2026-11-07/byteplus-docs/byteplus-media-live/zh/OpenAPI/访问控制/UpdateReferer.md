---
title: "UpdateReferer"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatereferer-2023-zh-CN"
---

调用 `UpdateReferer` API，创建域名级别的 Referer 黑名单或白名单配置。

## 要求

* 限制：默认情况下，同一域名最多可创建 100 条 Referer 规则。如需创建更多规则，请联系[技术支持](https://console.byteplus.com/workorder/create)获取帮助。

* 速率限制：每个账号每秒 1 次查询。

## HTTP 请求

* 方法：POST

* 接入点：https://open.byteplusapi.com/?Action=UpdateReferer&Version=2023\-01\-01

## 请求参数

### 公共参数

调用所有 API 时，除 API 特定参数外，还必须携带[公共参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

### Query

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |是 |`UpdateReferer` |API 操作。 |
|Version |String |是 |`2023-01-01` |该 API 操作的版本。当前版本：2023\-01\-01。 |

### Body 参数

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |配置适用的域名空间。你可以调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或访问 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 页面，获取域名空间。 |
|Domain |String |是 |`pull.example.com` |拉流域名。你可以调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或访问 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 页面，获取域名。 |
|RefererInfoList |Array of [RefererInfoList](https://docs.byteplus.com/en/docs/24/106890#refererinfolist) |是 |`-` |Referer 信息列表。<br><br>在同一个 `Domain` 内，最多可配置 100 条 Referer 规则，且单次请求最多可配置 100 条 Referer 规则。 |

### RefererInfoList

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Key |String |是 |`referer` |Referer 配置的关键字。只能设置为 `referer`。 |
|Type |String |是 |`deny` |Referer 限制类型。可取以下值：<br><br><br>* `deny`：黑名单配置。如果拉流请求匹配 Referer 规则，则拒绝该请求。<br><br>* `allow`：白名单配置。如果拉流请求匹配 Referer 规则，则允许该请求。<br><br><br>> **说明**<br><br><br>> 在同一次 API 调用中，`RefererInfoList` 中的所有规则必须使用相同的 `Type` 值。<br> |
|Value |String |否 |`live.example1.net` |Referer 限制规则，即需要校验的拉流请求 Referer 值。支持添加完整域名或泛域名。最多可输入 300 个字符。 |

## 响应参数

该 API 在响应中仅返回[公共参数](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

## 示例

### 请求示例

```json
POST https://open.byteplusapi.com/?Action=UpdateReferer&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "Domain": "pull.example.com",
    "RefererInfoList": [
        {
            "Type": "allow",
            "Key": "referer",
            "Value": "live.example1.net"
        },
        {
            "Type": "allow",
            "Key": "referer",
            "Value": "live.example2.net"
        },
        {
            "Type": "allow",
            "Key": "referer",
            "Value": "live.example3.net"
        }
    ]
}
```

### 响应示例

```json
{
    "ResponseMetadata": {
        "Action": "UpdateReferer",
        "Region": "ap-singapore-1",
        "RequestId": "20230604110420****100232280022D31",
        "Service": "live",
        "Version": "2023-01-01"
    }
}
```

## 错误码

以下为当前操作相关的错误码。其他错误码请参见 [BytePlus OpenAPI 公共错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|200 |CommonErr |\- |未分类错误。建议重试。如果仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |\- |输入参数无效或不满足要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/106890#request-parameters)说明进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验失败。请检查数据类型是否正确。 |
|400 |InvalidParam.OutOfRange |%s 应为 {[%s]} 之一%s 应介于 %d 和 %d 之间 |参数超出允许范围。请检查错误消息中指定参数的值是否超出取值范围。 |
|400 |InvalidParam.Length |%s 长度不应超过 %d |参数长度不正确。请检查错误消息中指定参数的长度是否超出限制。 |
|403 |RequestForbidden |\- |请求被拒绝，因为当前账号下不存在请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllow |此 AccountID 无权访问对应资源，请检查请求参数 |请求被拒绝，因为当前账号下不存在请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.BillingStatus |AccountID 的计费状态不可用，请开通服务或充值。 |视频直播服务未开通或账号欠费，导致账单不可用。请检查服务开通状态和账号欠费状态。 |
|404 |ResourceNotFound |\- |未找到资源（包括域名空间、域名、应用名称、配置和证书）。建议重试。如果仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |发生数据库相关内部错误，请联系管理员。 |发生数据库相关内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.VhostOrDomain |发生 vhost 或 domain 相关内部错误，请联系管理员。 |发生域名空间 (Vhost) 或域名 (Domain) 相关内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
