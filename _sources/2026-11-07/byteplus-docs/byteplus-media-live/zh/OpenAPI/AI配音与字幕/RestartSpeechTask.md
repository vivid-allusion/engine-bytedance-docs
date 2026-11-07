---
title: "RestartSpeechTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/RestartSpeechTask-zh-CN"
---

调用 `RestartSpeechTask` API，以重启正在运行或启动中的 AI 配音任务。

<span id="Requirements"></span>
## 要求


* **请求频率限制**：每个账号每秒最多 10 次请求。

* **前提条件**：AI 配音任务正在运行或启动中。你可以调用 [GetSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSpeechTask) 获取任务状态，并确保 `Status` 的值为 `running` 或 `prepare`。


<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=RestartSpeechTask&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用时，除了 API 专属参数外，还必须包含 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### Query


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`RestartSpeechTask` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|TaskID |String |是 |`49743067b675c378` |任务 ID。你可以通过调用 [CreateSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateSpeechTask?lang=en) 或 [SearchSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/SearchSpeechTask) 获取该 ID。 |


<span id="Response parameters"></span>
## 返回调用结果

有关唯一的 API 专属返回调用结果，请参见下表。更多详情请参考 [请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Code |Integer |`0` |状态码。 |
|Message |String |`success` |状态信息。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=RestartSpeechTask&Version=2023-01-01
{
    "TaskID": "497430****75c378"
}
```


<span id="Sample response"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestID": "2025111815174611F9EB957342DF410655",
        "RequestId": "20230604110420****100232280022D31",
        "Action": "RestartSpeechTask",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Code": 0,
        "Message": "success"
    }
}
```


<span id="Error codes"></span>
## 错误码

关于错误码的更多信息，请参见 [通用错误码](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes)。
