---
title: "CreateCert"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createcert-2023-zh-CN"
---

调用 `CreateCert` API，将证书添加或更新至 MediaLive，以便后续绑定到域名并启用 HTTPS。

<span id="Requirements"></span>
## 要求

频率限制：每个账号每秒 1 次请求。

<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=CreateCert&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用除需传递 API 专属参数外，还必须携带 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`CreateCert` |API 操作名称。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本号。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|ProjectName |String |否 |`default` |项目名称。设置证书的项目归属。默认值为 `Default`。设置项目后，拥有项目权限的子账号可使用该证书。 |
|CertName |String |否 |`pushCertName` |证书名称。 |
|ChainID |String |否 |`9*********a982edf6e84bba1f` |证书链 ID。用于标识整个证书链，包括终端实体证书（服务器证书）、中间证书（中间 CA 证书）和根证书（根 CA 证书）。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">使用当前 API 更新证书信息时，必须传入 <code>ChainID</code>。</div><br> |
|Rsa |[Rsa](https://docs.byteplus.com/en/docs/24/106905#rsa) 对象 |是 |`-` |证书信息，包含证书内容及证书私钥内容。 |
|UseWay |String |是 |`https` |证书用途。始终设置为 `https`，表示 HTTPS 加密。 |


<span id="rsa"></span>
### Rsa


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Pubkey |String |是 |`*******` |证书内容。需在电脑上使用文本编辑器打开证书，并将全部内容复制粘贴作为参数。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">系统支持自动获取证书链。只需上传为您的域名签发的证书，系统会自动获取完整证书链。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">如选择上传证书链，请确保包含服务器证书、中间证书和根证书，并按正确顺序排列：服务器证书在前，其次为中间证书，最后为根证书。顺序错误将导致证书链失效。</div><br> |
|Prikey |String |是 |`*******` |证书私钥内容。需在电脑上使用文本编辑器打开证书私钥，并将全部内容复制粘贴作为参数。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">请确保证书私钥未设置密码保护。</div><br> |


<span id="Response parameters"></span>
## 返回调用结果参数

关于 API 专属返回调用结果参数，请参见下表。更多详情请参见 [请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|ChainID |String |`9*********a982edf6e84bba1f` |证书链 ID。 |
|Domain |String |`live.example.com` |使用当前证书的域名。 |
|UseWay |String |`https` |证书用途。始终设置为 `https`，表示 HTTPS 加密。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=CreateCert&Version=2023-01-01
{
    "UseWay": "https",
    "Rsa": {
        "PubKey": "******",
        "PriKey": "******"
    }
}
```


<span id="Sample response"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestID": "2020091618492801022706705734830",
        "Action": "CreateCert",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "cn-north-1"
    },
    "Result": {
        "ChainID": "9**47c0151394d93a982edf6e84bba1f",
        "Domain": "push.example.com",
        "UseWay": "https"
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为本次操作相关的错误码。其他错误码请参见 [BytePlus OpenAPI 通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|200 |CommonErr |*  |未分类错误。建议重试。如果仍然返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/106905#request-parameters)接口行为进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据。 |参数校验失败。请检查数据类型是否正确。 |
|400 |InvalidParam.OutOfRange |%s 应为 {[%s]} 之一%s 应在 %d 到 %d 之间 |参数超出允许范围。请检查错误信息中指定参数的值是否超出取值范围。 |
|403 |RequestForbidden |*  |请求被拒绝，因为当前账号下不存在所请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllow |该 AccountID 无权限访问对应资源，请检查请求参数。 |请求被拒绝，因为当前账号下不存在所请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.BillingStatus |该 AccountID 的计费情况不可用，请开通服务或充值。 |视频直播服务未开启或账号欠费，导致账单不可用。请检查服务开通状态及账号欠费状态。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用名称、配置和证书）。建议重试。如果仍然返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |发生与数据库相关的内部错误，请联系管理员。 |发生与数据库相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
