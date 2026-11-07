---
title: "DescribeLicenseDRM"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelicensedrm-zh-CN"
---

获取DRM许可证。播放器使用该许可证对DRM加密的直播流进行解密。

<span id="Requirements"></span>
## 要求

速率限制：每个账号每秒最多1次查询。

<span id="HTTP request"></span>
## HTTP请求


* 方法：POST

* Endpoint：https://live\-gateway\-byteplus.byteintlapi.com/drm_api/?Action=DescribeLicenseDRM&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有API调用时，除了API专用参数外，还必须包含[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Headers"></span>
### 请求头


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Content\-Type |String |是 |`application/x-www-form-urlencoded` |只能为`application/x-www-form-urlencoded`，表示键值对以'&'分隔，键和值之间用'='连接。键和值中的非字母数字字符需[URL编码](https://en.wikipedia.org/wiki/URL_encoding)。 |


<span id="Query"></span>
### 查询参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLicenseDRM` |API操作。 |
|Version |String |是 |`2023-01-01` |该API操作的版本。当前版本：2023\-01\-01。 |
|Vhost |String |是 |`drm.example.com` |域名空间。可调用[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API或在BytePlus MediaLive控制台的[Domains](https://console.byteplus.com/live/main/domain/list)页面获取该域名所属的域名空间。 |
|Domain |String |是 |`pull.example.com` |拉流域名。可调用[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API或在BytePlus MediaLive控制台的[Domains](https://console.byteplus.com/live/main/domain/list)页面获取域名。 |
|应用 |String |是 |`live` |直播流URL中的AppName字段。可包含大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和点（.），长度为1至30个字符。 |
|StreamName |String |是 |`stream-drm` |直播流URL中的StreamName字段。可包含大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和点（.），长度为1至100个字符。 |
|DRMType |String |是 |`fp` |DRM加密类型。有效值包括：<br><br><br>* `fp`：FairPlay<br><br>* `wv`：Widevine<br><br>* `pr`：PlayReady |


<span id="Response parameters"></span>
## 返回参数

该API仅返回[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://live-gateway-byteplus.byteintlapi.com/drm_api/?Action=DescribeLicenseDRM&Version=2023-01-01&Vhost=drm.example.com&Domain=pull.example.com&App=live&StreamName=stream-drm&DRMType=fp
```


<span id="Sample response"></span>
### 返回调用结果示例

若请求处理成功，响应体将以二进制数据形式包含许可证文件。

<span id="Error codes"></span>
## 错误码

以下为当前操作相关的错误码。其他错误码请参见[BytePlus OpenAPI通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|200 |CommonErr |*  |未分类错误。建议重试。若仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/106908#request-parameters)说明进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验失败。请检查数据类型是否正确。 |
|403 |RequestForbidden |*  |请求被拒绝，因为当前账号下无所需资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllowed |该AccountID无权限访问对应资源，请检查请求参数 |请求被拒绝，因为当前账号下无所需资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.BillingStatus |AccountID 的计费情况不可用，请激活服务或充值。 |视频直播流服务未开启或账户存在欠费，导致账单不可用。请检查服务激活状态和账户欠费状态。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用名称、配置和证书）。建议重试。如果仍然返回错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |发生与数据库相关的内部错误，请联系管理员。 |发生与数据库相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
