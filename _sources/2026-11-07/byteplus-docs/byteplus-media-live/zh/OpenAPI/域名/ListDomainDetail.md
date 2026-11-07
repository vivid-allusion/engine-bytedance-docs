---
title: "ListDomainDetail"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023-zh-CN"
---

调用 `ListDomainDetail` API 查询您账号下的域名信息。您可以根据域名状态、域名类型及其他维度筛选查询结果。

<span id="Requirements"></span>
## 要求

频率限制：每个账号每秒最多查询 1 次。

<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=ListDomainDetail&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 除了特定参数外，还必须携带 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`ListDomainDetail` |API 操作。 |
|Version |String |是 |`2023-01-01` |该 API 操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### 请求体参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|PageNum |Integer |是 |`1` |页码。BytePlus MediaLive 会将查询结果分页，仅返回指定页的结果。支持范围：1–1000。 |
|PageSize |Integer |是 |`10` |每页结果数量。支持范围：1–1000。 |
|VhostList |Array of String |否 |`["push.example.com","pull.example.com"]` |名称空间列表，默认表示查询所有名称空间下的域名。 |
|DomainStatusList |Array of Integer |否 |`[0,2,3]` |查询包含的域名状态列表。如未指定，将查询所有状态的域名。支持的值包括：<br><br><br>* `0`: 已开启。<br><br>* `1`: 审核中。<br><br>* `2`: 未开启。注意，未开启的域名无法使用。<br><br>* `3`: 已删除。<br><br>* `4`: 已驳回。您需要重新提交域名审核。<br><br>* `5`: 因账号欠费被冻结。<br><br>* `6`: 因未备案被封禁。 |
|DomainTypeList |Array of String |否 |`["push","pull-flv"]` |查询包含的域名类型列表。如未指定，将查询两种类型的域名。支持的值包括：<br><br><br>* `push`: 推流域名。<br><br>* `pull-flv`: 拉流域名。 |
|DomainRegionList |Array of String |否 |`["cn"]` |加速区域。支持的值包括：<br><br><br>* `oversea`:（默认）中国大陆以外。<br><br>* `cn`: 中国大陆。<br><br>* `global`: 全球。 |
|DomainNameList |Array of String |否 |`["push.example.com","pull.example.com"]` |查询包含的域名列表。如未指定，将查询您所有的域名。 |


<span id="Response parameters"></span>
## 返回调用结果参数

关于唯一的 API 特定返回调用结果参数，请参见下表。更多详情请参考 [请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|DomainList |Array of [DomainList](https://docs.byteplus.com/en/docs/24/106903#domainlist) |`-` |域名信息。 |
|Total |Integer |`2` |查询结果总数。 |


<span id="domainlist"></span>
### DomainList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Vhost |String |`push.example.com` |对应的域名空间。 |
|Domain |String |`push.example.com` |域名。 |
|Status |Integer |`0` |域名状态。支持的值包括：<br><br><br>* `0`: 已开启。<br><br>* `1`: 审核中。<br><br>* `2`: 未开启。注意，未开启的域名无法使用。<br><br>* `3`: 已删除。<br><br>* `4`: 已驳回。您需要重新提交域名审核。<br><br>* `5`: 因账号欠费被冻结。<br><br>* `6`: 因未备案被封禁。 |
|Type |String |`pull` |域名类型。支持的值包括：<br><br><br>* `push`: 推流域名。<br><br>* `pull-flv`: 拉流域名。 |
|Region |String |`cn` |加速区域列表。有效值包括：<br><br><br>* `oversea`：中国大陆以外。<br><br>* `cn`：中国大陆。<br><br>* `global`：全球。 |
|CNAME |字符串 |`push.example.com.bytefcdn.com` |分配给域名的 CNAME 地址。 |
|CnameCheck |整数 |`0` |CNAME 地址的状态。<br><br><br>* `0`：未配置。<br><br>* `1`：已配置。 |
|DomainCheck |整数 |`0` |域名的可用性。<br><br><br>* `0`：正常。域名可用且已配置。<br><br>* `1`：配置中。域名可用，正在配置中。<br><br>* `2`：不可用。域名不可用。 |
|ICPCheck |整数 |`1` |域名是否已完成 ICP 备案。当域名加速区域包含中国大陆时，将校验该参数。当域名加速区域不包含中国大陆时，请忽略该参数。 |
|CreateTime |字符串 |`2006-01-02T15:04:05+08:00` |域名的创建时间。 |
|CertDomain |字符串 |`*.example.com` |由关联证书保护的泛域名。 |
|HTTP2 |布尔值 |`false` |是否已开启 HTTP/2 协议。取值如下：<br><br><br>* `false`：未开启<br><br>* `true`：已开启 |
|ChainID |字符串 |`21614` |关联证书的链 ID。 |
|PushDomain |字符串 |`push.example.com` |关联的推流域名。 |
|ProjectName |字符串 |`default` |与域名空间关联的项目。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=ListDomainDetail&Version=2023-01-01
{
    "DomainTypeList": [
        "pull-flv",
        "push"
    ],
    "PageNum": 1,
    "PageSize": 10
}
```


<span id="Sample response"></span>
### 返回示例

```json
{
    "ResponseMetadata":{
        "RequestId":"201806041104200100100232280022D30",
        "Action":"ListDomainDetail",
        "Version":"2023-01-01",
        "Service":"live",
        "Region": "cn-north-1"
    }
    "Resutl": { 
        "DomainList": [
            {
                "Domain": "push.example.com",
                "Status": 0,
                "Type": "push",
                "Region": "cn",
                "CName": "push.example.com.bytefcdn.com",
                "CnameCheck":0,
                "DomainCheck":0,
                "CreateTime":"2006-01-02T15:04:05+08:00"
            },
            {
                "Domain": "pull.example.com",
                "Status": 0,
                "Type": "pull",
                "Region": "cn",
                "CName": "pull.example.com.bytefcdn.com",
                "CnameCheck":0,
                "DomainCheck":0,
                "CreateTime":"2006-01-02T15:04:05+08:00"
            }
        ],
        "Total": 2 
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为当前操作相关的错误码。其他错误码请参见 [BytePlus OpenAPI 通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|200 |CommonErr |*  |未分类错误。建议重试。如仍返回错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/106903#request-parameters)说明进行排查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验未通过。请检查数据类型是否正确。 |
|403 |RequestForbidden |*  |请求被拒绝，当前账号下无请求的资源（资源包括域名空间、域名、应用、配置、证书）。 |
|403 |RequestForbidden.AccountIDNotAllowed |该 AccountID 无权访问对应资源，请检查请求参数 |请求被拒绝，当前账号下无请求的资源（资源包括域名空间、域名、应用、配置、证书）。 |
|403 |RequestForbidden.BillingStatus |该 AccountID 未开通计费情况，请开通服务或充值。 |未开通视频直播服务或账号欠费，导致账单不可用。请检查服务开通状态及账号欠费情况。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用、配置、证书）。建议重试。如仍返回错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |发生与数据库相关的内部错误，请联系管理员。 |发生与数据库相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParameter.Tags.Key |指定的参数 Tags.Key 无效。 |参数`Tags.Key`未通过校验。请检查参数是否正确。 |
|400 |InvalidParameter.Tags.Value |指定的参数 Tags.Value 无效。 |参数`Tags.Value`未通过验证。请检查参数是否正确。 |
