---
title: "WithdrawAward"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/WithdrawAward-zh-CN"
---

调用 `WithdrawAward`，从直播间撤回实时抽奖。注意，已撤回的抽奖无法再次发送或更新。

<span id="Requirements"></span>
## 要求


* 限速：每个账号每秒最多 10 次请求

* 前提条件：需拥有 BytePlus 账号，或具备 **Live control** \> **Edit** 权限的 IAM 用户。如需了解如何添加 IAM 用户，请参见 [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。


<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://livesaas.byteplusapi.com/?Action=WithdrawAward&Version=2023\-08\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

以下表格未包含所有通用请求参数。完整列表请参见 [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### Query


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`WithdrawAward` |API 操作。 |
|Version |String |是 |`2023-08-01` |该 API 操作的版本。当前版本：`2023-08-01`。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|ActivityId |Integer |是 |17218346\*\*\*\* |直播间的活动 ID。可通过调用 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi) 获取该 ID。 |
|Id |Integer |是 |36576 |需撤回的实时抽奖 ID。可通过调用 ListAwardConfigs API 获取该 ID。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">撤回实时抽奖时，请确保抽奖状态为“进行中”或“已完成”。当 <code>Status</code> 参数由 <code>ListAwardConfigs</code> API 返回值为 <code>2</code> 或 <code>4</code> 时，可调用此 API 撤回实时抽奖。</div><br> |


<span id="Response parameters"></span>
## 返回调用结果参数


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Status |Boolean |`true` |抽奖是否成功撤回。成功时返回 `true`。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```JSON
POST https://livesaas.byteplusapi.com/?Action=WithdrawAward&Version=2023-08-01
{
    "ActivityId": 17218346****,
    "Id": 36576
}
```


<span id="Sample response"></span>
### 返回示例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "WithdrawAward",
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

常见错误码列表请参见 [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
