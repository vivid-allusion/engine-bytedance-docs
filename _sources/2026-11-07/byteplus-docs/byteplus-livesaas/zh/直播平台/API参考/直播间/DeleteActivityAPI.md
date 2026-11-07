---
title: "DeleteActivityAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-deleteactivityapi-zh-CN"
---

删除指定的直播间。

<span id="requirement"></span>
## 要求

配额：每个账号每分钟最多 120 次查询

<span id="http-request"></span>
## HTTP 请求


* URL: `https://livesaas.byteplusapi.com/?Action=DeleteActivityAPI&Version=2020-06-01`

* 方法：POST


<span id="request-parameters"></span>
## 请求参数

以下表格未包含所有共享请求参数。完整列表请参见 [通用参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters-zh-CN)。

<span id="query"></span>
### 查询


|名称 |数据类型 |必填 |示例值 |接口行为 |
|---|---|---|---|---|
|Action |字符串 |是 |`DeleteActivityAPI` |API 操作。 |
|Version |字符串 |是 |`2020-06-01` |API 版本。本次发布的值为 `2020-06-01`。 |


<span id="body"></span>
### 请求体


|名称 |数据类型 |必填 |示例值 |接口行为 |
|---|---|---|---|---|
|ActivityId |长整型 |是 |`17218312****` |要删除的直播间的活动 ID。可通过调用 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-CN) 获取该 ID。 |


<span id="response-parameters"></span>
## 返回调用结果参数


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|ActivityId |长整型 |`17218312****` |被删除直播间的活动 ID。 |
|ActivityIdStr |字符串 |`-` |已弃用。 |
|状态 |整型 |`-` |已弃用。 |


<span id="samples"></span>
## 示例

<span id="sample-request"></span>
### 请求示例

```JSON
POST https://livesaas.byteplusapi.com/?Action=DeleteActivityAPI&Version=2020-06-01
{
  "ActivityId": 17218312****
}
```


<span id="sample-response"></span>
### 返回示例

```JSON
{
  "ResponseMetadata": {
    "RequestId": "2018060411042001001002322800209D2",
    "Action": "DeleteActivityAPI",
    "Version": "2020-06-01",
    "Service": "livesaas",
    "Region": "ap-singapore-1",
    "SystemTime": 1656067132
  },
  "Result": {
    "ActivityId": 17218312****,
    "ActivityIdStr": "",
    "Status": 0
  }
}
```


<span id="error-codes"></span>
## 错误码

共享错误码列表请参见 [常见错误和状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes-zh-CN)。
