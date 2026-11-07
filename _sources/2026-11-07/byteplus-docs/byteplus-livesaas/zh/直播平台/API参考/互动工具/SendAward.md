---
title: "SendAward"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/SendAward-zh-CN"
---

调用`SendAward`以在直播间启动实时抽奖。

<span id="Requirements"></span>
## 要求


* 频率限制：每个账号每秒最多 10 次请求

* 前提条件：需要 BytePlus 账号，或拥有**直播控制** \> **编辑**权限的 IAM 用户。关于如何添加 IAM 用户的更多信息，请参见[管理用户、组织和角色](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。


<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://livesaas.byteplusapi.com/?Action=SendAward&Version=2023\-08\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

下表未包含所有通用请求参数。完整列表请参见[通用请求参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### 查询参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`SendAward` |API 操作。 |
|Version |String |是 |`2023-08-01` |此 API 操作的版本。当前版本：`2023-08-01`。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|ActivityId |Integer |是 |17218346\*\*\*\* |直播间的活动 ID。可通过调用[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi)获取该 ID。 |
|Id |Integer |是 |`36***` |实时抽奖 ID。可通过调用`ListAwardConfigs` API 获取该 ID。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">启动实时抽奖时，请确保该抽奖尚未被启动。如果<code>Status</code> 参数由<code>ListAwardConfigs</code> API 返回的值为<code>1</code>，则可调用本 API 启动实时抽奖。</div><br> |


<span id="Response parameters"></span>
## 返回调用结果参数


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Status |Boolean |`true` |表示抽奖是否启动成功。若启动成功，则返回`true`。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```JSON
POST https://livesaas.byteplusapi.com/?Action=SendAward&Version=2023-08-01
{
    "ActivityId": 17218346****,
    "Id": 36***
}
```


<span id="Sample response"></span>
### 返回示例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "SendAward",
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

常见错误码列表请参见[常见错误和状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
