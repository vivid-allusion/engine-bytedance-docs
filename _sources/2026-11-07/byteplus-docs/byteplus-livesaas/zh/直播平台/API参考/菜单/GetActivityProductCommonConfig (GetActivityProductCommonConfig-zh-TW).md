---
title: "GetActivityProductCommonConfig"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/GetActivityProductCommonConfig-zh-TW"
---

获取指定直播间内商品的配置，包括商品库的 ID、名称、类型及配置。获取 ID 后，可调用[UpdateActivityProductLibrary](https://docs.byteplus.com/en/docs/byteplus-livesaas/updateactivityproductlibrary)更新商品库信息，或调用[DeleteActivityProductLibrary](https://docs.byteplus.com/en/docs/byteplus-livesaas/deleteactivityproductlibrary)删除商品库。

<span id="Requirements"></span>
## 要求

配额：每个账号每分钟最多查询 120 次

<span id="HTTP request"></span>
## HTTP 请求


* 方法：GET

* Endpoint：https://livesaas.byteplusapi.com/?Action=GetActivityProductCommonConfig&Version=2024\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

下表未包含所有通用请求参数。完整列表请参见[通用请求参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### Query


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`GetActivityProductCommonConfig` |API 操作。 |
|Version |String |是 |`2024-01-01` |此 API 操作的版本。当前版本：`2024-01-01`。 |
|ActivityId |Long |是 |`1783981136301234` |直播间的活动 ID。可通过调用[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi)获取 ID。 |


<span id="Response parameters"></span>
## 返回调用结果参数


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|RoomProductCommonConfig |[RoomProductCommonConfig](https://docs.byteplus.com/en/docs/11/113607#roomproductcommonconfig)对象 |`-` |直播间内商品的配置。 |


<span id="roomproductcommonconfig"></span>
### RoomProductCommonConfig


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|ProductLibraries |[ProductLibraries](https://docs.byteplus.com/en/docs/11/113607#productlibraries)数组 |`-` |商品库的配置。 |


<span id="productlibraries"></span>
### ProductLibraries


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|ProductLibraryId |Integer |`789` |商品库的 ID。 |
|Name |String |`商品库 A` |商品库的名称。 |
|ProductLibraryType |Integer |`1` |商品库的类型。有效值：<br><br><br>* `1`：自有系统的商品库。<br><br>* `2`：Shopify 商品库。 |
|ProductLibraryClientURL |[ProductLibraryClientURL](https://docs.byteplus.com/en/docs/11/113607#productlibraryclienturl)对象 |`-` |自有系统商品库的配置。 |
|ProductLibraryShopify |[ProductLibraryShopify](https://docs.byteplus.com/en/docs/11/113607#productlibraryshopify)对象 |`-` |Shopify 商品库的配置。 |


<span id="productlibraryclienturl"></span>
### ProductLibraryClientURL


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|ExternalQueryURL |String |`http://example.com/query` |用于从自有系统商品库获取商品的请求 URL。 |


<span id="productlibraryshopify"></span>
### ProductLibraryShopify


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|ShopifyMarketDomain |String |`market.example.com` |Shopify 店铺的域名。 |
|ShopifyStoreFrontToken |String |`token123` |Shopify 店铺 Storefront API 的公开访问令牌。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
GET https://livesaas.byteplusapi.com/?Action=GetActivityProductCommonConfig&Version=2024-01-01&ActivityId=1783981136301234
```


<span id="Sample response"></span>
### 返回调用结果示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetActivityProductCommonConfig",
        "Version": "2024-01-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1656067132
    },
    "Result": {
        "RoomProductCommonConfig": {
            "ProductLibraries": [
                {
                    "ProductLibraryId": 789,
                    "Name": "Product library A",
                    "ProductLibraryType": 1,
                    "ProductLibraryClientURL": {
                        "ExternalQueryURL": "http://example.com/query"
                    }
                }
            ]
        }
    }
}
```


<span id="Error codes"></span>
## 错误码

常见错误码列表请参见[常见错误及状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
