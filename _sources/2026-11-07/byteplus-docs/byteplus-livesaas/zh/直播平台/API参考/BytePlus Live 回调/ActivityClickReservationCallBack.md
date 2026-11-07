---
title: "ActivityClickReservationCallBack"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/activityclickreservationcallBack-zh-CN"
---

当用户在观看页点击**预约**以预约直播流时，BytePlus Live 会向你的自定义 URL 发送 POST 请求，并在请求体中传递用户信息和直播间信息。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">你必须先联系你的 BytePlus Live 销售代表，并提供一个自定义 URL 用于接收回调通知。</div>


* <div data-tips="true" data-tips-type="tip">如果 BytePlus Live 的回调服务器在请求发送后五秒内未收到你的服务器的返回调用结果，则请求失败。BytePlus Live 会以五秒间隔再次重试失败的请求两次。</div>



请求示例

```JSON
POST /xxxxx HTTP/1.1
Header1: ...
Header2: ...
...
{
     "AccountId": "200****914",
     "ActivityId": "1721****1234",
     "EventType": "ActivityClickReservationCallBack",
     "LiveTime": "1721099280",
     "ActivityName": "Live room A",
     "RequestUuid": "ActivityClickReservationCallBack-180469199****475",
     "ViewUrl": "https://live.byteplus.com/6688/322****",
     "Timestamp": "1721099426",
     "Sign": "b96c2ac3d6aed7557a****8bec3374fa",
     "UserInfo":{
        "ExternalId": "16057****",
        "Extra": "",
        "NickName": "Viewer A",
        "ReservationTel": "150****1345",
        "UserAccessIP": "43.*.*.143",
        "UserAgent": "Intel Mac OS X 10_15_7",
        "UserId": "17386867****4142"
                }
}
```



|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|AccountId |String |`200****914` |你的 BytePlus 账号的 ID。你可以通过点击 BytePlus Live 控制台右上角的个人头像来查看该 ID。 |
|ActivityId |String |`1721****1234` |直播间的活动 ID。 |
|EventType |String |`ActivityClickReservationCallBack` |事件类型。 |
|Timestamp |String |`1721099426` |发送回调请求的时间，Unix 时间戳格式。单位：秒。 |
|Sign |String |`b96c2ac3d6aed7557a****8bec3374fa` |用于校验的签名。<br><br>要获取`Sign`的值，你必须完成以下步骤：<br><br><br>1. 按如下顺序拼接所需值：AccountSecret、AccountId、ActivityId、EventType 和 Timestamp。联系你的销售代表获取 AccountSecret 的值。<br><br>2. 对拼接后的字符串生成 32 位小写 MD5 哈希值。<br><br><br>在本示例中，假设`AccountSecret`的值为`abc`。拼接后的字符串为`abc200****9141721****1234ActivityClickReservationCallBack1721099426`，`Sign`的值为`b96c2ac3d6aed7557a****8bec3374fa`。 |
|ActivityName |String |`直播间 A` |直播间名称。 |
|ViewUrl |String |`https://live.byteplus.com/6688/322****` |直播间观看页的 URL。 |
|LiveTime |String |`1721099426` |直播流计划开始时间，Unix 时间戳格式。单位：秒。 |
|RequestUuid |String |`ActivityClickReservationCallBack-180469199****475` |回调请求的唯一标识符。 |
|UserInfo |[UserReservationInfo](https://docs.byteplus.com/docs/byteplus-livesaas/activityclickreservationcallBack-zh-CN#30b07c7a) |`-` |在观看页点击**预约**以预约直播流的用户信息。 |


<span id="30b07c7a"></span>
### UserReservationInfo


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|UserId |String |`17386867****4142` |用户 ID。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">如果用户未通过输入昵称或其他方式登录直播间，则用户 ID 为<code>0</code>。</div><br> |
|ExternalId |String |`16057****` |用户在第三方平台上的唯一标识。你可以使用该 ID 在你的组织内识别用户，以便进行用户洞察和数据分析。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">该参数仅针对通过集成身份系统认证的用户填写，不针对仅通过昵称登录的嘉宾用户。</div><br> |
|Extra |String |`abc` |你的额外参数，对应观看页地址中的 extra 参数。例如，`https://live.byteplus.com/6688/322****?extra=xxx`。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">使用 iOS 观播 SDK 或 Android 时，该参数不会填写。</div><br> |
|NickName |String |`观众 A` |用户昵称。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">该参数仅在用户登录直播间时才有值。</div><br> |
|UserAccessIP |String |`43.*.*.143` |用户的 IP 地址。 |
|UserAgent |String |`Intel Mac OS X 10_15_7` |用户所使用的设备类型。 |
|ReservationTel |String |`150****1345` |用于预约直播流的手机号。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">在使用 iOS 观播 SDK 或 Android 观播 SDK 时，该参数不会被填充。</div><br> |
