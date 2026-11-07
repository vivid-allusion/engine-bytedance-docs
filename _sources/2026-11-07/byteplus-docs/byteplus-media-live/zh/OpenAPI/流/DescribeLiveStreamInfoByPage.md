---
title: "DescribeLiveStreamInfoByPage"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describelivestreaminfobypagev2023-zh-CN"
---

调用 `DescribeLiveStreamInfoByPage` API 按页获取正在进行的在线流的信息。

<span id="Requirements"></span>
## 要求

请求频率限制：每个账号每秒最多 1 次查询

<span id="HTTP request"></span>
## HTTP 请求


* 方法：GET

* Endpoint：https://open.byteplusapi.com/?Action=DescribeLiveStreamInfoByPage&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用时，除 API 专属参数外，还需包含 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveStreamInfoByPage` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。当前版本：2023\-01\-01。 |
|PageNum |Integer |是 |`1` |页码。BytePlus MediaLive 会将查询结果分页，仅返回指定页的结果。支持范围：≥ 1。 |
|PageSize |Integer |是 |`10` |每页返回结果数量。支持范围：1–1000。 |
|Vhost |String |否 |`push.example.com` |域名空间。若未指定，则表示查询所有域名空间下正在进行的在线流。可调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或在 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 页面获取域名所属的域名空间。 |
|Domain |String |否 |`push.example.com` |域名。若未指定，则表示查询结果不筛选直播流的域名。可调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或在 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 页面获取域名。 |
|App |String |否 |`live` |直播流 URL 中的 AppName 字段。若未指定，则表示查询结果不筛选直播流的 AppName 字段。可包含大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和点（.），长度为 1 到 30 个字符。 |
|Stream |String |否 |`example_stream` |直播流 URL 中的 StreamName 字段。若未指定，则表示查询结果不筛选直播流的 StreamName 字段。可包含大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和点（.），长度为 1 到 100 个字符。 |
|StreamType |String |否 |`origin` |要查询的流类型。若未指定，则查询结果包含两种流类型。<br><br><br>* `origin`：源流。<br><br>* `trans`：转码流。 |
|SourceType |String |否 |`push` |要查询的流来源。<br><br><br>* `push`：直接推送至 BytePlus MediaLive 并从 BytePlus MediaLive 拉取的流。<br><br>* `relay`：从第三方 CDN 拉取的流。 |
|QueryType |String |否 |`fuzzy` |流的查询方式。<br><br><br>* `fuzzy`：模糊匹配<br><br>* `strict`：（默认）精确匹配 |


<span id="Response parameters"></span>
## 返回调用结果参数

有关 API 专属返回调用结果参数，请参见下表。更多详情请参见 [请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|StreamInfoList |[StreamInfoList](https://docs.byteplus.com/en/docs/24/106976#streaminfolist) 数组 |`-` |流信息列表。 |
|RoughCount |Integer |`1` |流总数。 |


<span id="streaminfolist"></span>
### StreamInfoList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|ID |Long |`1005002` |流 ID。 |
|Vhost |String |`push.example.com` |域名空间。 |
|Domain |String |`push.example.com` |域名。 |
|App |String |`live` |AppNmae 字段。 |
|流 |字符串 |`example_stream` |StreamName 字段。 |
|SessionStartTime |字符串 |`2021-10-29T00:55:50.186Z` |直播流会话开始的时间。 |
|SourceType |字符串 |`push` |查询的流来源。<br><br><br>* `push`：直接推送到 BytePlus MediaLive 并从 BytePlus MediaLive 拉取的流。<br><br>* `relay`：从第三方 CDN 拉取的流。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```JSON
GET https://open.byteplusapi.com/?Action=DescribeLiveStreamInfoByPage&Version=2023-01-01&PageNum=1&PageSize=10&Vhost=push.example.com&Domain=push.example.com&App=live&Stream=example_stream&StreamType=origin&SourceType=push&QueryType=fuzzy
```


<span id="Sample response"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "202110291811420102250842170013F8D2",
        "Action": "DescribeLiveStreamInfoByPage",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "RoughCount": 1,
        "StreamInfoList": [
            {
                "App": "live",
                "Domain": "push.example.com",
                "ID": 1005002,
                "SessionStartTime": "2021-10-29T08:55:50.186Z",
                "Stream": "example_stream\t",
                "SourceType": "push",
                "Vhost": "push.example.com"
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
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/106976#request-parameters)说明进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验失败。请检查数据类型是否正确。 |
|400 |InvalidParam.OutOfRange |%s 应为 {[%s]} 之一，%s 应在 %d 到 %d 之间 |参数超出允许范围。请检查错误信息中指定参数的值是否超出取值范围。 |
|403 |RequestForbidden |*  |请求被拒绝，因为当前账号下没有请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllowed |该 AccountID 无权限访问对应资源，请检查请求参数 |请求被拒绝，因为当前账号下没有请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.BillingStatus |该 AccountID 的计费情况不可用，请开通服务或充值。 |视频直播流服务未开启或账号欠费，导致账单不可用。请检查服务开通状态及账号欠费状态。 |
|403 |AccessDenied |用户无权在资源 %s 上执行操作：%s |请求被拒绝。当前账号下没有请求的资源（域名空间、域名、应用、配置模版、证书）或接口权限。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用名称、配置和证书）。建议重试。如果仍然返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.VhostNotExist |未找到 vhost |未找到域名空间（Vhost）。请检查传入的域名空间是否与实际使用的域名空间一致。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |发生与数据库相关的内部错误，请联系管理员。 |发生与数据库相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.VhostOrDomain |发生与 vhost 或域名相关的内部错误，请联系管理员。 |发生与域名空间（Vhost）或域名（Domain）相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
