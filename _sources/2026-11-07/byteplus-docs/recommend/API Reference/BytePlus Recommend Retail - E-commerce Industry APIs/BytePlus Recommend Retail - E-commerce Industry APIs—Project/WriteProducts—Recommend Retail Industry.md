---
title: "WriteProducts—Recommend Retail Industry"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/reference-retail_writeproducts"
---

The WriteProducts API allows for the seamless uploading of new product data or updating of existing product information in the Retail/E\-commerce industry specifically for Recommend.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information on BytePlus Recommend token authentication, refer <a href="https://docs.byteplus.com/en/recommend/reference/api_token_authentication">here</a>.</div>


<span id="a1abe13f"></span>
# Limitations

The following limitations apply to WriteProducts API:


* Each request can upload no more than 2,000 product data records at a time. If you upload more than 2,000 product data records in a single request, you will encounter a rejection.

* The result obtained by multiplying QPS by the number of uploads per request must be less than 30,000.

* Deleting a product is not supported.


<span id="36c7c3c1"></span>
# HTTP request


|**URL** |https://rec\-ap\-singapore\-1.byteplusapi.com/data/api/retail/${tenant}/product |
|---|---|
|**Method** |POST |


<span id="d5e9f3b3"></span>
# Request parameters

The topics below details the parameters required for the WriteProducts API.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Not all request parameters are included in the following table. For a complete list, refer to <a href="https://docs.byteplus.com/recommend/reference/api_token_authentication">HTTP header parameters</a>.</div>


<span id="144f0eac"></span>
## Query

The following table details the query parameters required for the WriteProducts API:


|**Query String Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|method |String |Yes |Write |*  |


<span id="1dad2339"></span>
## Body

The following table details the body parameters required for the WriteProducts API:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|products |Array of Objects |Yes |*  |A list of product data to be uploaded on the platform. The maximum number of entries for the product list is 100. If you exceed that quota, you will encounter a rejection. |
|extra |Object |No |*  |This field is used to pack key\-value pairs.<br><br>For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |


<span id="c7965356"></span>
### **Products**

This field refers to a list of product data to be updated. The following table details the types of data it contains:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|product_id |String |Yes |632461 |The unique identifier for the product. |
|categories |Array of Objects |Yes |[<br><br>{"category_depth":1, "category_nodes": [{"id_or_name":"Shoes"}] },<br><br>{"category_depth":2, "category_nodes": [{"id_or_name":"Men's Shoes"}] },<br><br>{"category_depth":3, "category_nodes": [{"id_or_name":"Basketball Shoes"}] },<br><br>] |The categories that the product belongs to. The category value is a JSON serialized string.<br><br>If a product belongs to a single category, like "Shoes \-\> Men's Shoes \-\> Basketball Shoes", then this field should be like:<br><br>```JSON```<br>```[```<br>```{"category_depth":1, "category_nodes": [{"id_or_name":"Shoes"}] },```<br>```{"category_depth":2, "category_nodes": [{"id_or_name":"Men's Shoes"}] },```<br>```{"category_depth":3, "category_nodes": [{"id_or_name":"Basketball Shoes"}] },```<br>```]```<br><br><br>If a product belongs to two different categories, like "Shoes \-\> Men's shoes" and "Sports \-\> Basketball", then this field should be like:<br><br>```JSON```<br>```[```<br>```{"category_depth":1, "category_nodes": [{"id_or_name":"Shoes"}, {"id_or_name":"Men's shoes"}] },```<br>```{"category_depth":2, "category_nodes": [{"id_or_name":"Sports"}, {"id_or_name":"Basketball"}] },```<br>```]```<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you do not fill in this parameter, the accuracy and efficiency of the product recommendations will be affected.</div><br> |
|brands |Array of Objects |Yes |[<br><br>{"brand_depth": 1, "id_or_name":"Adidas"},<br><br>{"brand_depth": 2, "id_or_name":"Yeezy"},<br><br>] |The brands that the product belongs to. You should sort the brands by their brand_depth in ascending order.<br><br>For example, if a product belongs to "Adidas \-\> Yeezy", this field should be like:<br><br>```JSON```<br>```[```<br>```{"brand_depth": 1, "id_or_name":"Adidas"},```<br>```{"brand_depth": 2, "id_or_name":"Yeezy"},```<br>```]```<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you do not fill in this parameter, the accuracy and efficiency of the product recommendations will be affected.</div><br> |
|price |Object |*  |*  |The price proto. Ensure the products that need to be ranked are priced using the same currency. |
|is_recommendable |Boolean |Yes |True |This field is used to determine whether the product should be recommended to users. The accepted values are as follows:<br><br><br>* True—The product should be recommended to users.<br><br>* False—The product should not be recommended to users.<br><br><br>Even if a product is not recommended to your users, it is important to submit this parameter to us. Users may have interacted with this product in the past, and providing this information enables us to deliver more accurate recommendations.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Any change made to the <code>is_recommendable</code> parameter will take up to 1 hour to take effect.</div><br> |
|title |String |Yes |Grey Shoes 100 |The product title. You can use the text name of the product or the title on the HTML page. |
|quality_score |Double |No |4.4 |The product quality score given by the seller.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Quality_score is different from user ratings. It is normally computed as a composite score considering many factors, including sales, customer feedback, information completeness and so on.</div><br><br><br>This score range should be between 1.0 and 5.0. |
|tags |Array of Strings |*  |New Product |The product's internal tags.<br><br>The accepted values include:<br><br><br>* New Product<br><br>* Summer Product<br><br><br>For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |
|display |Object |*  |*  |The display information about the product. |
|product_spec |Object |*  |*  |The detailed product specs. |
|seller |Object |*  |*  |The seller's information. |
|extra |Object |No |*  |This field is used to pack key\-value pairs.<br><br>For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |


<span id="f26d9a61"></span>
#### Brands

This field refers to the brands that the product belongs to. It contains the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|brand_depth |Int32 |Yes |1 |The brand depth. The value is consecutive and ascending. |
|id_or_name |String |Yes |Grey Shoes 100 |The ID or name of the brand at this depth. |


<span id="c58ca38a"></span>
#### Categories

This field refers to the categories that the product belongs to. It contains the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|category_depth |Int32 |Yes |1 |The depth of the category. The value is consecutive and ascending. |
|category_nodes |Array of Objects |Yes |Shoes |The category nodes belong to the same depth. |


<span id="7e8433d0"></span>
##### Category_nodes

It refers to the ID or name of the categories. It contains the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|id_or_name |String |Yes |Shoes |The unique identifier for the category.<br><br>For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |


<span id="1f6f46d5"></span>
#### **Display**

This parameter refers to the display information about the product. It contains the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|listing_page_display_tags |Array of Strings |No |best seller |The product's tags displayed to the user on the listing page.<br><br>The accepted values include:<br><br><br>* best seller<br><br>* hot sales<br><br><br>For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |
|detail_page_display_tags |Array of Strings |No |FreeShipping |The product's tags displayed to the user on the product\-detail page.<br><br>The accepted values include:<br><br><br>* FreeShipping<br><br>* 1 year guarantee<br><br><br>For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |
|listing_page_display_type |String |No |image |It indicates the types that you choose to display your products on the listing page.<br><br>The acceptable values are:<br><br><br>* image<br><br>* video<br><br>* other |
|cover_multimedia_url |String |No |https://demo.jpg |If there is a value in `listing_page_display_type`, fill this parameter with the cover image's link. |


<span id="f207a95d"></span>
#### **Price**

This field provides detailed price information about the product. It contains the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|current_price |Int64 |Yes |49900 |Enter the current price of the product in cents.<br><br>For example, $100.12 = 10012. |
|origin_price |Int64 |Yes |69900 |Enter the original price of the product in cents.<br><br>For example, $100.12 = 10012. |


<span id="09cdd5d8"></span>
#### **Product_spec**

This parameter refers to detailed product specs. It contains the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|product_group_id |String |Yes |1356 |The unique identifier for the product group. For example, beer might have 6\-pack and 12\-pack options. Each of them has a different product_id and they should share the same product_group_id. |
|user_rating |Double |No |0.25 |The rating given by the users. This value range should be between 0.0 and 5.0. |
|comment_count |Int32 |No |100 |The number of comments for this product. |
|source |String |No |Self |The source of the product. The accepted values are:<br><br><br>* Self<br><br>* Third\-party<br><br>* Other |
|publish_timestamp |Int64 |No |1623193487 |The time when the product is on sale. |


<span id="953359df"></span>
#### **Seller**

This field refers to information about the seller. It contains the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|id |String |Yes |43485 |The unique identifier for the seller. |
|seller_level |String |No |gold |The seller's level. The accepted values include:<br><br><br>* gold<br><br>* silver<br><br><br>For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |
|seller_rating |Double |No |3.5 |The seller's rating given by the customers. The value range should be between 0.0 and 5.0. |


<span id="da536ff9"></span>
### **Extra**

This field is used to pack key\-value pairs. It contains the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|newKey |String |*  |*  |*  |
|New Value |String |*  |*  |*  |


<span id="0ce09166"></span>
# Response parameters

The following tables details the response parameters for the WriteProducts API:


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|status |Object |*  |This field defines an error model. It contains two types of data: error code and error message. |
|errors |Array of Objects |*  |This field is populated when the status is an error code: 1001. |


<span id="174bf16b"></span>
## **Status**

The `status` defines an error model. Each `status` message contains two types of data: error code and error message.


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|code |Int32 |0 |You should look at this response parameter to determine if your API request was successful or not. The accepted values include:<br><br><br>* 0: it indicates that the calling is successful.<br><br>* 4xx: it indicates user error.<br><br>* 5xx: it indicates server error.<br><br>* 1xxx: it indicates error relating to Import calls.<br><br>* 2xxx: it indicates errors relating to Predict calls. |
|message |String |An unexpected value XXX is included in the XXX field, only ["xx", "yy", "zz"] can be accepted. |Provides a detailed error message on the reasons why your API request was unsuccessful. |


<span id="3587f4e2"></span>
# Samples

The following section details the sample codes for the WriteProducts API.

<span id="fb01f45e"></span>
## Sample request

The following is a sample request for the API.

```JSON
curl --request POST \
     --url 'https://rec-ap-singapore-1.byteplusapi.com/data/api/retail/retail_demo/product?method=write' \
     --header 'Accept: application/json' \
     --header 'Content-Type: application/json' \
     --header 'Request-Id:12313208' \
     --header 'Tenant-Id:d7c5963593798b5263858b028f589' \
     --header 'Tenant-Nonce:1683628486' \
     --header 'Tenant-Ts:1683628486' \
     --header 'Tenant-Signature:5dd21c479acac4b9043af03bb0d4371a0c927d8094f1ae603ffa27d6187bd41f' \
     --data '{
     "products": [
          {
               "categories": [
                    {
                         "category_nodes": [
                              {
                                   "id_or_name": "Shoes"
                              }
                         ],
                         "category_depth": 1
                    },
                    {
                         "category_nodes": [
                              {
                                   "id_or_name": "Men Shoes"
                              }
                         ],
                         "category_depth": 2
                    }
               ],
               "brands": [
                    {
                         "brand_depth": 1,
                         "id_or_name": "Adidas"
                    },
                    {
                         "brand_depth": 2,
                         "id_or_name": "Yeezy"
                    }
               ],
               "price": {
                    "current_price": 49900,
                    "origin_price": 69900
               },
               "tags": [
                    "New Product",
                    "Summer Product"
               ],
               "display": {
                    "listing_page_display_tags": [
                         "best seller",
                         "hot sales"
                    ],
                    "detail_page_display_tags": [
                         "FreeShipping",
                         "Return in 7 days without any reasons"
                    ],
                    "listing_page_display_type": "image",
                    "cover_multimedia_url": "https://images-na.ssl-images-amazon.com/images/I/81WmojBxvbL._AC_UL1500_.jpg"
               },
               "product_spec": {
                    "product_group_id": "1356",
                    "comment_count": 100,
                    "user_rating": 0.25,
                    "source": "self",
                    "publish_timestamp": 1623193487
               },
               "seller": {
                    "id": "43485",
                    "seller_level": "1",
                    "seller_rating": 3.5
               },
               "product_id": "632461",
               "is_recommendable": true,
               "title": "adidas Yeezy Boost 350 V2 Grey/Borang/Dgsogr",
               "quality_score": 4.4,
               "extra": {
                    "custom_field": "value"
               }
          }
     ],
     "extra": {
          "additionalProp": "additionalVal"
     }
}'
```


<span id="de55caff"></span>
## Sample response

The following is a **successful** sample response.

```JSON
{ 
  "status": { 
    "message": "OK", 
    "success": true 
  }
}
```


The following is a **failed** sample response.

```JSON
{ 
  "status": { 
    "code": 400, 
    "message": "data is empty; errID:840491090 logID:2023040410191442531CEBDBB7FC46D5F4" 
  } 
}
```


The following is **failed** sample response if the data entries exceed 2,000.

```JSON
{
  "status": {
    "code": 413,
    "message": "The count of write items max to 2000; errID:840491090 logID:2023032311430332A733A4EA5CBF7B0926"
  }
}
```


The following is a **failed** sample response if the data is incomplete or inaccurate.

```JSON
{
  "status": {
    "code": 1001,
    "message": "Occur error, partial or all data handle fail"
  },
  "errors": [
    {
      "message": "in the 'product_id' field, required field is empty",
      "product": {
        "categories": [
          {
            "category_depth": 1,
            "category_nodes": [
              {
                "id_or_name": "Shoes"
              }
            ]
          },
          {
            "category_depth": 2,
            "category_nodes": [
              {
                "id_or_name": "Men Shoes"
              }
            ]
          }
        ],
        "brands": [
          {
            "brand_depth": 1,
            "id_or_name": "Adidas"
          },
          {
            "brand_depth": 2,
            "id_or_name": "Yeezy"
          }
        ],
        "price": {
          "current_price": "49900",
          "origin_price": "69900"
        },
        "is_recommendable": true,
        "title": "adidas Yeezy Boost 350 V2 Grey/Borang/Dgsogr",
        "quality_score": 4.4,
        "tags": [
          "New Product",
          "Summer Product"
        ],
        "display": {
          "listing_page_display_tags": [
            "best seller",
            "hot sales"
          ],
          "detail_page_display_tags": [
            "FreeShipping",
            "Return in 7 days without any reasons"
          ],
          "listing_page_display_type": "image",
          "cover_multimedia_url": "https://images-na.ssl-images-amazon.com/images/I/81WmojBxvbL._AC_UL1500_.jpg"
        },
        "product_spec": {
          "product_group_id": "1356",
          "user_rating": 0.25,
          "comment_count": 100,
          "source": "self",
          "publish_timestamp": "1623193487"
        },
        "seller": {
          "id": "43485",
          "seller_level": "1",
          "seller_rating": 3.5
        },
        "extra": {
          "custom_field": "value"
        }
      }
    }
  ]
}
```


<span id="9398e94b"></span>
# Error codes

For more information on the API error codes, refer to [BytePlus Recommend shared error and status codes](https://docs.byteplus.com/recommend/reference/shared_error_and_status_codes).
