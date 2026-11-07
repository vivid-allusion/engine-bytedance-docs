---
title: "ActivityAwardInfoCallBack"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/ActivityAwardInfoCallBack-zh-CN"
---

当进行实时抽奖时，BytePlus Live 会向你的自定义 URL 发送 POST 请求，并在请求体中传递如直播间 ID、奖品信息和获奖者信息等数据。

如果实时抽奖包含多个奖品，BytePlus Live 会针对每个奖品分别发送回调消息。每条回调最多可包含 2,000 名获奖者的信息。若某奖品的获奖者信息超过此限制，BytePlus Live 会发送多条回调消息。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">你需先联系 BytePlus Live 销售代表，并提供自定义 URL 以接收回调通知。</div>


* <div data-tips="true" data-tips-type="tip">若 BytePlus Live 的回调服务器在请求发送后五秒内未收到你的服务器的返回调用结果，则请求失败。BytePlus Live 会以五秒间隔再重试失败请求两次。</div>



请求示例

```JSON
POST /xxxxx HTTP/1.1
Header1: ...
Header2: ...
...
{
    "AccountID": "200000****",
    "ActivityID": "182573526550****",
    "ActivityName": "Live Room A",
    "AwardItemAmounts": "",
    "AwardItemId": "10****",
    "AwardItemNum": "",
    "AwardItemType": "2",
    "AwardName": "Prize A",
    "DeliveryMethod": "",
    "EventType": "ActivityAwardInfoCallBack",
    "RequestUuid": "ActivityAwardInfoCallBack-182572318444****",
    "Sign": "c7594afe578431086bf1c56eff54****",
    "Timestamp": "1741158904",
    "UserInfos": [
        {
            "ExternalID": "78989827691****",
            "Extra": "",
            "IsPriorityUser": "0",
            "NickName": "Audience A",
            "Telephone": "1803738****",
            "UserAccessIP": "fdbd:dc0********",
            "UserAgent": "Windows 10",
            "UserID": "182137188********"
        }
    ]
}
```



|参数 |类型 |接口行为 |
|---|---|---|
|AccountID |String |你的 BytePlus 账号的账号 ID。你可通过点击 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)右上角头像获取该 ID。 |
|ActivityID |String |直播间的活动 ID。 |
|EventType |String |回调通知的事件类型，固定值为 `ActivityAwardInfoCallBack`。 |
|Timestamp |String |回调请求发送时间，Unix 时间戳格式。单位：秒。 |
|Sign |String |用于校验的签名。<br><br>要获取 `Sign` 的值，你需完成以下步骤：<br><br><br>1. 按 `AccountSecretAccountIDEventTypeTimestamp` 格式拼接对应参数值。联系你的销售代表获取 `AccountSecret` 的值。<br><br>2. 将拼接后的字符串以 MD5（32 位小写）加密。<br><br><br>本示例中，假设 AccountSecret 的值为 abc。则拼接字符串为 abc30001234871823745212348678ActivityAwardInfoCallBack1739273121，Sign 的值为对应的 MD5 哈希。 |
|ActivityName |String |直播间名称。 |
|AwardItemId |String |奖品 ID。 |
|RequestUuid |String |回调请求的唯一标识符。 |
|AwardName |String |奖品名称。 |
|AwardItemType |String |奖品类型。有效值如下：<br><br><br>* `1`: 实物奖品<br><br>* `2`: 虚拟奖品<br><br>* `3`: 自定义奖品<br><br>* `4`: 代金券奖品 |
|DeliveryMethod |String |自定义奖品的分类。取值：<br><br><br>* `1`: 优惠券<br><br>* `2`: 积分<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">当<code>AwardItemType</code>设置为3时，该参数生效。</div><br> |
|AwardItemNum |String |积分奖品的批次号。长度范围为 1~256 个字符。你可通过该批次号识别企业积分，并分发给观众。 |
|AwardItemAmounts |String |每位获奖观众获得的积分数量。取值范围为 [0,99999]。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">当<code>AwardItemType</code>设置为3且<code>DeliveryMethod</code>设置为2时，该参数生效。</div><br> |
|UserInfos |Array of[UserAwardInfo](https://docs.byteplus.com/docs/byteplus-livesaas/ActivityAwardInfoCallBack-zh-CN#e727d716) |获奖者信息。 |


<span id="e727d716"></span>
### UserAwardInfo


|Name |数据类型 |接口行为 |
|---|---|---|
|UserId |String |用户 ID。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">如果用户未通过昵称或其他方式登录到直播间，则用户ID为<code>0</code>。</div><br> |
|ExternalID |String |用户在第三方平台的唯一标识。你可通过该 ID 在你的组织内识别用户，实现用户洞察和数据分析。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">该参数仅针对通过集成身份系统认证的用户填写，不针对仅通过昵称登录的嘉宾用户填写。</div><br> |
|Extra |String |该参数为额外参数，对应观看页 URL 中的 extra 参数。例如，`https://live.byteplus.com/6688/322****?extra=xxx`。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">使用iOS 观播 SDK或Android 观播 SDK时，该参数不会填写。</div><br> |
|NickName |String |用户昵称。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">该参数仅在用户登录到直播间时填写。</div><br> |
|UserAccessIP |String |用户的 IP 地址。 |
|UserAgent |String |用户使用的设备类型。 |
|Telephone |String |用户登录直播间时使用的手机号。 |
|IsPriorityUser |String |用户是否优先中奖。有效值如下：<br><br><br>* `0`：否<br><br>* `1`：是 |
