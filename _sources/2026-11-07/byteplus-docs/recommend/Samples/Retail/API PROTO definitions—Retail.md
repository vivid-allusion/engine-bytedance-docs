---
title: "API PROTO definitions—Retail"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/samples-retail_api_proto_definitions"
---

This reference guide contains the API PROTO definitions for the Retail Industry saas.proto and the scalar value types used in the .proto file.

<span id="saas.proto"></span>
# saas.proto

This section documents the PROTO definitions for saas.proto.

<span id="AckServerImpressionsRequest"></span>
## AckServerImpressionsRequest

The request proto for the AckServerImpressions API contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|project_id |string | |Required.<br><br>The unique identifier for the recommendation project. |
|model_id |string | |Required.<br><br>The unique identifier for the recommendation model used. |
|predict_request_id |string | |Required.<br><br>The unique identifier for the API request.<br><br>The value should be same as PredictRequest.request_id. |
|user_id |string | |Required.<br><br>The unique identifier for the user.<br><br>The value should be same as PredictRequest.user_id. |
|traffic_source |string | |Required.<br><br>The source of the recommendation.<br><br>The accepted values are:<br><br><br>* self—indicates that the recommendation came from the caller's own engine.<br><br>* byteplus—indicates that the recommendation came from BytePlus.<br><br>* other—indicates that the recommendation came from a third\-party engine. |
|scene |Scene | |Required.<br><br>The recommendation scene information.<br><br>Ensure that this is as close to UserEvent.scene as possible. |
|altered_products |AckServerImpressionsRequest.AlteredProduct |repeated |Required.<br><br>The list of altered products. |


<span id="AckServerImpressionsRequest.AlteredProduct"></span>
## AckServerImpressionsRequest.AlteredProduct

AckServerImpressionsRequest.AlteredProduct contains information about a product that has been altered in the recommendation result. Its proto contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|product_id |String | |Required.<br><br>The unique identifier for the product.<br><br>The value is same as Product.product_id. |
|altered_reason |String | |Required.<br><br>The product's final state.<br><br>The accepted values are:<br><br><br>* kept—indicates that the product was included in the actual impression.<br><br>* filtered—indicates that the product was filtered out of the actual impression by your platform's logic.<br><br>* inserted—indicates that the product was inserted into the actual impression by your platform's logic. |
|rank |Int32 | |Required.<br><br>The product's final recommendation ranking.<br><br>If the value is unset or 0, it is assumed that the product is filtered out from the actual impression. |


<span id="AckServerImpressionsResponse"></span>
## AckServerImpressionsResponse

The response message for the AckServerImpressions API contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|status |Status | |Output only.<br><br>The API call response status. |


<span id="DataError"></span>
## DataError

DataError contains a summary of error messages returned in a Write API response. Its proto contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|message |String | |Output only.<br><br>The detailed error message, which should be in English.<br><br>For example, "An unexpected value XXX is included in the XXX field. Only ["xx", "yy", "zz"] can be accepted." |
|data |String | |Output only.<br><br>The specific abnormal data. |


<span id="Device"></span>
## Device

The device proto contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|platform |String | |Required.<br><br>The platform used by the user.<br><br>The accepted values are:<br><br><br>* app<br><br>* desktop\-web<br><br>* mobile\-web<br><br>* other |
|os_type |String | |Optional.<br><br>The operating system used by the user.<br><br>The accepted values are:<br><br>android<br><br>ios<br><br>windows<br><br>other |
|app_version |String | |Optional.<br><br>The application version.<br><br>For example, "V9.0.8". |
|device_model |String | |Optional.<br><br>The device model used by the user.<br><br>For example, "iPhone 10", "Pixel 4". |
|device_brand |String | |Optional.<br><br>The brand of the device used by the user.<br><br>For example, "Samsung". |
|os_version |String | |Optional.<br><br>The operating system version used by the user.<br><br>For example, "14.4.2". |
|browser_type |String | |Optional.<br><br>The type of browser used by the user.<br><br>For example, "Chrome", "Firefox", and so on. |
|user_agent |String | |Optional.<br><br>The UserAgent for the browser. |
|network |String | |Optional.<br><br>The network used by the user.<br><br>The accepted values are:<br><br><br>* 2G<br><br>* 3G<br><br>* 4G<br><br>* 5G<br><br>* WIFI<br><br>* Other |


<span id="PredictRequest"></span>
## PredictRequest

The request proto for the Predict API contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|project_id |String | |Required.<br><br>The unique identifier for the recommendation project. |
|model_id |String | |Required.<br><br>The unique identifier for the recommendation model used. |
|user_id |String | |Required.<br><br>The unique identifier for the user.<br><br>The value is same as User.user_id. |
|size |Int32 | |Required.<br><br>The maximum number of products returned.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The actual number of products returned is the minimum of the following numbers\*:\*</div><br><br><br><div data-tips="true" data-tips-type="tip">siz<em>e</em></div><br><br><br><div data-tips="true" data-tips-type="tip">length(context.candidate_product_ids\*)\*</div><br><br><br><div data-tips="true" data-tips-type="tip">Total number of products with is_recommendable=<em>1</em></div><br> |
|scene |Scene | |Optional.<br><br>The recommendation scene information. |
|context |PredictRequest.Context | |Optional.<br><br>The context of the current Predict request. |
|extra |PredictRequest.ExtraEntry |repeated |Optional.<br><br>A catch\-all field to pass any additional information.<br><br>You should provide as much information as possible using this field. |


<span id="PredictRequest.Context"></span>
## PredictRequest.Context

PredictRequest.Context contains the context of a Predict API request. Its proto contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|root_product |Product | |Optional.<br><br>The parent product information, if any. The parent product refers to the product whose details page contains the recommended product that the user has seen or clicked on.<br><br>This field is only required for the product details page. |
|device |Device | |Optional.<br><br>The device information.<br><br>Ensure that the value is as close to UserEvent.device as possible. |
|candidate_product_ids |String |repeated |Optional.<br><br>The list of candidates for recommendation.<br><br>If this field is empty, all products are candidates. |


<span id="PredictRequest.ExtraEntry"></span>
## PredictRequest.ExtraEntry

PredictRequest.ExtraEntry contains additional information for a Predict API request. Its proto contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|key |String | |Key. |
|value |String | |Value. |


<span id="PredictResponse"></span>
## PredictResponse

The response message for the Predict API contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|status |Status | |Output only.<br><br>The API call response status. |
|request_id |String | |Output only.<br><br>The unique identifier for the API request.<br><br>The value is same as PredictRequest.request_id. |
|value |PredictResult | |Output only.<br><br>The API result.<br><br>This field is only populated when PredictResponse.status.code is 0. |


<span id="PredictResult"></span>
## PredictResult

PredictResult contains a single Predict API call result. Its proto contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|response_products |PredictResult.ResponseProduct |repeated |Output only.<br><br>The list of predicted products. |
|extra |PredictResult.ExtraEntry |repeated |Output only.<br><br>A catch\-all field that returns any additional information, typically for debugging. |


<span id="PredictResult.ExtraEntry"></span>
## PredictResult.ExtraEntry

PredictResult.ExtraEntry contains additional information for a Predict API call result. Its proto contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|key |String | |Key. |
|value |String | |Value. |


<span id="PredictResult.ResponseProduct"></span>
## PredictResult.ResponseProduct

PredictResult.ResponseProduct contains the product information of a single recommendation in a Predict API call result. Its proto contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|product_id |String | |Output only.<br><br>The unique identifier for the product.<br><br>The value is consistent with Product.product_id. |
|rank |Int32 | |Output only.<br><br>The product's recommendation ranking. |
|pctr |Double | |Output only.<br><br>The predicted Click\-Through Rate (CTR). |
|pcvr |Double | |Output only.<br><br>The predicted Conversion Rate (CVR). |
|rec_info |String | |Output only.<br><br>The strategy used for this particular recommendation result. |
|extra |PredictResult.ResponseProduct.ExtraEntry |repeated |Output only.<br><br>A catch\-all field that returns any additional information, typically for debugging. |


<span id="PredictResult.ResponseProduct.ExtraEntry"></span>
## PredictResult.ResponseProduct.ExtraEntry

PredictResult.ResponseProduct.ExtraEntry contains additional information for a Predict API call result response. Its proto contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|key |String | |Key. |
|value |String | |Value. |


<span id="Product"></span>
## Product

The product proto contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|product_id |String | |Required.<br><br>The unique identifier for the product. |
|categories |Product.Category |repeated |Required.<br><br>The product category.<br><br>The order of its depth should be ascending. For example, if a product is categorized as "Shoes \> Men's Shoes \> Basketball Shoes", the JSON array looks like the following:<br><br>```JSON```<br>```[```<br>``` {"category_depth":1,```<br>``` "category_nodes": [{"id_or_name":"Shoes"}] },```<br>``` {"category_depth":2,```<br>``` "category_nodes": [{"id_or_name":"Men's Shoes"}] },```<br>``` {"category_depth":3,```<br>``` "category_nodes": [{"id_or_name":"Basketball Shoes"}] },```<br>```]```<br><br><br>If a product belongs to two different categories, "Shoes \> Men's shoes" and "Sports \> Basketball", the JSON array looks like the following:<br><br>```JSON```<br>```[```<br>```{"category_depth":1,```<br>``` "category_nodes": [{"id_or_name":"Shoes"},```<br>``` {"id_or_name":"Sports"}] },```<br>``` {"category_depth":2,```<br>``` "category_nodes": [{"id_or_name":"Men's shoes"},```<br>``` {"id_or_name":"Basketball"}] },```<br>```]```<br><br><br>You should provide as much information as possible because missing values for this field will significantly affect recommendation performance. |
|brands |Product.Brand |repeated |Required.<br><br>The product brand.<br><br>The order of its depth should be ascending. For example, if a product belongs to "Adidas \> Yeezy", this field should look like the following:<br><br>```Plain```<br>```[```<br>```{"brand_depth": 1, "id_or_name":"Adidas"},```<br>``` {"brand_depth": 2, "id_or_name":"Yeezy"},```<br>```]```<br><br><br>Missing values for this field will significantly affect recommendation performance. |
|price |Product.Price | |Required.<br><br>The product price information.<br><br>Ensure that the value is accurate and recent. |
|is_recommendable |Bool | |Required.<br><br>Whether the product is recommendable.<br><br>The value is 1 if the product is recommendable and may appear in a Predict call result.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Changes to this value take up to 1 hour to take effect.</div><br><br><br><div data-tips="true" data-tips-type="tip">Even if the product is not recommendable, you should still send the product's information to BytePlus Recommend. Given that users may still interact with such products, such as viewing its details page, the product information provides strong signals about the user's preference.</div><br> |
|title |String | |Required.<br><br>The product title. |
|quality_score |Double | |Optional.<br><br>The product quality score.<br><br>The value is normalized to [0.0, 5.0].<br><br>***Note:* ** <br><br>*This field is different from user ratings. quality_score is normally computed as a composite score considering many factors, including sales, customer feedback, information completeness, and so on.*  |
|tags |String |repeated |Optional.<br><br>The tags given by the seller for the product.<br><br>For example, "New", "Summer", "Clearance", and so on.<br><br>This field is used to improve the recommendation performance. |
|display |Product.Display | |Optional.<br><br>The product display information. |
|product_spec |Product.ProductSpec | |Optional.<br><br>The product specifications. |
|seller |Product.Seller | |Optional.<br><br>The seller's information. |
|extra |Product.ExtraEntry |repeated |Optional.<br><br>A catch\-all field to pass any additional information.<br><br>You should provide as much information as possible using this field. |


<span id="Product.Brand"></span>
## Product.Brand

The brand proto contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|brand_depth |Int32 | |Required.<br><br>The brand depth, which is consecutive and ascending. |
|id_or_name |String | |Required.<br><br>The unique identifier or name for the brand at this depth. |


<span id="Product.Category"></span>
## Product.Category

The category proto contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|category_depth |Int32 | |Required.<br><br>The category depth, which is consecutive and ascending. |
|category_nodes |Product.Category.CategoryNode |repeated |Required.<br><br>The category nodes that belong to the same depth. |


<span id="Product.Category.CategoryNode"></span>
## Product.Category.CategoryNode

Product.Category.CategoryNode contains the information of a single node of a category. Its proto contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|id_or_name |String | |Required.<br><br>The unique identifier for the category. |


<span id="Product.Display"></span>
## Product.Display

Product.Display contains the product display information. Its proto contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|listing_page_display_tags |String |repeated |Optional.<br><br>The tags visible to the users on the listing page.<br><br>For example, "best seller", "hot sales", and so on.<br><br>You should fill in this field as much as possible. |
|detail_page_display_tags |String |repeated |Optional.<br><br>The tags visible to the users on the product details page.<br><br>For example, "free shipping", "1 year guarantee", and so on.<br><br>You should fill in this field as much as possible. |
|listing_page_display_type |String | |Optional.<br><br>The product display media type on the listing page.<br><br>The accepted values are:<br><br><br>* image<br><br>* video<br><br>* other |
|cover_multimedia_url |String | |Optional.<br><br>The URL of the product's associated multimedia on the listing page, if any. |


<span id="Product.ExtraEntry"></span>
## Product.ExtraEntry

Product.ExtraEntry contains additional product information. Its proto contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|key |String | |Key. |
|value |String | |Value. |


<span id="Product.Price"></span>
## Product.Price

The price proto contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|current_price |Int64 | |Required.<br><br>The current price in cents.<br><br>For example, $100.12 should be "10012". |
|origin_price |Int64 | |Required.<br><br>The original price in cents.<br><br>For example, $100.12 should be "10012". |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the products need to be ranked together, ensure that their prices are in the same currency.</div>


<span id="Product.ProductSpec"></span>
## Product.ProductSpec

Product.ProductSpec contains the detailed product specifications. Its proto contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|product_group_id |String | |Required.<br><br>The unique identifier for the product group.<br><br>For example, a beer product might have a 6\-pack, 12\-pack, and so on. Each product variation has a different product_id, but all of them will have the same product_group_id. |
|user_rating |Double | |Optional.<br><br>The product rating given by users.<br><br>The value is normalized to [0.0, 5.0]. |
|comment_count |Int32 | |Optional.<br><br>The number of comments for the product. |
|source |String | |Optional.<br><br>The product source.<br><br>The accepted values are:<br><br><br>* Self<br><br>* Third party<br><br>* Other |
|publish_timestamp |Int64 | |Optional.<br><br>The timestamp when the product is published for sale. |


<span id="Product.Seller"></span>
## Product.Seller

Product.Seller contains the seller's information. Its proto contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|id |String | |Required.<br><br>The unique identifier for the seller. |
|seller_level |String | |Optional.<br><br>The seller's level.<br><br>For example, "gold", "silver", and so on. |
|seller_rating |Double | |Optional.<br><br>The seller's rating.<br><br>The value is normalized to [0.0, 5.0]. |


<span id="Scene"></span>
## Scene

Scene refers to the location where the user interaction event happened. The scene proto contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|scene_name |String | |Optional.<br><br>The unique identifier for the scene.<br><br>For example, "home_page", "category_page", "product_detail_page", "shopping_cart", "purchase_complete", and so on.<br><br>The value is determined by the scene specified during model training.<br><br>***Note:* ** <br><br>*It is strongly recommended that you use one recommendation model per scene if possible.*  |
|page_number |Int32 | |Optional.<br><br>The page number.<br><br>This field can refer to:<br><br><br>* the page number that the product is found on.<br><br>* the number of times that users swipe the screen before seeing the product.<br><br><br>The default value is 0, which indicates that all products fit into a single page. |
|offset |Int32 | |Optional.<br><br>The product's position within the page itself. |


<span id="Status"></span>
## Status

Status defines a logical error model. The status proto contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|code |Int32 | |Output only.<br><br>The response code, which could be a success code or an error code. Users should expect this field for all responses.<br><br>The possible values are:<br><br><br>* 0—indicates that the request is successfully returned.<br><br>* xxx—3\-digit error codes, which align with standard HTTP error codes. For example, 4xx indicates user error while 5xx indicates server error.<br><br>* 2xxx—indicates errors related to Predict calls.<br><br><br>For more information, refer to Error codes. |
|message |String | |Output only.<br><br>The detailed error message. |


<span id="WriteDataRequest"></span>
## WriteDataRequest

The request proto for the Write APIs contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|project_id |String | |Required.<br><br>The unique identifier for the recommendation project. |
|stage |String | |Required.<br><br>The data import stage, corresponding to stages in the Recommendation Console.<br><br>The possible values are:<br><br><br>* trial—indicates the test data/pre\-synchronization stage, where data is only used for testing.<br><br>* production—indicates the historical data synchronization stage, where data is used to train the model.<br><br>* incrementalRealtime—indicates the incremental real\-time data synchronization stage, where data is used to update the model in real\-time.<br><br>* incrementalDaily—indicates the incremental daily data synchronization stage, where data is used to update the model daily. |
|data |String |repeated |Required.<br><br>An array where each element is a JSON serialized string of data representing one data record. For example, to send data using the Write APIs, the following JSON array should be serialized into a string:<br><br>```JSON```<br>```[```<br>``` {```<br>``` "user_id": "1457789",```<br>``` "gender": "male",```<br>``` "age": "23",```<br>``` "tags": "[\"new user\",\"low purchasing power\",\"bargain seeker\"]",```<br>``` "activation_channel": "AppStore",```<br>``` "membership_level": "silver",```<br>``` "registration_timestamp": 1623593487,```<br>``` "location_city": "Kirkland",```<br>``` "location_country": "USA",```<br>``` "location_district_or_area": "King County",```<br>``` "location_postcode": "98033",```<br>``` },```<br>``` {```<br>```  "user_id": "1457790",```<br>``` "gender": "female",```<br>``` "age": "20-40",```<br>``` "tags": "[\"new user\"]",```<br>``` "activation_channel": "AppStore",```<br>``` "membership_level": "silver",```<br>``` "registration_timestamp": 1623593490,```<br>``` "location_city": "Kirkland",```<br>``` "location_country": "USA",```<br>``` "location_district_or_area": "King County",```<br>``` "location_postcode": "98033",```<br>``` },```<br>```]```<br> |
|extra |WriteDataRequest.ExtraEntry |repeated |Optional.<br><br>A catch\-all field to pass any additional information.<br><br>You should provide as much information as possible using this field. |


<span id="WriteDataRequest.ExtraEntry"></span>
## WriteDataRequest.ExtraEntry

WriteDataRequest.ExtraEntry contains additional information for a Write API request. Its proto contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|key |String | |Key. |
|value |String | |Value. |


<span id="WriteResponse"></span>
## WriteResponse

The response message for the Write APIs contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|status |Status | |Output only.<br><br>The API call response status.<br><br>If status.code is 0, it indicates that no exception occurred during execution and the full data import has been successful. |
|errors |DataError |repeated |Output only.<br><br>The summary of error messages for when the data import fails.<br><br>This field contains a value when status.code is 1206. Even if this field contains no value, the data import is unsuccessful when status.code is not 0. |


<span id="BytePlusSaasService"></span>
## BytePlusSaasService

The BytePlus Recommend SaaS service contains the following APIs:


|**Method Name** |**Request Type** |**Response Type** |**Description** |
|---|---|---|---|
|WriteUsers |WriteDataRequest |WriteResponse |Batch writes User information up to 2,000 data entries in a single request. Exceeding 2,000 entries in a request results in a rejection.<br><br>You can use this method to upload new data or to update existing data. |
|WriteProducts |WriteDataRequest |WriteResponse |Batch writes Product information up to 2,000 data entries in a single request. Exceeding 2,000 entries in a request results in a rejection.<br><br>You can use this method to upload new data or to update existing data. |
|WriteUserEvents |WriteDataRequest |WriteResponse |Batch writes UserEvent information up to 2,000 data entries in a single request. Exceeding 2,000 entries in a request results in a rejection.<br><br>You can use this method to upload new data only. The method does not support updating existing data. |
|Predict |PredictRequest |PredictResponse |Gets the ranked list of products.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Any incremental User data will take effect in 24 hours. Any incremental Product data will take effect in 30 minutes. Depending on how the incremental UserEvent data is imported (in real\-time or in batch), it will be fed into the model and take effect afterwards.</div><br> |
|AckServerImpressions |AckServerImpressionsRequest |AckServerImpressionsResponse |Sends back to the server the actual products shown to the user, which may differ from the list of products in the PredictResponse.<br><br>For example, the Predict API returns a list of items [1, 2, 3, 4], but your platform logic has filtered product 3 because it has been sold out and inserted product 10 before product 2 based on a promotion rule. The AckServerImpressionsRequest will look like the following:<br><br>```Plain```<br>```[```<br>``` {id:1, altered_reason: "kept", rank:1},```<br>``` {id:10, altered_reason: "inserted", rank:2},```<br>``` {id:2, altered_reason: "kept", rank:3},```<br>``` {id:4, altered_reason: "kept", rank:4},```<br>``` {id:3, altered_reason: "filtered", rank:0},```<br>```]```<br> |


<span id="Methods with HTTP bindings"></span>
### Methods with HTTP bindings

The BytePlus Recommend APIs have the following HTTP bindings:


|**Method Name** |**Method** |**Path** |**Body** |
|---|---|---|---|
|WriteUsers |POST |/RetailSaaS/WriteUsers |*  |
|WriteProducts |POST |/RetailSaaS/WriteProducts |*  |
|WriteUserEvents |POST |/RetailSaaS/WriteUserEvents |*  |
|Predict |POST |/RetailSaaS/Predict |*  |
|AckServerImpressions |POST |/RetailSaaS/AckServerImpressions |*  |


<span id="Scalar value types"></span>
# Scalar value types

This section documents the scalar value types specified in the .proto file and their corresponding types in various programming languages:


| **.proto Type** |**Notes** |**C++ Type** |**Java Type** |**Python Type** |**Go Type** |**C# Type** |**PHP Type** |**Ruby Type** |
|---|---|---|---|---|---|---|---|---|
|Double |*  |Double |Double |Float |Float64 |Double |Float |Float |
|Float |*  |Float |Float |Float |Float32 |Float |Float |Float |
|Int32 |Uses variable\-length encoding. Inefficient for encoding negative numbers. If your field is likely to have negative values, use sint32 instead. |Int32 |Int |Int |Int32 |Int |Integer |Bignum or Fixnum (as required) |
|Int64 |Uses variable\-length encoding. Inefficient for encoding negative numbers. If your field is likely to have negative values, use sint64 instead. |Int64 |Long |Int/Long |Int64 |Long |Integer/<br><br>String |Bignum |
|Uint32 |Uses variable\-length encoding. |Uint32 |Int |Int/Long |Uint32 |Uint |Integer |Bignum or Fixnum (as required) |
|Uint64 |Uses variable\-length encoding. |Uint64 |long |Int/Long |Uint64 |Ulong |Integer/<br><br>String |Bignum or Fixnum (as required) |
|Sint32 |Uses variable\-length encoding. Signed int value. Encodes negative numbers more efficiently than regular int32. |Int32 |Int |Int |Int32 |Int |Integer |Bignum or Fixnum (as required) |
|Sint64 |Uses variable\-length encoding. Signed int value. Encodes negative numbers more efficiently than regular int64. |Int64 |Long |Int/Long |Int64 |Long |Integer/<br><br>String |Bignum |
|Fixed32 |Always four bytes. More efficient than uint32 if values are often greater than 2^28. |Uint32 |Int |Int |Uint32 |Uint |Integer |Bignum or Fixnum (as required) |
|Fixed64 |Always eight bytes. More efficient than uint64 if values are often greater than 2^56. |Uint64 |Long |Int/Long |Uint64 |Ulong |Integer/<br><br>String |Bignum |
|Sfixed32 |Always four bytes. |Int32 |Int |Int |Int32 |Int |Integer |Bignum or Fixnum (as required) |
|Sfixed64 |Always eight bytes. |Int64 |Long |Int/Long |Int64 |Long |Integer/<br><br>String |Bignum |
|Bool |*  |Bool |Boolean |Boolean |Bool |Bool |Boolean |TrueClass/<br><br>FalseClass |
|String |Must always contain UTF\-8 encoded or 7\-bit ASCII text. |String |String |Str/<br><br>Unicode |String |String |String |String (UTF\-8) |
|Bytes |May contain any arbitrary sequence of bytes. |String |ByteString |Str |[]Byte |ByteString |String |String (ASCII\-8BIT) |
