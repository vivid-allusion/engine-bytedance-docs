---
title: "ListAwardRecordStatisticsAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/ListAwardRecordStatisticsAPI-zh-CN"
---

调用 `ListAwardRecordStatisticsAPI` API 获取指定直播间某场抽奖的参与或中奖观众列表。

<span id="Requirements"></span>
## 要求


* 频率限制：每个账号每秒最多 10 次请求

* 前提条件：需拥有 BytePlus 账号，或具备 **Insights** \> **View only** 或 **Edit** 权限的 IAM 用户。关于如何添加 IAM 用户，详见 [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。


<span id="HTTP request"></span>
## HTTP 请求


* 方法：GET

* Endpoint：https://livesaas.byteplusapi.com/?Action=ListAwardRecordStatisticsAPI&Version=2023\-08\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

下表未包含所有通用请求参数。完整列表请参见 [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### Query


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`ListAwardRecordStatisticsAPI` |API 操作。 |
|Version |String |是 |`2023-08-01` |本 API 操作的版本。当前版本：`2023-08-01`。 |
|ActivityId |Long |是 |1798615803\*\*\*\* |直播间的活动 ID。可通过调用 [ListAwardConfigs](https://docs.byteplus.com/docs/byteplus-livesaas/ListAwardConfigs) 获取该 ID。 |
|SearchType |Integer |否 |1 |观众列表类型。支持以下取值，默认值为 `0`。<br><br><br>* `0`：参与观众列表<br><br>* `1`：中奖观众列表 |
|AwardId |Long |是 |1621615169 |抽奖 ID。可通过调用 [ListAwardConfigs](https://docs.byteplus.com/en/docs/byteplus-livesaas/ListAwardConfigs) 查询该 ID。 |
|PageNo |Integer |否 |1 |要返回的页码。默认值：`1`。 |
|PageItemCount |Integer |否 |10 |每页返回的结果数量。默认值：`10`。取值范围为 [1, 500]。 |


<span id="Response parameters"></span>
## 返回调用结果参数


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|AwardRecords |Array of[AwardRecords](https://docs.byteplus.com/docs/byteplus-livesaas/ListAwardRecordStatisticsAPI-zh-CN#awardrecords) |*  |观众信息列表。 |
|PageNo |Integer |1 |返回结果的页码。 |
|PageItemCount |Integer |10 |每页返回的结果数量。 |
|PageTotalCount |Integer |1 |查询结果总数。 |


<span id="awardrecords"></span>
### AwardRecords


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|ActivityId |Integer |17218346\*\*\*\* |直播间的活动 ID。 |
|AwardId |Long |1621615169 |抽奖 ID。 |
|UserId |String |1753988749\*\*\*\* |用户 ID。 |
|UserName |String |观众A |用户昵称。 |
|LoginTel |String |158xxxx66 |观众登录时使用的手机号。 |
|AwardAddress |String |北京 |收件人地址。 |
|AwardResult |Integer |4 |观众抽奖结果。支持以下取值：<br><br><br>* `4`：抽中<br><br>* `5`：未抽中 |
|NotifyResult |Integer |1 |表示观众是否已被通知抽奖结果。支持以下取值：<br><br><br>* `1`：未通知<br><br>* `2`：已通知 |
|ExternalId |String |160575648853\*\*\*\* |观众在第三方平台的唯一标识。支持模糊搜索。<br><br>该 ID 会根据观众登录直播间的方式而变化。更多信息请参见 [Viewer behavior data](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-data-statistics#viewer-behavior-data)。可使用该 ID 在您的组织内识别观众，实现用户洞察与数据分析。 |
|AwardName |String |抽奖活动 |抽奖名称。 |
|ReceiverName |String |李 |收件人姓名。 |
|ReceiverTel |String |157xxxx66 |收件人手机号。 |
|Email |String |zhibo@xxx.com |观众在注册账号时填写的邮箱地址。 |
|OpenAwardTime |Integer |1673199158 |抽奖结果公布时间，单位为秒的 Unix 时间戳。 |
|Extra |String |abc |一个可与观众关联的、同步到 BytePlus Live 的附加参数。例如，你可以将观众的部门从你自己的账号系统同步到 BytePlus Live。 |
|UserAgent |字符串 |Intel Mac OS X 10_15_7 |观众设备的 user agent 字符串。 |
|Ip |字符串 |192.0.2.1 |观众的 IP 地址。 |
|IsPriorityUser |整数 |1 |用户是否被优先考虑中奖。有效取值如下：<br><br><br>* `0`：否<br><br>* `1`：是 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```JSON
GET https://livesaas.byteplusapi.com/?Action=ListAwardRecordStatisticsAPI&Version=2023-08-01&ActivityId=1798615803****&SearchType=1&AwardId=1621615169&PageNo=1&PageItemCount=10
```


<span id="Sample response"></span>
### 返回示例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListAwardRecordStatisticsAPI",
        "Version": "2023-08-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1697446406
    },
    "Result": {
        "PageNo": 1,
        "PageItemCount": 10,
        "PageTotalCount": 1,
        "AwardRecords": [
            {
                "ActivityId": 17218346,
                "UserName": "Audience A",
                "LoginTel": "158xxxx66",
                "AwardAddress": "Beijing",
                "AwardResult": 4,
                "NotifyResult": 1,
                "ExternalId": "160575648853****",
                "AwardName": "lucky draw event",
                "ReceiverName": "Li",
                "ReceiverTel": "157xxxx66",
                "Email": "zhibo@xxx.com",
                "OpenAwardTime": 1673199158,
                "Extra": "abc",
                "UserAgent": "Intel Mac OS X 10_15_7",
                "Ip": "192.0.2.1",
                "IsPriorityUser": 1,
                "AwardId": 1621615169,
                "UserId": "1753988749****"
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 错误码

常见错误码请参见 [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
