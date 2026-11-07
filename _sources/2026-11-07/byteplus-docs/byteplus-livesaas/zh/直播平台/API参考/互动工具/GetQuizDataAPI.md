---
title: "GetQuizDataAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/GetQuizDataAPI-zh-CN"
---

调用`GetQuizDataAPI`以获取直播间中指定答题的详细信息。包括参与人数、答对人数以及每个选项的内容。

<span id="Requirements"></span>
## 要求


* 配额：每个账号每分钟最多可查询 120 次。

* 前提条件：需要 BytePlus 账号，或具有**Insights** \> **View only** 或 **Edit** 权限的 IAM 用户。如需了解如何添加 IAM 用户，请参见[Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。


<span id="HTTP request"></span>
## HTTP 请求


* 方法：GET

* Endpoint：https://livesaas.byteplusapi.com/?Action=GetQuizDataAPI&Version=2020\-06\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

下表未包含所有通用请求参数。完整列表请参见[Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`GetQuizDataAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。当前版本：`2020-06-01`。 |
|ActivityId |Long |是 |17218346\*\*\*\* |直播间的活动 ID。可通过调用[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi)获取该 ID。 |
|QuizID |Integer |是 |1779512495\*\*\*\* |答题的 ID。可通过调用[ListQuizStatisticsAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/ListQuizStatisticsAPI)获取该 ID。 |


<span id="Response parameters"></span>
## 返回调用结果参数


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|TotalCount |Integer |2 |参与人数。 |
|RightCount |Integer |1 |答对人数。 |
|QuizOptions |Array of[QuizOptions](https://docs.byteplus.com/docs/byteplus-livesaas/GetQuizDataAPI-zh-CN#quizoptions) |*  |答题的选项列表。 |


<span id="quizoptions"></span>
### QuizOptions


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|OptionSite |String |A |选项标识符。 |
|OptionName |String |1 |选项内容。 |
|OptionCount |String |1 |选择该选项的人数。 |
|OptionPercent |Integer |50 |选择该选项人数占总参与人数的百分比。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetQuizDataAPI&Version=2020-06-01&ActivityId=17218346****&QuizID=1779512495345672
```


<span id="Sample response"></span>
### 返回示例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetQuizDataAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1697446406
    },
    "Result": {
        "TotalCount": 2,
        "RightCount": 1,
        "QuizOptions": [
            {
                "OptionSite": "A",
                "OptionName": "1",
                "OptionCount": "1",
                "OptionPercent": 50
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 错误码

常见错误码请参见[Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
