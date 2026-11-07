---
title: "AckServerImpressions—Recommend Content Industry"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/reference-content_ackserverimpressions"
---

With the AckServerImpressions API, you can conveniently send back the actual content list shown to users in the Media/Content industry for BytePlus Recommend.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information on BytePlus Recommend token authentication, refer <a href="https://docs.byteplus.com/en/recommend/reference/api_token_authentication">here</a>.</div>


<span id="dd72161d"></span>
# HTTP request

This is the URL and HTTP request method for the AckServerImpressions API.


|**URL** |https://rec\-us\-east\-1.byteplusapi.com/predict/api/media/${tenant}/ack_server_impressions |
|---|---|
|**Method** |POST |


<span id="d5e9f3b3"></span>
# Request parameters

The topics below details the parameters required for the AckServerImpressions API.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Not all request parameters are included in the following table. For a complete list, refer to <a href="https://docs.byteplus.com/recommend/reference/api_token_authentication">HTTP header parameters</a>.</div>


<span id="144f0eac"></span>
## Body

The following table details the body parameters required for the AckServerImpressions API:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|predict_request_id |String |Yes |a098df23\-6e45\-47a9\-875a\-f48f06831bc3 |The `Predict`API's request ID. It should be the same value as `PredictRequest.request_id`. |
|user_id |String |Yes |1457789 |The user ID used in `Predict`API's call. It should be the same value as `PredictRequest.user_id`. |
|traffic_source |String |Yes |Self |The source of the recommendation.<br><br>The accepted values are:<br><br><br>* Self—indicates that the recommendation came from the caller's own engine.<br><br>* BytePlus—indicates that the recommendation came from BytePlus.<br><br>* Other—indicates that the recommendation came from a third\-party engine. |
|scene |Object |Yes |*  |The recommendation scene information.<br><br>Ensure that this is as close to `UserEvent.scene` as possible. |
|altered_contents |Array of Objects |Yes |*  |The list of altered contents. |
|extra |Object |No |*  |A catch\-all field to pass any additional information.<br><br>You should provide as much information as possible using this field. |


<span id="670630e2"></span>
### **Scene**

Scene refers to the location where the user interaction event happened. The scene proto contains the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|scene_name |String |Yes |home |The name of the scene the UserEvent occurred in. The same parameter value as `UserEvent.scene_name`. |
|page_number |Int32 |No |1 |The page number.<br><br>This field can refer to:<br><br><br>* the page number that the content is found on.<br><br>* the number of times that users swipe the screen before seeing the content.<br><br><br>The default value is 0, which indicates that all content fits into a single page. |
|offset |Int32 |No |10 |The content's position within the page itself. |


<span id="44bf6e30"></span>
### **Altered_contents**

AckServerImpressionsRequest.AlteredContent contains information about a piece of content that has been altered in the recommendation result. Its proto contains the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|content_id |String |Yes |632461 |The unique identifier for the content.<br><br>The value is the same as `Content.content_id`. |
|altered_reason |String |Yes |kept |The content's final state.<br><br>The accepted values are:<br><br><br>* kept—indicates that the content was included in the actual impression.<br><br>* filtered—indicates that the content was filtered out of the actual impression by your platform's logic.<br><br>* inserted—indicates that the content was inserted into the actual impression by your platform's logic.<br><br>* filled—indicates that the content was added as a supplement to the actual impression by your platform's logic. |
|rank |Int32 |Yes |1 |The content's final recommendation ranking.<br><br>If the value is unset or 0, the content is assumed to be filtered out from the actual impression. |
|content_id_hash |Int64 |Yes |632461 |The content ID hash.<br><br>If `content_id` is a number, the value of `content_id_hash` is the same as `content_id`. If `content_id` is not a number, the value of `content_id_hash` is `fnv(content_id)`. |


<span id="0ce09166"></span>
# Response parameters

The following tables details the response parameters for the AckServerImpressions API:


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|status |Object |*  |It defines a logical error model. It contains two types of data: error code and error message. |


<span id="380431e0"></span>
## **Status**

The status defines an error model. Each status message contains two types of data: error code and error message.


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|code |Int32 |0 |You should look at this response parameter to determine if your API request was successful. The accepted values are:<br><br><br>* 0: it indicates that the calling is successful.<br><br>* 4xx: it indicates user error.<br><br>* 5xx: it indicates server error.<br><br>* 1xxx: it indicates error relating to Import calls.<br><br>* 2xxx: it indicates errors relating to Predict calls. |
|message |String |An unexpected value XXX is included in the XXX field, only ["xx", "yy", "zz"] can be accepted. |Provides a detailed error message on the reasons why your API request was unsuccessful. |


<span id="ed90ff97"></span>
# Samples

The following section details the sample codes for the AckServerImpressions API.

<span id="fb01f45e"></span>
## Sample request

The following is a sample request for the API.

```JSON
curl --request POST \
     --url https://rec-us-east-1.byteplusapi.com/predict/api/media/media_demo/ack_server_impressions \
     --header 'Accept: application/json' \
     --header 'Request-Id: 2c568be9-1359-4c39-814c-e1f47d7571bc' \
     --header 'Content-Type: application/json' \
     --header 'Tenant-Id:d7c5963593798b5263858b028f589' \
     --header 'Tenant-Nonce:1683635274' \
     --header 'Tenant-Ts:1683635274' \
     --header 'Tenant-Signature:01c6789725810183bf1a90b659724e4c4fd7f9bd230bcf6abbc946e5831dac8b' \
     --data '{
     "predict_request_id": "221b7634-0a4c-497c-b268-e4b2f9b475b8",
     "scene": {
          "scene_name": "home",
          "page_number": 1
     },
     "altered_contents": [
          {
               "content_id": "632462",
               "altered_reason": "kept",
               "rank": 1
          },
          {
               "content_id": "632463",
               "altered_reason": "kept",
               "rank": 2
          },
          {
               "content_id": "632462",
               "altered_reason": "inserted",
               "rank": 3
          },
          {
               "content_id": "632465",
               "altered_reason": "kept",
               "rank": 4
          }
     ],
     "user_id": "123",
     "traffic_source": "byteplus",
     "extra": {
         "custom_field": "value"
     }
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


The following is a failed sample response.

```JSON
{
  "status": {
    "code": 400,
    "message": "unmarshal request body fail, plz make sure path is correct. path:/api/media/media_demo/ack_server_impressions, targetReqType:*media.AckServerImpressionsRequest; errID:1389471792 logID:2023033109270409BFE9F642F14569F555"
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

&nbsp;
