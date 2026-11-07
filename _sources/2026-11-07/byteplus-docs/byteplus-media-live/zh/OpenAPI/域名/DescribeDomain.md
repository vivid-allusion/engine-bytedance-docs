---
title: "DescribeDomain"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describedomain-2023-zh-CN"
---

调用 `DescribeDomain` API 查询指定域名的信息，包括域名空间、CNAME 地址、域名状态等。

<span id="Requirements"></span>
## 要求

频率限制：每个账号每秒最多查询 1 次。

<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DescribeDomain&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用时，除了 API 专属参数外，还必须携带 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`DescribeDomain` |API 操作。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### 请求体参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|DomainList |String 数组 |是 |`["push.example.com","pull.example.com"]` |要查询的域名列表。 |


<span id="Response parameters"></span>
## 返回参数

有关唯一的 API 专属返回参数，请参见下表。更多详情请参考 [请求返回](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|DomainList |[DomainList](https://docs.byteplus.com/en/docs/24/106887#domainlist) 数组 |`-` |域名相关信息。 |


<span id="domainlist"></span>
### DomainList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Vhost |String |`push.example.com` |对应的域名空间。 |
|Domain |String |`push.example.com` |域名。 |
|Status |Integer |`0` |域名状态。有效值包括：<br><br><br>* `0`：已开启。<br><br>* `1`：审核中。<br><br>* `2`：未开启。注意，未开启的域名无法使用。<br><br>* `3`：已删除。<br><br>* `4`：已拒绝。需重新提交域名审核。<br><br>* `5`：因账号欠费被冻结。<br><br>* `6`：因未备案被拦截。 |
|Type |String |`push` |域名类型。有效值包括：<br><br><br>* `push`：推流域名。<br><br>* `pull-flv`：拉流域名。 |
|Region |String |`cn` |加速区域。有效值包括：<br><br><br>* `oversea`：（默认）中国大陆以外。<br><br>* `cn`：中国大陆。<br><br>* `global`：全球。<br><br><br>需先为域名申请互联网内容提供商（ICP）许可证。 |
|CNAME |String |`push.example.com.c.byteplusfcdn.com` |分配给域名的 CNAME 地址。 |
|CnameCheck |Integer |`0` |域名的 CNAME 状态。<br><br><br>* `0`：未配置。<br><br>* `1`：已配置。 |
|DomainCheck |Integer |`0` |域名可用性。<br><br><br>* `0`：正常。域名可用且已配置。<br><br>* `1`：配置中。域名可用且正在配置。<br><br>* `2`：不可用。域名不可用。 |
|ICPCheck |Integer |`0` |域名是否已完成 ICP 备案。当域名加速区域包含中国大陆时，将校验此参数。若域名加速区域不包含中国大陆，请忽略此参数。 |
|CreateTime |String |`2006-01-02T15:04:05Z` |域名创建时间。 |
|CertDomain |String |`push.example.com` |由关联证书保护的泛域名。 |
|HTTP2 |Boolean |`false` |是否启用 HTTP/2 协议。取值如下：<br><br><br>* `false`：未开启<br><br>* `true`：已开启 |
|ChainID |String |`21614` |关联证书的链 ID。 |
|PushDomain |String |`push.example.com` |关联的推流域名。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=DescribeDomain&Version=2023-01-01
{
    "DomainList": [
        "push.example.com"
    ]
}
```


<span id="Sample response"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "DescribeDomain",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "DomainList": [
            {
                "Domain": "push.example.com",
                "Status": 0,
                "Type": "push",
                "Region": "cn",
                "CName": "push.example.com.c.byteplusfcdn.com",
                "PushDomain": "push.example.com",
                "Vhost": "push.example.com",
                "CnameCheck": 0,
                "DomainCheck": 0,
                "CreateTime": "2006-01-02T15:04:05Z"
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为当前操作相关的错误码。其他错误码请参见 [BytePlus OpenAPI 通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|200 |CommonErr |*  |未分类错误。建议重试。若仍返回错误码，请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/106887#request-parameters)说明进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据。 |参数校验失败。请检查数据类型是否正确。 |
|403 |RequestForbidden |*  |由于当前账号下不存在请求的资源（资源包括域名空间、域名、应用、配置和证书），请求被拒绝。 |
|403 |RequestForbidden.AccountIDNotAllowed |该AccountID无权访问对应资源，请检查请求参数。 |由于当前账号下不存在请求的资源（资源包括域名空间、域名、应用、配置和证书），请求被拒绝。 |
|403 |RequestForbidden.BillingStatus |该AccountID的计费情况不可用，请开通服务或充值。 |视频直播服务未已开启或账号欠费，导致账单不可用。请检查服务开通状态及账号欠费状态。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用、配置和证书）。建议重试。如果仍返回错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |发生与数据库相关的内部错误，请联系管理员。 |发生与数据库相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
