---
title: "UpdateCallback"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatecallback-2023-zh-CN"
---

调用 `UpdateCallback` API，以添加或更新流推送、录制和截图事件的回调配置。

<span id="Requirements"></span>
## 要求

频率限制：每个账号每秒最多查询 1 次。

<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=UpdateCallback&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用时，除了 API 专属参数外，还必须包含 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`UpdateCallback` |API 操作名称。 |
|Version |String |是 |`2023-01-01` |该 API 操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|MessageType |String |是 |`push` |需接收的回调消息类型。取值及含义如下：<br><br><br>* `push`：流推送开始时触发回调。<br><br>* `push_end`：流推送结束时触发回调。<br><br>* `snapshot`：截图事件发生时触发回调。<br><br>* `record`：录制事件发生时触发回调。<br><br>* `audit_sanpshot`：截图审核完成时触发回调。 |
|Vhost |String |否 |`push.example.com` |域名空间，即直播流地址所属的域名空间。可调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或在 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 页面获取域名所属的域名空间。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">必须指定 <code>Vhost</code> 或 <code>Domain</code>，不可同时指定。</div><br> |
|Domain |String |否 |`push.example.com` |推流域名。可调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或在 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 页面获取域名。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">必须指定 <code>Vhost</code> 或 <code>Domain</code>，不可同时指定。</div><br> |
|App |String |否 |`example_app` |直播流 URL 中的 AppName 字段。可包含大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和点（.），长度为 1 到 30 个字符。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">若指定 Domain，则不可指定 App。</div><br> |
|TranscodeCallback |Integer |否 |`0` |定义是否接收转码流的回调。取值及含义如下：<br><br><br>* `0`：（默认）否。<br><br>* `1`：是。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">仅当 <code>MessageType</code> 为 <code>Push</code> 或 <code>Push_end</code> 时生效。</div><br> |
|CallbackDetailList |[CallbackDetailList](https://docs.byteplus.com/en/docs/24/107023#callbackdetaillist) 数组 |是 |`-` |回调地址信息列表。 |
|AuthEnable |Boolean |否 |`false` |是否启用回调鉴权。启用鉴权后，可通过回调消息中的 `sign` 和 `t` 字段验证收到的回调是否来自 BytePlus MediaLive。<br><br><br>* `false`：（默认）不启用鉴权。<br><br>* `true`：启用鉴权。 |
|AuthKeyPrimary |String |否 |`1622194197-0-0-5552*****e4e20387c6dc18afce****` |回调密钥。若将 `AuthEnable` 设置为 `true`，则必须指定 `AuthKeyPrimary`。可包含数字和字母。最大长度：32 个字符。 |


<span id="callbackdetaillist"></span>
### CallbackDetailList


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|CallbackType |String |是 |`http` |所使用的回调地址类型。只能设置为 `http`，即支持 HTTP 和 HTTPS。 |
|URL |String |是 |`http://example.com/callback` |回调地址，长度必须为1到100个字符。 |


<span id="Response parameters"></span>
## 返回调用结果参数

该 API 的返回调用结果中仅包含 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=UpdateCallback&Version=2023-01-01
{
    "Vhost": "push.live.example.com",
    "App": "example_app",
    "MessageType": "push",
    "TranscodeCallback": 0,
    "CallbackDetailList": [
        {
            "CallbackType": "http",
            "URL": "http://example.com/callback"
        }
    ]
}
```


<span id="Sample response"></span>
### 返回调用结果示例

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "UpdateCallback",
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
|200 |CommonErr |*  |未分类错误。建议重试。如果仍然返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/107023#request-parameters)说明进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验未通过。请检查数据类型是否正确。 |
|400 |InvalidParam.Format |%s格式错误 |参数格式不正确。请检查错误信息中指定的参数是否包含非法字符或URL格式错误。 |
|400 |InvalidParam.OutOfRange |%s应为{[%s]}之一%s应在%d到%d之间 |参数超出允许范围。请检查错误信息中指定参数的值是否超出取值范围。 |
|400 |InvalidParam.DomainAndApp |domain和app不能同时存在 |不能同时传入域名和应用。请修改输入参数。 |
|400 |InvalidParam.Empty |%s为必填项 |参数缺失。请检查错误信息中指定的参数是否已传入。 |
|403 |RequestForbidden |*  |请求被拒绝，因为当前账号下不存在所请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllowed |该AccountID无权限访问对应资源，请检查请求参数 |请求被拒绝，因为当前账号下不存在所请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.BillingStatus |该AccountID的计费情况不可用，请开通服务或充值。 |视频直播流服务未开启或账号欠费，导致计费情况不可用。请检查服务开通状态及账号欠费情况。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用名称、配置和证书）。建议重试。如果仍然返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.VhostNotExist |未找到vhost |未找到域名空间（Vhost）。请检查传入的域名空间是否与实际使用的域名空间一致。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |发生与数据库相关的内部错误，请联系管理员。 |发生与数据库相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
