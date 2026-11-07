---
title: "UpdateEncryptDRM"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateencryptdrm-zh-CN"
---

上传 DRM API 密钥和/或 FairPlay 证书，或更新已有的密钥或证书。

<span id="Requirements"></span>
## 要求

请求频率限制：每个账号每秒最多 1 次查询。

<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=UpdateEncryptDRM&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用时，除了 API 专属参数外，还必须包含 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`UpdateEncryptDRM` |API 操作。 |
|Version |String |是 |`2023-01-01` |该 API 操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|APIKey |String |否 |`12312,162632123abfc344321234212344323432` |DRM API 密钥。 |
|CertificateName |String |否 |`test-drm-cert` |自定义证书名称。 |
|PrivateKeyFile |String |否 |`asdasdasdasd1w1wd1wd` |私钥文件内容。 |
|PrivateKeyFileName |String |否 |`pri.pem` |私钥文件名称。 |
|CertificateFile |String |否 |`asd13dsfdasdasd1ewd` |证书文件内容。 |
|CertificateFileName |String |否 |`certificate.cer` |证书文件名称。 |
|ApplicationSecretKey |String |否 |`NODIW347219BIUDW93` |申请证书时由 Apple 提供的 Application Secret Key（ASk）。 |
|PrivateKey |String |否 |`2023` |用于解密私钥文件的密钥。 |


<span id="Response parameters"></span>
## 返回调用结果

该 API 仅在返回调用结果中返回 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=UpdateEncryptDRM&Version=2023-01-01
{
    "APIKey": "12312,1626*****abfc344321234212344323432",
    "CertificateName": "test-drm-cert",
    "PrivateKeyFile": "asdasda*****1w1wd1wd",
    "PrivateKeyFileName": "pri.pem",
    "CertificateFile": "asd13*****dasd1ewd",
    "CertificateFileName": "certificate.cer",
    "ApplicationSecretKey": "NODIW3*****BIUDW93",
    "PrivateKey": "1234"
}
```


<span id="Sample response"></span>
### 返回调用结果示例

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "UpdateEncryptDRM",
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
|200 |CommonErr |*  |未分类错误。建议重试。若仍返回该错误码，请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考 [请求参数](https://docs.byteplus.com/en/docs/24/106914#request-parameters)说明进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验失败。请检查数据类型是否正确。 |
|403 |RequestForbidden |*  |请求被拒绝，当前账号下无请求资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllow |该 AccountID 无权限访问对应资源，请检查请求参数 |请求被拒绝，当前账号下无请求资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.BillingStatus |该 AccountID 的计费情况不可用，请开通服务或充值。 |视频直播服务未已开启或账号欠费，导致账单不可用。请检查服务开通状态及账号欠费情况。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用名称、配置和证书）。建议重试。若仍返回该错误码，请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |发生数据库相关的内部错误，请联系管理员。 |发生数据库相关的内部错误。请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
