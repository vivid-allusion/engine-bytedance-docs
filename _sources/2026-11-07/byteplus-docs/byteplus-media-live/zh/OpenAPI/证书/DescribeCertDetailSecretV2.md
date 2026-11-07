---
title: "DescribeCertDetailSecretV2"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecertdetailsecretv2-2023-zh-CN"
---

调用 `DescribeCertDetailSecretV2` API，通过证书 ID 或证书链 ID 查看证书的详细信息。

<span id="Requirements"></span>
## 要求

频率限制：每个账号每秒最多查询 10 次。

<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DescribeCertDetailSecretV2&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用时，除了 API 专属参数外，还必须携带 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`DescribeCertDetailSecretV2` |API 操作。 |
|Version |String |是 |`2023-01-01` |该 API 操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|CertID |String |否 |`812******1` |证书 ID。可调用 [ListCertV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listcertv2) API 获取 CertID。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">应仅提供 <code>ChainID</code> 或 <code>CertID</code>，不可同时提供。</div><br> |
|ChainID |String |否 |`188b5c6f6b3c47728418932*******d2` |证书的 ChainID。可调用 [ListCertV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listcertv2) API 获取 ChainID。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">应仅提供 <code>ChainID</code> 或 <code>CertID</code>，不可同时提供。</div><br> |


<span id="Response parameters"></span>
## 返回调用结果参数

有关唯一的 API 专属返回调用结果参数，请参见下表。更多详情请参考 [请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|CertDomainList |String 数组 |`["live.example.com"]` |证书保护的域名列表。 |
|ChainID |String |`188b5c6f6b3c47728418932*******d2` |证书链 ID。 |
|SSL |[SSL](https://docs.byteplus.com/en/docs/24/106919#ssl) 对象 |`-` |证书链信息。 |
|CertName |String |`live.example.com` |证书名称。 |
|NotBefore |String |`2019-09-05T00:00:00Z` |证书生效时间（UTC 时间，RFC 3339 格式，时间戳精确到秒）。 |
|NotAfter |String |`2020-09-04T12:00:00Z` |证书过期时间（UTC 时间，RFC 3339 格式，时间戳精确到秒）。 |
|Status |String |`OK` |证书状态，各值与含义的对应关系如下。<br><br><br>* `OK`：正常；<br><br>* `Expire`：已过期；<br><br>* `30days`：有效期剩余 30 天；<br><br>* `15days`：有效期剩余 15 天；<br><br>* `7days`：有效期剩余 7 天；<br><br>* `1days`：有效期剩余 1 天。 |


<span id="ssl"></span>
### SSL


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|KeyType |String |`rsa` |证书使用的加密算法，目前默认为 RSA 算法。 |
|Chain |String 数组 |`[ "-----BEGIN CERTIFICATE-----MIIFa**********5S98-----END CERTIFICATE-----", "-----BEGIN CERTIFICATE-----MIIEk**********0UiB-----END CERTIFICATE-----", "-----BEGIN CERTIFICATE-----MIIEN**********B5==-----END CERTIFICATE-----" ]` |证书链，包括叶子证书（服务器证书）、中间证书（中间 CA 证书）和根证书（根 CA 证书）。证书链中的证书采用 PEM 编码格式。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=DescribeCertDetailSecretV2&Version=2023-01-01
{
    "ChainID": "188b5c6f6b3c47728418932*******d2"
}
```


<span id="Sample response"></span>
### 返回调用结果示例

```json
{
    "ResponseMetadata": {
        "RequestId": "202306041104200100100232280022D31",
        "Action": "DescribeCertDetailV2",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "CertDomainList": [
        "pull.example.xyz"
        ],
        "CertName": "pull.example.xyz",
        "ChainID": "37a***b22d554a3b8785f111d51a2b88",
        "NotAfter": "2024-08-03T23:59:59Z",
        "NotBefore": "2024-05-06T00:00:00Z",
        "SSL": {
        "Chain": [
            "-----BEGIN CERTIFICATE-----\nMIIF+TCCBOG***UrNyWlJ7\n-----END CERTIFICATE-----\n",
            "-----BEGIN CERTIFICATE-----\nMIIEqjCCA5K***QjJNSg==\n-----END CERTIFICATE-----\n",
            "-----BEGIN CERTIFICATE-----\nMIIDjjCCAna***Zl\nMrY=\n-----END CERTIFICATE-----\n"
        ]
        "KeyType": "rsa",
        },
        "Status": "OK"
    }
    }
```


<span id="Error codes"></span>
## 错误码

以下为当前操作相关的错误码。其他错误码请参见 [BytePlus OpenAPI 通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|200 |CommonErr |*  |未分类错误。建议重试。若仍返回该错误码，请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考 [请求参数](https://docs.byteplus.com/en/docs/24/106919#request-parameters)说明进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验未通过。请检查数据类型是否正确。 |
|403 |RequestForbidden |*  |请求被拒绝，因为当前账号下无请求资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllowed |该 AccountID 无权限访问对应资源，请检查请求参数 |请求被拒绝。当前账号下不存在所请求的资源（域名空间、域名、应用、配置模版、证书）。 |
|403 |RequestForbidden.BillingStatus |该 AccountID 的计费情况不可用，请开通服务或充值。 |视频直播服务尚未开启或账号存在欠费，导致账单不可用。请检查服务开通状态及账号欠费情况。 |
|403 |AccessDenied |用户无权执行操作：%s 在资源 %s 上 |请求被拒绝。当前账号下不存在所请求的资源（域名空间、域名、应用、配置模版、证书）或接口权限。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用、配置、证书）。建议重试。若仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |发生与数据库相关的内部错误，请联系管理员。 |发生与数据库相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
