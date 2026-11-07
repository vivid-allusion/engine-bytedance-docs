---
title: "GeneratePlayURL"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023-zh-CN"
---

调用 `GeneratePlayURL` API，为指定流生成拉流地址。

<span id="Requirements"></span>
## 要求


* 频率限制：每个账号每秒最多查询 25 次。

* 前提条件：如需生成转码流的拉流地址，请先完成对应流的 [转码配置](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-configuring-transcoding)。


<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* 接口地址：https://open.byteplusapi.com/?Action=GeneratePlayURL&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用时，除 API 专属参数外，还需包含 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`GeneratePlayURL` |API 操作名称。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### 请求体参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Domain |String |是 |`pull.example.com` |拉流域名。可调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或在 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 页面获取域名。 |
|应用 |String |是 |`live` |推流 URL 中的 AppName 字段。可包含大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和点（.），长度为 1~30 个字符。 |
|流 |String |是 |`example_stream` |拉流 URL 中的 StreamName 字段。可包含大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和点（.），长度为 1~100 个字符。 |
|Type |String |否 |`fcdn` |CDN 类型。支持范围：<br><br><br>* `fcdn`：（默认）BytePlus MediaLive CDN。<br><br>* `3rd`：第三方 CDN。如使用 [拉流转推](https://docs.byteplus.com/byteplus-media-live/docs/relay)功能并需获取第三方拉流地址，请将 `Type` 设置为 `3rd`。 |
|Suffix |String |否 |`5` |转码流的后缀，默认为空。如配置不为空，则为生成转码流的拉流地址。可调用 [ListVhostTransCodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhosttranscodepreset_1) 查询已有转码模版及对应后缀。 |
|ValidDuration |Integer |否 |`5` |拉流地址自生成时起，按照 `ValidDuration` 指定的时长后失效。单位：秒。支持范围：\> 0。默认值：604800（七天）。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">M3U8 拉流地址过期后，拉流会立即停止。其他类型地址过期后，正在进行的拉流不会受影响。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">如同时设置 <code>ValidDuration</code> 和 <code>ExpiredTime</code>，仅 <code>ExpiredTime</code> 的配置生效。</div><br> |
|ExpiredTime |String |否 |`2022-08-19T16:07:25+08:00` |拉流地址的过期时间（RFC 3339 格式本地时间，精确到秒），单位为秒。默认过期时间为拉流地址生成后七天。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">M3U8 拉流地址过期后，拉流会立即停止。其他类型地址过期后，正在进行的拉流不会受影响。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">如同时设置 <code>ValidDuration</code> 和 <code>ExpiredTime</code>，仅 <code>ExpiredTime</code> 的配置生效。</div><br> |
|StreamType |String |是 |`source` |生成的地址类型，取值如下：<br><br><br>* `source`：生成源流地址。<br><br>* `transcode`：生成转码流地址。<br><br>* `abr`：生成 ABR 地址。 |


<span id="Response parameters"></span>
## 返回参数

有关 API 专属返回参数，请参见下表。更多详情请参见 [请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|URLList |[URLList](https://docs.byteplus.com/en/docs/24/107020#urllist) 数组 |`-` |拉流地址列表。 |
|AuthType |String |`TypeB` |用于生成拉流地址的 URL 鉴权类型。若值为空，表示当前域名未配置 URL 鉴权。<br><br><br>* `TypeA`：A 类型。<br><br>* `TypeB`：B 类型。<br><br>* `TypeC`：C 类型。<br><br>* `TypeCustom`：自定义类型。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">关于 A、B、C 类型的更多信息，请参见 <a href="https://docs.byteplus.com/en/docs/byteplus-media-live/docs-url-authentication">Configuring URL authentication</a>。</div><br> |


<span id="urllist"></span>
### URLList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|URL |String |`http://pull.example.com/live/example_stream.sdp` |拉流地址。 |
|Type |String |`pull` |地址类型。<br><br><br>* `pull`：拉流地址<br><br>* `3rd_play(replay_source)`：第三方拉流回源地址<br><br>* `3rd_play(relay_sink)`：第三方拉流转推地址 |
|CDN |String |`fcdn` |CDN 类型。<br><br><br>* `fcdn`：（默认）BytePlus 视频云 CDN；<br><br>* `3rd`：第三方 CDN。 |
|Protocol |String |`hls` |流协议。可选值包括 `hls`、`flv`、`rtmp`、`udp` 和 `cmaf`。 |
|SubStreamURL |[SubStreamURL](https://docs.byteplus.com/en/docs/24/107020#substreamurl) 数组 |`-` |子流地址。仅当 `StreamType` 为 `abr` 时返回。 |


<span id="substreamurl"></span>
### SubStreamURL


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Suffix |String |`_ld` |子流转码后缀。 |
|Tag |String |`LL-HLS` |地址标签，例如 `drm`、`hls encryption`。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=GeneratePlayURL&Version=2023-01-01
{
    "Domain": "pull.example.com",
    "App": "live",
    "Stream": "example_stream",
    "ExpiredTime": "2022-08-19T16:07:25Z"
}
```


<span id="Sample response"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GeneratePlayURL",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "URLList": [
            {
                "URL": "http://pull.example.com/live/example_stream.sdp",
                "CDN": "fcdn",
                "Protocol": "hls",
                "Type": "pull"
            }
        ],
        "AuthType": "TypeB"
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为当前操作相关的错误码。其他错误码请参见 [BytePlus OpenAPI 通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|200 |CommonErr |*  |未分类错误。建议重试。若仍返回错误码，请 [contact support](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考 [请求参数](https://docs.byteplus.com/en/docs/24/107020#request-parameters)说明进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验失败。请检查数据类型是否正确。 |
|400 |InvalidParam.Format |%s 格式错误 |参数格式不正确。请检查错误信息中指定参数是否存在非法字符或 URL 格式错误。 |
|400 |InvalidParam.OutOfRange |%s 应为 {[%s]} 之一%s 应在 %d 到 %d 之间 |参数超出允许范围。请检查错误信息中指定参数的值是否超出取值范围。 |
|400 |InvalidParam.TimeLogic |startTime 晚于 endTime 等 |传入的时间参数不符合时间逻辑。请检查是否存在以下问题：开始时间晚于结束时间。过期时间早于当前时间。 |
|403 |RequestForbidden |*  |请求被拒绝，当前账号下无请求资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllow |该 AccountID 无权限访问对应资源，请检查请求参数 |请求被拒绝，当前账号下无请求资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.BillingStatus |AccountID 未开通计费情况，请开通服务或充值。 |视频直播服务未开启或账号欠费，导致计费情况不可用。请检查服务激活状态和账户欠费状态。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用名称、配置和证书）。建议重试。如果仍然返回错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.VhostOrDomain |发生与 vhost 或域名相关的内部错误，请联系管理员。 |发生与域名空间（Vhost）或域名（Domain）相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
