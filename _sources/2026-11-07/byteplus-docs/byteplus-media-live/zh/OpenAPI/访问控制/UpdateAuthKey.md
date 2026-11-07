---
title: "UpdateAuthKey"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateauthkey-2023-zh-CN"
---

调用 `UpdateAuthKey` API，为推流和拉流地址添加或更新 URL 鉴权配置。使用该 API 更新配置时，所有鉴权参数将被更新。

<span id="Requirements"></span>
## 要求

频率限制：每个账号每秒最多 1 次查询。

<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=UpdateAuthKey&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用时，除 API 专属参数外，还需包含 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### Query


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`UpdateAuthKey` |API 操作。 |
|Version |String |是 |`2023-01-01` |该 API 操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Domain |String |是 |`live.push.example.com` |域名。可调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或在 BytePlus MediaLive 控制台的 [域名管理](https://console.byteplus.com/live/main/domain/list)页面获取域名。 |
|SceneType |String |是 |`push` |鉴权场景类型，取值及含义如下。<br><br><br>* `push`：推流鉴权。<br><br>* `pull`：拉流鉴权。 |
|AuthDetailList |[AuthDetailList](https://docs.byteplus.com/en/docs/24/106893#authdetaillist) 数组 |是 |`-` |鉴权信息列表。最多可添加 100 个数组元素。 |
|ValidDuration |Integer |否 |`60` |鉴权信息的有效期，单位为秒。默认值为 `0`。支持范围：[0,2592000]。 |
|PushPullEnable |Boolean |否 |`true` |当前鉴权配置是否已开启。<br><br><br>* `false`：（默认）未开启。<br><br>* `true`：已开启。 |
|TimeStampBase |Integer |否 |`10` |时间戳的时间格式。默认值为 `10`。但当 `AuthType` 设置为 `TypeC` 时，默认值为 `16`。有效取值：<br><br><br>* `2`：二进制。<br><br>* `8`：八进制。<br><br>* `10`：十进制。<br><br>* `16`：十六进制。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">当 <code>SceneType</code> 设置为 <code>push</code> 时，该参数值固定为 <code>10</code>。</div><br> |


<span id="authdetaillist"></span>
### AuthDetailList


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|SecretKey |String |是 |`1*****1` |鉴权密钥。可包含大写字母（A\-Z）、小写字母（a\-z）及数字（0\-9），长度为 1\-100 个字符。 |
|EncryptionAlgorithm |String |是 |`md5` |加密字符串生成算法。有效取值：<br><br><br>* `md5`：标准 MD5 算法。当 `AuthType` 设置为 `TypeA`、`TypeB` 或 `TypeC` 时，该参数必须设置为 `md5`。<br><br>* `md5_custom`：自定义 MD5 算法。当 `AuthType` 设置为 `TypeCustom` 时，该参数必须设置为 `md5_custom`。 |
|AuthField |JSON Map |否 |`{ "volcSecret":"signature","volcTime":"expireTime" }` |鉴权参数名称。仅当 `AuthType` 设置为 `TypeCustom` 时需配置该参数。<br><br>该参数值为 Key\-Value 对。默认值为 `{"volcSecret":"sign","volcTime":"expire"}`。可自定义 `volcSecret` 和 `volcTime` 的对应值，如 `{"volcSecret":"signature","volcTime":"expireTime"}`，即以 `signature` 作为加密字符串的鉴权参数名称，以 `expireTime` 作为时间戳的鉴权参数名称，从而实现 URL 鉴权。 |
|EncryptField |String 数组 |否 |`["key","volcTime","Domain"]` |生成加密字符串所需的字段。仅当`AuthType`的值设置为`TypeCustom`时，才需要配置此参数。<br><br>该参数默认值为空，但建议至少包含`SecretKey`（认证密钥）和`volcTime`（时间戳）。例如，若参数值为`["SecretKey","volcTime","Domain"]`，则可通过`md5({SecretKey}{volcTime}{Domain})`计算加密字符串。 |
|AuthType |字符串 |是 |`TypeB` |URL鉴权类型。有效值：<br><br><br>* `TypeA`：A类型。<br><br>* `TypeB`：B类型。<br><br>* `TypeC`：C类型。<br><br>* `TypeCustom`：自定义类型。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">当<code>SceneType</code>的值设置为<code>push</code>时，此参数的值只能为<code>TypeB</code>或<code>TypeCustom</code>。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">关于A、B或C类型的更多信息，请参见<a href="https://docs.byteplus.com/en/docs/byteplus-media-live/docs-url-authentication">Configuring URL authentication</a>。</div><br> |


<span id="Response parameters"></span>
## 返回调用结果参数

该 API 仅在返回调用结果中返回 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=UpdateAuthKey&Version=2023-01-01
{
    "AuthDetailList": [
        {
            "SecretKey": "1*****1",
            "EncryptionAlgorithm": "md5",
            "AuthType": "TypeB"
        }
    ],
    "Domain": "live.push.example.com",
    "PushPullEnable": true,
    "SceneType": "push",
    "ValidDuration": 60,
    "TimeStampBase": 10
}
```


<span id="Sample response"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "UpdateAuthKey",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "cn-north-1"
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为当前操作相关的错误码。其他错误码请参见 [BytePlus OpenAPI 通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|200 |CommonErr |*  |未分类错误。建议重试。若仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/106893#request-parameters)说明进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验未通过。请检查数据类型是否正确。 |
|400 |InvalidParam.Length |%s不应超过%d |参数长度不正确。请检查错误信息中指定参数的长度是否超出限制。 |
|403 |RequestForbidden |*  |请求被拒绝，因为当前账号下无请求资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllowed |该AccountID无权限访问对应资源，请检查请求参数 |请求被拒绝，因为当前账号下无请求资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.BillingStatus |该AccountID计费情况不可用，请开通服务或充值。 |视频直播服务未开启或账号欠费，导致账单不可用。请检查服务开通状态及账号欠费情况。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用名称、配置和证书）。建议重试。若仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.VhostNotExist |未找到vhost |未找到域名空间（Vhost）。请检查传入的域名空间是否与实际使用的域名空间一致。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |发生与数据库相关的内部错误，请联系管理员。 |发生与数据库相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
