---
title: "BindCert"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-bindcert-2023-zh-CN"
---

调用`BindCert` API，将已上传的 HTTPS 证书绑定到域名，并为该域名开启 HTTPS 安全传输。

<span id="Requirements"></span>
## 要求

频率限制：每个账号每秒 1 次查询。

<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=BindCert&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 除了需传递各自的 API 专属参数外，还必须携带[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### Query


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`BindCert` |API 操作名。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本号。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Domain |String |是 |`push.example.com` |需要绑定证书的域名。可调用[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或在 BytePlus MediaLive 控制台的[Domains](https://console.byteplus.com/live/main/domain/list)页面获取域名。 |
|ChainID |String |是 |`be37f********c487f486244759821f` |需要绑定到域名的证书链 ID。可调用[ListCertV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listcertv2) API 获取证书的 ChainID。 |
|HTTPS |Boolean |否 |`false` |是否开启 HTTPS 安全传输，默认值为`false`，取值及含义如下。<br><br><br>* `false`：关闭；<br><br>* `true`：开启。 |
|HTTP2 |Boolean |否 |`false` |是否开启 HTTP/2 协议。默认值为`false`。可选值如下：<br><br><br>* `false`：关闭 HTTP/2 协议。<br><br>* `true`：开启 HTTP/2 协议。 |


<span id="Response parameters"></span>
## 返回调用结果参数

该 API 的返回结果仅包含[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=BindCert&Version=2023-01-01
{
    "Domain": "push.example.com",
    "ChainID": "be***7c23b514c4987f486244759821f",
    "HTTPS": true
}
```


<span id="Sample response"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestID": "2020091615160501022706705738154",
        "Action": "BindCert",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为本次操作相关的错误码。其他错误码请参见[BytePlus OpenAPI 通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|200 |CommonErr |*  |未分类错误。建议重试。如多次重试后仍失败，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/106952#request-parameters)说明进行排查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验未通过。请检查数据类型是否正确。 |
|403 |RequestForbidden |*  |请求被拒绝，当前账号下无所请求的资源（资源包括域名空间、域名、应用、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllow |该 AccountID 无权访问对应资源，请检查请求参数 |请求被拒绝，当前账号下无所请求的资源（资源包括域名空间、域名、应用、配置和证书）。 |
|403 |RequestForbidden.BillingStatus |该 AccountID 的计费情况不可用，请开通服务或充值。 |未开通视频直播服务或账号欠费，导致账单不可用。请检查服务开通状态及账号欠费情况。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用、配置和证书）。建议重试。如多次重试后仍失败，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.VhostNotExist |未找到 vhost |未找到域名空间（Vhost）。请检查传入的域名空间是否与实际使用的域名空间一致。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |发生与数据库相关的内部错误，请联系管理员。 |发生与数据库相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
