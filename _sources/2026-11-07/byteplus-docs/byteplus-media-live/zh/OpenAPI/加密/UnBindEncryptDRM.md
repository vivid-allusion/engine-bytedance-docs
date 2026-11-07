---
title: "UnBindEncryptDRM"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-unbindencryptdrm-zh-CN"
---

调用`UnBindEncryptDRM` API 删除已创建的加密配置。

## 要求

* 频率限制：每个账号每秒 1 次查询。

* 生效时间：配置删除后约 3~5 分钟生效。

## HTTP 请求

* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=UnBindEncryptDRM&Version=2023\-01\-01

## 请求参数

### 通用参数

所有 API 除了需传递 API 专属参数外，还必须携带[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

### Query

|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`UnBindEncryptDRM` |API 操作。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。当前版本：2023\-01\-01。 |

### Body 参数

|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Vhost |String |是 |`example.com` |域名空间。可调用[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或在 BytePlus MediaLive 控制台的[Domains](https://console.byteplus.com/live/main/domain/list)页面获取域名所属的域名空间。 |
|应用 |String |是 |`live` |直播流 URL 中的 AppName 字段。可包含大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和点（.），长度为 1~30 个字符。 |

## 返回调用结果

该 API 的返回调用结果中仅包含[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

## 示例

### 请求示例

```json
POST https://open.byteplusapi.com/?Action=UnBindEncryptDRM&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "App": "live"
}
```

### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "202306041104200100100232280022D31",
        "Action": "UnBindEncryptDRM",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```

## 错误码

以下为本次操作相关的错误码。其他错误码请参见[BytePlus OpenAPI 通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|200 |CommonErr |*  |未分类错误。建议重试。若仍返回错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/124023#request-parameters)说明进行排查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验未通过。请检查数据类型是否正确。 |
|403 |RequestForbidden |*  |因当前账号下无请求资源（资源包括域名空间、域名、应用、配置、证书），请求被拒绝。 |
|403 |RequestForbidden.AccountIDNotAllow |该 AccountID 无权访问对应资源，请检查请求参数 |因当前账号下无请求资源（资源包括域名空间、域名、应用、配置、证书），请求被拒绝。 |
|403 |RequestForbidden.BillingStatus |该 AccountID 未开通计费情况，请开通服务或充值。 |未开通视频直播服务或账号欠费，导致账单不可用。请检查服务开通状态及账号欠费状态。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用、配置、证书）。建议重试。若仍返回错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |发生与数据库相关的内部错误，请联系管理员。 |发生与数据库相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |错误代码：InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
