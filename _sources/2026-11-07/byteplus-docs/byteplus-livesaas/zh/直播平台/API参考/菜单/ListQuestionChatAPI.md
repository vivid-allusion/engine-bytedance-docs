---
title: "ListQuestionChatAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/listquestionchatapi-zh-CN"
---

调用此 API 可获取直播间问答菜单中的问题。结果可按点赞数或发送时间排序，使您能够优先获取最受欢迎或最新的问题。要获取某个具体问题的回复，您可以使用返回调用结果中的问题 ID 调用 [ListAnswerChatAPI](https://docs.byteplus.com/ihay5kb0/7mknjxub)

<span id="fdea8512"></span>
## 要求


* 配额：每个账号每分钟最多查询 120 次

* 前提条件：需拥有 BytePlus 账号或具备 Live 控制 \> 编辑权限的 IAM 用户。如需了解如何添加 IAM 用户，请参见 [管理用户、组织和角色](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles-zh-CN)。


<span id="79719cd3"></span>
## HTTP 请求


* URL：`https://livesaas.byteplusapi.com/?Action=ListQuestionChatAPI&Version=2020-06-01`

* 方法：GET


<span id="c0f49424"></span>
## 请求参数

以下表格未包含所有通用请求参数。完整参数列表请参见 [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters-zh-CN#f1706967)。

<span id="32f3e185"></span>
### Query


|名称 |数据类型 |是否必填 |示例值 |接口行为 |
|---|---|---|---|---|
|Action |String |是 |`ListQuestionChatAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |该 API 操作的版本。当前版本：`2020-06-01`。 |
|ActivityId |Long |是 |`17218312****` |直播间的活动 ID。您可通过调用 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-CN) 获取该 ID。 |
|PageNumber |Long |否 |`1` |返回页码。默认值：`1`。 |
|PageSize |Long |否 |`100` |每页返回的结果数量。默认值：`100`。<br><br>取值范围：[1,1000]。 |
|OrderType |Integer |否 |`0` |指定返回的问题按点赞数或发送时间排序。<br><br>默认值：`0`。<br><br>有效值：<br><br><br>* `0`：问题按发送时间倒序排列。最新的问题将优先返回。<br><br>* `1`：问题按点赞数排序。最受欢迎的问题将优先返回。 |
|FilterPin |Integer |否 |`0` |指定返回哪些问题。<br><br>默认值：`0`。<br><br>有效值：<br><br><br>* `0`：所有问题。<br><br>* `1`：问答菜单置顶的问题。<br><br>* `2`：问答菜单未置顶的问题。 |


<span id="78eacc9f"></span>
## 返回调用结果参数


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|PageNumber |Long |`1` |返回页码。 |
|PageSize |Long |`100` |每页返回的结果数量。 |
|TotalCount |Long |`1` |返回的问题总数。 |
|QuestionMsgs |Array of[QuestionMsg](https://docs.byteplus.com/docs/byteplus-livesaas/listquestionchatapi-zh-CN#e2930158) |`-` |返回的问题列表。 |


<span id="e2930158"></span>
### QuestionMsg


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|QuestionMsgId |Long |`5941305` |问题 ID。 |
|UserNickName |String |`Viewer A` |发送问题用户的昵称。 |
|UserExternalId |String |`12387404123****` |发送问题用户在第三方平台的唯一标识。仅通过以下方式登录直播间的观众才拥有该 ID。您可使用该 ID 在您的组织内识别观众，以便进行用户洞察和数据分析。<br><br>该 ID 会根据观众登录直播间的方式而变化。<br><br><br>* 自定义账号：自定义登录时通过 `UserId` 参数传递的值。详情请参见 [自定义认证登录](https://docs.byteplus.com/docs/byteplus-livesaas/docs-applying-advanced-viewing-restrictions-zh-CN)。<br><br>* 手机号：观众使用手机号注册 BytePlus Live 时生成的 `passport_id`。<br><br>* OAuth 2.0：你自有账号体系中对应用户 ID 的字段。<br><br>* 白名单：观众输入的白名单校验信息。 |
|CreateTime |Long |`1717145029` |问题发送时间，Unix 时间戳格式。单位：秒。 |
|Content |String |`问题 A` |问题内容。 |
|LikeCount |Long |`20` |问题的点赞数。 |
|IsPined |Integer |`0` |表示该问题是否置顶在问答菜单。<br><br><br>* `0`：未置顶。<br><br>* `1`：已置顶。 |


<span id="8c70f7da"></span>
## 示例

<span id="bf1a2f5e"></span>
### 请求示例

```JSON
GET https://livesaas.byteplusapi.com/?Action=ListQuestionChatAPI&Version=2020-06-01&ActivityId=17218312****&PageNumber=1&PageSize=100&OrderType=0&FilterPin=0
```


<span id="34c8cb31"></span>
### 返回示例

```JSON
{
  "ResponseMetadata": {
    "RequestId": "201806041104200100100232280022D30",
    "Action": "ListQuestionChatAPI",
    "Version": "2020-06-01",
    "Service": "livesaas",
    "Region": "ap-singapore-1",
    "SystemTime": 1717593301
  },
    "Result": {
        "PageNumber": 1,
        "PageSize": 100,
        "TotalCount": 1,
        "QuestionMsgs": [
            {
                "QuestionMsgId": 5941305,
                "UserNickName": "Viewer A",
                "UserExternalId": "",
                "CreateTime": 1717145029,
                "Content": "Question A",
                "LikeCount": 20,
                "IsPined": 0
            }
        ]
    }
}
```


<span id="2b1e6a6a"></span>
## 错误码

通用错误码列表请参见 [常见错误和状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes-zh-CN)。
