---
title: "GetTemporaryLoginTokenAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-gettemporarylogintokenapi-zh-CN"
---

调用此 API 获取直播间的密钥，用于开播。

<span id="bac9c171"></span>
## 需求

配额：每个账号每分钟最多查询 120 次

<span id="b63c37e0"></span>
## HTTP 请求


* URL：`https://livesaas.byteplusapi.com/?Action=GetTemporaryLoginTokenAPI&Version=2020-06-01`

* 方法：GET


<span id="576d363d"></span>
## 请求参数

以下表格未包含所有通用请求参数。完整参数列表请参见 [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters-zh-CN#f1706967)。

<span id="64a0bda3"></span>
### 查询


|名称 |数据类型 |是否必填 |示例值 |接口行为 |
|---|---|---|---|---|
|Action |String |是 |`GetTemporaryLoginTokenAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。当前版本：`2020-06-01`。 |
|ActivityId |Long |是 |`17218312****` |直播间的活动 ID。可通过调用 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-CN) 获取该 ID。 |


<span id="a8e81e5f"></span>
## 返回调用结果参数


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|SecretKey |String |`0UmdWrZKAVWJJTxzCOJ****` |直播间的密钥，用于开播。 |
|ActivityId |Long |`17218312****` |直播间的活动 ID。 |


<span id="bf977fee"></span>
## 示例

<span id="875465ab"></span>
### 请求示例

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetTemporaryLoginTokenAPI&Version=2020-06-01&ActivityId=17218312****
```


<span id="8d037a06"></span>
### 返回示例

```JSON
{
  "ResponseMetadata": {
    "RequestId": "201806041104200100100232280022D30",
    "Action": "GetTemporaryLoginTokenAPI",
    "Version": "2020-06-01",
    "Service": "livesaas",
    "Region": "ap-singapore-1",
    "SystemTime": 1656067132
  },
  "Result": {
      "SecretKey": "0UmdWrZKAVWJJTxzCOJ****",
      "ActivityId": 17218312****
  }
}
```


<span id="53f720b3"></span>
## 错误码

通用错误码列表请参见 [常见错误和状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes-zh-CN)。
