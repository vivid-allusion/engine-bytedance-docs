---
title: "GetSpeechTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/GetSpeechTask-zh-CN"
---

调用 `GetSpeechTask` API 查询指定 AI 配音任务的信息。

<span id="Requirements"></span>
## 要求

**速率限制**：每个账号每秒最多 10 次请求。

<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=GetSpeechTask&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用时，除了 API 专属参数外，还必须包含 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`GetSpeechTask` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|TaskID |String |是 |`49743067b675c378` |任务 ID。可通过调用 [CreateSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateSpeechTask?lang=en) 或 [SearchSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/SearchSpeechTask) 获取该 ID。 |


<span id="Response parameters"></span>
## 返回调用结果参数

有关唯一的 API 专属返回调用结果参数，请参见下表。更多详情请参见 [请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Code |Integer |`0` |状态码。 |
|Message |String |`success` |状态信息。 |
|数据 |[Data](https://docs.byteplus.com/en/docs/24/118394#data) 对象 |`-` |任务信息。 |


<span id="data"></span>
### 数据


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Name |String |`TaskA` |任务名称。 |
|Status |String |`done` |任务状态。有效值：<br><br><br>* `running`：运行中。<br><br>* `done`：已结束。<br><br>* `prestop`：停止中。<br><br>* `init`：准备中。<br><br>* `prepare`：启动中。 |
|TaskID |String |`49743067b675c378` |任务 ID。 |
|CreatedAt |String |`2025-11-14T15:34:43+08:00` |任务创建时间。时间为 RFC3339 格式，使用 UTC+8，精确到秒。 |
|UpdatedAt |String |`2025-11-14T16:50:53+08:00` |任务更新时间。时间为 RFC3339 格式，使用 UTC+8，精确到秒。 |
|StoppedAt |String |`2025-11-14T16:50:49+08:00` |任务实际结束时间。时间为 RFC3339 格式，使用 UTC+8，精确到秒。 |
|Rule |String |`{"Pipe":"mix","Delay":15,"Source":{"Url":"https://pull.example.com/live/cloud.flv"},"Output":{"Url":["rtmp://push.example.com/live/cloud?auth_key=1779891783-0-0-e1f5a2a****4b5fe21cb3efdc89af901"]},"Subtitle":{"Original":{"Border":{"W":1,"Color":"black@0.5"},"Font":"arial","FontColor":"white","Language":"zh"},"Translation":[{"Border":{"W":1,"Color":"black@0.5"},"Font":"arial","FontColor":"white","Language":"en"}]}}` |任务规则配置。该值为 JSON 字符串，包含任务类型、拉流 URL、推流 URL、字幕配置及其他信息。字段详情请参见 [CreateSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateSpeechTask)。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=GetSpeechTask&Version=2023-01-01
{
    "TaskID": "497430****75c378"
}
```


<span id="Sample response"></span>
### 返回调用结果示例

```json
{
    "ResponseMetadata": {
        "RequestID": "20251114171722145C604658CB14014261",
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetSpeechTask",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Code": 0,
        "Message": "success",
        "Data": {
            "Name": "TaskA",
            "Status": "done",
            "TaskID": "497430****75c378",
            "CreatedAt": "2025-11-14T15:34:43+08:00",
            "UpdatedAt": "2025-11-14T16:50:53+08:00",
            "StoppedAt": "2025-11-14T16:50:49+08:00",
            "Rule": "{\"Pipe\":\"mix\",\"Delay\":15,\"Source\":{\"Url\":\"https://pull.example.com/live/cloud.flv\"},\"Output\":{\"Url\":[\"rtmp://push.example.com/live/cloud?auth_key=1779891783-0-0-e1f5a2a****4b5fe21cb3efdc89af901\"]},\"Subtitle\":{\"Original\":{\"Border\":{\"W\":1,\"Color\":\"black@0.5\"},\"Font\":\"arial\",\"FontColor\":\"white\",\"Language\":\"zh\"},\"Translation\":[{\"Border\":{\"W\":1,\"Color\":\"black@0.5\"},\"Font\":\"arial\",\"FontColor\":\"white\",\"Language\":\"en\"}]}}"
        }
    }
}
```


<span id="Error codes"></span>
## 错误码

有关错误码的更多信息，请参见 [通用错误码](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes)。
