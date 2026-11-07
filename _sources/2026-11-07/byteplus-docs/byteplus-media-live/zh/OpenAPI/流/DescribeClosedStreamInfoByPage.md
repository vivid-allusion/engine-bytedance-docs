---
title: "DescribeClosedStreamInfoByPage"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeclosedstreaminfobypage-2023-zh-CN"
---

调用 `DescribeClosedStreamInfoByPage` API 按页获取已结束在线流的信息。

<span id="Requirements"></span>
## 要求

请求频率限制：每个账号每秒最多查询 1 次。

<span id="HTTP request"></span>
## HTTP 请求


* 方法：GET

* Endpoint：https://open.byteplusapi.com/?Action=DescribeClosedStreamInfoByPage&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用时，除 API 专属参数外，还需包含 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`DescribeClosedStreamInfoByPage` |API 操作名称。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。当前版本：2023\-01\-01。 |
|PageNum |Integer |是 |`1` |页码。BytePlus MediaLive 将查询结果分页，仅返回指定页的结果。支持范围：≥ 1。 |
|PageSize |Integer |是 |`10` |每页返回结果数量。支持范围：1–1000。 |
|Vhost |String |否 |`push.example.net` |域名空间。如未指定，则表示查询所有域名空间下已结束在线流。可调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或在 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 页面获取域名所属的域名空间。 |
|Domain |String |否 |`push.example.net` |域名。如未指定，则表示查询结果不筛选直播流的域名。可调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或在 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 页面获取域名。 |
|应用 |String |否 |`live` |直播流 URL 中的 AppName 字段。如未指定，则表示查询结果不筛选直播流的 AppName 字段。可包含大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和点（.），长度为 1–30 个字符。 |
|Stream |String |否 |`stream001` |直播流 URL 中的 StreamName 字段。如未指定，则表示查询结果不筛选直播流的 StreamName 字段。可包含大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和点（.），长度为 1–100 个字符。 |
|Sort |String |否 |`desc` |按结束时间排序流。支持值包括：<br><br><br>* `asc`：升序。<br><br>* `desc`：（默认）降序。 |
|EndTimeFrom |String |是 |`2021-10-02T19:39:26Z` |查询范围的起始时间（UTC 时间，RFC 3339 格式）。检索结束时间晚于该时间的流。默认值为当前时间减去 24 小时。 |
|EndTimeTo |String |是 |`2021-10-02T19:39:26Z` |查询范围的结束时间（UTC 时间，RFC 3339 格式）。检索结束时间早于该时间的流。默认值为当前时间。 |
|SourceType |String |否 |`push` |要查询的流来源。<br><br><br>* `push`：直接推送至 BytePlus MediaLive 并拉取的流。<br><br>* `relay`：从第三方 CDN 拉流转推的流。 |
|QueryType |String |否 |`fuzzy` |流的查询方式。<br><br><br>* `fuzzy`：模糊匹配<br><br>* `strict`：（默认）精确匹配 |


<span id="Response parameters"></span>
## 返回调用结果参数

如需了解 API 专属返回调用结果参数，请参见下表。更多详情请参见 [请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|StreamInfoList |[StreamInfoList](https://docs.byteplus.com/en/docs/24/106987#streaminfolist) 数组 |`-` |流信息列表。 |
|RoughCount |整数 |`1` |历史流总数。 |


<span id="streaminfolist"></span>
### StreamInfoList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Vhost |字符串 |`push.example.com` |域名空间。 |
|Domain |字符串 |`push.example.com` |域名。 |
|应用 |字符串 |`live` |直播流 URL 中的 AppName 字段。 |
|Stream |字符串 |`exampel_stream` |直播流 URL 中的 StreamName 字段。 |
|StartTime |字符串 |`2021-10-29T00:55:50Z` |流的开始时间。 |
|EndTime |字符串 |`2021-10-29T09:30:17Z` |流的结束时间。 |
|SourceType |字符串 |`push` |要查询的流来源。<br><br><br>* `push`：直接推送至 BytePlus MediaLive 并从 BytePlus MediaLive 拉取的流。<br><br>* `relay`：从第三方 CDN 拉取的流。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
GET https://open.byteplusapi.com/?Action=DescribeClosedStreamInfoByPage&Version=2023-01-01&PageNum=1&PageSize=10&Vhost=push.example.com&Domain=push.example.com&App=live&Stream=example_stream&Sort=desc&EndTimeFrom=2021-10-02T19:39:26Z&EndTimeTo=2021-10-02T19:39:26Z&SourceType=push&QueryType=fuzzy
```


<span id="Sample response"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "202110291823170102250842170814F5D6",
        "Action": "DescribeClosedStreamInfoByPage",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "cn-north-1"
    },
    "Result": {
        "RoughCount": 1,
        "StreamInfoList": [
            {
                "App": "live",
                "Domain": "push.example.com",
                "EndTime": "2021-10-29 17:31:57",
                "StartTime": "2021-10-29 17:30:17",
                "Stream": "exampel_stream",
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
|200 |CommonErr |*  |未分类错误。建议重试。若仍返回错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/106987#request-parameters)接口行为进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验失败。请检查数据类型是否正确。 |
|400 |InvalidParam.Format |%s 格式错误 |参数格式不正确。请检查错误信息中指定参数是否存在非法字符或 URL 格式错误。 |
|400 |InvalidParam.OutOfRange |%s 应为 {[%s]} 之一，%s 应在 %d 到 %d 之间 |参数超出允许范围。请检查错误信息中指定参数的值是否超出取值范围。 |
|400 |InvalidParam.TimeLogic |startTime 晚于 endTime 等 |传入的时间参数不符合时间逻辑。请检查是否存在以下问题：开始时间晚于结束时间；过期时间早于当前时间。 |
|403 |RequestForbidden |*  |请求被拒绝，当前账号下无请求资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllowed |该 AccountID 无权限访问对应资源，请检查请求参数 |请求被拒绝，当前账号下无请求资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.BillingStatus |该 AccountID 未开通计费情况，请开通服务或充值。 |视频直播流服务未已开启或账号欠费，导致账单不可用。请检查服务开通状态及账号欠费情况。 |
|403 |AccessDenied |用户无权对资源 %s 执行操作：%s |请求被拒绝。当前账号下无请求资源（域名空间、域名、应用、配置模版、证书）或接口权限。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用名称、配置和证书）。建议重试。若仍返回错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |发生了与数据库相关的内部错误，请联系管理员。 |发生了与数据库相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.VhostOrDomain |发生了与虚拟主机或域名相关的内部错误，请联系管理员。 |发生了与域名空间（Vhost）或域名（Domain）相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生了内部错误，请联系管理员。 |发生了内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生了内部错误，请联系管理员。 |发生了内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
