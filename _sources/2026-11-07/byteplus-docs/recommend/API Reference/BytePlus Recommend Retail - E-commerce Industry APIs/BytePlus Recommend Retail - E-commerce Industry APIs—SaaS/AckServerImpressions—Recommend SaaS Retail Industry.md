---
title: "AckServerImpressions—Recommend SaaS Retail Industry"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/reference-retail_saas_ackserverimpressions"
---

With the AckServerImpressions API, you can conveniently send back the actual product list shown to users in the Retail/E\-commerce industry for BytePlus Recommend SaaS.

<span id="36c7c3c1"></span>
# HTTP request


|**URL** |https://rec\-api\-sg1.recplusapi.com/RetailSaaS/AckServerImpressions |
|---|---|
|**Method** |POST |


<span id="d5e9f3b3"></span>
# Request parameters

The topics below details the parameters required for the AckServerImpressions API.

<span id="df2272f4"></span>
## Header


|**Header Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Tenant\-Id |String |Yes |3000001813 |Your BytePlus account's ID. For more information on retrieving Recommend Tenant IDs, refer [here](https://docs.byteplus.com/recommend/docs/retail_standard_getting_started). |
|Request\-id |String |Yes |84kduxkls74lcdj73jdu3 |The client assigns the request id, and it should be unique for each request. No specific format is required for the request\-id, but it is advisable to keep it reasonably short.<br><br>For more information on request\-id generation code samples, refer [here](https://docs.byteplus.com/recommend/reference/api_token_authentication). |
|Other Auth Header |*  |Yes |*  |**Recommend Standard**<br><br>BytePlus Recommend SaaS Standard uses Access Key/Secret Key (AK/SK) for Byteplus Standard header authentication. The process of constructing these headers can be complex, so it is recommended to use the SDK for easier access and implementation.<br><br>For more information on using the AK/SK authentication, refer [here](https://docs.byteplus.com/en/recommend/reference/api_authentication#9e904017).<br><br>**Recommend Premium**<br><br>BytePlus Recommend SaaS Premium uses token header authentication.<br><br>For more information on using the SDK token authentication, refer [here](https://docs.byteplus.com/en/recommend/reference/api_token_authentication). |


<span id="1dad2339"></span>
## Body

The following table details the body parameters required for the AckServerImpressions API.


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|project_id |String |Yes |851467130 |The unique identifier for the Recommend project. |
|model_id |String |Yes |100000 |The unique identifier for the recommendation model used. |
|predict_request_id |String |Yes |*  |The Predict API's request ID. The value should be the same as `PredictRequest.request_id`. |
|user_id |String |Yes |*  |The user ID used in the Predict API's call. The value should be the same as `PredictRequest.user_id`. |
|traffic_source |String |Yes |*  |The source of the recommendation. For more details on ways to improve recommendation performance, refer [here](https://docs.byteplus.com/recommend/resources/ways_to_improve_recommendation_performance). |
|scene |Object |*  |*  |The recommendation scene information. |
|altered_products |Array of Objects |Yes |*  |The list of altered products. |
|extra |Map<String, String\> |No |*  |This is a field for additional information. You should provide as much information as possible. |


<span id="d7b2b1b5"></span>
### **Scene**

Scene refers to the location where the user interaction event happened. The scene proto contains the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|scene_name |String |No |home_page |The name of the scene the UserEvent occurred in. It's the unique identifier for a UserEvent scene. The scene will be determined by the scene specified when training the current model. The accepted values are:<br><br><br>* home_page<br><br>* category_page<br><br>* product_detail_page<br><br>* shopping_cart<br><br>* purchase_complete<br><br><br>It is strongly recommended that you split the scene if possible. |
|page_number |Int32 |No |1 |The page number.<br><br>This field can refer to:<br><br><br>* the page number that the content is found on.<br><br>* the number of times that users swipe the screen before seeing the content.<br><br><br>The default value is 0, which indicates that all content fits into a single page. |
|offset |Int32 |No |10 |The content's position within the page itself. |


<span id="d9716652"></span>
### **Altered_products**

This parameter refers to a list of altered products. It contains the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|product_id |String |Yes |*  |The unique identifier of the product. The value is the same as `Product.product_id`. |
|altered_reason |String |Yes |kept |The final state of the product. The accepted values are:<br><br><br>* kept: Indicates that the product was included in the actual impression.<br><br>* filtered: Indicates that the product was filtered out of the actual impression by your platform's logic.<br><br>* inserted: Indicates that the product was inserted into the actual impression by your platform's logic.<br><br>* filled: Indicates that the product was added as a supplement to the actual impression by your platform's logic. |
|rank |Int32 |Yes |*  |The final recommendation ranking of the product. If the value is unset or 0, the product is assumed to be filtered out from the actual impression. |
|extra |Object |No |*  |This is a field for additional information. You should provide as much information as possible. |


<span id="0cbe9927"></span>
### **Extra**

This is a field for additional information. This parameter contains the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|newKey |String |*  |*  |*  |
|New Value |String |*  |*  |*  |


<span id="0ce09166"></span>
# Response parameters

The following table details the response parameters for the AckServerImpressions API:


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|status |Object |*  |This field defines an error model. It contains two types of data: error code and error message. |


<span id="c3709059"></span>
## **Status**

The `status` defines an error model. Each `status` message contains two types of data: error code and error message.


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|code |Int32 |0 |You should look at this response parameter to determine if your API request was successful or not. The accepted values include:<br><br><br>* 0: it indicates that the calling is successful.<br><br>* 4xx: it indicates user error.<br><br>* 5xx: it indicates server error.<br><br>* 1xxx: it indicates error relating to Import calls.<br><br>* 2xxx: it indicates errors relating to Predict calls. |
|message |String |An unexpected value XXX is included in the XXX field, only ["xx", "yy", "zz"] can be accepted. |Provides detailed error messages on the reasons why your API request was unsuccessful. |


<span id="ed90ff97"></span>
# Samples

<span id="fb01f45e"></span>
## Sample request

The following is a sample request for the API.

```JSON
curl --request POST \
     --url https://rec-api-sg1.recplusapi.com/RetailSaaS/AckServerImpressions \
     --header 'Tenant-Id: 3000001813' \
     --header 'Request-Id: 2c568be9-1359-4c39-814c-e1f47d7571bc' \
     --header 'accept: application/json' \
     --header 'content-type: application/json' \
     --data '
{
  "project_id": "851467130",
  "model_id": "100000",
  "predict_request_id": "221b7634-0a4c-497c-b268-e4b2f9b475b8",
  "user_id": "14577890",
  "scene": {
    "scene_name": "home_page",
    "page_number": 1,
    "offset": 10
  },
  "altered_products": [
    {
      "extra": {
        "extra_key": "extra_value"
      },
      "product_id": "6324610",
      "altered_reason": "kept",
      "rank": 1
    },
    {
      "extra": {
        "extra_key": "extra_value"
      },
      "product_id": "6324611",
      "altered_reason": "kept",
      "rank": 2
    },
    {
      "extra": {
        "extra_key": "extra_value"
      },
      "product_id": "6324612",
      "altered_reason": "inserted",
      "rank": 3
    },
    {
      "extra": {
        "extra_key": "extra_value"
      },
      "product_id": "6324613",
      "altered_reason": "kept",
      "rank": 4
    }
  ],
  "traffic_source": "byteplus",
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
  } 
} 
```


The following is a **failed** sample response.

```JSON
{ 
  "status": { 
    "code": 400, 
    "message": "unmarshal request body fail, plz make sure path is correct. path:/RetailSaaS/AckServerImpressions, targetReqType:*saas.AckServerImpressionsRequest; errID:852940573 logID:202304041027049278AA2F7CA2A95A785F" 
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

&nbsp;
