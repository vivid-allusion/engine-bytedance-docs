---
title: "CreatePullRecordTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/CreatePullRecordTask-zh-CN"
---

调用 `CreatePullRecordTask` API 创建一个在指定时间开始和结束的直播拉流录制任务。创建成功后，可以在直播期间录制任意时长的单路直播流，并将其保存为视频文件。

<span id="bdd0cccc"></span>
## 使用场景

通过调用此 API，可根据配置的录制开始时间 `StartTime` 和结束时间 `EndTime`，对指定拉流地址 `StreamURL` 进行录制。该任务的录制规则与关联的录制配置保持一致。录制任务与录制配置通过 `Domain` 和 `App` 参数进行关联。因此，直播录制任务的 `Vhost`、`Domain` 和 `App` 必须在录制配置的有效范围内。例如，若需创建一个录制任务，其 `"Vhost":" live.example.com"`、`"Domain":" live.example.push.com"` 和 `"App":"live"`；则在调用 [CreateRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createrecordpresetv2-2023) 添加录制配置时，`Vhost` 的值应为 `live.example.com`，`App` 的值应为 `live` 或 `*`。

<span id="722109d2"></span>
## 要求


* 使用限制：对于同一路流，只有在前一个录制任务结束后才能创建新的录制任务。

* 流中断策略：若流中断超过 120 秒，录制任务将立即停止。若中断时长不超过 120 秒，则录制将根据 [录制配置](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createrecordpresetv2-2023) 中定义的规则继续进行。

* 频率限制：每个账号每秒最多查询 50 次。

* 前提条件：在启动录制任务前，必须为对应的 `Vhost`、`Domain` 和 `App` 配置录制设置。详情请参见 [CreateRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createrecordpresetv2-2023)。


<span id="a60cf2a4"></span>
## HTTP 请求


* 方法：POST

* 接口地址：https://open.byteplusapi.com/?Action=CreatePullRecordTask&Version=2023\-01\-01


<span id="29eb6e50"></span>
## 请求参数

<span id="75ca53a5"></span>
### 通用参数

所有 API 除了需传递 API 专属参数外，还必须携带 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="24b22b6f"></span>
### 查询参数


|参数 |数据类型 |是否必填 |示例值 |接口行为 |
|---|---|---|---|---|
|Action |String |是 |`CreatePullRecordTask` |API 操作。 |
|Version |String |是 |`2023-01-01` |该 API 操作的版本。当前版本：2023\-01\-01。 |


<span id="2dd6a206"></span>
### Body 参数


|参数 |数据类型 |是否必填 |示例值 |接口行为 |
|---|---|---|---|---|
|Vhost |String |否 |`push.example.com` |域空间。可调用 [ListVhostRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023) API 查看所用录制配置的 `Vhost` 值。 |
|Domain |String |是 |`push.example.com` |直播流使用的推流域名或拉流域名。可调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或在 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 页面获取域名。 |
|App |String |是 |`Live` |应用名称，即直播流地址中 `AppName` 字段的值，支持大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）、下划线（_）、短横线（\-）和点（.），长度为 1 到 30 个字符。 |
|Stream |String |是 |`example_stream` |流名称，即直播流地址中`StreamName`字段的值，支持由大写和小写字母（A \- Z，a \- z）、数字（0 \- 9）、下划线（_）、连字符（\-）和点（.）组成，长度为1到100个字符。 |
|StreamURL |String |是 |`http://example.push.com/Live/example_stream.flv` |待录制直播流的拉流地址。<br><br>提示<br><br>当前仅支持 FLV 格式的拉流地址。 |
|StartTime |String |否 |`2023-06-30T15:04:05Z` |指定录制任务的开始时间。时间戳采用 RFC3339 格式，精确到秒。默认为空，表示立即开始。 |
|EndTime |String |否 |`2023-06-30T15:05:05Z` |指定录制任务的结束时间，时间戳采用 RFC3339 格式，精确到秒。默认值为空，表示录制将持续到直播流结束。 |


<span id="6af9371c"></span>
## 返回调用结果参数

有关唯一的 API 专属返回调用结果参数，请参见下表。更多详情请参见 [请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 部分。


|参数 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|TaskId |String |`f831f3b0********1aa4dcf7621` |任务 ID，录制任务的唯一标识符。 |


<span id="933121a9"></span>
## 示例

<span id="59803f74"></span>
### 请求示例

```JSON
POST https://open.byteplusapi.com/?Action=CreatePullRecordTask&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "Domain": "push.example.com",
    "App": "Live",
    "Stream": "example_stream",
    "StreamURL": "http://example.push.com/Live/example_stream.flv",
    "StartTime": "2023-06-30T15:04:05Z",
    "EndTime": "2023-06-30T15:05:05Z"
}
```


<span id="7274cd08"></span>
### 返回调用结果示例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreatePullRecordTask",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "TaskId": "f831f3b0123412341aa4dcf7621"
    }
}
```


<span id="7685b1ca"></span>
## 错误码

以下为当前操作相关的错误码。其他错误码请参见 [BytePlus OpenAPI 通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|状态码 |错误码 |错误信息 |接口行为 |
|---|---|---|---|
|200 |CommonErr |*  |未分类错误。建议重试。如果仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](#Request Parameters)说明进行排查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数未通过校验。请检查参数类型是否正确。 |
|403 |RequestForbidden |*  |请求被拒绝。当前账号下无请求的资源（域名空间、域名、应用、配置模版、证书）。 |
|403 |RequestForbidden.AccountIDNotAllow |该 AccountID 无权访问对应资源，请检查请求参数 |请求被拒绝。当前账号下无请求的资源（域名空间、域名、应用、配置模版、证书）。 |
|403 |RequestForbidden.BillingStatus |该 AccountID 的计费情况不可用，请开通服务或充值。 |视频直播服务未开通或账号欠费，导致计费情况不可用。请检查服务开通状态及账号欠费状态。 |
|404 |ResourceNotFound |*  |未找到资源（域名空间、域名、应用、配置模版、证书）。建议重试。如果仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|429 |RequestLimitExceeded |*  |请求创建的资源（域名空间、域名、应用、配置模版、证书）超出限制。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |服务间发生错误，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |服务间发生错误，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时，请[联系支持](https://console.byteplus.com/workorder/create)。 |
