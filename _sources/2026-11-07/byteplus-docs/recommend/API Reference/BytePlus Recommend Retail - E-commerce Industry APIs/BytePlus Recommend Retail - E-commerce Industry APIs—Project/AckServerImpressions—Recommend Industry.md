---
title: "AckServerImpressions—Recommend Industry"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/reference-retail_ackserverimpressions"
---

With the AckServerImpressions API, you can conveniently send back the actual product list shown to users in the Retail/E\-commerce industry for BytePlus Recommend.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information on BytePlus Recommend token authentication, refer <a href="https://docs.byteplus.com/en/recommend/reference/api_token_authentication">here</a>.</div>


<span id="36c7c3c1"></span>
# HTTP request


|**URL** |https://rec\-ap\-singapore\-1.byteplusapi.com/predict/api/retail/${tenant}/ack_server_impressions |
|---|---|
|**Method** |POST |


<span id="d5e9f3b3"></span>
# Request parameters

The topics below details the parameters required for the AckServerImpressions API.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Not all request parameters are included in the following table. For a complete list, refer to <a href="https://docs.byteplus.com/recommend/reference/api_token_authentication">HTTP header parameters</a>.</div>


<span id="1dad2339"></span>
## Body

The following table details the body parameters required for the AckServerImpressions API:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|project_id |String |Yes |1692729105 |The unique identifier for the recommendation project. |
|model_id |String |Yes | |The unique identifier for the recommendation model used. |
|predict_request_id |String |Yes |0a8c61a2\-be57\-44a7\-a31d\-cb861905e00a |The Predict API's request ID. The value should be the same as `PredictRequest.request_id`. |
|user_id |String |Yes |1457789 |The user ID used in the Predict API's call. The value should be the same as `PredictRequest.user_id`. |
|traffic_source |String |Yes |*  |The source of the recommendation. |
|scene |Object |*  |*  |The scene where the event happened. |
|altered_products |Array of Objects |Yes |*  |The list of altered products. |


<span id="e1c28139"></span>
### **Scene**

It refers to the location where the user interaction event happened. The scene proto contains the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|scene_name |String |Yes |Details page |The name of the scene the UserEvent occurred in. It's the unique identifier for a UserEvent scene. The accepted values are:<br><br><br>* Home page<br><br>* Search page<br><br>* Details page<br><br><br>It is strongly recommended that you split the scene if possible. |
|page_number |Int32 |No |1 |The page number.<br><br>This field can refer to:<br><br><br>* the page number that the content is found on.<br><br>* the number of times that users swipe the screen before seeing the content.<br><br><br>The default value is 0, which indicates that all content fits into a single page. |
|offset |Int32 |No |10 |The content's position within the page itself. |


<span id="45d822fe"></span>
### **Altered_products**

This parameter refers to a list of altered products. It contains the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|product_id |String |Yes |632461 |The unique identifier for the product. The value is the same as Product.product_id. |
|altered_reason |String |Yes |kept |The final state of the product. The accepted values are:<br><br><br>* kept—indicates that the product was included in the actual impression.<br><br>* filtered—indicates that the product was filtered out of the actual impression by your platform's logic.<br><br>* inserted—indicates that the product was inserted into the actual impression by your platform's logic.<br><br>* filled—indicates that the product was added as a supplement to the actual impression by your platform's logic. |
|rank |Int32 |Yes |1 |The product's final recommendation ranking. If the value is unset or 0, the product is assumed to be filtered out from the actual impression. |


<span id="0ce09166"></span>
# Response parameters

The following tables details the response parameters for the AckServerImpressions API:


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|status |Object |*  |This field defines an error model. It contains two types of data: error code and error message. |


<span id="d26b2367"></span>
## **Status**

The `status` defines an error model. Each `status` message contains two types of data: error code and error message.


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|code |Int32 |0 |You should look at this response parameter to determine if your API request was successful or not. The accepted values include:<br><br><br>* 0: it indicates that the calling is successful.<br><br>* 4xx: it indicates user error.<br><br>* 5xx: it indicates server error.<br><br>* 1xxx: it indicates error relating to Import calls.<br><br>* 2xxx: it indicates errors relating to Predict calls. |
|message |String |An unexpected value XXX is included in the XXX field, only ["xx", "yy", "zz"] can be accepted. |Provides detailed error messages on the reasons why your API request was unsuccessful. |


<span id="ed90ff97"></span>
# Samples

The following section details the sample codes for the AckServerImpressions API.

<span id="fb01f45e"></span>
## Sample request

The following is a sample request for the API.

```JSON
curl --request POST \
     --url https://rec-ap-singapore-1.byteplusapi.com/predict/api/retail/retail_demo/ack_server_impressions \
     --header 'Accept: application/json' \
     --header 'Request-Id: 2c568be9-1359-4c39-814c-e1f47d7571bc' \
     --header 'Content-Type: application/json' \
     --header 'Tenant-Id:d7c5963593798b5263858b028f589' \
     --header 'Tenant-Nonce:1683632868' \
     --header 'Tenant-Ts:1683632868' \
     --header 'Tenant-Signature:e1aea6af8aa8e837a7e0ed105d220f048605cdb63b2c3823ca53e0833c1faa65' \
     --data '{
     "scene": {
          "scene_name": "Home Page"
     },
     "altered_products": [
          {
               "product_id": "632462"
          },
          {
               "product_id": "632463"
          },
          {
               "product_id": "632464"
          }
     ],
     "predict_request_id": "221b7634-0a4c-497c-b268-e4b2f9b475b8",
     "user_id": "1457789"
}'
```


<span id="de55caff"></span>
## Sample response

The following is a successful sample response.

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
    "message": "unmarshal request body fail, plz make sure path is correct. path:/api/retail/retail_demo/ack_server_impressions, targetReqType:*retail.AckServerImpressionsRequest; errID:852940573 logID:202304041027049278AA2F7CA2A95A785F" 
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
