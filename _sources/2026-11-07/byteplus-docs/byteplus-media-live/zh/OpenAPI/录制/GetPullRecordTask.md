---
title: "GetPullRecordTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/GetPullRecordTask-zh-CN"
---

调用 `GetPullRecordTask` API 查询单个直播录制任务的信息。

<span id="4b5fc640"></span>
## 要求

限速：每个账号每秒最多查询 50 次。

<span id="c6f0364b"></span>
## HTTP 请求


* 方法：POST

* 接口地址：https://open.byteplusapi.com/?Action=GetPullRecordTask&Version=2023\-01\-01


<span id="b4bba97f"></span>
## 请求参数

<span id="754fb9f4"></span>
### 通用参数

所有 API 调用时，除了 API 专属参数外，还必须携带 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="b104238e"></span>
### 查询


|参数 |数据类型 |是否必填 |示例值 |接口行为 |
|---|---|---|---|---|
|Action |String |是 |`GetPullRecordTask` |API 操作。 |
|Version |String |是 |`2023-01-01` |本次 API 操作的版本。当前版本：2023\-01\-01。 |


<span id="05a50648"></span>
### 请求体参数


|参数 |数据类型 |是否必填 |示例值 |接口行为 |
|---|---|---|---|---|
|TaskID |String |是 |`5b903f78c7f5ae*******01f6fe2eea` |任务 ID，即录制任务的唯一标识。可调用 [ListPullRecordTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpullrecordtask) API 获取任务 ID。 |


<span id="721ebd5b"></span>
## 返回调用结果参数

关于唯一的 API 专属返回调用结果参数，请参见下表。更多详情请参考 [请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 部分。


|参数 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|TaskDetail |[TaskDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/GetPullRecordTask#taskdetail) 对象 |`-` |任务详情。 |


<span id="58d749ae"></span>
### TaskDetail


|参数 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|TaskId |String |`5b903f78c7f5ae*******01f6fe2eea` |任务 ID。 |
|StartTime |String |`2023-10-09T15:16:15Z` |任务开始时间，UTC 时间，RFC3339 格式，精确到秒。 |
|EndTime |String |`2023-10-09T15:18:28Z` |任务结束时间，UTC 时间，RFC3339 格式，精确到秒。 |
|Vhost |String |`example.com` |创建录制任务时传入的域空间。 |
|Domain |String |`pull.example.com` |创建录制任务时传入的域名。 |
|App |String |`live` |创建录制任务时传入的应用名称。 |
|Status |String |`未开始` |录制任务状态。可能的取值如下。<br><br><br>* `停用`：录制任务已停止；<br><br>* `未开始`：录制任务尚未开始；<br><br>* `生效中`：录制任务进行中；<br><br>* `已结束`：录制已完成。 |


<span id="70ec6ad3"></span>
## 示例

<span id="888ee4c6"></span>
### 请求示例

```JSON
POST https://open.byteplusapi.com/?Action=GetPullRecordTask&Version=2023-01-01
{
    "TaskID": "5b903f78c7f5ae*******01f6fe2eea"
}
```


<span id="f6ebe8b7"></span>
### 返回调用结果示例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetPullRecordTask",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "TaskDetail": {
            "TaskId": "5b903f78c7f5ae*******01f6fe2eea",
            "StartTime": "2023-10-09T15:16:15Z",
            "EndTime": "2023-10-09T15:18:28Z",
            "Vhost": "example.com",
            "Domain": "pull.example.com",
            "App": "live",
            "Status": "生效中"
        }
    }
}
```


<span id="821e3fe0"></span>
## 错误码

以下为当前操作相关的错误码。其他错误码请参见 [BytePlus OpenAPI 通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|状态码 |错误码 |错误信息 |接口行为 |
|---|---|---|---|
|200 |CommonErr |*  |未分类错误。建议重试。如仍返回该错误码，请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考 [请求参数](#Request Parameters) 描述进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验未通过。请检查参数类型是否正确。 |
|403 |RequestForbidden |*  |请求被拒绝。当前账号下无请求资源（域空间、域名、应用、配置模版、证书）。 |
|403 |RequestForbidden.AccountIDNotAllowed |该 AccountID 无权限访问对应资源，请检查请求参数 |请求被拒绝。当前账号下无请求资源（域空间、域名、应用、配置模版、证书）。 |
|403 |RequestForbidden.BillingStatus |该 AccountID 的计费情况不可用，请开通服务或充值。 |视频直播服务未开通或账号欠费，导致账单不可用。请检查服务开通状态及账号欠费情况。 |
|404 |ResourceNotFound |*  |未找到资源（域命名空间、域名、应用、配置模版、证书）。建议重试。如果仍然返回此错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |服务之间发生错误，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |服务之间发生错误，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时，请[联系支持](https://console.byteplus.com/workorder/create)。 |
