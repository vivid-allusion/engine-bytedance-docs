---
title: "GetActivityProductCommonConfig"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/GetActivityProductCommonConfig-zh-TW2"
---

獲取指定直播間中的商品資訊，包括商品庫的 ID、名稱、類型及商品庫的配置。獲取 ID 後，可以調用 [UpdateActivityProductLibrary](https://docs.byteplus.com/en/docs/byteplus-livesaas/updateactivityproductlibrary) 來更新商品庫資訊，或調用 [DeleteActivityProductLibrary](https://docs.byteplus.com/en/docs/byteplus-livesaas/deleteactivityproductlibrary) 來刪除商品庫。

<span id="Requirements"></span>
## 需求

配額：每個帳號每分鐘 120 次查詢

<span id="HTTP request"></span>
## HTTP 請求


* 方法：GET

* 端點：https://livesaas.byteplusapi.com/?Action=GetActivityProductCommonConfig&Version=2024\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

下列表格未包含所有通用請求參數。完整列表請參見 [通用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`GetActivityProductCommonConfig` |API 操作。 |
|Version |String |是 |`2024-01-01` |本 API 操作的版本。當前版本：`2024-01-01`。 |
|ActivityId |Long |是 |`1783981136301234` |直播間的活動 ID。可通過調用 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi) 獲取 ID。 |


<span id="Response parameters"></span>
## 回應參數


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|RoomProductCommonConfig |[RoomProductCommonConfig](https://docs.byteplus.com/en/docs/11/113608#roomproductcommonconfig) 物件 |`-` |直播間內商品的配置。 |


<span id="roomproductcommonconfig"></span>
### RoomProductCommonConfig


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|ProductLibraries |[ProductLibraries](https://docs.byteplus.com/en/docs/11/113608#productlibraries) 陣列 |`-` |商品庫的各項配置。 |


<span id="productlibraries"></span>
### ProductLibraries


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|ProductLibraryId |Integer |`789` |商品庫的 ID。 |
|Name |String |`商品庫 A` |商品庫的名稱。 |
|ProductLibraryType |Integer |`1` |商品庫的類型。有效值：<br><br><br>* `1`：自有系統的商品庫。<br><br>* `2`：Shopify 商品庫。 |
|ProductLibraryClientURL |[ProductLibraryClientURL](https://docs.byteplus.com/en/docs/11/113608#productlibraryclienturl) 物件 |`-` |自有系統商品庫的配置。 |
|ProductLibraryShopify |[ProductLibraryShopify](https://docs.byteplus.com/en/docs/11/113608#productlibraryshopify) 物件 |`-` |Shopify 商品庫的配置。 |


<span id="productlibraryclienturl"></span>
### ProductLibraryClientURL


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|ExternalQueryURL |String |`http://example.com/query` |用於從自有系統商品庫獲取商品的請求 URL。 |


<span id="productlibraryshopify"></span>
### ProductLibraryShopify


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|ShopifyMarketDomain |String |`market.example.com` |Shopify 商店的網域名稱。 |
|ShopifyStoreFrontToken |String |`token123` |Shopify 商店 Storefront API 的公開存取權杖。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
GET https://livesaas.byteplusapi.com/?Action=GetActivityProductCommonConfig&Version=2024-01-01&ActivityId=1783981136301234
```


<span id="Sample response"></span>
### 範例回應

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
## 錯誤碼

常見錯誤碼請參見 [常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
