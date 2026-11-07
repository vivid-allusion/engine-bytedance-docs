---
title: "UpdateSpeechTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/UpdateSpeechTask-zh-CN"
---

调用 `UpdateSpeechTask` API 以更新 AI 配音任务的功能开关状态。该 API 通常用于在直播流过程中根据需要开启或关闭翻译功能。

<span id="Requirements"></span>
## 要求


* **请求频率限制**：每个账号每秒最多可发起 10 次请求。

* **计费情况**：AI 配音任务根据任务的**实际流推送时长**计费。更多信息请参见 [AI 配音计费](https://docs.byteplus.com/en/docs/byteplus-media-live/ai_dubbing)。


<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* 接口地址：https://open.byteplusapi.com/?Action=UpdateSpeechTask&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用时，除需传递 API 专属参数外，还必须包含 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`UpdateSpeechTask` |API 操作。 |
|Version |String |是 |`2023-01-01` |该 API 操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### 请求体参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|TaskID |String |是 |`49743067b675c378` |任务 ID。可通过调用 [CreateSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateSpeechTask?lang=en) 或 [SearchSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/SearchSpeechTask) 获取该 ID。 |
|Switch |String |是 |`AllDisable` |开关状态。有效值：<br><br><br>* `AllDisable`：禁用当前模式下的所有功能。<br><br>* `AllEnable`：启用在创建 AI 配音任务时通过调用 [CreateSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateSpeechTask) 已开启的当前模式下所有功能。<br><br><br>例如，在面向英语用户的直播流中，仅当非英语用户发言时，可将此参数设置为 `AllEnable`，以输出翻译内容。其他时间则设置为 `AllDisable`，以输出未经 AI 配音处理的原始内容。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">更改该参数值不会中断任务。任务计费持续进行。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">当该参数设置为 <code>AllDisable</code> 时，原始音量配置也将失效。</div><br> |


<span id="Response parameters"></span>
## 返回调用结果参数

如需了解 API 专属返回参数，请参见下表。更多详情请参考 [请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)章节。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Code |Integer |`0` |状态码。 |
|Message |String |`success` |状态信息。 |
|Data |[Data](https://docs.byteplus.com/en/docs/24/118391#data) 对象 |`-` |任务信息。 |


<span id="data"></span>
### 数据


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|OptID |Integer |`2` |任务更新序号。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=UpdateSpeechTask&Version=2023-01-01
{
    "TaskID": "497430****75c378",
    "Switch": "AllDisable"
}
```


<span id="Sample response"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestID": "20251117142336C37E6DC6C26C2529018E",
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UpdateSpeechTask",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Code": 0,
        "Message": "success",
        "Data": {
            "OptID": 2
        }
    }
}
```


<span id="Error codes"></span>
## 错误码

关于错误码的更多信息，请参见 [通用错误码](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes)。
