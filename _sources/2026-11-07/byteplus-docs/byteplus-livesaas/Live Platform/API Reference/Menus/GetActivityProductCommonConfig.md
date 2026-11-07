---
title: "GetActivityProductCommonConfig"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/getactivityproductcommonconfig"
---

Gets the configurations of products in a specified live room, including the ID, name, type, and configurations of product libraries. After getting the ID, you can call [UpdateActivityProductLibrary](https://docs.byteplus.com/en/docs/byteplus-livesaas/updateactivityproductlibrary) to update the product library information or call [DeleteActivityProductLibrary](https://docs.byteplus.com/en/docs/byteplus-livesaas/deleteactivityproductlibrary) to delete the product library.

<span id="requirements"></span>
## Requirements

Quota: 120 queries per minute per account

<span id="http-request"></span>
## HTTP request


* Method: GET

* Endpoint: https://livesaas.byteplusapi.com/?Action=GetActivityProductCommonConfig&Version=2024\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

Not all common request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`GetActivityProductCommonConfig` |API operation. |
|Version |String |Yes |`2024-01-01` |The version of this API operation. Current version: `2024-01-01`. |
|ActivityId |Long |Yes |`1783981136301234` |The activity ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|RoomProductCommonConfig |Object of [RoomProductCommonConfig](https://docs.byteplus.com/en/docs/11/28515#roomproductcommonconfig) |`-` |The configurations of products in the live room. |


<span id="roomproductcommonconfig"></span>
### RoomProductCommonConfig


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|ProductLibraries |Array of [ProductLibraries](https://docs.byteplus.com/en/docs/11/28515#productlibraries) |`-` |The configurations of product libraries. |


<span id="productlibraries"></span>
### ProductLibraries


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|ProductLibraryId |Integer |`789` |The ID of the product library. |
|Name |String |`Product library A` |The name of the product library. |
|ProductLibraryType |Integer |`1` |The type of the product library. Valid values:<br><br><br>* `1`: A product library of your own system.<br><br>* `2`: A product library of Shopify. |
|ProductLibraryClientURL |Object of [ProductLibraryClientURL](https://docs.byteplus.com/en/docs/11/28515#productlibraryclienturl) |`-` |The configuration of your own system's product library. |
|ProductLibraryShopify |Object of [ProductLibraryShopify](https://docs.byteplus.com/en/docs/11/28515#productlibraryshopify) |`-` |The configuration of Shopify's product library. |


<span id="productlibraryclienturl"></span>
### ProductLibraryClientURL


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|ExternalQueryURL |String |`http://example.com/query` |The request URL used to get products from the product library of your own system. |


<span id="productlibraryshopify"></span>
### ProductLibraryShopify


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|ShopifyMarketDomain |String |`market.example.com` |The domain name of your Shopify store. |
|ShopifyStoreFrontToken |String |`token123` |The public access token for the Storefront API of your Shopify store. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
GET https://livesaas.byteplusapi.com/?Action=GetActivityProductCommonConfig&Version=2024-01-01&ActivityId=1783981136301234
```


<span id="sample-response"></span>
### Sample response

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


<span id="error-codes"></span>
## Error codes

For a list of common error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).

&nbsp;
