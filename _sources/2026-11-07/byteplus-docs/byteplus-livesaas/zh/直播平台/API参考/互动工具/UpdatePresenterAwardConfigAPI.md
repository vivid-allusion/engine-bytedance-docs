---
title: "UpdatePresenterAwardConfigAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/UpdateAwardConfig-zh-CN"
---

调用 `UpdatePresenterAwardConfigAPI`，可为直播间新增、更新或删除实时抽奖。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">更新抽奖时，必须传递所有自定义参数的值，以避免参数被重置为默认值。</div>


<span id="Requirements"></span>
## 要求


* 限流：每个账号每秒最多 10 次请求

* 前提条件：需拥有 BytePlus 账号，或具备 **Live control** \> **Edit** 权限的 IAM 用户。如需了解如何添加 IAM 用户，请参见 [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。


<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* 接口地址：https://livesaas.byteplusapi.com/?Action=UpdatePresenterAwardConfigAPI&Version=2023\-08\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

下表未包含所有通用请求参数。完整参数列表请参见 [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### Query


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`UpdatePresenterAwardConfigAPI` |API 操作。 |
|Version |String |是 |`2023-08-01` |本 API 操作的版本。当前版本：`2023-08-01`。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|ActivityId |Long |是 |17218346\*\*\*\* |直播间的活动 ID。可通过调用 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi) 获取该 ID。 |
|AccountId |Long |是 |3000\*\*\*\* |您的账号 ID，可在 [My Account](https://console.byteplus.com/user/basics/) 页面找到。 |
|Id |Long |是 |`36576` |实时抽奖 ID。该值根据如下情况变化：<br><br><br>* 创建实时抽奖时，传入 `0`。<br><br>* 更新或删除抽奖配置时，传入抽奖 ID。可通过 [ListAwardConfigs](https://docs.byteplus.com/docs/byteplus-livesaas/ListAwardConfigs) API 获取该 ID。 |
|Name |String |否 |抽奖活动 |抽奖名称。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">创建或更新实时抽奖时，必须填写此参数。</div><br> |
|AwardType |Integer |否 |1 |抽奖方式。取值如下：<br><br><br>* `1`：自动抽奖<br><br>* `2`：手动抽奖<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">创建或更新抽奖时，必须填写此参数。</div><br> |
|DeadLine |Long |否 |30 |抽奖倒计时时长，单位为分钟。默认值为 `0`。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">仅当<code>AwardType</code>的值为<code>1</code>时，此参数有效。</div><br> |
|BarragePwd |String |否 |弹幕密码 |抽奖弹幕密码。默认值为空。 |
|WinnerInfoType |String |否 |1 |中奖者需提供的个人信息。支持的取值包括：<br><br><br>* 1：收货地址<br><br>* 2：手机号<br><br>* 3：收件人姓名 |
|AwardNum |Integer |否 |1000 |奖品数量。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">创建或更新实时抽奖时，必须填写此参数。</div><br> |
|RangeStatus |Integer |否 |0 |抽奖规则。默认值为 `0`。取值如下：<br><br><br>* `0`：所有观众中奖概率相同。<br><br>* `1`：未中奖观众优先。 |
|ShowPeopleNumber |Integer |否 |0 |是否在观看页显示抽奖实际参与人数。默认值为 `0`。取值如下：<br><br><br>* `0`：显示<br><br>* `1`：不显示 |
|Status |Integer |是 |`1` |指定对实时抽奖执行的操作。取值如下：<br><br><br>* `1`：创建或更新实时抽奖<br><br>* `5`：删除实时抽奖 |
|AwardCondition |Object of[AwardCondition](https://docs.byteplus.com/docs/byteplus-livesaas/UpdateAwardConfig-zh-CN#awardcondition) |否 |*  |参与抽奖的条件。 |
|ShowWinnerComment |Integer |否 |0 |是否显示中奖者详情。默认值为 `0`。取值如下：<br><br><br>* `0`：不显示<br><br>* `1`：显示 |
|AwardId |Long |否 |1621615169 |奖品 ID。可通过调用 [GetAwardItemList](https://docs.byteplus.com/en/docs/byteplus-livesaas/getawarditemlist?lang=en) 获取该 ID。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">创建或更新实时抽奖时，必须填写此参数。</div><br> |


<span id="awardcondition"></span>
### AwardCondition


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|答题 |字符串 |否 |all |设置用户参与问答以获得抽奖资格的要求。如果未设置此参数（默认），则该条件为未开启。<br><br><br>* `"all"`：用户必须在抽奖前答完直播期间发送的**所有**问题。<br><br>* `1`\-`999`：用户必须提交**至少**该数量的答案才有资格。例如，值为`3`时，要求用户至少答完三道题。 |
|RightQuiz |字符串 |否 |`1` |用户必须答对的最少题数。 |
|问卷 |字符串 |否 |1 |用户必须提交的最少问卷数。 |
|签到 |字符串 |否 |all |用户必须完成的最少签到次数。 |
|投票 |字符串 |否 |1 |用户必须提交的最少投票数。 |


<span id="awarditemconfigs"></span>
### 返回调用结果参数


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|状态 |布尔值 |`true` |如果配置更新成功，则返回`true`。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```JSON
POST https://livesaas.byteplusapi.com/?Action=UpdatePresenterAwardConfigAPI&Version=2023-08-01
{
    "ActivityId": 172183461234****,
    "AccountId": 3000****,
    "Id": 0,
    "Status": 1,
    "Name": "Prize A",
    "AwardType": 1,
    "DeadLine": 1,
    "AwardId": 1001,
    "AwardNum": 100,
    "RangeStatus": 1,
    "WinnerInfoType": "1",
    "AwardCondition": {
        "CheckIn": "1"
    }
}
```


<span id="Sample response"></span>
### 返回示例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UpdatePresenterAwardConfigAPI",
        "Version": "2023-08-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1697446406
    },
    "Result": {
        "Status": true
    }
}
```


<span id="Error codes"></span>
## 错误码

常见错误码列表请参见 [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
