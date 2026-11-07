---
title: "StopPullRecordTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-stoppullrecordtask-zh-CN"
---

调用 `StopPullRecordTask` API，以停止尚未开始或正在执行的录制任务。停止正在执行的录制任务会生成录制文件。

<span id="83d84d76"></span>
## 要求

频率限制：每个账号每秒最多 50 次查询。

<span id="4cd90e5f"></span>
## HTTP 请求


* 方法：POST

* 接口地址：https://open.byteplusapi.com/?Action=StopPullRecordTask&Version=2023\-01\-01


<span id="d5669adc"></span>
## 请求参数

<span id="a293ff65"></span>
### 通用参数

所有 API 调用时，除了 API 专属参数外，还必须携带 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="99f0e3ec"></span>
### 查询


|参数 |数据类型 |是否必填 |示例值 |接口行为 |
|---|---|---|---|---|
|Action |String |是 |`StopPullRecordTask` |API 操作。 |
|Version |String |是 |`2023-01-01` |该 API 操作的版本。当前版本：2023\-01\-01。 |


<span id="c262ce78"></span>
### Body 参数


|参数 |数据类型 |是否必填 |示例值 |接口行为 |
|---|---|---|---|---|
|TaskId |String |是 |`f831f3b0********1aa4dcf7621` |录制任务的唯一标识。可调用 [ListPullRecordTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpullrecordtask) API 查看直播录制任务的任务 ID。 |


<span id="6308500a"></span>
## 返回参数

该 API 的返回调用结果仅包含 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="e814026d"></span>
## 示例

<span id="da1c188d"></span>
### 请求示例

```JSON
POST https://open.byteplusapi.com/?Action=StopPullRecordTask&Version=2023-01-01
{
    "TaskId": "f831f3b0********1aa4dcf7621"
}
```


<span id="6ab439ca"></span>
### 返回示例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "StopPullRecordTask",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```


<span id="1469dbba"></span>
## 错误码

以下为当前操作相关的错误码。其他错误码请参见 [BytePlus OpenAPI 通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|状态码 |错误码 |错误信息 |描述 |
|---|---|---|---|
|200 |CommonErr |*  |未分类错误。建议重试。如仍返回该错误码，请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考 [请求参数](#Request Parameters) 中的说明进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数未通过校验。请检查参数类型是否正确。 |
|403 |RequestForbidden |*  |请求被拒绝。当前账号下无请求的资源（域名空间、域名、应用、配置模版、证书）。 |
|403 |RequestForbidden.AccountIDNotAllow |该 AccountID 无权限访问对应资源，请检查请求参数 |请求被拒绝。当前账号下无请求的资源（域名空间、域名、应用、配置模版、证书）。 |
|403 |RequestForbidden.BillingStatus |该 AccountID 的计费情况不可用，请开通服务或充值。 |由于视频直播服务未开通或账号逾期，账单不可用。请检查服务开通状态及账号逾期情况。 |
|404 |ResourceNotFound |*  |未找到资源（域名空间、域名、应用、配置模版、证书）。建议重试。如仍返回该错误码，请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误，请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |如服务间发生错误，请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |服务间发生错误，请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时，请 [联系支持](https://console.byteplus.com/workorder/create)。 |
