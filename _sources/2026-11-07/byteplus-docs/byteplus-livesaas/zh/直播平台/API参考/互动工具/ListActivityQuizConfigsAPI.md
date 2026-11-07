---
title: "ListActivityQuizConfigsAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/ListActivityQuizConfigs-zh-CN"
---

调用`ListActivityQuizConfigsAPI`以获取指定直播间的答题配置信息。

<span id="Requirements"></span>
## 要求


* 速率限制：每个账号每秒最多 10 次请求

* 前提条件：需拥有 BytePlus 账号或具备**直播控制** \> **编辑**权限的 IAM 用户。关于如何添加 IAM 用户的更多信息，请参见[管理用户、组织和角色](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。


<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://livesaas.byteplusapi.com/?Action=ListActivityQuizConfigsAPI&Version=2023\-08\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

下表未包含所有通用请求参数。完整参数列表请参见[通用请求参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### Query


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`ListActivityQuizConfigsAPI` |API 操作。 |
|Version |String |是 |`2023-08-01` |此 API 操作的版本。当前版本：`2023-08-01`。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|ActivityId |Long |是 |17218346\*\*\*\* |直播间的活动 ID。可通过调用[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi)获取该 ID。 |


<span id="Response parameters"></span>
## 返回调用结果参数


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|QuizConfigs |Array of[QuizConfigs](https://docs.byteplus.com/docs/byteplus-livesaas/ListActivityQuizConfigs-zh-CN#quizconfigs) |*  |答题配置信息。 |


<span id="quizconfigs"></span>
### QuizConfigs


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Id |Long |`180848123521****` |答题 ID。 |
|ActivityId |Long |1770637083\*\*\*\* |直播间 ID。 |
|QuizTitle |String |Quiz 1 |答题标题。 |
|QuizResultType |Integer |`0` |指定答案的公布时机。有效值如下：<br><br><br>* `0`：提交后自动公布答案<br><br>* `1`：答题时间结束后自动公布答案<br><br>* `2`：手动公布答案 |
|QuizOptions |Array of[QuizOptions](https://docs.byteplus.com/docs/byteplus-livesaas/ListActivityQuizConfigs-zh-CN#quizoptions) |*  |选项信息。 |
|RightOptions |Array of String |["A"] |正确答案。 |
|Deadline |Long |`30` |答题时间限制。单位：秒。 |
|SendTime |Long |1621111109 |发送时间。Unix 时间戳，单位为秒。如未发送，值为`-1`。 |
|QuizStatus |Integer |[0,1,2,3,5] |答题状态。有效值如下：<br><br><br>* `0`：已初始化，即已创建但未发送<br><br>* `1`：已发送<br><br>* `2`：答案已手动公布。该值仅适用于历史数据<br><br>* `3`：已结束<br><br>* `4`：已删除<br><br>* `5`：已撤回 |
|QuizTitleType |Integer |`1` |题型。有效值如下：<br><br><br>* `0`：单选题<br><br>* `1`：多选题 |
|QuizAnalysis |String |1 的倒数是 1 |答案解析。 |


<span id="quizoptions"></span>
### QuizOptions


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|OptionSite |String |`A` |选项。 |
|OptionName |String |1 |选项内容。 |
|OptionCount |Long |`50` |选择该选项的用户数量。 |
|OptionPercent |String |`100` |该选项在所有参与者中的选择百分比。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```JSON
POST https://livesaas.byteplusapi.com/?Action=ListActivityQuizConfigsAPI&Version=2023-08-01
{
    "ActivityId": 1770637083****
}
```


<span id="Sample response"></span>
### 返回调用结果示例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListActivityQuizConfigsAPI",
        "Version": "2023-08-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1697446406
    },
    "Result": {
        "QuizConfigs": [
            {
                "Id": 180848123521****,
                "ActivityId": 1770637083****,
                "QuizTitle": "Quiz 1",
                "QuizResultType": 0,
                "QuizOptions": [
                    {
                        "OptionSite": "A",
                        "OptionName": "1",
                        "OptionCount": 50,
                        "OptionPercent": "100"
                    }
                ],
                "RightOptions": [
                    "A"
                ],
                "Deadline": 30,
                "SendTime": 1621111109,
                "QuizStatus": 1,
                "QuizTitleType": 1,
                "QuizAnalysis": "The reciprocal of 1 is 1"
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 错误码

常见错误码列表请参见[常见错误码和状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
