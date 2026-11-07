---
title: "WriteProducts—Recommend SaaS Retail Industry"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/reference-retail_saas_writeproducts"
---

The WriteProducts API allows for the seamless uploading of new product data or updating of existing product information in the Retail/E\-commerce industry specifically for Recommend SaaS.

<span id="a1abe13f"></span>
# Limitations

The following limitations apply to WriteProducts API:


* Each request can upload no more than 2,000 product data records at a time. If you upload more than 2,000 product data records in a single request, you will encounter a rejection.

* The result obtained by multiplying QPS by the number of uploads per request must be less than 30,000.


<span id="36c7c3c1"></span>
# HTTP request


|**URL** |https://rec\-api\-sg1.recplusapi.com/RetailSaaS/WriteProducts |
|---|---|
|**Method** |POST |


<span id="d5e9f3b3"></span>
# Request parameters

The topics below details the parameters required for the WriteProducts API.

<span id="df2272f4"></span>
## Header


|**Header Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Tenant\-Id |String |Yes |3000001813 |Your BytePlus account's ID. For more information on retrieving Recommend Tenant IDs, refer [here](https://docs.byteplus.com/recommend/docs/retail_standard_getting_started). |
|Request\-id |String |Yes |84kduxkls74lcdj73jdu3 |The client assigns the request id, and it should be unique for each request. No specific format is required for the request\-id, but it is advisable to keep it reasonably short.<br><br>For more information on request\-id generation code samples, refer [here](https://docs.byteplus.com/recommend/reference/api_token_authentication). |
|Other Auth Header |*  |Yes |*  |**Recommend Standard**<br><br>BytePlus Recommend SaaS Standard uses Access Key/Secret Key (AK/SK) for Byteplus Standard header authentication. The process of constructing these headers can be complex, so it is recommended to use the SDK for easier access and implementation.<br><br>For more information on using the AK/SK authentication, refer [here](https://docs.byteplus.com/en/recommend/reference/api_authentication#9e904017).<br><br>**Recommend Premium**<br><br>BytePlus Recommend SaaS Premium uses token header authentication.<br><br>For more information on using the SDK token authentication, refer [here](https://docs.byteplus.com/en/recommend/reference/api_token_authentication). |


<span id="1dad2339"></span>
## Body

The following table details the body parameters required for the WriteProducts API.


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|project_id |String |Yes |851467130 |The unique identifier for the Recommend project. |
|stage |String |Yes |production |The data import stage corresponds to the stages in the BytePlus Recommend Console. Accepted values for this stage include:<br><br><br>* production: this indicates the historical data synchronization stage, where the data is used for training the model.<br><br>* incremental_sync_streaming: this indicates the incremental real\-time data synchronization stage, where data is used to update the model in real\-time. |
|data |Array of Strings |Yes |*  |This is an array of product data where the field names and field types align with the Schema defined in the BytePlus Recommend Console. Each element in the array represents a single data record and is serialized as a JSON string. When using the Write APIs to send data, you should serialize the following JSON array into a string:<br><br>```JSON```<br>```[```<br>``` {```<br>```   "product_id": "632461",```<br>```   "categories": "[{\"category_depth\":1,\"category_nodes\":[{\"id_or_name\":\"Shoes\"}]},{\"category_depth\":2,\"category_nodes\":[{\"id_or_name\":\"Mens Shoes\"}]}]",```<br>```   "brands": "Adidas",```<br>```   "is_recommendable": 1,```<br>```   "title": "adidas Mens Yeezy Boost 350 V2 Grey/Borang/Dgsogr",```<br>```   "current_price": 499.50,```<br>```   "original_price": 699.50,```<br>```   "tags": "[\"New Product\",\"Summer Product\"]",```<br>```   "display_cover_multimedia_url": "[\"www.demo.jpg\"]",```<br>```   "seller_id": "43485",```<br>```   "seller_level": "1",```<br>```   "seller_rating": 3.5,```<br>```   "product_group_id": "1356",```<br>```   "user_rating": 0.25,```<br>```   "comment_count": 100,```<br>```   "source": "self",```<br>```   "publish_timestamp": 1623193487,```<br>```   "sold_count": 10```<br>``` }```<br>```]```<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The format of this parameter should match the schema you defined in the BytePlus Recommend Console.</div><br> |
|extra |Map<String, String\> |No |*  |This is a field for additional information. You should provide as much information as possible. |


<span id="d00b1567"></span>
### Extra

This is a field for additional information. It contains the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|newKey |String |*  |*  |*  |
|New Value |String |*  |*  |*  |


<span id="0ce09166"></span>
# Response parameters

The following tables details the response parameters for the WriteProducts API.


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|status |Object |*  |This field defines an error model. It contains two types of data: error code and error message. |
|errors |Array of Objects |*  |This field is populated when the status is an error code: 1001. |


<span id="8c61d0b1"></span>
## **Status**

The `status` defines an error model. Each `status` message contains two types of data: error code and error message.


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|code |Int32 |0 |You should look at this response parameter to determine if your API request was successful or not. The accepted values include:<br><br><br>* 0: it indicates that the calling is successful.<br><br>* 4xx: it indicates user error.<br><br>* 5xx: it indicates server error.<br><br>* 1xxx: it indicates error relating to Import calls.<br><br>* 2xxx: it indicates errors relating to Predict calls. |
|message |String |An unexpected value XXX is included in the XXX field, only ["xx", "yy", "zz"] can be accepted. |Provides a detailed error message on the reasons why your API request was unsuccessful. |


<span id="7883d404"></span>
### Samples

The following tables details the response parameters for the WriteProducts API:

<span id="fb01f45e"></span>
## Sample request

The following is a sample request for the API.

```JSON
curl --request POST \
     --url https://rec-api-sg1.recplusapi.com/RetailSaaS/WriteProducts \
     --header 'Tenant-Id: 3000001813' \
     --header 'Request-Id:123132089' \
     --header 'accept: application/json' \
     --header 'content-type: application/json' \
     --data '
{
  "project_id": "851467130",
  "stage": "production",
  "data": [
    "{\"product_id\": \"632461\", \"categories\": \"[{\\\"category_depth\\\":1,\\\"category_nodes\\\":[{\\\"id_or_name\\\":\\\"Shoes\\\"}]},{\\\"category_depth\\\":2,\\\"category_nodes\\\":[{\\\"id_or_name\\\":\\\"Mens Shoes\\\"}]}]\", \"brands\": \"Adidas\", \"is_recommendable\": 1, \"title\": \"adidas Mens Yeezy Boost 350 V2 Grey/Borang/Dgsogr\", \"current_price\": 499.5, \"original_price\": 699.5, \"tags\": \"[\\\"New Product\\\",\\\"Summer Product\\\"]\", \"display_cover_multimedia_url\": \"[\\\"www.demo.jpg\\\"]\", \"seller_id\": \"43485\", \"seller_level\": \"1\", \"seller_rating\": 3.5, \"product_group_id\": \"1356\", \"user_rating\": 0.25, \"comment_count\": 100, \"source\": \"self\", \"publish_timestamp\": 1623193487, \"sold_count\": 10}"
  ]
}
'
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


The following is a **failed** sample response due to authentication failure.

```JSON
{ 
  "status": { 
    "code": 401, 
    "message": "auth fail, need signature; errID:1225400911 logID:202304041005450A6279A8AAA75F41B1A1" 
  } 
}
```


The following is **failed** sample response if the data entries exceed 2000.

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
      "data": "{\"quality_score\":4.4,\"tags\":\"[\\\"New Product\\\",\\\"Summer Product\\\"]\",\"seller_id\":\"43485\",\"seller_seller_level\":\"1\",\"seller_seller_rating\":3.5,\"product_spec_publish_timestamp\":1623193487,\"brands\":\"Adidas\",\"is_recommendable\":1,\"display_listing_page_display_type\":\"image\",\"display_detail_page_display_tags\":\"[\\\"FreeShipping\\\",\\\"Return in 7 days without any reasons\\\"]\",\"product_spec_comment_count\":100,\"price_current_price\":49900,\"display_cover_multimedia_url\":\"https://images-na.ssl-images-amazon.com/images/I/81WmojBxvbL._AC_UL1500_.jpg\",\"product_spec_user_rating\":0.25,\"category\":\"[{\\\"category_depth\\\":1,\\\"category_nodes\\\":[{\\\"id_or_name\\\":\\\"Shoes\\\"}]},{\\\"category_depth\\\":2,\\\"category_nodes\\\":[{\\\"id_or_name\\\":\\\"Men Shoes\\\"}]}]\",\"display_listing_page_display_tags\":\"[\\\"best seller\\\",\\\"hot sales\\\"]\",\"price_origin_price\":69900,\"product_spec_product_group_id\":\"1356\",\"product_spec_source\":\"self\",\"product_id\":\"\",\"title\":\"adidas Men Yeezy Boost 350 V2 Grey/Borang/Dgsogr\"}"
    }
  ]
}
```


<span id="9398e94b"></span>
# Error codes

For more information on the API error codes, refer to [BytePlus Recommend shared error and status codes](https://docs.byteplus.com/recommend/reference/shared_error_and_status_codes).

&nbsp;
