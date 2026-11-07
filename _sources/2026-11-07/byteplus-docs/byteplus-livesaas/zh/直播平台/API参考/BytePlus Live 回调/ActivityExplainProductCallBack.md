---
title: "ActivityExplainProductCallBack"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/activityexplainproductcallBack-zh-CN"
---

当你的直播间中的商品处于以下任意一种情况时，BytePlus Live 会向你的自定义 URL 发送 POST 请求，并在请求体中传递信息，例如直播间的活动 ID 和商品信息：


* 商品被置顶于菜单顶部，并在观看页以悬浮窗形式展示。

* 商品恢复至菜单下方的原始位置，并不再在观看页以悬浮窗形式展示。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">若未开启多商品置顶功能，请使用此回调。关于该功能的更多信息，请参见<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream-zh-CN">管理商品卡片</a>。</div>


* <div data-tips="true" data-tips-type="tip">你需先联系 BytePlus Live 销售代表，并提供自定义 URL 以接收回调通知。</div>


* <div data-tips="true" data-tips-type="tip">若 BytePlus Live 的回调服务器在请求发送后五秒内未收到你的服务器的返回调用结果，则该请求视为失败。BytePlus Live 会对失败的请求额外重试两次，每次间隔五秒。</div>



请求示例

```JSON
POST /xxxxx HTTP/1.1
Header1: ...
Header2: ...
...
{
     "AccountId": "3000123487",
     "ActivityId": "1823745212348678",
     "CancelExplainExternalProductId": "120056",
     "CancelExplainProductId": "500067",
     "CancelExplainProductName": "Eggs",
     "EventType": "ActivityExplainProductCallBack",
     "ExplainExternalProductId": "780012",
     "ExplainProductId": "500028",
     "ExplainProductName": "Cake",
     "RequestUuid": "ActivityExplainProductCallBack - 1823712342538389",
     "Sign": "e11de95caf53091963fc92092dce9450",
     "Timestamp": "1739273121"
}
```



|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|AccountId |String |`3000123487` |你的 BytePlus 账号的账号 ID。你可通过点击 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)右上角的个人头像获取该 ID。 |
|ActivityId |String |`1823745212348678` |直播间的活动 ID。 |
|EventType |String |`ActivityExplainProductCallBack` |回调事件类型。该值始终为`ActivityExplainProductCallBack`。 |
|Timestamp |String |`1739273121` |回调请求发送时间，Unix 时间戳格式。单位：秒。 |
|Sign |String |`e11de95caf53091963fc92092dce9450` |用于校验的签名。<br><br>要获取`Sign`的值，你需完成以下步骤：<br><br><br>1. 按顺序拼接 AccountSecret、AccountId、ActivityId、EventType 和 Timestamp 参数的值。联系你的销售代表获取`AccountSecret`值。<br><br>2. 对拼接后的字符串生成 32 位小写 MD5 哈希值。<br><br><br>本示例假设`AccountSecret`值为`abc`。则拼接字符串为`abc30001234871823745212348678ActivityExplainProductCallBack1739273121`，`Sign`值为`e11de95caf53091963fc92092dce9450`。 |
|ExplainProductName |String |`Cake` |被置顶于菜单顶部并在观看页以悬浮窗形式展示的商品名称。 |
|ExplainProductId |String |`500028` |被置顶于菜单顶部并在观看页以悬浮窗形式展示的商品（商品卡片）ID。 |
|ExplainExternalProductId |String |`780012` |被置顶于菜单顶部并在观看页以悬浮窗形式展示的商品外部 ID。 |
|CancelExplainProductName |String |`Eggs` |恢复至菜单下方原始位置且不再在观看页以悬浮窗形式展示的商品名称。 |
|CancelExplainProductId |String |`500067` |恢复至菜单下方原始位置且不再在观看页以悬浮窗形式展示的商品（商品卡片）ID。 |
|CancelExplainExternalProductId |String |`120056` |恢复至菜单下方原始位置且不再在观看页以悬浮窗形式展示的商品外部 ID。 |
|RequestUuid |String |`ActivityExplainProductCallBack - 1823712342538389` |回调请求的唯一标识符。 |
