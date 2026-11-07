---
title: "ActivityStatusModifyCallBack"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/activitystatusmodifycallback-zh-CN"
---

当直播间状态发生变化时，BytePlus Live 会向你的自定义 URL 发送 GET 请求，并在查询字符串中传递活动 ID 和新的状态。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">你必须先联系你的 BytePlus Live 销售代表，并提供一个自定义 URL 以接收回调。</div>


* <div data-tips="true" data-tips-type="tip">如果 BytePlus Live 的回调服务器在请求发送后五秒内未收到你服务器的返回调用结果，则该请求失败。BytePlus Live 会以五秒间隔最多重试失败请求两次。</div>



请求示例

```Plain
http://abc.com/test.do?ActivityID=123&EventType=ActivityStatusModifyCallBack&Status=1&Timestamp=1582518318&Sign=xxxx
```



|参数 |数据类型 |接口行为 |
|---|---|---|
|ActivityID |String |直播间的活动 ID。 |
|EventType |String |ActivityStatusModifyCallBack |
|Status |String |直播间的状态。<br><br>有效值：<br><br><br>* `1`：Live<br><br>* `2`：预告<br><br>* `3`：回放<br><br>* `4`：结束 |
|Timestamp |String |回调请求发送的时间，采用 Unix 时间戳格式。单位：秒。 |
|Sign |String |用于身份验证的加密字符串。<br><br>要获取 `Sign` 值，你必须完成以下步骤：<br><br><br>1. 按 `AccountSecretActivityIDEventTypeStatusTimestamp` 格式拼接字符串。联系你的销售代表获取 `AccountSecret` 值。<br><br>2. 对拼接后的字符串生成 32 位小写 MD5 哈希值。<br><br><br>在本示例中，假设 `AccountSecret` 的值为 `abc`。拼接后的字符串为 `abc123ActivityStatusModifyCallBack11582518318`，最终生成的 `Sign` 值为 `3d5fc13702c89c3c34c811ba8ac8fbbc`。 |
