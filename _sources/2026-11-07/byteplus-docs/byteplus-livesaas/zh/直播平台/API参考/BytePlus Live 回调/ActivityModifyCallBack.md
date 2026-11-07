---
title: "ActivityModifyCallBack"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/activitymodifycallBack-zh-CN"
---

当直播间被创建或删除时，BytePlus Live 会向你的自定义 URL 发送 GET 请求，并在查询字符串中传递活动 ID 以及对直播间执行的操作。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">你必须先联系 BytePlus Live 销售代表，并提供自定义 URL 以接收回调。</div>


* <div data-tips="true" data-tips-type="tip">如果你的服务器在五秒内未响应，请求将失败。随后 BytePlus Live 会以五秒为间隔重试两次请求。</div>



请求示例

```Plain
http://abc.com/test.do?ActivityID=123&EventType=ActivityModifyCallBack&Type=1&Timestamp=1582518318&Sign=xxxx
```



|参数 |数据类型 |接口行为 |
|---|---|---|
|ActivityID |String |直播间的活动 ID。 |
|EventType |String |ActivityModifyCallBack |
|Timestamp |String |回调请求发送的时间，使用以秒为单位的 Unix 时间戳表示。 |
|Type |String |表示直播间是被创建还是被删除。<br><br>有效值：<br><br><br>* `1`：创建<br><br>* `2`：删除 |
|Sign |String |用于认证的加密字符串。<br><br>要获取 `Sign` 值，你必须完成以下步骤：<br><br><br>1. 以 `AccountSecretActivityIDEventTypeStatusTimestamp` 格式拼接字符串。联系你的销售代表以获取 `AccountSecret` 值。<br><br>2. 对拼接后的字符串生成 32 位小写 MD5 哈希值。<br><br><br>在本例中，假设 `AccountSecret` 的值为 `abc`。那么拼接后的字符串为 `abc123ActivityModifyCallBack11582518318`，最终生成的 `Sign` 值为 `3d5fc13702c89c3c34c811ba8ac8fbbc`。 |
