---
title: "ListLiveVideoQualityAnalysisTasks"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listlivevideoqualityanalysistasks-2023-zh-CN"
---

调用 `ListLiveVideoQualityAnalysisTasks` API 查询转码档位分析任务信息列表。

<span id="Requirements"></span>
## 要求

频率限制：每个账号每秒最多查询 10 次。

<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=ListLiveVideoQualityAnalysisTasks&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 除了需传入 API 专属参数外，还必须传入 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### Query


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`ListLiveVideoQualityAnalysisTasks` |API 操作。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Names |Array of String |否 |`["test"]` |查询的任务名称列表，默认为空，表示查询结果不按任务名称过滤。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>Name</code> 和 <code>ID</code> 不能同时输入。</div><br> |
|IDs |Array of Long |否 |`[23123523]` |查询的任务 ID 列表，默认为空，表示查询结果不按任务 ID 过滤。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>Name</code> 和 <code>ID</code> 不能同时输入。</div><br> |
|PageNum |Integer |是 |`1` |数据获取的页码，必须为正整数。 |
|PageSize |Integer |是 |`10` |每页展示的数据条数，最大为 1000。 |


<span id="Response parameters"></span>
## 返回调用结果参数

关于 API 专属的返回调用结果参数，请参见下表。更多详情请参见 [请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|任务 |Array of [Tasks](https://docs.byteplus.com/en/docs/24/106999#tasks) |`-` |转码档位分析任务列表。 |
|PageNum |Integer |`1` |查询数据的页码。 |
|PageSize |Integer |`10` |每页展示的条目数。 |


<span id="tasks"></span>
### 任务


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Name |String |`concert` |任务名称。 |
|SrcURL |String |`https://pull.example.com/live/example_stream.flv` |用于分析的流地址。 |
|Interval |Integer |`5` |质量分析采样点的间隔，单位为秒。默认值为 10，支持范围为 3 到 10。 |
|时长 |Integer |`300` |分析任务的时长 |
|ID |Long |`23123523` |任务 ID。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=ListLiveVideoQualityAnalysisTasks&Version=2023-01-01
{
    "PageNum": 1,
    "PageSize": 10,
    "IDs": [
        23123523
    ]
}
```


<span id="Sample response"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListLiveVideoQualityAnalysisTasks",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Tasks": [
            {
                "Name": "test",
                "SrcURL": "https://pull.example.com/live/example_stream.flv",
                "Interval": 5,
                "Duration": 300,
                "ID": 23123523
            }
        ],
        "PageNum": 1,
        "PageSize": 10
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为本操作相关的错误码。其他错误码请参见 [BytePlus OpenAPI 通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**Status Code** |**Error Code** |**Error Message** |**接口行为** |
|---|---|---|---|
|200 |CommonErr |*  |未分类错误。建议重试。若仍返回错误码，请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参见 [请求参数](https://docs.byteplus.com/en/docs/24/106999#request-parameters) 说明进行排查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验未通过。请检查数据类型是否正确。 |
|400 |InvalidParam.Empty |%s 为必填项 |参数缺失。请检查错误信息中指定的参数是否已传入。 |
|400 |InvalidParam.Format |%s 格式错误 |参数格式不正确。请检查错误信息中指定的参数是否存在非法字符或 URL 格式错误。 |
|400 |InvalidParam.Length |%s 不应超过 %d 个字符 |参数长度不正确。请检查错误信息中指定参数的长度是否超出限制。 |
|400 |InvalidParam.OutOfRange |%s 应为 {[%s]} 之一%s 应在 %d 到 %d 之间 |参数超出允许范围。请检查错误信息中指定参数的值是否超出取值范围。 |
|400 |InvalidParam.TimeLogic |startTime 晚于 endTime 等。 |传入的时间参数不符合时间逻辑。请检查是否存在以下问题：<br><br><br>* 开始时间晚于结束时间。<br><br>* 过期时间早于当前时间。 |
|400 |InvalidParam.DomainAndApp |domain 和 app 不能同时存在 |不能同时传入域名和应用。请修改输入参数。 |
|400 |InvalidParam.VhostOrDomainEmpty |请输入 vhost 或 domain |需要传入 vhost 或 domain 其中之一作为输入参数。请修改输入参数。 |
|400 |InvalidParam.StillUsing |%s 仍在使用中，无法删除 |错误信息中指定的资源正在被使用，导致无法删除。请释放资源后重试。 |
|403 |RequestForbidden |*  |由于当前账号下不存在请求的资源（资源包括域名空间、域名、应用、配置和证书），请求被拒绝。 |
|403 |RequestForbidden.AccountIDNotAllow |该 AccountID 无权限访问对应资源，请检查请求参数 |由于当前账号下不存在请求的资源（资源包括域名空间、域名、应用、配置和证书），请求被拒绝。 |
|403 |RequestForbidden.BillingStatus |该 AccountID 的计费情况不可用，请开通服务或充值。 |未开通视频直播服务或账号欠费，导致账单不可用。请检查服务开通状态及账号欠费状态。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用、配置和证书）。建议重试。如仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.VhostNotExist |未找到 vhost |未找到域名空间（Vhost）。请检查传入的域名空间是否与实际使用的域名空间一致。 |
|404 |ResourceNotFound.DomainNotExist |未找到 domain |未找到域名（Domain）。请检查传入的域名是否与实际使用的域名一致。 |
|404 |ResourceNotFound.AppNotExist |未找到 app |未找到应用名称（App）。请检查传入的应用名称是否与实际使用的应用名称一致。 |
|404 |ResourceNotFound.PresetNotExist |未找到 preset |未找到配置。请检查传入的配置是否与已创建的配置一致。 |
|429 |RequestLimitExceeded |*  |请求创建的资源（包括域名空间、域名、应用、配置、证书）超出限制。 |
|429 |RequestLimitExceeded.Exist |%s 已存在 |请求创建的资源（包括域名空间、域名、应用、配置、证书）已存在。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |发生与数据库相关的内部错误，请联系管理员。 |发生与数据库相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.VhostOrDomain |发生与 vhost 或域名相关的内部错误，请联系管理员。 |发生与域名空间（Vhost）或域名（Domain）相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.ServicesOrBilling |发生与服务或计费情况相关的内部错误，请联系管理员。 |发生与服务或账单相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.Preset |发生与预设相关的内部错误，请联系管理员。 |发生与服务或账单相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.Stream |发生与流相关的内部错误，请联系管理员。 |发生与流相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
