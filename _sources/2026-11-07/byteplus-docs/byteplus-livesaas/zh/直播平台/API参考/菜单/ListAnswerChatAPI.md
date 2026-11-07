---
title: "ListAnswerChatAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/listanswerchatapi-zh-CN"
---

调用此 API 获取答案列表，并按点赞数或发送时间进行排序，优先返回最受欢迎或最新的回复。

<span id="b82ccfd8"></span>
## 要求


* 配额：每个账号每分钟最多 120 次查询

* 前提条件：

   * 调用 [ListQuestionChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/listquestionchatapi-zh-CN) 获取问题 ID。

   * 您必须拥有 BytePlus 账号或具备 `Live control > Edit` 权限的 IAM 用户。有关如何添加 IAM 用户的更多信息，请参见 [管理用户、组织和角色](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles-zh-CN)。


<span id="6825fb68"></span>
## HTTP 请求


* URL：`https://livesaas.byteplusapi.com/?Action=ListAnswerChatAPI&Version=2020-06-01`

* 方法：GET


<span id="d85f0706"></span>
## 请求参数

以下表格未包含所有通用请求参数。完整列表请参见 [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters-zh-CN#f1706967)。

<span id="e1a6bb09"></span>
### 查询


|名称 |数据类型 |是否必填 |示例值 |接口行为 |
|---|---|---|---|---|
|Action |String |是 |`ListAnswerChatAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。当前版本：`2020-06-01`。 |
|ActivityId |Long |是 |`17218312****` |直播间的活动 ID。您可以通过调用 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-CN) 获取该 ID。 |
|QuestionMsgIds |Long 数组 |是 |`[5941305,5941306]` |用于检索回复的问题 ID。您可以通过调用 [ListQuestionChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/listquestionchatapi-zh-CN) 获取该 ID。<br><br>该数组最多可包含 100 个问题 ID。 |
|PageNumber |Long |否 |`1` |返回的页码。默认值：`1`。 |
|PageSize |Long |否 |`100` |每页返回的结果数量。默认值：`100`。<br><br>取值范围：[1,1000]。 |
|OrderType |Integer |否 |`1` |指定按点赞数或创建时间排序回复。<br><br>默认值：`0`。<br><br>有效值：<br><br><br>* `0`：按创建时间倒序排序回复。每个问题将优先返回最新回复。<br><br>* `1`：按点赞数排序回复。每个问题将优先返回最受欢迎的回复。 |
|FilterPin |Integer |否 |`0` |指定返回的回复类型。<br><br>默认值：`0`。<br><br>有效值：<br><br><br>* `0`：全部回复。<br><br>* `1`：仅返回问答菜单中置顶的问题回复。<br><br>* `2`：仅返回问答菜单中未置顶的问题回复。 |


<span id="2eac1c31"></span>
## 返回调用结果


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|PageNumber |Long |`1` |返回的页码。 |
|PageSize |Long |`100` |每页返回的结果数量。 |
|TotalCount |Long |`3` |返回的回复总数。 |
|AnswerMsgMap |JSON Map |`-` |每个键为问题 ID，对应值为该问题的回复列表的映射。<br><br><br>* `"Key"`：Long。问题 ID。<br><br>* `"Value"`：[AnswerMsg](https://docs.byteplus.com/docs/byteplus-livesaas/listanswerchatapi-zh-CN#82034406) 数组。回复列表。 |


<span id="82034406"></span>
### AnswerMsg


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|AnswerMsgId |Long |`5941311` |回复 ID。 |
|UserNickName |String |`Viewer A` |回复该问题用户的昵称。 |
|UserExternalId |String |`12387404123****` |用户在第三方平台的唯一标识。仅当观众通过支持的方式登录时，该 ID 才会存在。您可以使用该 ID 在您的组织内识别观众，以便进行用户洞察和数据分析。<br><br>该 ID 会根据观众登录直播间的方式而变化。<br><br><br>* 自定义账号：在自定义登录过程中传入的`UserId`参数的值。更多信息，请参见[自定义认证登录](https://docs.byteplus.com/docs/byteplus-livesaas/docs-applying-advanced-viewing-restrictions-zh-CN)。<br><br>* 手机号：观众使用手机号注册 BytePlus Live 时生成的`passport_id`。<br><br>* OAuth 2.0：在您自有账号系统中对应用户 ID 的字段。<br><br>* 白名单：观众输入的白名单校验信息。 |
|CreateTime |Long |`1717148059` |回复发送时间，Unix 时间戳格式（秒）。 |
|Content |String |`回复 A` |回复的内容。 |
|LikeCount |Long |`20` |该回复的点赞数。 |
|IsPined |Integer |`0` |表示该回复是否置顶于问答菜单下的问题顶部。<br><br><br>* `0`：未置顶。<br><br>* `1`：已置顶。 |


<span id="e861fb28"></span>
## 示例

<span id="8057a437"></span>
### 请求示例

```JSON
GET https://livesaas.byteplusapi.com/?Action=ListAnswerChatAPI&Version=2020-06-01&ActivityId=17218312****&QuestionMsgIds=5941305&QuestionMsgIds=5941306&PageNumber=1&PageSize=100&OrderType=1&FilterPin=0
```


<span id="3d8f9cde"></span>
### 返回示例

```JSON
{
  "ResponseMetadata": {
    "RequestId": "201806041104200100100232280022D30",
    "Action": "ListAnswerChatAPI",
    "Version": "2020-06-01",
    "Service": "livesaas",
    "Region": "ap-singapore-1",
    "SystemTime": 1717593301
  },
    "Result": {
        "PageNumber": 1,
        "PageSize": 100,
        "TotalCount": 3,
        "AnswerMsgMap": {
            "5941305": [
                {
                    "AnswerMsgId": 5941311,
                    "UserNickName": "Viewer A",
                    "UserExternalId": "",
                    "CreateTime": 1717148059,
                    "Content": "Reply A",
                    "LikeCount": 20,
                    "IsPined": 0
                },
                {
                    "AnswerMsgId": 5941309,
                    "UserNickName": "Viewer B",
                    "UserExternalId": "",
                    "CreateTime": 1717145103,
                    "Content": "Reply B",
                    "LikeCount": 10,
                    "IsPined": 1
                }
            ],
            "5941306": [
                {
                    "AnswerMsgId": 5941308,
                    "UserNickName": "Viewer C",
                    "UserExternalId": "",
                    "CreateTime": 1717145064,
                    "Content": "Reply C",
                    "LikeCount": 15,
                    "IsPined": 0
                }
            ]
        }
    }
}
```


<span id="6ccfa3f6"></span>
## 错误码

有关通用错误码列表，请参见 [常见错误和状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes-zh-CN)。
