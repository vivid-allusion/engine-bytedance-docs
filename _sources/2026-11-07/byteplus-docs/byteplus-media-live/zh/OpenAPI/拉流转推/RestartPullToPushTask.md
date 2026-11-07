---
title: "RestartPullToPushTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-restartpulltopushtask-2023-zh-CN"
---

调用`RestartPullToPushTask` API，以重启处于未开启状态的拉流转推任务。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">自2025年3月15日起，我们将不再维护此旧版API。其文档将于2025年6月14日下架。建议迁移至新版API。详情请参见<a href="https://docs.byteplus.com/en/docs/byteplus-media-live/continuepulltopushtask">ContinuePullToPushTask</a>文档。</div>


<span id="Requirements"></span>
## 要求

频率限制：每个账号每秒最多查询1次。

<span id="HTTP request"></span>
## HTTP请求


* 方法：POST

* 接口地址：https://open.byteplusapi.com/?Action=RestartPullToPushTask&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有API调用时，除API专属参数外，还需携带[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`RestartPullToPushTask` |API操作。 |
|Version |String |是 |`2023-01-01` |该API操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|TaskId |String |是 |`8fde6aa0281d********986e242365` |任务ID。可调用[ListPullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpulltopushtask-2023) API获取任务ID。 |
|GroupName |String |否 |`default` |任务所属的分组名称。可调用[ListPullToPushGroup](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpulltopushgroup-2023) API获取分组名称。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">主账号调用时，该字段非必填。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">子账号调用时，该字段为必填项。</div><br> |


<span id="Response parameters"></span>
## 返回调用结果参数

该API仅在返回调用结果中返回[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=RestartPullToPushTask&Version=2023-01-01
{
    "TaskId": "8fde6aa0281d********9a6e242365"
}
```


<span id="Sample response"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20211231152846010225099008082A0F4D",
        "Action": "RestartPullToPushTask",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为当前操作相关的错误码。其他错误码请参见[BytePlus OpenAPI通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|200 |CommonErr |*  |未分类错误。建议重试。如仍返回错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/107053#request-parameters)说明进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验失败。请检查数据类型是否正确。 |
|403 |RequestForbidden |*  |请求被拒绝，当前账号下无所需资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllow |该AccountID无权限访问对应资源，请检查请求参数 |请求被拒绝，当前账号下无所需资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.BillingStatus |该AccountID计费情况不可用，请开通服务或充值。 |视频直播服务未开通或账号欠费，导致账单不可用。请检查服务开通状态及账号欠费情况。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用名称、配置和证书）。建议重试。如仍返回错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|429 |RequestLimitExceeded |*  |请求创建的资源（包括域名空间、域名、应用名称、配置、证书）超出限制。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
