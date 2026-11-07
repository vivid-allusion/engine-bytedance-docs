---
title: "ExplainProduct"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/explainproduct-zh-CN"
---

将商品置顶于菜单，并在观看页以悬浮窗形式展示，或将商品恢复至菜单下的原始位置，并从观看页的悬浮窗展示中移除。

<span id="Requirements"></span>
## 要求

限流：每个账号每分钟最多 120 次请求

<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://livesaas.byteplusapi.com/?Action=ExplainProduct&Version=2023\-08\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

以下表格未包含所有通用请求参数。完整参数列表请参见[通用请求参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### Query


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`ExplainProduct` |API 操作。 |
|Version |String |是 |`2023-08-01` |此 API 操作的版本。当前版本：`2023-08-01`。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|ActivityId |Long |是 |`17791682871580` |直播间的活动 ID。你可以调用[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi)，在返回调用结果参数`Id`中获取该 ID。 |
|ExplainStatus |Integer |是 |`1` |对商品执行的操作。有效值：<br><br><br>* `1`：将商品置顶于菜单，并在观看页以悬浮窗形式展示。<br><br>* `2`：将商品恢复至菜单下的原始位置，并从观看页的悬浮窗展示中移除。 |
|ProductId |Long |否 |`492046` |商品卡片的 ID。你可以调用[GetActivityProductAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getactivityproductapi)，在返回调用结果参数`Id`中获取该 ID。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">请传入<code>ProductId</code>或<code>ExternalProductId</code>。若同时传入，则仅<code>ProductId</code>生效。</div><br> |
|ExternalProductId |String |否 |`your_product_id_12345` |商品卡片的外部商品 ID，在每个菜单中唯一。你可以通过调用[GetActivityProductAPI](https://docs.byteplus.com/zh-CN/docs/byteplus-livesaas/docs-getactivityproductapi)获取该 ID。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">请传入<code>ProductId</code>或<code>ExternalProductId</code>。若同时传入，则仅<code>ProductId</code>生效。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">如果你的直播间中有多个商品使用该 ID，则操作会针对商品卡片左侧菜单下的商品执行。</div><br> |


<span id="Response parameters"></span>
## 返回调用结果参数


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Status |Boolean |`true` |表示操作是否成功执行。有效值：<br><br><br>* `true`：成功。<br><br>* `false`：失败。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://livesaas.byteplusapi.com/?Action=ExplainProduct&Version=2023-08-01
{
    "ActivityId": 17791****71580,
    "ProductId": 49**46,
    "ExternalProductId": "your_product_id_12345",
    "ExplainStatus": 1
}
```


<span id="Sample response"></span>
### 返回调用结果示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ExplainProduct",
        "Version": "2023-08-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1697446406
    },
    "Result": {
        "Status": true
    }
}
```


<span id="Error codes"></span>
## 错误码

常见错误码列表请参见[常见错误及状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
