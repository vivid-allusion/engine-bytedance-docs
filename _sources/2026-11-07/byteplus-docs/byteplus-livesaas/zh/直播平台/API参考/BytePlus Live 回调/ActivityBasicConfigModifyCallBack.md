---
title: "ActivityBasicConfigModifyCallBack"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/activitybasicconfigmodifycallback-zh-CN"
---

当直播间的基础配置发生变更时，BytePlus Live 会向你的自定义 URL 发送 POST 请求，并在请求体中传递活动 ID 和基础配置。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">你需先联系 BytePlus Live 销售代表，并提供自定义 URL 以接收回调。</div>


* <div data-tips="true" data-tips-type="tip">若 BytePlus Live 的回调服务器在请求发送后五秒内未收到你的服务器返回调用结果，则该请求视为失败。BytePlus Live 会对失败的请求额外重试两次，每次重试间隔五秒。</div>



请求示例

```JSON
POST /xxxxx HTTP/1.1
Header1: ...
Header2: ...
...

{
 "ActivityID": "123",
 "EventType": "ActivityBasicConfigModifyCallBack",
 "Timestamp": "1582518318",
 "Sign": "xxxx",
 "Name": "Live Room A",
 "Announcement": "Live Room A",
 "CoverImage": "//gjr78lqtd0-image.image",
 "ViewUrl": "https://live.byteplus.com/7420/1234",
 "LiveTime": "1583070536"
}
```



|参数 |数据类型 |接口行为 |
|---|---|---|
|ActivityID |String |直播间的活动 ID。 |
|EventType |String |ActivityBasicConfigModifyCallBack |
|Timestamp |String |回调请求的时间戳，Unix 格式。单位：秒。 |
|Sign |String |用于鉴权的加密字符串。<br><br>要获取`Sign`值，你需完成以下步骤：<br><br><br>1. 按`AccountSecretActivityIDAnnouncementCoverImageEventTypeLiveTimeNameTimestampViewUrl`格式拼接字符串。联系你的销售代表获取`AccountSecret`值。<br><br>2. 对拼接后的字符串生成 32 位小写 MD5 哈希值。<br><br><br>本示例中，假设`AccountSecret`值为`abc`。拼接后的字符串为`abc123Live Room A//gjr78lqtd0-image.imageActivityBasicConfigModifyCallBack1583070536Live Room A1582518318 https://live.byteplus.com/7420/1234`，生成的`Sign`值为`85c1ba868bf4e30b6055ccfbbdd7bc3a`。 |
|Name |String |直播间名称。 |
|Announcement |String |直播间公告。 |
|CoverImage |String |直播间封面图的 URL。 |
|ViewUrl |String |直播间观看页的 URL。 |
|LiveTime |String |直播流开始时间，Unix 时间戳格式。单位：秒。<br><br>该时间可能并非直播流实际开始时间。 |
