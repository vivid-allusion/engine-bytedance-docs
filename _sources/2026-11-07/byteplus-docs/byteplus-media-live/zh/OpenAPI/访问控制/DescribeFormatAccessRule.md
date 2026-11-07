---
title: "DescribeFormatAccessRule"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeformataccessrule-zh-CN"
---

调用 `DescribeFormatAccessRule` API 查询协议限制。

## 要求

速率限制：每个账号每秒 10 次查询。

## HTTP 请求

* 方法：POST

* 端点：https://open.byteplusapi.com/?Action=DescribeFormatAccessRule&Version=2023\-01\-01

## 请求参数

### 公共参数

调用所有 API 时，除 API 特有参数外，还必须传入[公共参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

### 查询参数

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Action |String |是 |`DescribeFormatAccessRule` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。当前版本：2023\-01\-01。 |

### 请求体参数

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |域名空间。您可以调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或访问 BytePlus MediaLive 控制台中的[域名](https://console.byteplus.com/live/main/domain/list)页面，获取域名空间。 |
|Domain |String |是 |`pull.example.com` |拉流域名。您可以调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或访问 BytePlus MediaLive 控制台中的[域名](https://console.byteplus.com/live/main/domain/list)页面，获取域名。 |

## 响应参数

有关 API 特有的响应参数，请参见下表。更多详情，请参阅[请求响应](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|AccessRuleLists |[AccessRuleLists](https://docs.byteplus.com/en/docs/24/106950#accessrulelists) 数组 |`-` |协议限制。 |

### AccessRuleLists

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|Vhost |String |`push.example.com` |域名空间。 |
|Domain |String |`pull.example.com` |拉流域名。 |
|FormatAccessRule |[FormatAccessRule](https://docs.byteplus.com/en/docs/24/106950#formataccessrule) 对象 |`-` |协议限制。 |

### FormatAccessRule

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|Type |String |`deny` |访问控制类型。唯一支持的取值为 `deny`，表示禁止通过黑名单中的协议进行拉流。 |
|Enable |String |`true` |是否启用该配置。<br><br><br>* `true`：启用该配置。<br><br>* `false`：禁用该配置。 |
|FormatList |String 数组 |`["flv","hls"]` |协议列表。有效选项包括：<br><br><br>* `flv`<br><br>* `hls`<br><br>* `rtmp`<br><br>* `webrtc`，表示 RTM 协议 |

## 示例

### 请求示例

```json
POST https://open.byteplusapi.com/?Action=DescribeFormatAccessRule&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "Domain": "pull.example.com"
}
```

### 响应示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeFormatAccessRule",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "AccessRuleLists": [
            {
                "Vhost": "push.example.com",
                "Domain": "pull.example.com",
                "FormatAccessRule": {
                    "Type": "deny",
                    "Enable": "true",
                    "FormatList": [
                        "flv",
                        "hls"
                    ]
                }
            }
        ]
    }
}
```

## 错误码

以下是与当前操作相关的错误码。其他错误码请参见 [BytePlus OpenAPI 通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|状态码 |错误码 |错误信息 |描述 |
|---|---|---|---|
|200 |CommonErr |\- |未分类错误。建议重试。如果仍然返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |\- |输入参数无效或不符合要求。请参阅[请求参数](https://docs.byteplus.com/en/docs/24/106950#request-parameters)说明进行检查。 |
|400 |InvalidParam.BindError |Request parameter error, please check input data |参数校验失败。请检查数据类型是否正确。 |
|403 |RequestForbidden |\- |请求被拒绝，因为当前账号下没有请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllow |this AccountID does not have permission to access the corresponding resource, please check the request parameters |请求被拒绝，因为当前账号下没有请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |视频直播服务未开通或账号欠费，导致账单不可用。请检查服务开通状态和账号欠费状态。 |
|404 |ResourceNotFound |\- |未找到资源（包括域名空间、域名、应用名称、配置和证书）。建议重试。如果仍然返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.DomainNotExist |domain not found |未找到域名（Domain）。请检查传入的域名是否与实际使用的域名一致。 |
|500 |InternalError |an internal error occurred, please contact the administrator. |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |an internal error related to database occurred, please contact the administrator. |发生与数据库相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
