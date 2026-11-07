---
title: "CreateDomainV2"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-dj3h3u96xn-zh-CN"
---

调用 `CreateDomainV2` API 以添加一个或多个用于推流或拉流的域名。

<span id="Requirements"></span>
## 要求

频率限制：每个账号每秒最多 10 次请求。

<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=CreateDomainV2&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用除需包含 API 专用参数外，还必须携带 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### Query


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`CreateDomainV2` |API 操作。 |
|Version |String |是 |`2023-01-01` |本次 API 操作的版本号。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Domains |[Domains](https://docs.byteplus.com/en/docs/24/106917#domains) 数组 |是 |`-` |域名数组。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">一个域名空间最多可包含 10 个域名。</div><br> |
|Vhost |String |是 |`vhost` |域名空间是相关域名的集合，由字母（A\-Z，a\-z）、数字（0\-9）和连字符（\-）组成。你可以自定义新的域名空间，或调用 ListDomainDetail 接口获取现有域名所使用的域名空间。 |
|ProjectName |String |否 |`default` |与域名空间关联的项目。默认情况下为空，表示属于“default”项目。<br><br>域名空间与项目关联后，可按项目管理资源用量和计费情况。域名空间创建后，项目设置不可更改。如需管理项目，请前往 BytePlus 控制台的 [Project](https://console.byteplus.com/iam/resourcemanage/project) 页面。 |


<span id="domains"></span>
### Domains


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|DomainName |String |是 |`push.example.com` |域名由字母（A\-Z，a\-z）、数字（0\-9）和连字符（\-）组成，长度为 1 到 60 个字符。 |
|ChainID |String |否 |`93cb8cf3*******ece5600142` |SSL 证书链 ID。默认情况下为空，表示该域名未绑定 SSL 证书。你可以调用 [ListCertV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listcertv2) 接口或前往直播控制台的 [证书管理](https://console.byteplus.com/live/main/certificate)页面获取待绑定的证书链 ID。 |
|Type |String |是 |`push` |域名类型：<br><br><br>* `push`：推流域名。<br><br>* `pull-flv`：拉流域名。 |
|Region |String |是 |`cn` |加速区域。可选值包括：<br><br><br>* `oversea`：中国大陆以外。<br><br>* `cn`：中国大陆。<br><br>* `global`：全球。 |


<span id="Response parameters"></span>
## 返回调用结果参数

该 API 的返回调用结果仅包含 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=CreateDomainV2&Version=2023-01-01
{
    "Vhost": "vhost",
    "Domains": [
        {
            "DomainName": "push.example.com",
            "Type": "push",
            "Region": "cn",
            "ChainID": "93cb8cf3*******ece5600142"
        },
        {
            "DomainName": "pull.example.com",
            "Type": "pull-flv",
            "Region": "cn",
            "ChainID": "93c56cf3*******ece522142"
        }
    ],
    "ProjectName": "default"
}
```


<span id="Sample response"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "202306041104200100100232280022D31",
        "Action": "CreateDomainV2",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "cn-north-1"
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为本次操作相关的错误码。其他错误码请参见 [BytePlus OpenAPI 通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|200 |CommonErr |*  |未分类错误。建议重试。如仍返回错误码，请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考 [请求参数](https://docs.byteplus.com/en/docs/24/106917#request-parameters)说明进行排查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验未通过。请检查数据类型是否正确。 |
|400 |InvalidParam.Format |%s 格式错误 |参数格式不正确。请检查错误信息中指定参数是否存在非法字符或 URL 格式错误。 |
|400 |InvalidParam.OutOfRange |%s 应为 {[%s]} 之一%s 应在 %d 和 %d 之间 |参数超出允许范围。请检查错误信息中指定参数的值是否超出取值范围。 |
|400 |InvalidParameter.Tags.Key |指定参数 Tags.Key 无效。 |参数 `Tags.Key` 校验失败。请检查参数是否正确。 |
|400 |InvalidParameter.Tags.Value |指定参数 Tags.Value 无效。 |参数 `Tags.Value` 校验失败。请检查参数是否正确。 |
|400 |InvalidParameter.Tags |指定参数 Tags 无效。 |参数 `Tags` 校验失败。请检查参数是否正确。 |
|400 |Duplicate.Tags.Key |指定的 tags 对象包含重复的 key。 |参数 `Tags.Key` 的值重复。请检查参数是否正确。 |
|403 |RequestForbidden |*  |请求被拒绝，因为当前账号下没有请求的资源（资源包括域名空间、域名、应用、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllowed |该 AccountID 无权限访问对应资源，请检查请求参数 |请求被拒绝，因为当前账号下没有请求的资源（资源包括域名空间、域名、应用、配置和证书）。 |
|403 |RequestForbidden.BillingStatus |该 AccountID 的计费情况不可用，请开通服务或充值。 |视频直播服务未已开启或账号欠费，导致账单不可用。请检查服务开通状态及账号欠费状态。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用、配置和证书）。建议重试。如果仍返回错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |发生与数据库相关的内部错误，请联系管理员。 |发生与数据库相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
