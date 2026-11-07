---
title: "Predict—Recommend Retail Industry"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/reference-retail_predict"
---

The Predict API enables updating and ranking of product lists in the Retail/E\-commerce industry for BytePlus Recommend. User data takes effect within 24 hours, while product data has an impact in just 30 minutes. By compiling and utilizing UserEvent data, the API refines recommendation results for improved user experiences.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information on BytePlus Recommend token authentication, refer <a href="https://docs.byteplus.com/en/recommend/reference/api_token_authentication">here</a>.</div>


<span id="36c7c3c1"></span>
# HTTP request


|**URL** |https://rec\-ap\-singapore\-1.byteplusapi.com/predict/api/retail/${tenant}/$ |
|---|---|
|**Method** |POST |


<span id="d5e9f3b3"></span>
# Request parameters

The topics below details the parameters required for the Predict API.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Not all request parameters are included in the following table. For a complete list, refer to <a href="https://docs.byteplus.com/recommend/reference/api_token_authentication">HTTP header parameters</a>.</div>


<span id="1dad2339"></span>
## Body

The following table details the body parameters required for the Predict API:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|user_id |String |Yes |1457789 |The unique identifier for the user.<br><br>The value is same as `User.user_id`. |
|size |Int32 |Yes |20 |The maximum number of products returned. The actual number of products returned is the minimum of the following numbers:<br><br><br>* `size`<br><br>* length(`context.candidates_product_ids`)<br><br>* total number of products with `is_recommendable`= True |
|scene |Object |*  |*  |The recommendation scene information. |
|context |Object |*  |*  |The context of the current Predict request. |
|extra |Object |No |*  |This field is used to pack key\-value pairs. For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |


<span id="715fcc00"></span>
### **Scene**

Scene refers to the location where the user interaction event happened. It contains the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|scene_name |String |Yes |product_detail_page |The name of the scene the UserEvent occurred in. It's the unique identifier for the scene. The value will be determined by the scene specified when training the current recommendation model. The accepted values include:<br><br><br>* home_page<br><br>* category_page<br><br>* product_detail_page<br><br>* shopping_cart<br><br>* purchase_complete<br><br><br>It is strongly recommended that you split the scene if possible. |
|page_number |Int32 |No |1 |The page number.<br><br>This field can refer to:<br><br><br>* the page number that the content is found on.<br><br>* the number of times that users swipe the screen before seeing the content.<br><br><br>The default value is 0, which indicates that all content fits into a single page. |
|offset |Int32 |No |10 |The content's position within the page itself. |


<span id="90698130"></span>
### **Context**

Context refers to the context of a Predict API request. The context proto contains the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|root_product |Object |*  |*  |The parent product information, if any. The parent product refers to the products whose details page contains the recommended product the user has seen or clicked on.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This field is only required for the product details page.</div><br> |
|device |Object |*  |app |The platform used by a user to access the product. The accepted values are:<br><br><br>* app<br><br>* desktop\-web<br><br>* mobile\-web<br><br>* other |
|candidate_product_ids |Array of Strings |No |*  |The list of candidates for the product recommendation. If this value is empty, it means all products are the candidates. |


<span id="5876ab59"></span>
#### Root_product

The parent product information, if any. The parent product refers to the products whose details page contains the recommended product the user has seen or clicked on. This parameter contains the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|product_id |String |Yes | |The unique identifier for the product. |
| | | | | |
|brands |Array of objects |Yes | |You must sort the brands by their brand_depth in ascending order. For example, if a product belongs to "Adidas \-\> Yeezy", the value should look like this: |



|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|product_id |String |Yes |632461 |The unique identifier for the recommended product. |
|categories |Array of Objects |Yes |[<br><br>{"category_depth":1, "category_nodes": [{"id_or_name":"Shoes"}] },<br><br>{"category_depth":2, "category_nodes": [{"id_or_name":"Men's Shoes"}] },<br><br>{"category_depth":3, "category_nodes": [{"id_or_name":"Basketball Shoes"}] },<br><br>] |The categories that the product belongs to. The category value is a JSON serialized string.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you do not fill in this parameter, the accuracy and efficiency of the product recommendations will be affected.</div><br><br><br>If a product belongs to a single category, like "Shoes \-\> Men's Shoes \-\> Basketball Shoes", the value should look like this:<br><br>```JSON```<br>```[```<br>```{"category_depth":1, "category_nodes": [{"id_or_name":"Shoes"}] },```<br>```{"category_depth":2, "category_nodes": [{"id_or_name":"Men's Shoes"}] },```<br>```{"category_depth":3, "category_nodes": [{"id_or_name":"Basketball Shoes"}] },```<br>```]```<br><br><br>If a product belongs to two different categories, like "Shoes \-\> Men's shoes" and "Sports \-\> Basketball", then the value should look like this:<br><br>```JSON```<br>```[```<br>```{"category_depth":1, "category_nodes": [{"id_or_name":"Shoes"}, {"id_or_name":"Men's shoes"}] },```<br>```{"category_depth":2, "category_nodes": [{"id_or_name":"Sports"}, {"id_or_name":"Basketball"}] },```<br>```]```<br> |
|brands |Array of Objects |Yes |[<br><br>{"brand_depth": 1, "id_or_name":"Adidas"},<br><br>{"brand_depth": 2, "id_or_name":"Yeezy"},<br><br>] |The brands that the product belongs to. You must sort the brands by their brand_depth in ascending order.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you do not fill in this parameter, the accuracy and efficiency of the product recommendations will be affected.</div><br><br><br>If a product belongs to "Adidas \-\> Yeezy", this value should look like this:<br><br>```JSON```<br>```[```<br>```{"brand_depth": 1, "id_or_name":"Adidas"},```<br>```{"brand_depth": 2, "id_or_name":"Yeezy"},```<br>```]```<br> |
|price |Object |*  |*  |The price proto. You must ensure that the products that need to be ranked are priced using the same currency. |
|is_recommendable |Boolean |Yes |True |This field determines if the product should be recommended to the user.<br><br>The accepted values are:<br><br><br>* True—The product should be recommended to users.<br><br>* False—The product should not be recommended to users.<br><br><br>Even if a product is not recommended to your users, you must submit this parameter to us. Users might have interacted with this product before, and this information allows us to provide more accurate recommendations.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Any change made to this value will take up to 1 hour to take effect.</div><br> |
|title |String |Yes |Grey Shoes 100 |The product title. You can use the text name of the product or the title on the HTML page. |
|quality_score |Double |No |4.4 |The product quality score given by the seller.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Quality_score is different from user ratings. It is normally computed as a composite score considering many factors, including sales, customer feedback, information completeness and so on.</div><br><br><br>The value range should be between 1.0 and 5.0. |
|tags |Array of Strings |No |New Product |The tags given by the seller for this product. It is used to improve performance.<br><br>For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |
|display |Object |*  |*  |The display information about the product. |
|product_spec |Object |*  |*  |The detailed product specs. |
|seller |Object |*  |*  |The seller' information. |
|extra |Object |No |*  |This is a field that is used to pack key\-value pairs.<br><br>For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |


<span id="0d664259"></span>
##### **Categories**

This field refers to the categories that the product belongs to. It contains the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|category_depth |Int32 |Yes |1 |The depth of the category. The value is consecutive and ascending. |
|category_nodes |Array of Objects |Yes |Shoes |The category nodes belong to the same depth. |


<span id="4207fbaa"></span>
###### Category_nodes

This field provides information on the category nodes for the product. It contains the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|id_or_name |String |Yes |Shoes |The unique identifier for the category. For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |


<span id="25b8b6cc"></span>
##### **Brands**

This parameter refers to the brand(s) that the product belongs to. It contains the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|brand_depth |Int32 |Yes |1 |The brand's depth. The value is consecutive and ascending. |
|id_or_name |String |Yes |Grey Shoes 100 |The ID or name of the brand at this depth. |


<span id="a1937536"></span>
##### **Price**

The price proto. It contains the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|current_price |Int64 |Yes |49900 |Enter the current price of the product in cents.<br><br>For example, $100.12 = 10012. |
|origin_price |Int64 |Yes |69900 |Enter the original price of the product in cents.<br><br>For example, $100.12 = 10012. |


<span id="b75466e1"></span>
##### **Display**

This parameter refers to the display information about the product. It contains the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|listing_page_display_tags |Array of Strings |No |best seller |The tags shown to users on the listing page. You should fill in this field as much as possible.<br><br>The accepted values include:<br><br><br>* best seller<br><br>* hot sales<br><br><br>For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |
|detail_page_display_tags |Array of Strings |No |FreeShipping |The tags shown to users on the details page. You should fill in this field as much as possible.<br><br>The accepted values include:<br><br><br>* free shipping<br><br>* 1 year guarantee<br><br><br>For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |
|listing_page_display_type |String |No |image |It indicates the types that you choose to display your products on the listing page.<br><br>The accepted values are:<br><br><br>* image<br><br>* video<br><br>* other |
|cover_multimedia_url |String |No |https://demo.jpg |When listing_page_display_type is one of the multimedia types, you should provide the url to the media file here. |


<span id="a3e0f70d"></span>
##### **Product_spec**

This parameter refers to detailed product specs. It contains the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|product_group_id |String |Yes |1356 |The unique identifier for the product group. For example, beer might have 6\-pack and 12\-pack options. Each of these choices has a different product_id and they must share the same product_group_id. |
|user_rating |Double |No |0.25 |The rating given by the users. The value range should be between 0.0 and 5.0. |
|comment_count |Int32 |No |100 |The number of comments for this product. |
|source |String |No |Self |The source of the product. The accepted values are:<br><br><br>* Self<br><br>* Third\-party<br><br>* Other |
|publish_timestamp |Int64 |No |1623193487 |The time when the product is on sale. |


<span id="06c39440"></span>
##### **Seller**

This field provides information about the seller. It contains the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|id |String |Yes |43485 |The unique identifier for the seller. |
|seller_level |String |No |gold |The seller's level. The accepted values include:<br><br><br>* gold<br><br>* silver<br><br><br>For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |
|seller_rating |Double |No |3.5 |The seller's rating given by the customers. The value range should be between 0.0 and 5.0. |


<span id="beb50b69"></span>
##### Extra

This field is used to pack key\-value pairs. It contains the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|newKey |String |*  |*  |*  |
|New Value |String |*  |*  |*  |


<span id="fd58a020"></span>
#### **Device**

It refers to the platform used by a user to access the product. This parameter contains the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|platform |String |Yes |app |The platform used by users. The accepted values are:<br><br><br>* app<br><br>* desktop\-web<br><br>* mobile\-web<br><br>* other |
|os_type |String |No |Android |The platform used by users. The accepted values are:<br><br><br>* Android<br><br>* iOS<br><br>* Windows<br><br>* Other |
|app_version |String |No |9.2.0 |The application version.<br><br>For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |
|device_model |String |No |Huawei\-mate30 |The device model. The accepted values include:<br><br><br>* iPhone10<br><br>* Pixel 4<br><br><br>For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |
|device_brand |String |No |Huawei |The brand of the device.<br><br>For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |
|os_version |String |No |14.4.2 |The operating system version.<br><br>For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |
|browser_type |String |No |Firefox |The type of browser. The accepted values include:<br><br><br>* Firefox<br><br>* Chrome<br><br><br>For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |
|user_agent |String |No |Chrome |The UserAgent for the browser.<br><br>For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |
|network |String |No |3G |The network used. The accepted values are:<br><br><br>* 2G<br><br>* 3G<br><br>* 4G<br><br>* 5G<br><br>* Wifi<br><br>* Other |



|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|product_id |String |Yes |632461 |The unique identifier for the product. |
| | | | | |
|categories |Array of objects |Yes |[<br><br>{"category_depth":1, "category_nodes": [{"id_or_name":"Shoes"}] },<br><br>{"category_depth":2, "category_nodes": [{"id_or_name":"Men's Shoes"}] },<br><br>{"category_depth":3, "category_nodes": [{"id_or_name":"Basketball Shoes"}] },<br><br>] |The categorical information of the product.<br><br>If a product belongs to a single category, like "Shoes \-\> Men's Shoes \-\> Basketball Shoes", the value should look like this:<br><br>If a product belongs to two different categories, like "Shoes \-\> Men's shoes" and "Sports \-\> Basketball", then the value should look like this: |
|brands |Array of objects |Yes | |You must sort the brands by their brand_depth in ascending order.<br><br>If a product belongs to "Adidas \-\> Yeezy", this value should look like this: |
|price |Object |Yes | |The price proto. You must ensure that the products that need to be ranked are priced using the same currency. |
|is_recommendable |Boolean |Yes |true |Even if a product is not recommended to your users, you must submit this parameter to us. Users might have interacted with this product before, and this information allows us to provide more accurate recommendations. |
|title |String |Yes |adidas Men's Yeezy Boost 350 V2 Grey/Borang/Dgsogr |The title of the product. Callers can use the text name of the product or the title on the HTML page. |
|quality_score |Double |No |4.4 |The product quality score given by the seller.<br><br>This score should be normalized to [1.0, 5.0]. |
|tags |Array of strings |Yes | |The tags given by the seller for this product. It is used to improve performance.<br><br>For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |
|display |Object |Yes | |The display information of the product. |
|product_spec |Object |Yes | |The detailed product specs. |
|seller |Object |Yes | |The Seller' information. |
|extra |Object |No |*  |This is a field used to combine key\-value pairs. For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |



|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|product_id |String |Yes | |The unique identifier for the product. |
|categories |Array of objects |Yes | |The categorical information of the product.<br><br>If a product belongs to a single category, like "Shoes \-\> Men's Shoes \-\> Basketball Shoes", the value should look like this:<br><br>If a product belongs to two different categories, like "Shoes \-\> Men's shoes" and "Sports \-\> Basketball" , then the value should look like this: |


<span id="37d2e688"></span>
### Extra

This field is used to pack key\-value pairs. It contains the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|newKey |String |*  |*  |*  |
|New Value |String |*  |*  |*  |


<span id="0ce09166"></span>
# Response parameters

The following tables details the response parameters for the Predict API:


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|status |Object |*  |This field defines an error model. It contains two types of data: error code and error message. |
|request_id |String |*  |The unique identifier of a request. The value is the same as `PredictRequest.request_id`. |
|value |Object |*  |The result of a single Predict call. |


<span id="758a6efd"></span>
## value

This parameter contains the following fields:


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|response_products |Array of Objects |*  |The list of predicted products. |
|extra |Object |*  |This is a field used to provide customized information. You must contact BytePlus Recommend team first before using it. |


<span id="573aa25b"></span>
### **Response_products**

This parameter contains the following fields:


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|product_id |String |*  |The unique identifier for the product. The value is consistent with `Product.product_id`. |
|rank |Int32 |*  |The product's recommendation ranking. |
|pctr |Double |*  |The predicted Click\-Through Rate (CTR). |
|pcvr |Double |*  |The predicted Conversion Rate (CVR). |
|rec_info |String |*  |The strategy used for this particular recommendation result. For more information on ways to improve recommendation performance, refer [here](https://docs.byteplus.com/recommend/resources/ways_to_improve_recommendation_performance). |
|extra |Object |*  |This is a field used to provide customized information. You must contact BytePlus Recommend team first before using it. |


<span id="abe5daa6"></span>
### Extra

This field is used to provide customized information. It contains two types of data: newKey and New Value.


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|newKey |String |*  |*  |
|New Value |String |*  |*  |


<span id="ed90ff97"></span>
# Samples

The following section details the sample codes for the AckServerImpressions API.

<span id="fb01f45e"></span>
## Sample request

The following is a sample request for the API.

```JSON
curl --request POST \
     --url https://rec-ap-singapore-1.byteplusapi.com/predict/api/retail/retail_demo/home \
     --header 'Accept: application/json' \
     --header 'Request-Id: 221b7634-0a4c-497c-b268-e4b2f9b475b8' \
     --header 'Content-Type: application/json' \
     --header 'Tenant-Id:d7c5963593798b5263858b028f589' \
     --header 'Tenant-Nonce:1683631228' \
     --header 'Tenant-Ts:1683631228' \
     --header 'Tenant-Signature:73b6077badd2cc700144dd551058634c1d949bfaec9853f8ff426125a9d61d76' \
     --data '{
     "scene": {
          "scene_name": "Home page",
          "page_number": 2,
          "offset": 10
     },
     "context": {
          "root_product": {
               "product_id": "632461"
          },
          "device": {
               "platform": "app",
               "os_type": "android",
               "app_version": "9.2.0",
               "device_model": "huawei-mate30",
               "device_brand": "huawei",
               "os_version": "10",
               "browser_type": "chrome",
               "user_agent": "Mozilla/5.0 (Linux; Android 10; TAS-AN00; HMSCore 5.3.0.312) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.106 HuaweiBrowser/11.0.8.303 Mobile Safari/537.36",
               "network": "3g"
          },
          "candidate_product_ids": [
               "632462",
               "632463",
               "632464",
               "632465",
               "632466"
          ]
     },
     "extra": {
          "additionalProp2": "additionalVal2"
     },
     "user_id": "1457789",
     "size": 3
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
  },
  "request_id": "221b7634-0a4c-497c-b268-e4b2f9b475b8",
  "value": {
    "response_products": [
      {
        "product_id": "product_id_1",
        "rank": 1,
        "pctr": 0.3,
        "pcvr": 0.6,
        "rec_info": "CggxMjgzMTAwMRITCgp2aWtpbmdfY3RyFVDOFb4YABITCgp2aWtpbmdfY3ZyFZAESr4YHxIaChFyZWNlbnRfa=",
        "extra": {
          "category": "cate_1"
        }
      },
      {
        "product_id": "product_id_2",
        "rank": 2,
        "pctr": 0.15,
        "pcvr": 0.32,
        "rec_info": "3ZyFZAESr4YHxIaChFyZWNlbnRfaCggxMjgzMTAwMRITCgp2aWtpbmdfY3RyFVDOFb4YABITCgp2aWtpbmdfY=",
        "extra": {
          "category": "cate_1"
        }
      },
      {
        "product_id": "product_id_3",
        "rank": 1,
        "pctr": 0.09,
        "pcvr": 0.43,
        "rec_info": "MjgzMTAwMRITCgp2aWtpbmd3ZyFZAESr4YHxIaChFyZWNlbnRfaCggxfY3RyFVDOFb4YABITCgp2aWtpbmdfY=",
        "extra": {
          "category": "cate_2"
        }
      }
    ]
  }
}
```


The following is a **failed** sample response.

```JSON
{ 
  "status": { 
    "code": 400, 
    "message": "unmarshal request body fail, plz make sure path is correct. path:/api/retail/retail_demo/home, targetReqType:*retail.PredictRequest; errID:852940573 logID:202304041027049278AA2F7CA2A95A785F" 
  } 
}
```


The following is a **failed** sample response due to internal server error.

```JSON
{
  "status": {
    "code": 500,
    "message": "internal error encountered; errID:840491090 logID:2023032311430332A733A4EA5CBF7B0926"
  }
}
```


<span id="9398e94b"></span>
# Error codes

For more information on the API error codes, refer to [BytePlus Recommend shared error and status codes](https://docs.byteplus.com/recommend/reference/shared_error_and_status_codes).
