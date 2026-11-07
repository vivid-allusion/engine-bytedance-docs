---
title: "DeleteCarouselTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletecarouseltask-zh-CN"
---

调用 `DeleteCarouselTask` API 删除指定的轮播任务。任务删除后，系统将停止播放该任务的所有轮播内容，并释放相关资源。

<span id="Requirements"></span>
## 要求


* 频率限制：每个账号每秒最多 10 次查询。

* 不可恢复：调用 `DeleteCarouselTask` 接口后，任务及其相关资源将被释放且无法恢复。请谨慎操作。

* 立即停止：任务删除后，所有正在进行的轮播回放将立即终止，无需等待当前回放完成。


<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DeleteCarouselTask&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 除了需要传递各自的专用参数外，还必须携带 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### Query


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`DeleteCarouselTask` |API 操作。 |
|Version |String |是 |`2023-01-01` |本次 API 操作的版本号。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|TaskID |String |是 |`44c5da50318440*********2d62c910b8` |待删除轮播任务的 ID，即任务的唯一标识。调用 `CreateCarouselTask` 接口创建轮播任务时返回。 |


<span id="Response parameters"></span>
## 返回参数

关于唯一的 API 专用返回参数，请参见下表。更多详情请参见 [请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Data |String |`kill task [e1fb009334fc5b16] success,mesos id is [live_bff26015_000000000025852],rowsAffect [0]` |已删除任务的操作结果信息，返回任务是否删除成功、相关 Mesos ID 及操作影响记录数。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=DeleteCarouselTask&Version=2023-01-01
{
    "TaskID": "44c5da50318440*********2d62c910b8"
}
```


<span id="Sample response"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestID": "202410301524025B4509E7E242BD12477C",
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DeleteCarouselTask",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Data": "kill task [e1fb009334fc5b16] success,mesos id is [live_bff26015_000000000025852],rowsAffect [0]"
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为本次操作相关的错误码。其他错误码请参见 [BytePlus OpenAPI 通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考 [请求参数](#Request Parameters) 说明进行排查。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请 [联系支持](https://console.byteplus.com/workorder/create)。 |
