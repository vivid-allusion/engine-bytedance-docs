---
title: "Predict—Recommend SaaS Retail Industry"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/reference-retail_saas_predict"
---

The Predict API for BytePlus Recommend SaaS empowers the updating and ranking of product lists in the Retail/E\-commerce industry. User data takes approximately 24 hours to take effect, while product data influences the results within just 30 minutes. By leveraging UserEvent data, the API enhances recommendation outcomes, delivering improved user experiences tailored to individual preferences.

<span id="dd72161d"></span>
# HTTP request


|**URL** |https://rec\-api\-sg1.recplusapi.com/RetailSaaS/Predict |
|---|---|
|**Method** |POST |


<span id="d5e9f3b3"></span>
# Request parameters

The topics below details the parameters required for the Predict API.

<span id="df2272f4"></span>
## Header


|**Header Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Tenant\-Id |String |Yes |3000001813 |Your BytePlus account's ID. For more information on retrieving Recommend Tenant IDs, refer [here](https://docs.byteplus.com/recommend/docs/retail_standard_getting_started). |
|Request\-id |String |Yes |84kduxkls74lcdj73jdu3 |The client assigns the request id, and it should be unique for each request. No specific format is required for the request\-id, but it is advisable to keep it reasonably short.<br><br>For more information on request\-id generation code samples, refer [here](https://docs.byteplus.com/recommend/reference/api_token_authentication). |
|Other Auth Header |*  |Yes |*  |**Recommend Standard**<br><br>BytePlus Recommend SaaS Standard uses Access Key/Secret Key (AK/SK) for Byteplus Standard header authentication. The process of constructing these headers can be complex, so it is recommended to use the SDK for easier access and implementation.<br><br>For more information on using the AK/SK authentication, refer [here](https://docs.byteplus.com/en/recommend/reference/api_authentication#9e904017).<br><br>**Recommend Premium**<br><br>BytePlus Recommend SaaS Premium uses token header authentication.<br><br>For more information on using the SDK token authentication, refer [here](https://docs.byteplus.com/en/recommend/reference/api_token_authentication). |


<span id="1dad2339"></span>
## Body

The following table details the body parameters required for the Predict API:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|project_id |String |Yes |851467130 |The unique identifier for the Recommend project. |
|model_id |String |Yes |100000 |The unique identifier for the Recommendation model used. |
|user_id |String |Yes |*  |The unique identifier for the user. The value is the same as `User.user_id`. |
|size |Int32 |Yes |*  |The maximum number of products returned. The actual number of products returned is the minimum of the following numbers:<br><br><br>* `size`<br><br>* length(`context.candidates_product_ids`)<br><br>* total number of products with `is_recommendable`= True. |
|scene |Object |*  |*  |The recommendation scene information. |
|context |Object |*  |*  |The context of the current Predict request. |
|extra |Map<String, String\> |No |*  |This is a field is for additional information. You should provide as much information as possible. |


<span id="24dd7646"></span>
### **Scene**

Scene refers to the location where the user interaction event happened. The scene proto contains the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|scene_name |String |No |home_page |The name of the scene the UserEvent occurred in. It's the unique identifier for the scene. The value will be determined by the scene specified when training the current recommendation model. The accepted values are:<br><br><br>* home_page<br><br>* category_page<br><br>* product_detail_page<br><br>* shopping_cart<br><br>* purchase_complete<br><br><br>It is strongly recommended that you split the scene if possible. |
|page_number |Int32 |No |1 |The page number.<br><br>This field can refer to:<br><br><br>* the page number that the content is found on.<br><br>* the number of times that users swipe the screen before seeing the content.<br><br><br>The default value is 0, which indicates that all content fits into a single page. |
|offset |Int32 |No |10 |The content's position within the page itself. |


<span id="3521fe6d"></span>
### **Context**

Context refers to the context of a Predict API request. The context parameters contain the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|root_product |Object |*  |*  |The parent product information, if any. The parent product refers to the products whose details page contains the recommended product the user has seen or clicked on.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This field is only required for the product details page.</div><br> |
|device |Object |*  |app |The platform used by a user to access the product. The accepted values are:<br><br><br>* app<br><br>* desktop\-web<br><br>* mobile\-web<br><br>* other |
|candidate_products |Array of Objects |No |*  |The list of candidates for product recommendation. If this value is empty, it means all products are the candidates. |


<span id="4f9fd0f9"></span>
#### **Root_product**

The parent product information, if any. The parent product refers to the products whose details page contains the recommended product the user has seen or clicked on. It contains the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|product_id |String |Yes |7324310 |The unique identifier for the recommended product. |
|is_recommendable |Int32 |No |1 |This field determines if the product should be recommended to the user.<br><br>The accepted values are:<br><br><br>* 1—The product should be recommended to users.<br><br>* 0—The product should not be recommended to users.<br><br><br>Even if a product is not recommended to your users, you must submit this parameter to us. Users might have interacted with this product before, and this information allows us to provide more accurate recommendations. |
|current_price |Float |No |49900 |Enter the current price of the product, if discounted. This parameter value is rounded to two decimal places. |
|original_price |Float |No |69900 |The original price of the product. This parameter value is rounded to two decimal places. |
|publish_timestamp |Int64 |No |1623193487 |Indicates when the product is published. |
|categories |String |No |[<br><br>{"category_depth":1,<br><br>"category_nodes": [{"id_or_name":"Shoes"}] },<br><br>{"category_depth":2,<br><br>"category_nodes": [{"id_or_name":"Men's Shoes"}] },<br><br>{"category_depth":3,<br><br>"category_nodes": [{"id_or_name":"Basketball Shoes"}] },<br><br>] |The categories that the product belongs to. It is formatted as a JSON serialized string and contains the following subparameters:<br><br><br>* category_depths: Indicates the depth of the category. It is a consecutive and ascending positive number.<br><br>* category_nodes: Indicates the category nodes in the same "category_depth". It must not contain empty value. If empty value exists, replace it with "null" . Each "category_nodes"" can only associate with one "id_or_name" key\-value pair.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you do not fill in this parameter, the accuracy and efficiency of the product recommendations will be affected.</div><br><br><br>If a product belongs to a single category, like "Shoes \-\> Men's Shoes \-\> Basketball Shoes", the value should look like this:<br><br>```JSON```<br>```[```<br>``` {"category_depth":1,```<br>```  "category_nodes": [{"id_or_name":"Shoes"}] },```<br>``` {"category_depth":2,```<br>```  "category_nodes": [{"id_or_name":"Men's Shoes"}] },```<br>``` {"category_depth":3,```<br>```  "category_nodes": [{"id_or_name":"Basketball Shoes"}] },```<br>```]```<br><br><br>If a product belongs to two different categories, like "Shoes \-\> Men's shoes" and "Sports \-\> Basketball" , then the value should look like this:<br><br>```JSON```<br>```[```<br>``` {"category_depth":1,```<br>```  "category_nodes": [{"id_or_name":"Shoes"},```<br>```                     {"id_or_name":"Sports"}] },```<br>``` {"category_depth":2,```<br>```  "category_nodes": [{"id_or_name":"Men's shoes"},```<br>```                     {"id_or_name":"Basketball"}] },```<br>```]```<br> |
|tags |String |No |["New", "Summer", "Clearance"] |The tags given by the seller for this product and formatted as a JSON serialized string. It is used to improve performance.<br><br>The available values include:<br><br><br>* New<br><br>* Summer<br><br>* Clearance<br><br><br>For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |
|title |String |No |Grey Shoes 100 |The title of the product. You can use the text name of the product or the title on the HTML page. |
|brands |String |No |[<br><br>{"brand_depth": 1, "id_or_name":"Adidas"},<br><br>{"brand_depth": 2, "id_or_name":"Yeezy"},<br><br>] |The brands that the product belongs to. You should sort the brands by their brand_depth in ascending order.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you do not fill in this parameter, the accuracy and efficiency of the product recommendations will be affected.</div><br><br><br>If a product belongs to "Adidas \-\> Yeezy", the value should look like this:<br><br>```Plain```<br>```[```<br>``` {"brand_depth": 1, "id_or_name":"Adidas"},```<br>``` {"brand_depth": 2, "id_or_name":"Yeezy"},```<br>```]```<br> |
|user_rating |Float |No |3.5 |The rating score given by the users. It is a non\-negative value. |
|sold_count |Int32 |No |1,000 |If the product needs payment, enter the number of purchases of the product. |
|product_group_id |String |No |13324678 |The unique identifier for the product group. |
|display_cover_multimedia_url |String |No |https://test_image.png |The URL of the product's multimedia cover. It is formatted as a JSON serialized string. |
|comment_count |Int32 |No |100 |The number of comments for the product. |
|source |String |No |Self |The source of the recommendation. Acceptable values include:<br><br><br>* Self: Indicates that the recommendation comes from the caller's own engine.<br><br>* Other: Indicates that the recommendation comes from a third\-party engine. |
|seller_id |String |No |12345678 |The unique identifier of the seller. |
|seller_level |String |No |gold |The seller's level. The accepted values include:<br><br><br>* gold<br><br>* silver |
|seller_rating |Float |No |3.5 |The rating score of sellers given by customers. It is a non\-negative value. |
|extra |Map<String, String\> |No |*  |This is a field for additional information. You should provide as much information as possible. |


<span id="06479af6"></span>
#### **Device**

It refers to the platform used by a user to access the product. This parameter contains the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|platform |String |Yes |app |The platform used by users. The accepted values are:<br><br><br>* app<br><br>* desktop\-web<br><br>* mobile\-web<br><br>* other |
|os_type |String |No |Android |The platform used by users. The accepted values are:<br><br><br>* Android<br><br>* iOS<br><br>* Windows<br><br>* Other |
|app_version |String |No |9.2.0 |The application version.<br><br>For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |
|device_model |String |No |Huawei\-mate30 |The device model. The accepted values include:<br><br><br>* iPhone 10<br><br>* Pixel 4<br><br><br>For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |
|device_brand |String |No |Huawei |The brand of the device. For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |
|os_version |String |No |14.4.2 |The operating system version. For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |
|browser_type |String |No |Firefox |The type of browser. The accepted values include:<br><br><br>* Firefox<br><br>* Chrome<br><br><br>For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |
|user_agent |String |No |Chrome |The UserAgent for the browser.<br><br>For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |
|network |String |No |3G |The network used. The accepted values are:<br><br><br>* 2G<br><br>* 3G<br><br>* 4G<br><br>* 5G<br><br>* Wifi<br><br>* Other |


<span id="08cce5b6"></span>
#### **Candidate_products**

The list of candidates for product recommendation. If this value is empty, it means all products are the candidates. It contains the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|product_id |String |Yes |632461 |The unique identifier for the recommended product. |
|is_recommendable |Int32 |No |1 |This field determines if the product should be recommended to the user.<br><br>The accepted values are:<br><br><br>* 1—The product should be recommended to users.<br><br>* 0—The product should not be recommended to users.<br><br><br>Even if a product is not recommended to your users, you must submit this parameter to us. Users might have interacted with this product before, and this information allows us to provide more accurate recommendations. |
|current_price |Float |No |49900 |Enter the current price of the product, if discounted. This parameter value is rounded to two decimal places. |
|original_price |Float |No |69900 |The original price of the product. This parameter value is rounded to two decimal places. |
|publish_timestamp |Int64 |No |1623193487 |Indicates when the product is published. |
|categories |String |No |[<br><br>{"category_depth":1, "category_nodes": [{"id_or_name":"Shoes"}] },<br><br>{"category_depth":2, "category_nodes": [{"id_or_name":"Men's Shoes"}] },<br><br>{"category_depth":3, "category_nodes": [{"id_or_name":"Basketball Shoes"}] },<br><br>] |The categories that the product belongs to. It is formatted as a JSON serialized string and contains the following subparameters:<br><br><br>* category_depths: Indicates the depth of the category. It is a consecutive and ascending positive number.<br><br>* category_nodes: Indicates the category nodes in the same "category_depth". It must not contain empty value. If empty value exists, replace it with "null" . Each "category_nodes"" can only associate with one "id_or_name" key\-value pair.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you do not fill in this parameter, the accuracy and efficiency of the product recommendations will be affected.</div><br><br><br>If a product belongs to a single category, like "Shoes \-\> Men's Shoes \-\> Basketball Shoes", the value should look like this:<br><br>```JSON```<br>```[```<br>``` {"category_depth":1,```<br>```  "category_nodes": [{"id_or_name":"Shoes"}] },```<br>``` {"category_depth":2,```<br>```  "category_nodes": [{"id_or_name":"Men's Shoes"}] },```<br>``` {"category_depth":3,```<br>```  "category_nodes": [{"id_or_name":"Basketball Shoes"}] },```<br>```]```<br><br><br>If a product belongs to two different categories, like "Shoes \-\> Men's shoes" and "Sports \-\> Basketball", then the value should look like this:<br><br>```JSON```<br>```[```<br>``` {"category_depth":1,```<br>```  "category_nodes": [{"id_or_name":"Shoes"},```<br>```                     {"id_or_name":"Sports"}] },```<br>``` {"category_depth":2,```<br>```  "category_nodes": [{"id_or_name":"Men's shoes"},```<br>```                     {"id_or_name":"Basketball"}] },```<br>```]```<br> |
|tags |String |No |["New", "Summer", "Clearance"] |The tags given by the seller for this product and formatted as a JSON serialized string. It is used to improve performance.<br><br>The available values include:<br><br><br>* New<br><br>* Summer<br><br>* Clearance<br><br><br>For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |
|title |String |No |Grey Shoes 100 |The title of the product. You can use the text name of the product or the title on the HTML page. |
|brands |String |Yes |[<br><br>{"brand_depth": 1, "id_or_name":"Adidas"},<br><br>{"brand_depth": 2, "id_or_name":"Yeezy"},<br><br>] |The brands that the product belongs to. You should sort the brands by their brand_depth in ascending order.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you do not fill in this parameter, the accuracy and efficiency of the product recommendations will be affected.</div><br><br><br>For example, if a product belongs to "Adidas \-\> Yeezy", this field should be:<br><br>```JSON```<br>```[```<br>```{"brand_depth": 1, "id_or_name":"Adidas"},```<br>```{"brand_depth": 2, "id_or_name":"Yeezy"},```<br>```]```<br> |
|user_rating |Float |No |3.5 |The rating score given by the users. It is a non\-negative value. |
|sold_count |Int32 |No |1,000 |If the product needs payment, enter the number of purchases of the product. |
|product_group_id |String |No |13324678 |The unique identifier for the product group. |
|display_cover_multimedia_url |String |No |https://demo.jpg |The URL of the product's multimedia cover. It is formatted as a JSON serialized string. |
|comment_count |Int32 |No |100 |The number of comments for the product. |
|source |String |No |Self |The source of the recommendation. Acceptable values include:<br><br><br>* Self: Indicates that the recommendation comes from the caller's own engine.<br><br>* Other: Indicates that the recommendation comes from a third\-party engine. |
|seller_id |String |No |12345678 |The unique identifier of the seller. |
|seller_level |String |No |gold |The seller's level. The accepted values include:<br><br><br>* gold<br><br>* silver |
|seller_rating |Float |No |3.5 |The rating score of sellers given by customers. It is a non\-negative value. |
|extra |Object |No |*  |This field is used to pack key\-value pairs.<br><br>For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |


<span id="0ce09166"></span>
# Response parameters

The following tables details the response parameters for the Predict API:


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|status |Object |*  |This field defines an error model. It contains these types of data: error code and error message. |
|request_id |String |*  |The unique identifier of a request. The value is the same as `PredictRequest.request_id`. |
|value |Object |*  |The result of a single Predict call. |


<span id="3a53300e"></span>
## **Value**

This parameter, `PredictResult` contains the following fields:


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|response_products |Array of Objects |*  |The list of predicted products. |
|extra |Object |*  |This is a field for additional debug information. |


<span id="aee0edc3"></span>
### **Response_products**

This parameter refers to a list of predicted products. It contains the following fields:


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|product_id |String |*  |The unique identifier for the product. The value is consistent with `Product.product_id`. |
|rank |Int32 |*  |The product's recommendation ranking. |
|pctr |Double |*  |The predicted Click\-Through Rate (CTR). |
|pcvr |Double |*  |The predicted Conversion Rate (CVR). |
|rec_info |String |*  |The strategy used for this particular recommendation result. For more information on ways to improve recommendation performance, refer [here](https://docs.byteplus.com/recommend/resources/ways_to_improve_recommendation_performance). |
|extra |Object |*  |This is a field for additional debug information. |


<span id="c051628d"></span>
### Extra

This is a field for additional debug information. It contains the following fields:


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|newkey |String |*  |*  |
|New Value |String |*  |*  |


<span id="ed90ff97"></span>
# Samples

The following section details the sample codes for the Predict API.

<span id="fb01f45e"></span>
## Sample request

The following is a sample request for the API.

```JSON
curl --request POST \
     --url https://rec-api-sg1.recplusapi.com/RetailSaaS/Predict \
     --header 'Tenant-Id: 3000001813' \
     --header 'Request-Id: 221b7634-0a4c-497c-b268-e4b2f9b475b8' \
     --header 'accept: application/json' \
     --header 'content-type: application/json' \
     --data '
{
  "project_id": "851467130",
  "model_id": "100000",
  "user_id": "14577890",
  "size": 10,
  "scene": {
    "scene_name": "home_page",
    "page_number": 1,
    "offset": 10
  },
  "context": {
    "root_product": {
      "product_id": "7324310"
    },
    "device": {
      "platform": "app",
      "os_type": "android",
      "app_version": "V9.0.8",
      "device_model": "iPhone10",
      "device_brand": "Samsung",
      "os_version": "14.4.2",
      "browser_type": "chrome",
      "network": "5g",
      "user_agent": "mock_user_agent"
    },
    "candidate_products": [
      {
        "product_id": "6324610"
      },
      {
        "product_id": "6324611"
      },
      {
        "product_id": "6324612"
      },
      {
        "product_id": "6324613"
      }
    ]
  },
  "extra": {
    "extra_key": "extra_value"
  }
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
    "message": "unmarshal request body fail, plz make sure path is correct. path:/RetailSaaS/Predict, targetReqType:*saas.PredictRequest; errID:852940573 logID:202304041027049278AA2F7CA2A95A785F" 
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
