---
title: "GetCheckInListAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/GetCheckInListAPI-zh-CN"
---

调用 `GetCheckInListAPI` API 获取指定直播间的全部签到或指定签到信息，包括签到 ID、参与人数、签到时长等。

<span id="Requirements"></span>
## 要求


* 配额：每个账号每分钟最多可查询 120 次。

* 前提条件：需拥有 BytePlus 账号，或具备 **Insights** \> **仅查看** 或 **编辑**权限的 IAM 用户。关于如何添加 IAM 用户的更多信息，请参见 [管理用户、组织和角色](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。


<span id="HTTP request"></span>
## HTTP 请求


* 方法：GET

* Endpoint：https://livesaas.byteplusapi.com/?Action=GetCheckInListAPI&Version=2020\-06\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

以下表格未包含所有通用请求参数。完整参数列表请参见 [通用请求参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`GetCheckInListAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。当前版本：`2020-06-01`。 |
|ActivityId |Long |是 |17218346\*\*\*\* |直播间的活动 ID。可通过调用 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi) 获取该 ID。 |
|PageNo |Integer |否 |1 |返回的页码。默认值：`1`。 |
|PageCount |Integer |否 |10 |每页返回的结果数量。默认值：`10`。 |
|CheckInId |String |否 |checkIn1754478641140736 |签到 ID。 |


<span id="Response parameters"></span>
## 返回调用结果参数


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|CheckInList |Array of[CheckInList](https://docs.byteplus.com/docs/byteplus-livesaas/GetCheckInListAPI-zh-CN#checkinlist) |`-` |签到信息列表。 |
|PageNo |Integer |`1` |返回结果的页码。 |
|PageCount |Integer |`10` |每页返回的结果数量。 |


<span id="checkinlist"></span>
### CheckInList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|CheckInId |String |`checkIn1754478641140736` |签到 ID。 |
|CheckInName |String |开始签到 |签到标题。 |
|CheckInCount |Integer |`0` |签到参与人数。 |
|Deadline |Long |`1` |签到时长（分钟）。 |
|Status |String |`Deadline` |签到状态。有效值如下：<br><br><br>* `Init`：已创建<br><br>* `Export`：已发送<br><br>* `Deadline`：已结束<br><br>* `Delete`：已删除<br><br>* `Retract`：已撤回 |
|ActivityId |Long |`175450930238536` |直播间 ID。 |
|NeedPersonInfo |Integer |`0` |是否需要签到信息。有效值如下：<br><br><br>* `0`：不需要<br><br>* `1`：需要 |
|OpenCheckTime |Integer |`1673202771` |签到结束时间（截止时间）。该值为 Unix 时间戳（秒）。 |
|CheckInInfo |String |签到 |签到提示文本 |
|StartTime |String |`1673202711` |签到开始时间。Unix 时间戳（秒）。 |
|IsSendComment |Integer |`1` |是否在签到后发送评论。有效值如下：<br><br><br>* `0`：不发送<br><br>* `1`：发送 |
|CommentContent |String |#用户昵称#已签到 |签到后发送的评论内容。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">仅当 <code>IsSendComment</code> 设置为 <code>1</code> 时该参数生效</div><br> |
|DeadlineSecond |Integer |31 |签到时长的秒数部分。 |
|CannotWathcLiveWhenNotCheckIn |Integer |1 |未按时签到的观众是否会被移出直播间。有效值如下：<br><br><br>* `0`：不移出。<br><br>* `1`：移出。 |
|SendType |Integer |1 |签到发送方式。有效值如下：<br><br><br>* `0`：手动发送<br><br>* `1`：定时发送 |
|AutoSendTime |Long |1723455354 |定时发送时间。Unix 时间戳（秒）。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">仅当<code>SendType</code>设置为<code>1</code>时，该参数才有效。</div><br> |
|CannotWatchLivePrompt |String |因长时间未签到，观看已被暂停 |移出用户时发送的通知消息。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">仅当<code>CannotWathcLiveWhenNotCheckIn</code>设置为<code>1</code>时，该参数才生效。</div><br> |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetCheckInListAPI&Version=2020-06-01&ActivityId=17218346****&PageNo=1&PageCount=10&CheckInId=checkIn1754478641140736
```


<span id="Sample response"></span>
### 返回示例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetCheckInListAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1697446406
    },
    "Result": {
        "CheckInList": [
            {
                "CheckInId": "checkIn1754478641140736",
                "CheckInName": "Start check-in",
                "CheckInCount": 0,
                "Deadline": 1,
                "Status": "Deadline",
                "ActivityId": 175450930238****,
                "NeedPersonInfo": 0,
                "OpenCheckTime": 1673202771,
                "CheckInInfo": "Check in",
                "StartTime": "1673202711",
                "CommentContent": "#User nickname# has checked in",
                "IsSendComment": 1,
                "AutoSendTime": 1723455354,
                "CannotWathcLiveWhenNotCheckIn": 1,
                "DeadlineSecond": 31,
                "SendType": 1,
                "CannotWatchLivePrompt": "Viewing has been suspended due to prolonged failure to check in"
            }
        ],
        "PageNo": 1,
        "PageCount": 10
    }
}
```


<span id="Error codes"></span>
## 错误码

常见错误码列表请参见 [常见错误及状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
