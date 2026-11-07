---
title: "UpdateActivityProductLibrary"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/UpdateActivityProductLibrary-zh-TW"
---

更新指定直播间中商品库的信息，包括商品库的名称、类型和配置信息。

<span id="Requirements"></span>
## 要求

配额：每个账号每分钟最多 120 次查询

<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://livesaas.byteplusapi.com/?Action=UpdateActivityProductLibrary&Version=2024\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

下表未包含所有通用请求参数。完整列表请参见[通用请求参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### Query


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`UpdateActivityProductLibrary` |API 操作。 |
|Version |String |是 |`2024-01-01` |本 API 操作的版本。当前版本：`2024-01-01`。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|ActivityId |Long |是 |`1783981136301234` |直播间的活动 ID。可通过调用[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi)获取 ID。 |
|ProductLibraries |[ProductLibraries](https://docs.byteplus.com/en/docs/11/113604#productlibraries) 数组 |是 |`-` |待更新信息的商品库列表。 |


<span id="productlibraries"></span>
### ProductLibraries


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|ProductLibraryId |Integer |是 |`789` |商品库的 ID。可通过调用[GetActivityProductCommonConfig](https://docs.byteplus.com/en/docs/byteplus-livesaas/getactivityproductcommonconfig)获取 ID。 |
|Name |String |是 |`商品库 A` |商品库的名称。<br><br>请确保商品库名称在直播间内唯一，且长度为 1\-256 个字符。 |
|ProductLibraryType |Integer |是 |`1` |商品库的类型。有效值：<br><br><br>* `1`：自有系统的商品库。<br><br>* `2`：Shopify 商品库。<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">在添加自有系统商品库前，需按照规范开发 OpenAPI，将您的系统集成至 BytePlus Live。更多信息请参见<a href="https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream#integrating-your-system-with-byteplus-live">集成您的系统至 BytePlus Live</a>。</div><br> |
|ProductLibraryClientURL |[ProductLibraryClientURL](https://docs.byteplus.com/en/docs/11/113604#productlibraryclienturl) 对象 |否 |`-` |自有系统商品库的配置信息。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">当<code>ProductLibraryType</code>的值为<code>1</code>时，该参数为必填。</div><br> |
|ProductLibraryShopify |[ProductLibraryShopify](https://docs.byteplus.com/en/docs/11/113604#productlibraryshopify) 对象 |否 |`-` |Shopify 商品库的配置信息。<br><br>BytePlus Live 可调用 GraphQL StoreFront API（包含[Product](https://shopify.dev/docs/api/storefront/2024-04/objects/Product)和[Shop](https://shopify.dev/docs/api/storefront/2024-04/objects/Shop)对象），以获取 Shopify 商品库中的商品。在 BytePlus Live 调用 API 前，您需传入 Storefront API 的公共访问令牌和 Shopify 店铺的域名。关于 GraphQL Storefront API 的更多信息，请参见[GraphQL Storefront API](https://shopify.dev/docs/api/storefront)。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">当<code>ProductLibraryType</code>的值为<code>2</code>时，该参数为必填。</div><br> |


<span id="productlibraryclienturl"></span>
### ProductLibraryClientURL


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|ExternalQueryURL |String |是 |`http://example.com/query` |用于从自有系统商品库获取商品的请求 URL。<br><br>取值长度为 1\-256 个字符。 |


<span id="productlibraryshopify"></span>
### ProductLibraryShopify


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|ShopifyMarketDomain |String |是 |`market.example.com` |您的 Shopify 店铺的域名。<br><br>取值长度为 1\-256 个字符。<br><br>要获取域名，请在 Shopify 店铺左侧导航栏点击**Settings**，即可在店铺名称下方查看域名。您也可以点击**Settings** \> **Domains**，在 Domains 页面查看域名。<br><br><span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_abc7df155a1797057d4b2017c1273d54.png) </span> |
|ShopifyStoreFrontToken |String |是 |`token123` |你 Shopify 商店的 Storefront API 公共访问令牌。<br><br>要获取该令牌，请在 Shopify 商店的无头销售渠道页面点击 **管理**，以管理 Storefront API，然后在 **Storefront API** 页面查看公共访问令牌。<br><br><span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_44ef7418085b6297c8f755b2144a83ef.png) </span> |


<span id="Response parameters"></span>
## 返回参数


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|状态 |布尔类型 |`true` |指示商品库信息是否已更新。<br><br>有效值：<br><br><br>* `true`：所有指定商品库的信息均已更新。<br><br>* `false`：所有指定商品库的信息均未更新。 |
|校验失败列表 |字符串数组 |`["商品库A"]` |配置无效或不包含任何商品的商品库列表。<br><br>仅当 `Status` 的值为 `false` 时，该参数有值。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

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
### 返回示例

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
## 错误码

下表列出了本 API 操作特有的错误码。通用错误码请参见[通用错误码和状态码](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|400 |InvalidParameter.ProductLibraryIdNotFound |ProductLibraryId 参数的值不存在。 |请确保该 ID 属于直播间中已存在的商品库。 |
|400 |InvalidParameter.NameRepeated |Name 参数的值在直播间中必须唯一。 |商品库的名称不能与直播间中其他商品库名称相同。请确保 `Name` 参数的值在直播间中唯一。 |
|400 |InvalidParameter.ShopifyMarketDomainLengthExceed256 |ShopifyMarketDomain 的长度超过了 256 个字符的最大限制。 |请更改 `ShopifyMarketDomain` 参数的值。 |
|400 |InvalidParameter.ExternalQueryURLLengthExceed256 |ExternalQueryURL 的长度超过了 256 个字符的最大限制。 |请更改 `ExternalQueryURL` 参数的值。 |
|400 |InvalidParameter.NameLengthExceed256 |Name 的长度超过了 256 个字符的最大限制。 |请更改 `Name` 参数的值。 |
