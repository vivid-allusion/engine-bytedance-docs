---
title: "UpdateIPAccessRule"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateipaccessrule-zh-CN"
---

调用 `UpdateIPAccessRule` API，为指定域名配置 IP 黑名单或白名单。

<span id="Requirements"></span>
## 要求

速率限制：每个账号每秒最多 10 次查询。

<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=UpdateIPAccessRule&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用时，除了 API 专属参数外，还必须包含 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### Query


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`UpdateIPAccessRule` |API 操作。 |
|Version |String |是 |`2023-01-01` |该 API 操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |域名空间。可调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或访问 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 页面获取域名空间。 |
|Domain |String |是 |`push.example.com` |拉流或推流的域名。可调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或访问 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 页面获取域名。 |
|IPAccessRule |[IPAccessRule](https://docs.byteplus.com/en/docs/24/106927#ipaccessrule) 对象 |是 |`-` |IP 限制规则。 |


<span id="ipaccessrule"></span>
### IPAccessRule


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Type |String |是 |`deny` |IP 访问规则类型。取值及含义如下。<br><br><br>* `allow`：白名单。仅允许白名单中的 IP 地址发起请求访问资源。<br><br>* `deny`：黑名单。黑名单中的 IP 地址发起请求无法访问资源。 |
|Enable |Boolean |是 |`true` |是否启用当前 IP 访问规则配置。取值及含义如下。<br><br><br>* `true`：启用；<br><br>* `false`：禁用。 |
|IPList |String 数组 |是 |`["1.1.1.2","192.168.0.1/24"]` |白名单或黑名单中的 IP 地址列表。仅支持 IPv4 地址。支持 CIDR 表示法。例如，可以指定 192.168.0.0 或 192.168.0.0/24。 |


<span id="Response parameters"></span>
## 返回参数

该 API 仅在返回调用结果中返回 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=UpdateIPAccessRule&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "Domain": "push.example.com",
    "IPAccessRule": [
        {
            "Type": "deny",
            "Enable": true,
            "IPList": [
                "192.168.1.1",
                "192.168.1.2"
            ]
        }
    ]
}
```


<span id="Sample response"></span>
### 响应示例

```json
{
    "ResponseMetadata": {
        "RequestID": "202011121850010102250920591B011F85",
        "Action": "UpdateIPAccessRule",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为当前操作相关的错误码。其他错误码请参见 [BytePlus OpenAPI 通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|200 |CommonErr |*  |未分类错误。建议重试。如仍返回该错误码，请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考 [请求参数](https://docs.byteplus.com/en/docs/24/106927#request-parameters)说明进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验失败。请检查数据类型是否正确。 |
|400 |InvalidParam.Empty |%s 为必填项 |参数缺失。请检查错误信息中指定的参数是否已传入。 |
|403 |RequestForbidden |*  |请求被拒绝，因为当前账号下无所请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllow |该 AccountID 无权限访问对应资源，请检查请求参数 |请求被拒绝，因为当前账号下无所请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.BillingStatus |该 AccountID 未开通计费情况，请激活服务或充值。 |视频直播服务尚未开启或账户存在欠费，导致账单不可用。请检查服务激活状态及账户欠费状态。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用名称、配置和证书）。建议重试。如果仍然返回错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.DomainNotExist |未找到域名 |未找到域名（Domain）。请检查传入的域名是否与实际使用的域名一致。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |发生与数据库相关的内部错误，请联系管理员。 |发生与数据库相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
