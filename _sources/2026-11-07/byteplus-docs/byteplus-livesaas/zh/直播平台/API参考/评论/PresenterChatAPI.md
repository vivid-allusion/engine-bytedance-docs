---
title: "PresenterChatAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-presenterchatapi-zh-CN"
---

调用此 API 以主播身份在直播间发送评论。

<span id="459d9053"></span>
## 要求

配额：每个账号每分钟最多 120 次查询

<span id="b2acb75e"></span>
## HTTP 请求


* URL：`https://livesaas.byteplusapi.com/?Action=PresenterChatAPI&Version=2020-06-01`

* 方法：POST


<span id="5ad3f4d9"></span>
## 请求参数

以下表格未包含所有通用请求参数。完整列表请参见 [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters-zh-CN#f1706967)。

<span id="91ba5468"></span>
### 查询


|名称 |数据类型 |是否必填 |示例值 |接口行为 |
|---|---|---|---|---|
|Action |String |是 |`PresenterChatAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。当前版本：`2020-06-01`。 |


<span id="Body parameters"></span>
### 请求体


|名称 |数据类型 |是否必填 |示例值 |接口行为 |
|---|---|---|---|---|
|ActivityId |Long |是 |`17218346****` |直播间的活动 ID。可通过调用 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-CN) 获取该 ID。 |
|Comment |String |是 |`Hello` |要发送的评论。 |


<span id="e21e2025"></span>
## 返回调用结果参数


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|status |Boolean |`true` |表示评论是否发送成功。<br><br><br>* `true`：成功。<br><br>* `false`：失败。 |


<span id="b574ac21"></span>
## 示例

<span id="3ca901e7"></span>
### 请求示例

```JSON
POST https://livesaas.byteplusapi.com/?Action=PresenterChatAPI&Version=2020-06-01
{
    "ActivityId": 17218346****,
    "Comment": "Hello" 
}
```


<span id="Sample response"></span>
### 返回示例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "PresenterChatAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1656067132
    },
    "Result":{
        "status": true
    }
}
```


<span id="6d8a9dad"></span>
## 错误码

通用错误码列表请参见 [常见错误和状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes-zh-CN)。
