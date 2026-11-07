---
title: "ActivityTaskAwardInfoCallBack"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/ActivityTaskAwardInfoCallBack-zh-CN"
---

当用户参与基于观看时长的抽奖并中奖时，BytePlus Live 会向您的自定义 URL 发送 POST 请求，并在请求体中传递直播间 ID、奖品信息和中奖者信息。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">您需先联系您的 BytePlus Live 销售代表，并提供自定义 URL 以接收回调通知。</div>


* <div data-tips="true" data-tips-type="tip">若 BytePlus Live 的回调服务器在请求发送后五秒内未收到您的服务器的返回调用结果，则该请求失败。BytePlus Live 会以五秒间隔再次重试失败请求两次。</div>


* <div data-tips="true" data-tips-type="tip">每次回调最多可包含 1,000 名中奖者的信息。若某奖品的中奖者信息超出该限制，BytePlus Live 会发送多条回调消息。</div>



请求示例

```JSON
POST /xxxxx HTTP/1.1
Header1: ...
Header2: ...
...
{
    "AccountId": "200000****",
    "ActivityId": "185304015484****",
    "ActivityName": "Live room A",
    "AwardItemAmounts": "99999",
    "AwardItemId": "17012",
    "AwardItemNum": "1323421123",
    "AwardItemType": "3",
    "AwardName": "Prize A",
    "DeliveryMethod": "2",
    "EventType": "ActivityTaskAwardInfoCallBack",
    "RequestUuid": "ActivityTaskAwardInfoCallBack-1853040247559201",
    "Sign": "5b81b108bee1e6aba81412a2e8802a3a",
    "Timestamp": "1774943600",
    "UserInfos": [
        {
            "ExternalID": "7613760946837832760",
            "Extra": "",
            "IsPriorityUser": "",
            "NickName": "User A",
            "Telephone": "185****3186",
            "UserAccessIP": "AwardItemAmounts",
            "UserAgent": "Intel Mac OS X 10_15_7",
            "UserID": "185304024682****"
        }
    ]
}
```



|参数 |类型 |接口行为 |
|---|---|---|
|AccountID |String |您的 BytePlus 账号的账号 ID。您可通过点击 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)右上角头像获取该 ID。 |
|ActivityId |String |直播间的活动 ID。 |
|ActivityName |String |直播间名称。 |
|AwardItemAmounts |String |每位中奖观众获得的积分数量。取值范围为 [0,99999]。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">当<code>AwardItemType</code>设置为3且<code>DeliveryMethod</code>设置为2时，此参数生效。</div><br> |
|AwardItemId |String |奖品 ID。 |
|AwardItemNum |String |积分奖品的批次号。长度范围为 1 到 256 个字符。您可通过该批次号识别企业积分，并将其分发给观众。 |
|AwardItemType |String |奖品类型。有效取值如下：<br><br><br>* `1`: 实物奖品<br><br>* `2`: 虚拟奖品<br><br>* `3`: 自定义奖品<br><br>* `4`: 代金券奖品 |
|AwardName |String |奖品名称。 |
|DeliveryMethod |String |自定义奖品的类型。取值：<br><br><br>* `1`: 优惠券<br><br>* `2`: 积分<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">当<code>AwardItemType</code>设置为3时，此参数生效。</div><br> |
|EventType |String |回调通知的事件类型，固定值为 `ActivityTaskAwardInfoCallBack`。 |
|RequestUuid |String |回调请求的唯一标识符。 |
|Sign |String |用于校验的签名。<br><br>要获取 `Sign` 的值，需完成以下步骤：<br><br><br>1. 按 `AccountSecretAccountIdActivityIdEventTypeTimestamp` 格式拼接对应参数值。联系您的销售代表获取 `AccountSecret` 的值。<br><br>2. 将拼接后的字符串以 MD5（32 位小写）加密。<br><br><br>本示例假设 AccountSecret 的值为 abc。拼接后的字符串为 abc30001234871823745212348678ActivityAwardInfoCallBack1739273121，Sign 的值即为对应的 MD5 哈希值。 |
|Timestamp |String |回调请求发送时间，Unix 时间戳格式。单位：秒。 |
|UserInfos |Array of[UserInfos](https://docs.byteplus.com/docs/byteplus-livesaas/ActivityTaskAwardInfoCallBack-zh-CN#fd57e72d) |中奖者信息。 |


<span id="fd57e72d"></span>
## UserInfos


|Name |数据类型 |接口行为 |
|---|---|---|
|UserID |String |用户 ID。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">对于未登录加入直播间的匿名用户，用户ID为<code>0</code>。</div><br> |
|ExternalID |String |用户在第三方平台的唯一标识。您可通过该 ID 在您的组织内识别用户，实现用户洞察和数据分析。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">此参数仅为通过集成身份系统认证的用户填充，对于仅提供昵称登录的嘉宾用户不会填充。</div><br> |
|Extra |String |您的额外参数，对应观看页地址中的 extra 参数。例如，`https://live.byteplus.com/6688/322****?extra=xxx`。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">使用iOS 观播 SDK或Android 观播 SDK时，此参数不会被填充。</div><br> |
|IsPriorityUser |String |用户是否优先中奖。有效取值如下：<br><br><br>* `0`: 否<br><br>* `1`: 是 |
|NickName |String |用户昵称。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">只有用户登录直播间时，此参数才有值。</div><br> |
|UserAccessIP |String |用户的 IP 地址。 |
|UserAgent |String |用户所用设备类型。 |
|Telephone |String |用于预约直播流的手机号。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">使用iOS 观播 SDK或Android 观播 SDK时，此参数不会被填充。</div><br> |
