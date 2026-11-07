---
title: "UpdateUserAgentAccessRule"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateuseragentaccessrule-zh-CN"
---

调用 `UpdateUserAgentAccessRule` API 添加或更新 User\-Agent 限制。

## 要求

速率限制：每个账号每秒 10 次查询。

## HTTP 请求

* 方法：POST

* 端点：https://open.byteplusapi.com/?Action=UpdateUserAgentAccessRule&Version=2023\-01\-01

## 请求参数

### 公共参数

调用所有 API 时，除 API 特定参数外，还必须携带[公共参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

### Query

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Action |String |是 |`UpdateUserAgentAccessRule` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。当前版本：2023\-01\-01。 |

### Body 参数

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |域名空间。您可以调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或访问 BytePlus MediaLive 控制台中的[域名](https://console.byteplus.com/live/main/domain/list)页面获取域名空间。 |
|Domain |String |是 |`pull.example.com` |拉流域名。您可以调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或访问 BytePlus MediaLive 控制台中的[域名](https://console.byteplus.com/live/main/domain/list)页面获取域名。 |
|UaAccessRule |[UaAccessRule](https://docs.byteplus.com/en/docs/24/106946#uaaccessrule) 的 Object |是 |`-` |UA 阻止列表或允许列表详情。 |

### UaAccessRule

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|AllowEmpty |Boolean |是 |`true` |指定是否将配置应用于包含空 UA 头或不包含 UA 头的请求。例如，如果将 **Type** 设置为 **deny**，并将 **AllowEmpty** 设置为 **true**，则包含空 UA 头或不包含 UA 头的请求将被拒绝。<br><br><br>* `true`：应用。<br><br>* `false`：不应用。 |
|Type |String |是 |`deny` |限制类型。<br><br><br>* `allow`：允许列表。<br><br>* `deny`：阻止列表。 |
|Enable |Boolean |是 |`true` |指定是否启用 UA 允许列表或阻止列表。<br><br><br>* `true`：启用。<br><br>* `false`：禁用。 |
|UserAgent |Array of String |是 |`["Mozilla/5.0","*curl*"]` |阻止列表或允许列表中的 UA 头列表。配置长度不能超过 30,000 个字符。最多可输入 1,000 个 UA 头。<br><br><br>* UA 头区分大小写。<br><br>* 您可以使用通配符（\*）表示任意数量的字符。`*` 只能出现在 UA 头的开头或结尾。您可以在 UA 头的开头和结尾都添加 `*`，例如 `*curl*`。<br><br>* UA 头不能为 `*`。<br><br>* UA 头不能包含 `**`。<br><br>* UA 头只能包含可打印的 ASCII 字符，Delete（ASCII 码 127）除外。<br><br>* UA 头不能仅包含空格。 |

## 响应参数

此 API 的响应中仅返回[公共参数](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

## 示例

### 示例请求

```json
POST https://open.byteplusapi.com/?Action=UpdateUserAgentAccessRule&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "Domain": "pull.example.com",
    "UaAccessRule": {
        "AllowEmpty": true,
        "Type": "deny",
        "Enable": true,
        "UserAgent": [
            "Mozilla/5.0",
            "*curl*"
        ]
    }
}
```

### 示例响应

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UpdateUserAgentAccessRule",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```

## 错误码

以下是与当前操作相关的错误码。有关其他错误码，请参阅 [BytePlus OpenAPI 公共错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|状态码 |错误码 |错误消息 |描述 |
|---|---|---|---|
|200 |CommonErr |\- |未分类错误。建议重试。如果仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |\- |输入参数无效或不满足要求。请参阅[请求参数](https://docs.byteplus.com/en/docs/24/106946#request-parameters)说明进行检查。 |
|400 |InvalidParam.BindError |Request parameter error, please check input data |参数验证失败。请检查数据类型是否正确。 |
|403 |RequestForbidden |\- |由于当前账号下没有请求的资源，请求被拒绝。资源包括域名空间、域名、应用名称、配置和证书。 |
|403 |RequestForbidden.AccountIDNotAllow |this AccountID does not have permission to access the corresponding resource, please check the request parameters |由于当前账号下没有请求的资源，请求被拒绝。资源包括域名空间、域名、应用名称、配置和证书。 |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |视频直播服务未开通，或账号欠费，导致账单不可用。请检查服务开通状态和账号欠费状态。 |
|404 |ResourceNotFound |\- |未找到资源。资源包括域名空间、域名、应用名称、配置和证书。建议重试。如果仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.DomainNotExist |domain not found |未找到域名（Domain）。请检查传入的域名是否与实际使用的域名一致。 |
|500 |InternalError |an internal error occurred, please contact the administrator. |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |an internal error related to database occurred, please contact the administrator. |发生与数据库相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
