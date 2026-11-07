---
title: "DeleteActivityProductLibrary"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/DeleteActivityProductLibrary-zh-TW"
---

删除指定直播间中的一个或多个商品库。

<span id="Requirements"></span>
## 要求

配额：每个账号每分钟 120 次查询

<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://livesaas.byteplusapi.com/?Action=DeleteActivityProductLibrary&Version=2024\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

下表未包含所有通用请求参数。完整列表请参见[通用请求参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### Query


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`DeleteActivityProductLibrary` |API 操作。 |
|Version |String |是 |`2024-01-01` |此 API 操作的版本。当前版本：`2024-01-01`。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|ActivityId |Long |是 |`1783981136301234` |直播间的活动 ID。可通过调用[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi)获取该 ID。 |
|ProductLibraryIds |Long 数组 |是 |`[789, 790]` |待删除商品库的 ID 列表。可通过调用[GetActivityProductCommonConfig](https://docs.byteplus.com/en/docs/byteplus-livesaas/getactivityproductcommonconfig)获取该 ID。 |


<span id="Response parameters"></span>
## 返回参数


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Status |Boolean |`true` |指示是否已删除所有指定的商品库。若全部删除，则返回`true`。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://livesaas.byteplusapi.com/?Action=DeleteActivityProductLibrary&Version=2024-01-01
{
    "ActivityId": 1783981136301234,
    "ProductLibraryIds": [
        789,
        790
    ]
}
```


<span id="Sample response"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DeleteActivityProductLibrary",
        "Version": "2024-01-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1656067132
    },
    "Result": {
        "Status": true
    }
}
```


<span id="Error codes"></span>
## 错误码

下表列出了此 API 操作特有的错误码。通用错误码请参见[通用错误码和状态码](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|400 |InvalidParameter.ProductLibraryIdNotFound |ProductLibraryId 参数的值不存在。 |请确保该 ID 属于直播间中已存在的商品库。 |
