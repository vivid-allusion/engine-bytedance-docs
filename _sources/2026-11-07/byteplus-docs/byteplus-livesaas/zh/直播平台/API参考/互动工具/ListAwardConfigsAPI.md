---
title: "ListAwardConfigsAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/ListAwardConfigs-zh-CN"
---

调用`ListAwardConfigsAPI`以获取抽奖的配置详情。

<span id="Requirements"></span>
## 要求


* 速率限制：每个账号每秒最多 10 次请求

* 前提条件：需拥有 BytePlus 账号，或具备**直播控制** \> **仅查看**或**编辑**权限的 IAM 用户。如需了解如何添加 IAM 用户，请参见[管理用户、组织和角色](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。


<span id="HTTP request"></span>
## HTTP 请求


* 方法：GET

* Endpoint：https://livesaas.byteplusapi.com/?Action=ListAwardConfigsAPI&Version=2023\-08\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

以下表格未包含所有通用请求参数。完整列表请参见[通用请求参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`ListAwardConfigsAPI` |API 操作。 |
|Version |String |是 |`2023-08-01` |该 API 操作的版本。当前版本：`2023-08-01`。 |
|ActivityId |Long |是 |17218346\*\*\*\* |直播间的活动 ID。可通过调用[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi)获取该 ID。 |
|All |Integer |是 |1 |指定是否查询直播间内所有实时抽奖配置。默认值为`0`。有效值如下：<br><br><br>* `0`：仅查询已发送的抽奖配置<br><br>* `1`：查询直播间内所有抽奖配置 |


<span id="Response parameters"></span>
## 返回调用结果参数


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|AwardConfigs |Array of[AwardConfigs](https://docs.byteplus.com/docs/byteplus-livesaas/ListAwardConfigs-zh-CN#awardconfigs) |`-` |实时抽奖配置信息列表。 |


<span id="awardconfigs"></span>
### AwardConfigs


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Id |Long |`36576` |实时抽奖 ID。 |
|ActivityId |Long |17218346\*\*\*\* |直播间 ID。 |
|Name |String |抽奖 |抽奖名称。 |
|AwardType |Integer |1 |抽奖方式。有效值如下：<br><br><br>* `1`：自动抽奖<br><br>* `2`：手动抽奖 |
|DeadLine |Long |`1` |抽奖倒计时剩余分钟数。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">仅当<code>AwardType</code>的值为<code>1</code>时，该参数有效。</div><br> |
|BarragePwd |String |comment |抽奖弹幕评论密码。 |
|Status |Integer |`4` |抽奖状态。有效值如下：<br><br><br>* `1`：未发送<br><br>* `2`：进行中<br><br>* `4`：已完成<br><br>* `5`：已删除<br><br>* `7`：已撤回<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">要获取未发送抽奖的信息，请将<code>All</code>参数设置为<code>1</code>。</div><br> |
|WinnerCount |Integer |1 |当前奖项的获奖人数。 |
|ParticipantCount |Integer |`5` |参与人数。 |
|SendTime |Integer |`1673199096` |抽奖发送时间，单位为秒的 Unix 时间戳。 |
|OpenAwardTime |Integer |`1673199158` |抽奖结果公布时间，单位为秒的 Unix 时间戳。 |
|AwardNum |Integer |`1` |奖品总数。 |
|RangeStatus |Integer |0 |抽奖规则。有效值如下：<br><br><br>* `0`：所有观众中奖概率相同。<br><br>* `1`：优先未中奖观众。 |
|ShowPeopleNumber |Integer |0 |是否在观看页展示抽奖实际参与人数。有效值如下：<br><br><br>* `0`：展示<br><br>* `1`：不展示 |
|MsgIds |String |`155681` |通过控制台发送抽奖图文消息的 ID。 |
|AwardCondition |Object of[AwardCondition](https://docs.byteplus.com/docs/byteplus-livesaas/ListAwardConfigs-zh-CN#awardcondition) |`-` |参与抽奖的条件 |
|ShowWinnerComment |Integer |`0` |是否展示抽奖获奖者详情。<br><br><br>* `0`：不展示<br><br>* `1`：展示 |
|AwardItemInfo |Array of[AwardItemInfo](https://docs.byteplus.com/docs/byteplus-livesaas/ListAwardConfigs-zh-CN#awarditeminfo) |`-` |奖品信息。 |


<span id="awardcondition"></span>
### AwardCondition


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Quiz |String |all |设置用户参与抽奖所需的问答条件。如果未设置此参数（默认），则该条件未开启。<br><br><br>* `"all"`：用户必须在直播期间抽奖前答完**所有**发送的问题。<br><br>* `1`\-`999`：用户必须提交**至少**该数量的答题才能符合资格。例如，值为`3`时，要求用户至少答完三道题。 |
|RightQuiz |String |1 |用户必须答对的最少题目数量。如果未设置此参数（默认），则该条件未开启。<br><br><br>* `"all"`：用户必须在直播期间抽奖前答对**所有**发送的问题。<br><br>* `1`\-`999`：用户必须答对**至少**该数量的问题才能符合资格。例如，值为`3`时，要求用户至少答对三道题。 |
|Questionnaire |String |1 |用户必须提交的最少问卷数量。如果未设置此参数（默认），则该条件未开启。<br><br><br>* `"all"`：用户必须在直播期间抽奖前提交**所有**发送的问卷。<br><br>* `1`\-`999`：用户必须提交**至少**该数量的问卷才能符合资格。例如，值为`3`时，要求用户至少提交三份问卷。 |
|CheckIn |String |all |用户必须完成的最少签到次数。如果未设置此参数（默认），则该条件未开启。<br><br><br>* `"all"`：用户必须在直播期间抽奖前完成**所有**发送的签到。<br><br>* `1`\-`999`：用户必须完成**至少**该数量的签到才能符合资格。例如，值为`3`时，要求用户至少完成三次签到。 |
|Vote |String |1 |用户必须提交的最少投票次数。如果未设置此参数（默认），则该条件未开启。<br><br><br>* `"all"`：用户必须在直播期间抽奖前提交**所有**发送的投票。<br><br>* `1`\-`999`：用户必须提交**至少**该数量的投票才能符合资格。例如，值为`3`时，要求用户至少提交三次投票。 |


<span id="awarditeminfo"></span>
### AwardItemInfo


|**Parameter** |**Data Type** |**Sample Value** |**接口行为** |
|---|---|---|---|
|AwardItemId |Long |`908` |奖品ID。 |
|AwardItemName |String |奖品券 |奖品名称。 |
|AwardItemCount |Long |`1000` |奖品数量。 |
|AwardItemType |Integer |`4` |奖品类型。有效值如下：<br><br><br>* `1`：实物奖品<br><br>* `2`：虚拟奖品<br><br>* `3`：自定义奖品<br><br>* `4`：券类奖品 |
|AwardItemIcon |String |`//p.org/04ae0f42a3a04e7387e5f6fe7a18c4fb~tplv-6ed59yyum2-image.image` |奖品图标的URL，不含协议部分。 |
|AwardItemNum |String |48151841 |积分奖品批次号。长度范围为1到256个字符。可通过该批次号识别企业积分并发放给观众。 |
|AwardItemAmounts |Long |1 |每位中奖观众获得的积分数量。取值范围为[0,99999]。 |
|AwardLotteryTicketAddr |String |https://example.com |券类奖品的领取URL。长度范围为1到256个字符。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">该参数为必填项，仅在<code>AwardItemType</code>设置为4时适用。</div><br> |
|WinnerInfoType |String |[1,2,3] |实物或虚拟奖品中奖者需提供的信息类型。取值：<br><br><br>* `1`：收货地址<br><br>* `2`：手机号<br><br>* `3`：收件人姓名 |
|WinnerCount |Long |1 |当前奖项的获奖人数。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```JSON
GET https://livesaas.byteplusapi.com/?Action=ListAwardConfigsAPI&Version=2023-08-01&ActivityId=17218346****&All=1
```


<span id="Sample response"></span>
### 返回调用结果示例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListAwardConfigsAPI",
        "Version": "2023-08-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1697446406
    },
    "Result": {
        "AwardConfigs": [
            {
                "Name": "Lucky draw",
                "AwardType": 1,
                "DeadLine": 1,
                "BarragePwd": "comment",
                "Status": 4,
                "ActivityId": 17218346****,
                "SendTime": 1673199096,
                "OpenAwardTime": 1673199158,
                "RangeStatus": 0,
                "ShowPeopleNumber": 0,
                "MsgIds": "155681",
                "AwardCondition": {
                    "Quiz": "all",
                    "RightQuiz": "1",
                    "Questionnaire": "1",
                    "CheckIn": "all",
                    "Vote": "1"
                },
                "Id": 36576,
                "WinnerCount": 1,
                "ParticipantCount": 5,
                "ShowWinnerComment": 0,
                "AwardItemInfo": [
                    {
                        "AwardItemId": 908,
                        "AwardItemName": "Prize coupon",
                        "AwardItemCount": 1000,
                        "AwardItemType": 4,
                        "WinnerCount": 1,
                        "AwardItemIcon": "//p.org/04ae0f42a3a04e7387e5f6fe7a18c4fb~tplv-6ed59yyum2-image.image",
                        "AwardLotteryTicketAddr": "https://example.com",
                        "WinnerInfoType": "[1,2,3]",
                        "AwardItemNum": "48151841",
                        "AwardItemAmounts": 1
                    }
                ],
                "AwardNum": 1,
                "AwardSendTime": 1726734970,
                "AwardSendType": 1
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 错误码

有关常见错误码列表，请参见[常见错误及状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
