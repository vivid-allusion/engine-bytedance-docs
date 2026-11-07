---
title: "ListActivityProductCommons"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/ListActivityProductCommons-zh-TW"
---

一次獲取一個或多個直播間的商品庫資訊。

<span id="Requirements"></span>
## 需求

配額：每個帳戶每分鐘 120 次查詢

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://livesaas.byteplusapi.com/?Action=ListActivityProductCommons&Version=2023\-08\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

下列表格未包含所有通用請求參數。完整列表請參見[通用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`ListActivityProductCommons` |API 操作。 |
|Version |String |是 |`2023-08-01` |此 API 操作的版本。當前版本：`2023-08-01`。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|ActivityIds |Long 陣列 |是 |`[178398****301234,178398****305678]` |直播間的活動 ID。可透過呼叫[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi)獲取 ID。 |


<span id="Response parameters"></span>
## 回應參數


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|RoomProductCommonConfigs |[RoomProductCommonConfigs](https://docs.byteplus.com/en/docs/11/113519#roomproductcommonconfigs) 陣列 |`-` |直播間商品的配置。 |
|FailedActivityIds |Long 陣列 |`[-1]` |已刪除或不存在的直播間活動 ID。 |


<span id="roomproductcommonconfigs"></span>
### RoomProductCommonConfigs


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|ActivityId |Long |`178398****301234` |直播間的活動 ID。 |
|ProductLibraries |[ProductLibraries](https://docs.byteplus.com/en/docs/11/113519#productlibraries) 陣列 |`-` |商品庫的配置。 |


<span id="productlibraries"></span>
### ProductLibraries


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|ProductLibraryId |Integer |`1776244` |商品庫 ID。 |
|Name |String |`商品庫 A` |商品庫名稱。 |
|ProductLibraryType |Integer |`1` |商品庫型別。有效值：<br><br><br>* `1`：自有系統的商品庫。<br><br>* `2`：Shopify 商品庫。 |
|ProductLibraryShopify |[ProductLibraryShopify](https://docs.byteplus.com/en/docs/11/113519#productlibraryshopify) 物件 |`-` |Shopify 商品庫的配置。 |
|ProductLibraryClientURL |[ProductLibraryClientURL](https://docs.byteplus.com/en/docs/11/113519#productlibraryclienturl) 物件 |`-` |自有系統商品庫的配置。 |


<span id="productlibraryshopify"></span>
### ProductLibraryShopify


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|ShopifyMarketDomain |String |`market.example.com` |Shopify 商店的網域名稱。 |
|ShopifyStoreFrontToken |String |`2571dc6afdf3832857fb02bccc8fd611` |Shopify 商店 Storefront API 的公開存取權杖。 |


<span id="productlibraryclienturl"></span>
### ProductLibraryClientURL


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|ExternalQueryURL |String |`https://example.com/query` |用於從自有系統商品庫獲取商品的請求 URL。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```json
POST https://livesaas.byteplusapi.com/?Action=ListActivityProductCommons&Version=2023-08-01
{
    "ActivityIds": [
        178398****301234,178398****305678,-1
    ]
}
```


<span id="Sample response"></span>
### 回應範例

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
## 錯誤碼

常見錯誤碼請參見[常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
