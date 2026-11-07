---
title: "ListActivityProductCommons"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/listactivityproductcommons"
---

Gets the product library information of one or more live rooms at a time.

<span id="requirements"></span>
## Requirements

Quota: 120 queries per minute per account

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://livesaas.byteplusapi.com/?Action=ListActivityProductCommons&Version=2023\-08\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

Not all common request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ListActivityProductCommons` |API operation. |
|Version |String |Yes |`2023-08-01` |The version of this API operation. Current version: `2023-08-01`. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|ActivityIds |Array of Long |Yes |`[178398****301234,178398****305678]` |The activity IDs of live rooms. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|RoomProductCommonConfigs |Array of [RoomProductCommonConfigs](https://docs.byteplus.com/en/docs/11/35910#roomproductcommonconfigs) |`-` |The configurations of products in live rooms. |
|FailedActivityIds |Array of Long |`[-1]` |The activity IDs of live rooms that either have been deleted or do not exist. |


<span id="roomproductcommonconfigs"></span>
### RoomProductCommonConfigs


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|ActivityId |Long |`178398****301234` |The activity ID of the live room. |
|ProductLibraries |Array of [ProductLibraries](https://docs.byteplus.com/en/docs/11/35910#productlibraries) |`-` |The configurations of product libraries. |


<span id="productlibraries"></span>
### ProductLibraries


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|ProductLibraryId |Integer |`17***44` |The ID of the product library. |
|Name |String |`Product library A` |The name of the product library. |
|ProductLibraryType |Integer |`1` |The type of the product library. Valid values:<br><br><br>* `1`: A product library of your own system.<br><br>* `2`: A product library of Shopify. |
|ProductLibraryShopify |Object of [ProductLibraryShopify](https://docs.byteplus.com/en/docs/11/35910#productlibraryshopify) |`-` |The configuration of Shopify's product library. |
|ProductLibraryClientURL |Object of [ProductLibraryClientURL](https://docs.byteplus.com/en/docs/11/35910#productlibraryclienturl) |`-` |The configuration of your own system's product library. |


<span id="productlibraryshopify"></span>
### ProductLibraryShopify


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|ShopifyMarketDomain |String |`market.example.com` |The domain name of your Shopify store. |
|ShopifyStoreFrontToken |String |`2571dc6afdf383****fb02bccc8fd611` |The public access token for the Storefront API of your Shopify store. |


<span id="productlibraryclienturl"></span>
### ProductLibraryClientURL


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|ExternalQueryURL |String |`https://example.com/query` |The request URL used to get products from the product library of your own system. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://livesaas.byteplusapi.com/?Action=ListActivityProductCommons&Version=2023-08-01
{
    "ActivityIds": [
        178398****301234,178398****305678,-1
    ]
}
```


<span id="sample-response"></span>
### Sample response

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


<span id="error-codes"></span>
## Error codes

For a list of common error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).

&nbsp;
