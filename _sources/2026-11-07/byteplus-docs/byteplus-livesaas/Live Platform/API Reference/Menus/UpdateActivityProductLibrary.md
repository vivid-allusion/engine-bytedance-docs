---
title: "UpdateActivityProductLibrary"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/updateactivityproductlibrary"
---

Updates the information of product libraries in a specific live room, including the name, type, and configurations of product libraries.

<span id="requirements"></span>
## Requirements

Quota: 120 queries per minute per account

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://livesaas.byteplusapi.com/?Action=UpdateActivityProductLibrary&Version=2024\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

Not all common request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`UpdateActivityProductLibrary` |API operation. |
|Version |String |Yes |`2024-01-01` |The version of this API operation. Current version: `2024-01-01`. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|ActivityId |Long |Yes |`1783981136301234` |The activity ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |
|ProductLibraries |Array of [ProductLibraries](https://docs.byteplus.com/en/docs/11/28513#productlibraries) |Yes |`-` |The list of product libraries whose information is to be updated. |


<span id="productlibraries"></span>
### ProductLibraries


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|ProductLibraryId |Integer |Yes |`789` |The ID of the product library. You can get the ID by calling [GetActivityProductCommonConfig](https://docs.byteplus.com/en/docs/byteplus-livesaas/getactivityproductcommonconfig). |
|Name |String |Yes |`Product library A` |The name of the product library.<br><br>Make sure the product library name is unique in the live room and must be 1\-256 characters in length. |
|ProductLibraryType |Integer |Yes |`1` |The type of the product library. Valid values:<br><br><br>* `1`: A product library of your own system.<br><br>* `2`: A product library of Shopify.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">You must develop an OpenAPI according to the specifications to integrate your system with BytePlus Live before adding a product library of your own system. For more information, see <a href="https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream#integrating-your-system-with-byteplus-live">Integrating your system with BytePlus Live</a>.</div><br> |
|ProductLibraryClientURL |Object of [ProductLibraryClientURL](https://docs.byteplus.com/en/docs/11/28513#productlibraryclienturl) |No |`-` |The configuration of your own system's product library.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is required if the value of <code>ProductLibraryType</code> is <code>1</code>.</div><br> |
|ProductLibraryShopify |Object of [ProductLibraryShopify](https://docs.byteplus.com/en/docs/11/28513#productlibraryshopify) |No |`-` |The configuration of Shopify's product library.<br><br>BytePlus Live can call the GraphQL StoreFront API, which includes [Product](https://shopify.dev/docs/api/storefront/2024-04/objects/Product) and [Shop](https://shopify.dev/docs/api/storefront/2024-04/objects/Shop) objects, to get products from Shopify's product library. Before BytePlus Live can call the API, you must pass in the public access token for the Storefront API and the domain name of your Shopify store. For more information about GraphQL Storefront API, see [GraphQL Storefront API](https://shopify.dev/docs/api/storefront).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is required if the value of <code>ProductLibraryType</code> is <code>2</code>.</div><br> |


<span id="productlibraryclienturl"></span>
### ProductLibraryClientURL


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|ExternalQueryURL |String |Yes |`http://example.com/query` |The request URL used to get products from the product library of your own system.<br><br>The value must be 1\-256 characters in length. |


<span id="productlibraryshopify"></span>
### ProductLibraryShopify


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|ShopifyMarketDomain |String |Yes |`market.example.com` |The domain name of your Shopify store.<br><br>The value must be 1\-256 characters in length.<br><br>To get the domain name, click **Settings** on the left navigation pane of your Shopify store and then you can view the domain name under the store name. You can also click **Settings** \> **Domains** to view the domain name on the Domains page.<br><br><span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_abc7df155a1797057d4b2017c1273d54.png) </span> |
|ShopifyStoreFrontToken |String |Yes |`token123` |The public access token for the Storefront API of your Shopify store.<br><br>To get the token, click **Manage** to manage the Storefront API on the headless sales channel page of your Shopify store and then view the public access token on the **Storefront API** page.<br><br><span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_44ef7418085b6297c8f755b2144a83ef.png) </span> |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Status |Boolean |`true` |Indicates whether the information of product libraries is updated.<br><br>Valid values:<br><br><br>* `true`: The information of all the specified product libraries is updated.<br><br>* `false`: None of the specified product libraries has information updated. |
|CheckFailedList |Array of String |`["Product library A"]` |The list of product libraries whose configurations are invalid or do not contain any products.<br><br>This parameter has a value only when the value of `Status` is `false`. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

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


<span id="sample-response"></span>
### Sample response

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


<span id="error-codes"></span>
## Error codes

The following table lists error codes specific to this API operation. For a list of common error codes, see [Common error and status codes](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-shared-error-and-status-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|400 |InvalidParameter.ProductLibraryIdNotFound |The value of the ProductLibraryId parameter does not exist. |Make sure the ID belongs to an existing product library in the live room. |
|400 |InvalidParameter.NameRepeated |The value of the Name parameter must be unique in the live room. |The name of a product library cannot be the same as that of another one in the live room. Make sure the value of the `Name` parameter is unique in the live room. |
|400 |InvalidParameter.ShopifyMarketDomainLengthExceed256 |The length of ShopifyMarketDomain exceeds the maximum limit of 256 characters. |Change the value of the `ShopifyMarketDomain` parameter. |
|400 |InvalidParameter.ExternalQueryURLLengthExceed256 |The length of ExternalQueryURL exceeds the maximum limit of 256 characters. |Change the value of the `ExternalQueryURL` parameter. |
|400 |InvalidParameter.NameLengthExceed256 |The length of Name exceeds the maximum limit of 256 characters. |Change the value of the `Name` parameter. |


&nbsp;
