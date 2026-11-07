---
title: "ListStorageSpaceDetail"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-liststoragespacedetail-zh-CN"
---

调用 `ListStorageSpaceDetail` API 查询账户下指定存储空间的详细信息。

<span id="Requirements"></span>
## 要求

限流：每个账户每秒最多 100 次查询。

<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=ListStorageSpaceDetail&Version=2020\-08\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用时，除 API 专属参数外，还需包含 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`ListStorageSpaceDetail` |API 操作名称。 |
|Version |String |是 |`2020-08-01` |此 API 操作的版本。当前版本：2020\-08\-01。 |


<span id="Body parameters"></span>
### 请求体参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|StorageSpaceList |String 数组 |否 |`["bucket112233"]` |需要查询的存储空间列表。如未指定，则会查询账户下所有存储空间。 |


<span id="Response parameters"></span>
## 返回调用结果参数

关于唯一的 API 专属返回调用结果参数，请参见下表。更多详情请参考 [请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|StorageSpaceListDetail |[StorageSpaceListDetail](https://docs.byteplus.com/en/docs/24/107027#storagespacelistdetail) 数组 |`-` |每个被查询存储空间的详细信息。 |


<span id="storagespacelistdetail"></span>
### StorageSpaceListDetail


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|AccountID |String |`3000000285` |您的账户 ID。 |
|Name |String |`fcdn-boe` |存储空间名称。 |
|PublicDomain |String |`该参数已废弃。`<br><br>` \|存储空间的公共域名。 \| | |
|CnameDomain |String |`ccama.test.example.com` |公共域名指向的规范名称。 |
|TTL |Integer |`-` |该参数已废弃。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

<span id="Sample response"></span>
### 返回调用结果示例

```json
{
    "ResponseMetadata": {
        "RequestId": "202204060959170101742350380764F506",
        "Action": "ListStorageSpace",
        "Version": "2020-08-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "StorageSpaceListDetail": [
            {
                "AccountID": "3000000285",
                "Name": "fcdn-boe",
                "PublicDomain": "test.example.com",
                "CnameDomain": "cname.test.example.com"
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
|200 |CommonErr |*  |未分类错误。建议重试。如仍返回错误码，请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考 [请求参数](https://docs.byteplus.com/en/docs/24/107027#request-parameters)说明进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验失败。请检查数据类型是否正确。 |
|403 |RequestForbidden |*  |请求被拒绝，因为当前账户下无所请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllow |该 AccountID 无权限访问对应资源，请检查请求参数 |请求被拒绝，因为当前账户下无所请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.BillingStatus |该 AccountID 的计费情况不可用，请先开通服务或充值。 |视频直播服务未开启或账户欠费，导致账单不可用。请检查服务开通状态及账户欠费情况。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用名称、配置和证书）。建议重试。如仍返回错误码，请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |发生与数据库相关的内部错误，请联系管理员。 |发生与数据库相关的内部错误。请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系客服](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系客服](https://console.byteplus.com/workorder/create)。 |
