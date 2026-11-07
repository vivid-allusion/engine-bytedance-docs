---
title: "UpdateActivityProductLibrary"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/UpdateActivityProductLibrary-zh-TW2"
---

更新指定直播間內商品庫的資訊，包括商品庫的名稱、類型及配置。

<span id="Requirements"></span>
## 需求

配額：每個帳戶每分鐘最多 120 次查詢

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://livesaas.byteplusapi.com/?Action=UpdateActivityProductLibrary&Version=2024\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

下表並未包含所有通用請求參數。完整列表請參見[通用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`UpdateActivityProductLibrary` |API 操作。 |
|Version |String |是 |`2024-01-01` |此 API 操作的版本。目前版本：`2024-01-01`。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|ActivityId |Long |是 |`1783981136301234` |直播間的活動 ID。可透過呼叫[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi)取得 ID。 |
|ProductLibraries |[ProductLibraries](https://docs.byteplus.com/en/docs/11/113603#productlibraries) 陣列 |是 |`-` |需更新資訊的商品庫列表。 |


<span id="productlibraries"></span>
### ProductLibraries


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|ProductLibraryId |Integer |是 |`789` |商品庫的 ID。可透過呼叫[GetActivityProductCommonConfig](https://docs.byteplus.com/en/docs/byteplus-livesaas/getactivityproductcommonconfig)取得 ID。 |
|Name |String |是 |`商品庫 A` |商品庫的名稱。<br><br>請確保商品庫名稱在直播間內唯一，且長度須為 1\-256 字元。 |
|ProductLibraryType |Integer |是 |`1` |商品庫的類型。有效值：<br><br><br>* `1`：自有系統的商品庫。<br><br>* `2`：Shopify 商品庫。<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">在新增自有系統商品庫前，必須依規範開發 OpenAPI 並將系統整合至 BytePlus Live。更多資訊請參見<a href="https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream#integrating-your-system-with-byteplus-live">將系統整合至 BytePlus Live</a>。</div><br> |
|ProductLibraryClientURL |[ProductLibraryClientURL](https://docs.byteplus.com/en/docs/11/113603#productlibraryclienturl) 物件 |否 |`-` |自有系統商品庫的配置。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若<code>ProductLibraryType</code>值為<code>1</code>，此參數為必填。</div><br> |
|ProductLibraryShopify |[ProductLibraryShopify](https://docs.byteplus.com/en/docs/11/113603#productlibraryshopify) 物件 |否 |`-` |Shopify 商品庫的配置。<br><br>BytePlus Live 可呼叫 GraphQL StoreFront API，該 API 包含[Product](https://shopify.dev/docs/api/storefront/2024-04/objects/Product)及[Shop](https://shopify.dev/docs/api/storefront/2024-04/objects/Shop)物件，以取得 Shopify 商品庫中的商品。在 BytePlus Live 呼叫 API 前，必須傳入 Storefront API 的公開存取權杖及 Shopify 商店的網域名稱。關於 GraphQL Storefront API 的更多資訊，請參見[GraphQL Storefront API](https://shopify.dev/docs/api/storefront)。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若<code>ProductLibraryType</code>值為<code>2</code>，此參數為必填。</div><br> |


<span id="productlibraryclienturl"></span>
### ProductLibraryClientURL


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|ExternalQueryURL |String |是 |`http://example.com/query` |用於取得自有系統商品庫商品的請求 URL。<br><br>值須為 1\-256 字元。 |


<span id="productlibraryshopify"></span>
### ProductLibraryShopify


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|ShopifyMarketDomain |String |是 |`market.example.com` |您的 Shopify 商店網域名稱。<br><br>值須為 1\-256 字元。<br><br>取得網域名稱，請點選 Shopify 商店左側導覽窗格的**Settings**，即可在商店名稱下方查看網域名稱。您也可點選**Settings** \> **Domains**，於 Domains 頁面查看網域名稱。<br><br><span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_abc7df155a1797057d4b2017c1273d54.png) </span> |
|ShopifyStoreFrontToken |String |是 |`token123` |您 Shopify 商店 Storefront API 的公開存取權杖。<br><br>若要取得權杖，請在 Shopify 商店的 headless 銷售通路頁面點擊 **管理** 以管理 Storefront API，然後在 **Storefront API** 頁面檢視公開存取權杖。<br><br><span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_44ef7418085b6297c8f755b2144a83ef.png) </span> |


<span id="Response parameters"></span>
## 回應參數


|**參數** |**資料類型** |**範例值** |**說明** |
|---|---|---|---|
|狀態 |布林值 |`true` |指示產品庫資訊是否已更新。<br><br>有效值：<br><br><br>* `true`：所有指定產品庫的資訊均已更新。<br><br>* `false`：所有指定產品庫的資訊皆未更新。 |
|CheckFailedList |字串陣列 |`["產品庫 A"]` |配置無效或不包含任何產品的產品庫清單。<br><br>僅當 `狀態` 的值為 `false` 時，此參數才有值。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://livesaas.byteplusapi.com/?Action=UpdateActivityProductLibrary&Version=2024-01-01
{
    "ActivityId": 1783981136301234,
    "ProductLibraries": [
        {
            "ProductLibraryId": 789,
            "Name": "Product library A",
            "ProductLibraryType": 1,
            "ProductLibraryClientURL": {
                "ExternalQueryURL": "http://example.com/query"
            }
        },
        {
            "ProductLibraryId": 789,
            "Name": "Product library B",
            "ProductLibraryType": 2,
            "ProductLibraryShopify": {
                "ShopifyMarketDomain": "market.example.com",
                "ShopifyStoreFrontToken": "token123"
            }
        }
    ]
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UpdateActivityProductLibrary",
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
## 錯誤碼

下表列出此 API 操作專屬的錯誤碼。通用錯誤碼請參見[通用錯誤與狀態碼](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|400 |InvalidParameter.ProductLibraryIdNotFound |ProductLibraryId 參數的值不存在。 |請確保該 ID 屬於直播間中現有的產品庫。 |
|400 |InvalidParameter.NameRepeated |Name 參數的值在直播間中必須唯一。 |產品庫的名稱不可與直播間中的其他產品庫相同。請確保 `Name` 參數的值在直播間中唯一。 |
|400 |InvalidParameter.ShopifyMarketDomainLengthExceed256 |ShopifyMarketDomain 的長度超過 256 字元的最大限制。 |請變更 `ShopifyMarketDomain` 參數的值。 |
|400 |InvalidParameter.ExternalQueryURLLengthExceed256 |ExternalQueryURL 的長度超過 256 字元的最大限制。 |請變更 `ExternalQueryURL` 參數的值。 |
|400 |InvalidParameter.NameLengthExceed256 |Name 的長度超過 256 字元的最大限制。 |請變更 `Name` 參數的值。 |
