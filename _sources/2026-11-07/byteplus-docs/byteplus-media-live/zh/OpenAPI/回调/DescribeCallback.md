---
title: "DescribeCallback"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecallback-2023-zh-CN"
---

调用 `DescribeCallback` API，以获取您的应用的回调配置。

<span id="Requirements"></span>
## 要求

频率限制：每个账号每秒最多查询 1 次。

<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DescribeCallback&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 必须同时携带 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) 和 API 专属参数。

<span id="Query"></span>
### Query


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`DescribeCallback` |该 API 操作。 |
|Version |String |是 |`2023-01-01` |该 API 操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Vhost |String |否 |`push.example.com` |域名空间。您可以调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或访问 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 页面，获取该域名所属的域名空间。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">您必须指定 <code>Vhost</code> 或 <code>Domain</code>，不可同时指定。</div><br> |
|Domain |String |否 |`push.example.com` |推流域名。您可以调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或访问 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 页面，获取域名。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">您必须指定 <code>Vhost</code> 或 <code>Domain</code>，不可同时指定。</div><br> |
|App |String |否 |`Live` |直播流 URL 中的 AppName 字段。可包含大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和点（.），长度为 1 到 30 个字符。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">若指定 Vhost 且未指定 App，则会查询该域名空间下所有应用。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">若指定 Domain，则不可指定 App。</div><br> |
|MessageType |String |否 |`push` |待接收的回调消息类型。有效值包括：<br><br><br>* `push`：推流开始时触发回调。<br><br>* `push_end`：推流结束时触发回调。<br><br>* `snapshot`：截图事件发生时触发回调。<br><br>* `record`：录制事件发生时触发回调。 |


<span id="Response parameters"></span>
## 返回调用结果参数

有关 API 专属的唯一返回调用结果参数，请参见下表。更多详情请参见 [请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|CallbackList |[CallbackList](https://docs.byteplus.com/en/docs/24/107048#callbacklist) 数组 |`-` |回调信息列表。 |


<span id="callbacklist"></span>
### CallbackList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|MessageType |String |`push` |待接收的回调消息类型。有效值包括：<br><br><br>* `push`：推流开始时触发回调。<br><br>* `push_end`：推流结束时触发回调。<br><br>* `snapshot`：截图事件发生时触发回调。<br><br>* `record`：录制事件发生时触发回调。 |
|Vhost |String |`push.example.com` |域名空间。 |
|App |String |`push.example.com` |应用名称。 |
|TranscodeCallback |Integer |`0` |定义是否接收转码流的回调。<br><br><br>* `0`：否。<br><br>* `1`：是。 |
|CallbackDetailList |[CallbackDetailList](https://docs.byteplus.com/en/docs/24/107048#callbackdetaillist) 数组 |`-` |回调地址信息列表。 |
|CreateTime |String |`2021-01-02 15:04:05` |回调配置创建时间。 |
|CreateTimeUTC |String |`2021-01-02T15:04:05Z` |回调配置创建时间（RFC 3339 格式的 UTC 时间，精确到秒）。 |
|AuthKeyPrimary |String |`1622194197-0-0-5552*****e4e20387c6dc18afce****` |回调密钥。 |
|AuthEnable |Boolean |`false` |是否已开启认证。<br><br><br>* `false`：未开启认证。<br><br>* `true`：已开启认证。 |


<span id="callbackdetaillist"></span>
### CallbackDetailList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|CallbackType |字符串 |`http` |所使用的回调地址类型。如果返回`http`，表示支持 HTTP 和 HTTPS。 |
|URL |字符串 |`http://example.com/callback` |回调地址，长度为 1 到 100 个字符。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=DescribeCallback&Version=2023-01-01
{
    "Vhost": "push.example.com"
}
```


<span id="Sample response"></span>
### 返回调用结果示例

```json
{
    "ResponseMetadata": {
        "RequestID": "202108291443190102121532040E197F15",
        "Action": "DescribeCallback",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "CallbackList": [
            {
                "App": "live",
                "AuthEnable": false,
                "AuthKeyPrimary": "",
                "CallbackDetailList": [
                    {
                        "CallbackType": "http",
                        "URL": "http://example.com/callback"
                    }
                ],
                "CreateTime": "2021-01-02 23:04:05",
                "CreateTimeUTC": "2021-01-02T15:04:05Z",
                "Domain": "",
                "MessageType": "push",
                "TranscodeCallback": 0,
                "Vhost": "push.live.example.com"
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
|200 |CommonErr |*  |未分类错误。建议重试。如果仍然返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/107048#request-parameters)说明进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验失败。请检查数据类型是否正确。 |
|403 |RequestForbidden |*  |请求被拒绝，因为当前账号下不存在所请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllow |该 AccountID 无权限访问对应资源，请检查请求参数 |请求被拒绝，因为当前账号下不存在所请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.BillingStatus |该 AccountID 的计费情况不可用，请开通服务或充值。 |未开通视频直播流服务或账号欠费，导致账单不可用。请检查服务已开启状态及账号欠费情况。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用名称、配置和证书）。建议重试。如果仍然返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.VhostNotExist |未找到 vhost |未找到域名空间（Vhost）。请检查传入的域名空间是否与实际使用的域名空间一致。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |发生与数据库相关的内部错误，请联系管理员。 |发生与数据库相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
