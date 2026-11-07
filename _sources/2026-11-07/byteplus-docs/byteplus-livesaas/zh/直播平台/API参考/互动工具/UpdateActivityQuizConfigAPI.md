---
title: "UpdateActivityQuizConfigAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/UpdateActivityQuizConfig-zh-CN"
---

调用`UpdateActivityQuizConfigAPI`，用于更新指定直播间中未发送的答题的配置信息。

<span id="Requirements"></span>
## 要求


* 限流：每个账号每秒最多 10 次请求

* 前提条件：

   * 答题尚未发送。可调用[ListActivityQuizConfigsAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/ListActivityQuizConfigs?lang=en)。若`QuizStatus`设置为`0`，表示答题尚未发送。

   * 具备 BytePlus 账号或拥有**Live control** \> **Edit** 权限的 IAM 用户。关于如何添加 IAM 用户，详见[Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。


<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://livesaas.byteplusapi.com/?Action=UpdateActivityQuizConfigAPI&Version=2023\-08\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

下表未包含所有通用请求参数。完整列表请参见[Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### Query


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`UpdateActivityQuizConfigAPI` |API 操作。 |
|Version |String |是 |`2023-08-01` |本 API 操作的版本。当前版本：`2023-08-01`。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Id |Long |是 |`1808481235212316` |答题 ID。可通过调用 ListActivityQuizConfigs API 获取 ID。 |
|ActivityId |Long |是 |17218346\*\*\*\* |直播间的活动 ID。可通过调用[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi)获取 ID。 |
|QuizTitle |String |否 |Quiz 1 |答题标题。默认为空。 |
|QuizResultType |Integer |是 |`1` |控制答案的公布时机。可选值如下：<br><br><br>* `0`：提交后自动公布答案<br><br>* `1`：答题时间结束后自动公布答案<br><br>* `2`：手动公布答案 |
|QuizOptions |Array of[QuizOptions](https://docs.byteplus.com/docs/byteplus-livesaas/UpdateActivityQuizConfig-zh-CN#quizoptions) |是 |*  |选项信息。数组元素最大数量为 8。 |
|RightOptions |Array of String |是 |`["A"]` |正确答案。确保该值与本次调用中的某个`OptionSite`的值一致。 |
|Deadline |Long |是 |`30` |答题的时间限制，单位为秒。最小值为`10`。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">仅当<code>QuizResultType</code>设置为<code>0</code>或<code>1</code>时，该参数有效。</div><br> |
|QuizTitleType |Integer |是 |`0` |题目类型。可选值如下：<br><br><br>* `0`：单选<br><br>* `1`：多选 |
|QuizAnalysis |String |否 |1 的倒数是 1 |答案解析。默认为空。 |


<span id="quizoptions"></span>
### QuizOptions


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|OptionSite |String |是 |`A` |选项标识符。 |
|OptionName |String |否 |1 |选项内容。默认为空。 |


<span id="Response parameters"></span>
## 返回调用结果参数


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Status |Boolean |`true` |若配置更新成功，则返回`true`。 |
|Id |Long |`1808481235212316` |答题 ID。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```JSON
POST https://livesaas.byteplusapi.com/?Action=UpdateActivityQuizConfigAPI&Version=2023-08-01
{
    "Id": 1808481235212316,
    "ActivityId": 17218346,
    "QuizTitle": "Quiz 1",
    "QuizResultType": 1,
    "QuizOptions": [
        {
            "OptionSite": "A",
            "OptionName": "1"
        }
    ],
    "RightOptions": [
        "A"
    ],
    "Deadline": 30,
    "QuizTitleType": 0,
    "QuizAnalysis": "The reciprocal of 1 is 1"
}
```


<span id="Sample response"></span>
### 返回示例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UpdateActivityQuizConfigAPI",
        "Version": "2023-08-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1697446406
    },
    "Result": {
        "Status": true,
        "Id": 1808481235212316
    }
}
```


<span id="Error codes"></span>
## 错误码

下表列出了本 API 操作特有的错误码。通用错误码请参见[Common error and status codes](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|403 |OperationDenied.QuizStatusNotMatchExpectedStatus |QuizStatus 与期望状态不符 |该操作仅支持更新未发送答题的配置信息。可调用 ListActivityQuizConfigs API。若`QuizStatus`设置为`0`，表示答题尚未发送。 |
