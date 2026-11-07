---
title: "SearchSpeechTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/SearchSpeechTask-zh-CN"
---

调用 `SearchSpeechTask` API，根据指定条件搜索符合要求的 AI 配音任务。

<span id="Requirements"></span>
## 要求

**速率限制**：每个账号每秒最多 10 次请求。

<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=SearchSpeechTask&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用时，除了 API 专属参数外，还必须包含 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`SearchSpeechTask` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|TaskStatus |String 数组 |否 |`["running", "init"]` |任务状态。默认返回所有状态的任务。有效值：<br><br><br>* `running`：运行中。<br><br>* `done`：已结束。<br><br>* `prestop`：停止中。<br><br>* `init`：准备中。<br><br>* `prepare`：启动中。 |
|Name |String |否 |`TaskA` |任务名称。默认返回所有任务。名称长度必须为 1 到 20 个字符。不支持模糊搜索，英文字符区分大小写。名称可包含以下字符：<br><br><br>* 数字（0\-9）<br><br>* 大写字母（A\-Z）<br><br>* 小写字母（a\-z）<br><br>* 中文字符<br><br>* 下划线（_）<br><br>* 连字符（\-） |
|CreateTimeSt |String |否 |`2025-11-13 17:01:06` |返回创建时间大于或等于该时间的任务。时间格式为 RFC3339，使用 UTC+8，精确到秒。默认返回所有任务。 |
|CreateTimeEd |String |否 |`2025-11-14 15:34:43` |返回创建时间小于或等于该时间的任务。时间格式为 RFC3339，使用 UTC+8，精确到秒。默认返回所有任务。 |
|Page |Integer |是 |`1` |返回的页码。该值必须为正整数。 |
|PageSize |Integer |是 |`10` |每页返回的结果数量。该值必须大于 `0`。 |


<span id="Response parameters"></span>
## 返回调用结果参数

有关唯一的 API 专属返回调用结果参数，请参见下表。更多详情请参考 [请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Code |Integer |`0` |状态码。 |
|Message |String |`success` |状态信息。 |
|数据 |[Data](https://docs.byteplus.com/en/docs/24/118393#data) 对象 |`-` |任务信息。 |


<span id="data"></span>
### 数据


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Count |Integer |`1` |返回任务总数。 |
|任务 |[Tasks](https://docs.byteplus.com/en/docs/24/118393#tasks) 数组 |`-` |任务信息。 |


<span id="tasks"></span>
### 任务


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Name |String |`TaskA` |任务名称。 |
|Status |String |`done` |任务状态。有效值：<br><br><br>* `running`：运行中。<br><br>* `done`：已结束。<br><br>* `prestop`：停止中。<br><br>* `init`：准备中。<br><br>* `prepare`：启动中。 |
|TaskID |String |`b71c61469024ae4f` |任务 ID。 |
|CreatedAt |String |`2025-11-14T15:34:43+08:00` |任务开始时间。时间格式为 RFC3339，使用 UTC+8，精确到秒。 |
|UpdatedAt |String |`2025-11-14T16:50:53+08:00` |任务更新时间。时间格式为 RFC3339，使用 UTC+8，精确到秒。 |
|StoppedAt |String |`2025-11-14T16:50:49+08:00` |任务实际结束时间。时间格式为 RFC3339，使用 UTC+8，精确到秒。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=SearchSpeechTask&Version=2023-01-01
{
    "TaskStatus": [
        "running",
        "init"
    ],
    "Name": "TaskA",
    "CreateTimeSt": "2025-11-13 17:01:06",
    "CreateTimeEd": "2025-11-14 15:34:43",
    "Page": 1,
    "PageSize": 10
}
```


<span id="Sample response"></span>
### 返回调用结果示例

```json
{
    "ResponseMetadata": {
        "RequestID": "2025111417350416C47E772ECEBC01847B",
        "RequestId": "20230604110420****100232280022D31",
        "Action": "SearchSpeechTask",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Code": 0,
        "Message": "success",
        "Data": {
            "Count": 1,
            "Tasks": [
                {
                    "Name": "TaskA",
                    "Status": "done",
                    "TaskID": "b71c61****24ae4f",
                    "CreatedAt": "2025-11-14T15:34:43+08:00",
                    "UpdatedAt": "2025-11-14T16:50:53+08:00",
                    "StoppedAt": "2025-11-14T16:50:49+08:00"
                }
            ]
        }
    }
}
```


<span id="Error codes"></span>
## 错误码

关于错误码的更多信息，请参见 [通用错误码](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes)。
