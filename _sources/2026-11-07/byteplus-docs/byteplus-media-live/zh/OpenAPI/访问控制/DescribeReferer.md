---
title: "DescribeReferer"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describereferer-2023-zh-CN"
---

调用 `DescribeReferer` API 查询 Referer 黑名单或白名单配置。

## 要求

速率限制：每个账号每秒 1 次查询。

## HTTP 请求

* 方法：POST

* 端点：https://open.byteplusapi.com/?Action=DescribeReferer&Version=2023\-01\-01

## 请求参数

### 公共参数

调用所有 API 时，除 API 特定参数外，还必须传入[公共参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

### 查询

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Action |String |是 |`DescribeReferer` |API 操作。 |
|Version |String |是 |`2023-01-01` |该 API 操作的版本。当前版本：2023\-01\-01。 |

### 请求体参数

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Vhost |String |否 |`push.example.com` |域名空间。您可以调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或访问 BytePlus MediaLive 控制台中的 [域名](https://console.byteplus.com/live/main/domain/list) 页面获取域名空间。<br><br>> **说明**<br><br><br>> 请指定 `Vhost` 或 `Domain` 之一，不要同时指定。<br> |
|Domain |String |否 |`pull.example.com` |用于拉流的域名。您可以调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或访问 BytePlus MediaLive 控制台中的 [域名](https://console.byteplus.com/live/main/domain/list) 页面获取域名。<br><br>> **说明**<br><br><br>> 请指定 `Vhost` 或 `Domain` 之一，不要同时指定。<br> |

## 响应参数

有关 API 特有的响应参数，请参见下表。更多详细信息，请参阅[请求响应](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|RefererList |[RefererList](https://docs.byteplus.com/en/docs/24/106889#refererlist) 数组 |`-` |查询结果列表。 |

### RefererList

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|Vhost |String |`push.example.com` |域名空间。 |
|Domain |String |`pull.example.com` |域名。 |
|RefererInfoList |[RefererInfoList](https://docs.byteplus.com/en/docs/24/106889#refererinfolist) 数组 |`-` |Referer 信息列表。 |

### RefererInfoList

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|Key |String |`referer` |Referer 配置的名称，固定为 `referer`。 |
|Type |String |`deny` |Referer 限制类型。可取以下值：<br><br><br>* `deny`：黑名单配置。如果拉流请求匹配 Referer 规则，则拒绝该请求。<br><br>* `allow`：白名单配置。如果拉流请求匹配 Referer 规则，则允许该请求。 |
|Value |String |`example1.com` |Referer 限制规则，即待校验的拉流请求的 Referer 值。可添加完整域名或泛域名。最多可输入 300 个字符。 |
|Priority |Integer |`0` |已弃用。 |

## 示例

### 请求示例

```json
POST https://open.byteplusapi.com/?Action=DescribeReferer&Version=2023-01-01
{
    "Domain": "pull.example.com"
}
```

### 响应示例

```json
{
    "ResponseMetadata": {
        "Action": "DescribeReferer",
        "Region": "ap-singapore-1",
        "RequestId": "20230604110420****100232280022D31",
        "Service": "live",
        "Version": "2023-01-01"
    },
    "Result": {
        "RefererList": [
            {
                "Domain": "pull.example.com",
                "RefererInfoList": [
                    {
                        "Key": "referer",
                        "Priority": 0,
                        "Type": "deny",
                        "Value": "example1.com"
                    }
                ],
                "Vhost": "push.example.com"
            }
        ]
    }
}
```

## 错误码

以下是与当前操作相关的错误码。其他错误码请参见 [BytePlus OpenAPI 公共错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|状态码 |错误码 |错误消息 |描述 |
|---|---|---|---|
|200 |CommonErr |\- |未分类错误。建议重试。如果仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |\- |输入参数无效或不符合要求。请参阅[请求参数](https://docs.byteplus.com/en/docs/24/106889#request-parameters)说明进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验失败。请检查数据类型是否正确。 |
|403 |RequestForbidden |\- |请求被拒绝，因为当前账号下没有请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllow |此 AccountID 无权访问对应资源，请检查请求参数 |请求被拒绝，因为当前账号下没有请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.BillingStatus |AccountID 的账单状态不可用，请开通服务或充值。 |视频直播服务未开通或账号欠费，导致账单不可用。请检查服务开通状态和账号欠费状态。 |
|404 |ResourceNotFound |\- |未找到资源（包括域名空间、域名、应用名称、配置和证书）。建议重试。如果仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |发生数据库相关的内部错误，请联系管理员。 |发生数据库相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.VhostOrDomain |发生 vhost 或 domain 相关的内部错误，请联系管理员。 |发生域名空间 (Vhost) 或域名 (Domain) 相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
