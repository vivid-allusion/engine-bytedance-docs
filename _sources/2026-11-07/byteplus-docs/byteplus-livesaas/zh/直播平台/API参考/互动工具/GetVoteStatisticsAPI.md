---
title: "GetVoteStatisticsAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/GetVoteStatisticsAPI-zh-CN"
---

调用`GetVoteStatisticsAPI`以获取直播间的投票数据。

<span id="Requirements"></span>
## 要求


* 配额：每个账号每分钟最多查询 120 次。

* 前提条件：需拥有 BytePlus 账号，或具有**Insights** \> **仅查看**或**编辑**权限的 IAM 用户。如需了解如何添加 IAM 用户，请参见[管理用户、组织和角色](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。


<span id="HTTP request"></span>
## HTTP 请求


* 方法：GET

* Endpoint：https://livesaas.byteplusapi.com/?Action=GetVoteStatisticsAPI&Version=2020\-06\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

下表未包含所有通用请求参数。完整列表请参见[通用请求参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`GetVoteStatisticsAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |该 API 操作的版本。当前版本：`2020-06-01`。 |
|ActivityId |Long |是 |17218346\*\*\*\* |直播间的活动 ID。可通过调用[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi)获取该 ID。 |
|PageNo |Integer |否 |1 |返回的页码。默认值：`1`。 |
|PageCount |Integer |否 |10 |每页返回的结果数量。默认值：`10`。 |
|VoteId |String |是 |vote1754472505032763 |投票 ID。可通过调用[GetVoteListAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/GetVoteListAPI)获取投票 ID。 |


<span id="Response parameters"></span>
## 返回调用结果


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|PageNo |Integer |1 |返回的页码。 |
|PageCount |Integer |10 |每页返回的结果数量。 |
|TotalCount |Integer |1 |总条目数。 |
|VoteStatisticsList |Array of[VoteStatisticsList](https://docs.byteplus.com/docs/byteplus-livesaas/GetVoteStatisticsAPI-zh-CN#votestatisticslist) |*  |投票人信息列表。 |


<span id="votestatisticslist"></span>
### VoteStatisticsList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|UserChose |Array of[UserChose](https://docs.byteplus.com/docs/byteplus-livesaas/GetVoteStatisticsAPI-zh-CN#userchose) |*  |用户选择的选项。 |
|UserName |String |观众 A |观众昵称。 |
|IP |String |10.5.xx.xx |观众的 IP 地址。 |
|VoteTime |Integer |1673169500 |投票时间，Unix 时间戳格式。 |
|Extra |String |abc |同步到 BytePlus Live 的附加参数，可用于与观众关联。例如，可以将观众所在部门从自有账号系统同步到 BytePlus Live。 |
|UserID |Long |1738686737584142 |观众在 BytePlus Live 的唯一标识。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若观众未通过昵称或其他方式登录直播间，其用户 ID 为 0。</div><br> |
|UserTel |String |137xxxxx88 |观众的手机号。 |
|Email |String |zhibo@xxx.com |观众的邮箱。 |
|UserAgent |String |Intel Mac OS X 10_15_7 |观众设备的 User\-Agent 字符串。 |
|ExternalId |String |1605756488530014 |观众在第三方平台的唯一标识。支持模糊搜索。<br><br>该 ID 会根据观众登录直播间的方式而变化。更多信息请参见[观众行为数据](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-data-statistics#viewer-behavior-data)。可使用该 ID 在组织内识别观众，实现用户洞察与数据分析。 |


<span id="userchose"></span>
### UserChose


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|OptionSite |String |D |所选选项的标识。 |
|OptionName |String |选项内容 |所选选项的文本。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetVoteStatisticsAPI&Version=2020-06-01&ActivityId=17218346****&PageNo=1&PageCount=10&VoteId=vote1754472505032763
```


<span id="Sample response"></span>
### 返回示例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetVoteStatisticsAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1697446406
    },
    "Result": {
        "PageNo": 1,
        "PageCount": 10,
        "TotalCount": 1,
        "VoteStatisticsList": [
            {
                "UserChose": [
                    {
                        "OptionSite": "D",
                        "OptionName": "Option content"
                    }
                ],
                "UserName": "Audience A",
                "IP": "10.5.xx.xx",
                "VoteTime": 1673169500,
                "Extra": "abc",
                "UserID": 1738686737584142,
                "UserTel": "137xxxxx88",
                "Email": "zhibo@xxx.com",
                "UserAgent": "Intel Mac OS X 10_15_7",
                "ExternalId": "1605756488530014"
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 错误码

常见错误码列表请参见[常见错误及状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
