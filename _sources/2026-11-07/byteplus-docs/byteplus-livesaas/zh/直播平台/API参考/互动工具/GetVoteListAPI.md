---
title: "GetVoteListAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/GetVoteListAPI-zh-CN"
---

调用`GetVoteListAPI`以获取指定直播间的投票配置信息。

<span id="Requirements"></span>
## 要求


* 配额：每个账号每分钟最多可查询 120 次。

* 前提条件：需拥有 BytePlus 账号，或具有**Insights** \> **仅查看**或**编辑**权限的 IAM 用户。如需了解如何添加 IAM 用户，请参见[管理用户、组织和角色](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。


<span id="HTTP request"></span>
## HTTP 请求


* 方法：GET

* Endpoint：https://livesaas.byteplusapi.com/?Action=GetVoteListAPI&Version=2020\-06\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

以下表格未包含所有通用请求参数。完整列表请参见[通用请求参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`GetVoteListAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。当前版本：`2020-06-01`。 |
|ActivityId |Long |是 |17218346\*\*\*\* |直播间的活动 ID。可通过调用[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi)获取该 ID。 |
|PageNo |Integer |否 |`1` |返回的页码。默认值：`1`。 |
|PageCount |Integer |否 |`10` |每页返回的结果数量。默认值：`10`。 |


<span id="Response parameters"></span>
## 返回调用结果参数


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|PageNo |Integer |`1` |返回的页码。 |
|PageCount |Integer |`10` |每页返回的结果数量。 |
|VoteList |Array of[VoteList](https://docs.byteplus.com/docs/byteplus-livesaas/GetVoteListAPI-zh-CN#votelist) |`-` |直播间的投票配置列表。 |


<span id="votelist"></span>
### VoteList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|VoteId |String |`vote1779514244272189` |投票 ID。 |
|Title |String |Vote |投票标题。 |
|TotalCount |Integer |`1` |参与人数。 |
|ChoiceType |String |`Single` |投票类型。取值如下：<br><br><br>* `Single`：单选<br><br>* `Multiple`：多选 |
|Deadline |Integer |`1697166317` |投票截止时间。Unix 时间戳，单位为秒。 |
|Status |String |`Export` |投票状态。取值如下：<br><br><br>* `Init`：已创建<br><br>* `Export`：已发送<br><br>* `Deadline`：已结束<br><br>* `Delete`：已删除 |
|ActivityId |Long |17218346\*\*\*\* |直播间的活动 ID。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetVoteListAPI&Version=2020-06-01&ActivityId=17218346****&PageNo=1&PageCount=10
```


<span id="Sample response"></span>
### 返回示例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetVoteListAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1697446406
    },
    "Result": {
        "PageNo": 1,
        "PageCount": 10,
        "VoteList": [
            {
                "VoteId": "vote1779514244272189",
                "Title": "Vote",
                "TotalCount": 1,
                "ChoiceType": "Single",
                "Deadline": 1697166317,
                "Status": "Export",
                "ActivityId": 17218346****
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 错误码

常见错误码列表请参见[常见错误及状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
