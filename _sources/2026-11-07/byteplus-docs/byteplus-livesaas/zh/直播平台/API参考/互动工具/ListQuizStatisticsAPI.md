---
title: "ListQuizStatisticsAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/ListQuizStatisticsAPI-zh-CN"
---

调用`ListQuizStatisticsAPI`以获取答题及其互动统计数据的分页列表。数据包括参与人数、答对数量以及指定直播间的其他相关信息。

<span id="Requirements"></span>
## 要求


* 配额：每个账号每分钟最多可查询 120 次。

* 前提条件：需拥有 BytePlus 账号或具备**Insights** \> **仅查看**或**编辑**权限的 IAM 用户。如需了解如何添加 IAM 用户，请参见[管理用户、组织和角色](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。


<span id="HTTP request"></span>
## HTTP 请求


* 方法：GET

* 终端：https://livesaas.byteplusapi.com/?Action=ListQuizStatisticsAPI&Version=2020\-06\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

以下表格未包含所有通用请求参数。完整列表请参见[通用请求参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`ListQuizStatisticsAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。当前版本：`2020-06-01`。 |
|ActivityId |Long |是 |17218346\*\*\*\* |直播间的活动 ID。可通过调用[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi)获取该 ID。 |
|PageNo |Integer |否 |1 |返回的页码。默认值：`1`。 |
|PageItemCount |Integer |否 |10 |每页返回的结果数量。默认值：`10`。 |


<span id="Response parameters"></span>
## 返回调用结果参数


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|PageNo |Integer |1 |返回的页码。 |
|PageItemCount |Integer |10 |每页返回的结果数量。 |
|PageTotalCount |Integer |`1` |查询结果总数。 |
|QuizStatisticsList |Array of[QuizStatisticsList](https://docs.byteplus.com/docs/byteplus-livesaas/ListQuizStatisticsAPI-zh-CN#quizstatisticslist) |`-` |答题列表。 |


<span id="quizstatisticslist"></span>
### QuizStatisticsList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|TotalCount |Integer |`1` |参与人数。 |
|QuizTitle |String |Quiz 1 |答题标题。 |
|QuizTitleType |Integer |`0` |题型。有效值如下：<br><br><br>* `0`：单选<br><br>* `1`：多选 |
|SendTime |Integer |`1673348926` |发送时间。Unix 时间戳，单位为秒。 |
|Deadline |Integer |30 |答题时限。单位：秒。 |
|RightCount |Integer |1 |答对人数。 |
|QuizID |Integer |`1754628061265087` |答题 ID。 |
|IsDelete |Boolean |`false` |答题是否已被删除。有效值如下：<br><br><br>* `false`：未删除<br><br>* `true`：已删除 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```JSON
GET https://livesaas.byteplusapi.com/?Action=ListQuizStatisticsAPI&Version=2020-06-01&ActivityId=17791682****&PageNo=1&PageItemCount=10
```


<span id="Sample response"></span>
### 返回示例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListQuizStatisticsAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1697446406
    },
    "Result": {
        "PageNo": 1,
        "PageItemCount": 10,
        "PageTotalCount": 1,
        "QuizStatisticsList": [
            {
                "TotalCount": 1,
                "QuizTitle": "Quiz 1",
                "QuizTitleType": 0,
                "SendTime": 1673348926,
                "Deadline": 30,
                "RightCount": 1,
                "QuizID": 1754628061265087,
                "IsDelete": false
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 错误码

有关常见错误码列表，请参见[常见错误及状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
