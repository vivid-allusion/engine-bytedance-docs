---
title: "CheckinStatusModifyCallback"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/CheckinStatusModifyCallback-zh-CN"
---

当发生签到事件（如签到创建、删除、发送或截止时间到达）时，BytePlus Live 会向你的自定义 URL 发送 POST 请求，并在请求体中传递直播间 ID 和已更新的签到状态。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">你必须先联系你的 BytePlus Live 销售代表，并提供自定义 URL 以接收回调通知。</div>


* <div data-tips="true" data-tips-type="tip">如果 BytePlus Live 的回调服务器在请求发送后五秒内未收到你的服务器的返回调用结果，则该请求会失败。BytePlus Live 会以五秒间隔再次重试失败的请求两次。</div>



请求示例

```JSON
POST /xxxxx HTTP/1.1
Header1: ...
Header2: ...
...
{
    "ActivityId": "1840847565136997",
    "CheckInId": "checkIn1853040247525505",
    "EventType": "CheckinStatusModifyCallback",
    "RequestUuid": "CheckinStatusModifyCallback-1853040247354881",
    "Sign": "c26ca0fe5c09f56222d22e9525bd3739",
    "Status": "Init",
    "SubAccountName": "admin@example.com",
    "Timestamp": "1774933967"
}
```



|名称 |数据类型 |接口行为 |
|---|---|---|
|ActivityId |String |直播间的活动 ID。 |
|CheckInId |String |签到 ID。 |
|EventType |String |回调通知的事件类型，固定值为`CheckinStatusModifyCallback`。 |
|RequestUuid |String |回调请求的唯一标识符。 |
|Sign |String |用于校验的签名。<br><br>要获取`Sign`的值，你需要完成以下步骤：<br><br><br>1. 按`AccountSecretActivityIdCheckInIdEventTypeStatusTimestamp`格式拼接字符串。联系你的销售代表获取`AccountSecret`的值。<br><br>2. 使用 MD5（32 位小写）对拼接后的字符串进行哈希。 |
|Status |String |签到状态。有效值如下：<br><br><br>* `Init`：已创建<br><br>* `Export`：已发送<br><br>* `Deadline`：已结束<br><br>* `Delete`：已删除<br><br>* `Retract`：已撤回 |
|SubAccountName |String |用于创建直播间的账号。参数值`admin@bytedance.com`表示该直播间由 BytePlus 账号创建。 |
|Timestamp |String |回调请求发送的时间，采用 Unix 时间戳格式。单位：秒。 |
