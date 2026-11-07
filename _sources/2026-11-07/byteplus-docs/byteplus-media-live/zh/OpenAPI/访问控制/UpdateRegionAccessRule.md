---
title: "UpdateRegionAccessRule"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateregionaccessrule-zh-CN"
---

调用 `UpdateRegionAccessRule` API，为指定域名创建地理位置限制。

<span id="Requirements"></span>
## 要求

速率限制：每个账号每秒最多 10 次查询。

<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=UpdateRegionAccessRule&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用时，除了 API 专属参数外，还必须包含 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### Query


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`UpdateRegionAccessRule` |API 操作。 |
|Version |String |是 |`2023-01-01` |该 API 操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |域名空间。你可以调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或访问 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 页面，获取该域名所属的域名空间。 |
|Domain |String |是 |`pull.example.com` |拉流域名。你可以调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或访问 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 页面，获取用于创建地理位置限制的域名。 |
|RegionAccessRule |[RegionAccessRule](https://docs.byteplus.com/en/docs/24/106892#regionaccessrule) 对象 |是 |`-` |地理位置限制。 |


<span id="regionaccessrule"></span>
### RegionAccessRule


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Type |String |是 |`allow` |访问控制类型。<br><br><br>* `allow`：仅允许指定地区的请求访问你的域名。<br><br>* `deny`：禁止指定地区的请求访问你的域名。 |
|Enable |String |是 |`true` |是否启用该配置。<br><br><br>* `true`：启用该配置。<br><br>* `false`：禁用该配置。 |
|CountryList |Array of String |否 |`CN` |allowlist 或 blocklist 中的国家和地区。使用 ISO 3166\-1 代码表示国家和地区，例如 CN、SG 或 US。 |
|ProvinceList |Array of String |否 |`HK` |allowlist 或 blocklist 中的省份，目前仅支持中国的香港、澳门和台湾地区。对应代码分别为 HK、MO 和 TW。 |


<span id="Response parameters"></span>
## 返回调用结果参数

该 API 仅在返回调用结果中返回 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=UpdateRegionAccessRule&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "Domain": "pull.example.com",
    "RegionAccessRule": [
        {
            "Type": "allow",
            "Enable": true,
            "CountryList": [
                "CN",
                "SG"
            ]
        }
    ]
}
```


<span id="Sample response"></span>
### 返回调用结果示例

```json
{
    "ResponseMetadata": {
        "RequestID": "202011121850010102250920591B011F85",
        "Action": "UpdateRegionAccessRule",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为当前操作相关的错误码。其他错误码请参见 [BytePlus OpenAPI 通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**Status Code** |**Error Code** |**Error Message** |**接口行为** |
|---|---|---|---|
|200 |CommonErr |*  |未分类错误。建议重试。如果仍返回该错误码，请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考 [请求参数](https://docs.byteplus.com/en/docs/24/106892#request-parameters)说明进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验失败。请检查数据类型是否正确。 |
|400 |InvalidParam.DomainAndApp |domain 和应用不能同时存在 |不能同时传入 Domain 和应用。请修改输入参数。 |
|403 |RequestForbidden |*  |请求被拒绝，因为当前账号下无所请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllow |该 AccountID 无权限访问对应资源，请检查请求参数 |请求被拒绝，因为当前账号下无所请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.BillingStatus |AccountID 的计费情况不可用，请激活服务或充值。 |视频直播服务尚未开启或账户存在欠费，导致账单不可用。请检查服务激活状态和账户欠费状态。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用、配置和证书）。建议重试。如果仍然返回错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.DomainNotExist |未找到域名 |未找到域名（Domain）。请检查传入的域名是否与实际使用的域名一致。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |发生与数据库相关的内部错误，请联系管理员。 |发生与数据库相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
