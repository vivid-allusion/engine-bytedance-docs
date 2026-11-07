---
title: "BindEncryptDRM"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-bindencryptdrm-zh-CN"
---

调用 `BindEncryptDRM` API，为直播流添加或更新DRM加密配置。

## 要求

* 计费情况：对转码流进行加密会产生转码费用。有关详细费用信息，请参阅 [转码计费](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-transcoding)。

* 频率限制：每个账号每秒最多查询1次。

* 生效时间：配置添加或更新后，3至5分钟生效。

## HTTP请求

* 方法：POST

* 接口地址：https://open.byteplusapi.com/?Action=BindEncryptDRM&Version=2023\-01\-01

## 请求参数

### 通用参数

所有API调用时，除API专属参数外，还需包含 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

### 查询参数

|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`BindEncryptDRM` |API操作名称。 |
|Version |String |是 |`2023-01-01` |该API操作的版本。当前版本：2023\-01\-01。 |

### Body参数

|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |该域名所属的域名空间。可调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或在 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 页面获取域名空间。 |
|应用 |String |是 |`live` |直播流URL中的AppName字段。可包含大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和点（.），长度为1至30个字符。 |
|DRMSystems |String数组 |是 |`["FairPlay","Widevine"]` |加密类型。支持的取值如下。<br><br><br>* `FairPlay`：使用FairPlay技术的商业DRM加密；<br><br>* `Widevine`：使用Widevine技术的商业DRM加密；<br><br>* `PlayReady`：使用PlayReady技术的商业DRM加密；<br><br>* `ClearKey`：HLS标准加密。<br><br><br>> **说明**<br><br><br>> DRM加密与HLS标准加密不可同时配置。<br> |
|EncryptOriginStream |Boolean |是 |`true` |是否开启源流加密，取值及含义如下。<br><br><br>* `true`：已开启；<br><br>* `false`：未开启。<br><br><br>> **说明**<br><br><br>> 源流和转码流至少有一个需开启录制。<br> |
|EncryptTranscodeStream |Boolean |是 |`true` |是否开启转码流加密，取值及含义如下。<br><br><br>* `true`：已开启；<br><br>* `false`：未开启。<br><br><br>> **说明**<br><br><br>> 源流和转码流至少有一个需开启录制。<br> |
|EncryptTranscodeSuffix |String数组 |否 |`["_uhd","hd"]` |开启转码流加密时，配置需加密的转码流后缀。 |

## 返回调用结果参数

该API仅在返回调用结果中返回 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

## 示例

### 请求示例

```json
POST https://open.byteplusapi.com/?Action=BindEncryptDRM&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "App": "live",
    "Enable": true,
    "EncryptTranscodeSuffix": [
        "_uhd",
        "hd"
    ],
    "EncryptTranscodeStream": true,
    "EncryptOriginStream": true,
    "DRMSystems": [
        "FairPlay",
        "Widevine"
    ]
}
```

### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "202306041104200100100232280022D31",
        "Action": "BindEncryptDRM",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "cn-north-1"
    }
}
```

## 错误码

以下为当前操作相关的错误码。其他错误码请参见 [BytePlus OpenAPI通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|200 |CommonErr |*  |未分类错误。建议重试。如仍返回该错误码，请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考 [请求参数](https://docs.byteplus.com/en/docs/24/124022#request-parameters)说明进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验失败。请检查数据类型是否正确。 |
|403 |RequestForbidden |*  |请求被拒绝，当前账号下无所需资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllow |该 AccountID 没有权限访问对应资源，请检查请求参数 |请求被拒绝，因为当前账号下没有请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.BillingStatus |该 AccountID 的计费情况不可用，请激活服务或充值。 |视频直播流服务尚未开启或账号存在欠费，导致账单不可用。请检查服务开通状态及账号欠费状态。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用名称、配置和证书）。建议重试。如果仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |发生与数据库相关的内部错误，请联系管理员。 |发生与数据库相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
