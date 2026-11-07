---
title: "ActivityAutoReplayCallBack"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/activityautoreplaycallback-zh-CN"
---

当视频作为直播间的回放生成时，BytePlus Live 会向你的自定义 URL 发送 POST 请求，并在请求体中传递活动 ID 和视频 ID。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">你必须先联系你的 BytePlus Live 销售代表，并提供一个自定义 URL 以接收回调。</div>


* <div data-tips="true" data-tips-type="tip">如果 BytePlus Live 的回调服务器在五秒内未收到你的服务器的返回调用结果，则请求超时。BytePlus Live 会以五秒间隔再次重试失败的请求两次。</div>



请求示例

```JSON
POST /xxxxx HTTP/1.1
Header1: ...
Header2: ...
...

{
 "ActivityID": "123",
 "EventType": "ActivityAutoReplayCallBack",
 "Sign": "xxxx",
 "Timestamp": "1582518318",
 "LiveStartTime": "1751520600",
 "LiveEndTime": "1751526000",
 "Vid": "v0c251g7007abc1"
}
```



|参数 |数据类型 |接口行为 |
|---|---|---|
|ActivityID |String |直播间的活动 ID。 |
|EventType |String |ActivityAutoReplayCallBack |
|Vid |String |生成视频的 ID。 |
|Timestamp |String |回调请求发送的时间，Unix 时间戳格式。单位：秒。 |
|LiveStartTime |String |对应回放视频的直播流开始时间，Unix 时间戳格式。单位：秒。<br><br>例如，若直播流开始于 2025\-07\-03 13:30:00，结束于 2025\-07\-03 15:00:00，则该参数的值为`1751520600`。 |
|LiveEndTime |String |对应回放视频的直播流结束时间，Unix 时间戳格式。单位：秒。<br><br>例如，若直播流开始于 2025\-07\-03 13:30:00，结束于 2025\-07\-03 15:00:00，则该参数的值为`1751526000`。 |
|Sign |String |用于认证的加密字符串。<br><br>要获取`Sign`值，你必须完成以下步骤：<br><br><br>1. 将`AccountSecret`、`ActivityID`、`Timestamp` 和 `Vid` 的值拼接为一个字符串。联系你的销售代表以获取 AccountSecret 的值。<br><br>2. 使用 MD5 算法（32 位小写）对拼接字符串进行加密。<br><br><br>例如，若`AccountSecret`为 abc，拼接字符串为`abc1231582518318v0c251g7007abc1`，最终得到的`Sign`值为`884c08f1458e39888fb9ba4f51406c7a`。 |
