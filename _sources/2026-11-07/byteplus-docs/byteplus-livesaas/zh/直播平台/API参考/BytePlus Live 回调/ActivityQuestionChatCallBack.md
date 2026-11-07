---
title: "ActivityQuestionChatCallBack"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/activityquestionchatcallback-zh-CN"
---

当用户在问答菜单下发送问题时，BytePlus Live 会向你的自定义 URL 发送 POST 请求，并在请求体中传递问题数据。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">你需要先联系 BytePlus Live 销售代表，并提供自定义 URL 以接收回调。</div>


* <div data-tips="true" data-tips-type="tip">如果你的服务器在五秒内未响应，请求将会失败。随后 BytePlus Live 会以五秒为间隔重试两次请求。</div>



请求示例

```JSON
POST /xxxxx HTTP/1.1
Header1: ...
Header2: ...
...

{
 "ActivityId": "172183121234",
 "EventType": "ActivityQuestionChatCallBack",
 "CreateTime": "1716795991",
 "QuestionMsgId": "5941305",
 "UserNickName": "Viewer A",
 "UserExternalId": "123874041231234",
 "Content": "Question A",
 "Sign": "5ad620fab18b8c78ab90f277aea8c562"
}
```



|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|ActivityId |String |`172183121234` |直播间的活动 ID。 |
|EventType |String |`ActivityQuestionChatCallBack` |事件类型。 |
|CreateTime |String |`1716795991` |问题发送时间，Unix 时间戳格式。单位：秒。 |
|QuestionMsgId |String |`5941305` |问题 ID。 |
|UserNickName |String |`Viewer A` |发送问题用户的昵称。 |
|UserExternalId |String |`123874041231234` |用户在第三方平台的唯一标识。你可以使用该 ID 在你的组织内识别用户，以便进行洞察和数据分析。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">该参数仅在用户登录直播间时才会被赋值。仅昵称加入的用户无法获取该参数。</div><br> |
|Content |String |`Question A` |问题内容。 |
|Sign |String |`5ad620fab18b8c78ab90f277aea8c562` |用于校验的签名。<br><br>要计算`Sign`值，你需要完成以下步骤：<br><br><br>1. 按顺序拼接以下参数的值：`AccountSecret`、ActivityId、CreateTime、EventType、QuestionMsgId、UserExternalId 和 UserNickName。联系你的销售代表获取`AccountSecret`值。<br><br>2. 使用 MD5 算法（32 位小写）对拼接后的字符串进行加密。<br><br><br>例如，`AccountSecret`为`abc`，拼接字符串为`abc1721831212341716795991ActivityQuestionChatCallBack5941305123874041231234Viewer A`，最终得到的`Sign`值为`5ad620fab18b8c78ab90f277aea8c562`。 |
