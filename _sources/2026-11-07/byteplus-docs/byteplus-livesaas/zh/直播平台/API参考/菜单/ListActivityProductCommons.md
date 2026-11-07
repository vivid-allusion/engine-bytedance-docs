---
title: "ListActivityProductCommons"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/ListActivityProductCommons-zh-CN"
---

一次获取一个或多个直播间的商品库信息。

<span id="Requirements"></span>
## 要求

配额：每个账号每分钟最多查询 120 次

<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://livesaas.byteplusapi.com/?Action=ListActivityProductCommons&Version=2023\-08\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

以下表格未包含所有通用请求参数。完整参数列表请参见[通用请求参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`ListActivityProductCommons` |API 操作。 |
|Version |String |是 |`2023-08-01` |此 API 操作的版本。当前版本：`2023-08-01`。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|ActivityIds |Long 数组 |是 |`[178398****301234,178398****305678]` |直播间的活动 ID。可通过调用[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi)获取 ID。 |


<span id="Response parameters"></span>
## 返回调用结果参数


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|RoomProductCommonConfigs |[RoomProductCommonConfigs](https://docs.byteplus.com/en/docs/11/113518#roomproductcommonconfigs) 数组 |`-` |直播间商品的配置。 |
|FailedActivityIds |Long 数组 |`[-1]` |已被删除或不存在的直播间活动 ID。 |


<span id="roomproductcommonconfigs"></span>
### RoomProductCommonConfigs


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|ActivityId |Long |`178398****301234` |直播间的活动 ID。 |
|ProductLibraries |[ProductLibraries](https://docs.byteplus.com/en/docs/11/113518#productlibraries) 数组 |`-` |商品库的配置。 |


<span id="productlibraries"></span>
### ProductLibraries


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|ProductLibraryId |Integer |`1776244` |商品库的 ID。 |
|Name |String |`商品库 A` |商品库名称。 |
|ProductLibraryType |Integer |`1` |商品库类型。有效值：<br><br><br>* `1`：自有系统的商品库。<br><br>* `2`：Shopify 商品库。 |
|ProductLibraryShopify |[ProductLibraryShopify](https://docs.byteplus.com/en/docs/11/113518#productlibraryshopify) 对象 |`-` |Shopify 商品库的配置。 |
|ProductLibraryClientURL |[ProductLibraryClientURL](https://docs.byteplus.com/en/docs/11/113518#productlibraryclienturl) 对象 |`-` |自有系统商品库的配置。 |


<span id="productlibraryshopify"></span>
### ProductLibraryShopify


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|ShopifyMarketDomain |String |`market.example.com` |Shopify 店铺的域名。 |
|ShopifyStoreFrontToken |String |`2571dc6afdf3832857fb02bccc8fd611` |Shopify 店铺 Storefront API 的公共访问令牌。 |


<span id="productlibraryclienturl"></span>
### ProductLibraryClientURL


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|ExternalQueryURL |String |`https://example.com/query` |用于从自有系统商品库获取商品的请求 URL。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://livesaas.byteplusapi.com/?Action=ListActivityProductCommons&Version=2023-08-01
{
    "ActivityIds": [
        178398****301234,178398****305678,-1
    ]
}
```


<span id="Sample response"></span>
### 返回调用结果示例

```json
{
    "ResponseMetadata": {
        "RequestId": "202411150253157******0B796DF96AD0D",
        "Action": "ListActivityProductCommons",
        "Version": "2023-08-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1731639196
    },
    "Result": {
        "RoomProductCommonConfigs": [
            {
                "ActivityId": 178398****301234,
                "ProductLibraries": [
                    {
                        "ProductLibraryId": 17***44,
                        "Name": "Product library A",
                        "ProductLibraryType": 1,
                        "ProductLibraryClientURL": {
                            "ExternalQueryURL": "https://example.com/query"
                        },
                        "ProductLibraryShopify": {}
                    }
                ]
            },
            {
                "ActivityId": 178398****305678,
                "ProductLibraries": [
                    {
                        "ProductLibraryId": 17***45,
                        "Name": "Product library B",
                        "ProductLibraryType": 2,
                        "ProductLibraryClientURL": {},
                        "ProductLibraryShopify": {
                            "ShopifyMarketDomain": "market.example.com",
                            "ShopifyStoreFrontToken": "2571dc6afdf383****fb02bccc8fd611

"
                        }
                    }
                ]
            }
        ],
        "FailedActivityIds": [
            -1
        ]
    }
}
```


<span id="Error codes"></span>
## 错误码

常见错误码列表请参见[通用错误码和状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
