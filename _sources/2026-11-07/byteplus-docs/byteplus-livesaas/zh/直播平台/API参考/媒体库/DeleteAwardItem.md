---
title: "DeleteAwardItem"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/DeleteAwardItem-zh-CN"
---

您可以使用此 API 从奖品库中删除指定奖品。

<span id="Requirements"></span>
## 前提条件


* 请求频率限制：每个账号每秒最多 10 次请求

* 前提条件：需拥有 BytePlus 账号，或具备 **媒体库** \> **奖品库** \> **编辑** 权限的 IAM 用户。如需了解如何添加 IAM 用户，请参见 [管理用户、组织和角色](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。


<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* 接口地址：https://livesaas.byteplusapi.com/?Action=DeleteAwardItem&Version=2023\-08\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

以下表格未包含所有通用请求参数。完整参数列表请参见 [通用请求参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### 查询参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`DeleteAwardItem` |API 操作。 |
|Version |String |是 |`2023-08-01` |此 API 操作的版本。当前版本：`2023-08-01`。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Id |Long |是 |1715\*\*\*\*1256 |奖品 ID。您可通过调用 [GetAwardItemList](https://docs.byteplus.com/en/docs/byteplus-livesaas/getawarditemlist) API 获取该 ID。 |


<span id="Response parameters"></span>
## 返回调用结果参数


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Status |Boolean |true |奖品是否删除成功。成功时返回 `true`。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```JSON
POST https://livesaas.byteplusapi.com/?Action=DeleteAwardItem&Version=2023-08-01
{
    "Id": 1715****1256
}
```


<span id="Sample response"></span>
### 返回调用结果示例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DeleteAwardItem",
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

常见错误码列表请参见 [常见错误及状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
