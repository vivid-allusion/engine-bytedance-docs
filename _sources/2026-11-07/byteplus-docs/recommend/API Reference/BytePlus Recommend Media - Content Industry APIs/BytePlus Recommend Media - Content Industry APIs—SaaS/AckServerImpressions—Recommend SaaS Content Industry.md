---
title: "AckServerImpressions—Recommend SaaS Content Industry"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/reference-content_saas_ackserverimpressions"
---

With the AckServerImpressions API, you can conveniently send back the actual content list shown to users in the Media/Content industry for BytePlus Recommend SaaS.

<span id="36c7c3c1"></span>
# HTTP request

This is the URL and HTTP request method for the AckServerImpressions API.


|**URL** |https://rec\-api\-sg1.recplusapi.com/ContentSaaS/AckServerImpressions |
|---|---|
|**Method** |POST |


<span id="d5e9f3b3"></span>
# Request parameters

The topics below details the parameters required for the AckServerImpressions API:

<span id="67b5f9b5"></span>
## Header


|**Header Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Tenant\-Id |String |Yes |3000001813 |Your BytePlus account's ID. For more information on retrieving Recommend Tenant IDs, refer [here](https://docs.byteplus.com/recommend/docs/content_standard_getting_started). |
|Request\-id |String |Yes |84kduxkls74lcdj73jdu3 |The client assigns the request id, and it should be unique for each request. No specific format is required for the request\-id, but it is advisable to keep it reasonably short.<br><br>For more information on request\-id generation code samples, refer [here](https://docs.byteplus.com/recommend/reference/api_token_authentication). |
|Other Auth Header |*  |Yes |*  |**Recommend Standard**<br><br>BytePlus Recommend SaaS Standard uses Access Key/Secret Key (AK/SK) for Byteplus Standard header authentication. The process of constructing these headers can be complex, so it is recommended to use the SDK for easier access and implementation.<br><br>For more information on using the AK/SK authentication, refer [here](https://docs.byteplus.com/en/recommend/reference/api_authentication#9e904017).<br><br>**Recommend Premium**<br><br>BytePlus Recommend SaaS Premium uses token header authentication.<br><br>For more information on using the SDK token authentication, refer [here](https://docs.byteplus.com/en/recommend/reference/api_token_authentication). |


<span id="1dad2339"></span>
## Body

The following table details the body parameters required for the AckServerImpressions API:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|project_id |String |Yes |807247981 |The unique identifier for the recommendation project. |
|model_id |String |Yes |100001 |The unique identifier for the recommendation model used. |
|predict_request_id |String |Yes |a098df23\-6e45\-47a9\-875a\-f48f06831bc3 |The Predict API's request ID. The value should be the same as `PredictRequest.request_id`. |
|user_id |String |Yes |1457789 |The user ID used in the Predict API's call. The value should be the same as `PredictRequest.user_id`. |
|traffic_source |String |Yes |Self |The source of the recommendation.<br><br>The accepted values are:<br><br><br>* Self—indicates that the recommendation came from the caller's own engine.<br><br>* BytePlus—indicates that the recommendation came from BytePlus.<br><br>* Other—indicates that the recommendation came from a third\-party engine. |
|scene |Object |Yes |*  |The recommendation scene information.<br><br>You should ensure that this value is as close to `UserEvent.scene` as possible. |
|altered_contents |Array of Objects |Yes |*  |The list of altered contents. |
|extra |Object |No |*  |A catch\-all field to pass any additional information.<br><br>You should provide as much information as possible using this field. |


<span id="8421c784"></span>
### **Scene**

Scene refers to the location where the user interaction event happened. The scene proto contains the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|scene_name |String |Yes |home |The name of the scene the UserEvent occurred in. The same parameter value as `UserEvent.scene_name`. |
|page_number |Int32 |No |1 |The page number.<br><br>This field can refer to:<br><br><br>* the page number that the content is found on.<br><br>* the number of times that users swipe the screen before seeing the content.<br><br><br>The default value is 0, which indicates that all content fits into a single page. |
|offset |Int32 |No |10 |The content's position within the page itself. |


<span id="35def908"></span>
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

<span id="819a237c"></span>
## Default


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|error |String |*  |*  |
|code |Int32 |0 |You should look at this response parameter to determine if your API request was successful or not.<br><br><br>* 0: it indicates that the calling is successful.<br><br>* 4xx: it indicates user error.<br><br>* 5xx: it indicates server error.<br><br>* 1xxx: it indicates error relating to Import calls.<br><br>* 2xxx: it indicates errors relating to Predict calls. |
|message |String |An unexpected value XXX is included in the XXX field, only ["xx", "yy", "zz"] can be accepted. |Provides a detailed error message on the reasons why your API request was unsuccessful. |
|details |Array of Objects |*  |Provides detailed information about the error. |


<span id="7ce314fc"></span>
### Details

This parameter provides detailed information about the error. It contains the following fields:


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|status |Object |*  |This field defines a logical error model. It contains two types of data: error code and error message. |


<span id="dc98bae8"></span>
## **Status**

The `status` defines an error model. Each `status` message contains two types of data: error code and error message.


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
     --url https://rec-api-sg1.recplusapi.com/ContentSaaS/AckServerImpressions \
     --header 'Tenant-Id: 3000001813' \
     --header 'Request-Id: 2c568be9-1359-4c39-814c-e1f47d7571bc' \
     --header 'accept: application/json' \
     --header 'content-type: application/json' \
     --data '
{
  "project_id": "807247981",
  "model_id": "100001",
  "predict_request_id": "221b7634-0a4c-497c-b268-e4b2f9b475b8",
  "user_id": "14577890",
  "scene": {
    "scene_name": "home_page",
    "page_number": 1,
    "offset": 10
  },
  "altered_contents": [
    {
      "extra": {
        "extra_key": "extra_value"
      },
      "content_id": "6324610",
      "altered_reason": "kept",
      "rank": 1
    },
    {
      "extra": {
        "extra_key": "extra_value"
      },
      "content_id": "6324611",
      "altered_reason": "kept",
      "rank": 2
    },
    {
      "extra": {
        "extra_key": "extra_value"
      },
      "content_id": "6324612",
      "altered_reason": "inserted",
      "rank": 3
    },
    {
      "extra": {
        "extra_key": "extra_value"
      },
      "content_id": "6324613",
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
    "message": "unmarshal request body fail, plz make sure path is correct. path:/ContentSaaS/AckServerImpressions, targetReqType:*saas.AckServerImpressionsRequest; errID:852940573 logID:202304041027049278AA2F7CA2A95A785F" 
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


<span id="62018f80"></span>
# Error codes

For more information on the API error codes, refer to [BytePlus Recommend shared error and status codes](https://docs.byteplus.com/recommend/reference/shared_error_and_status_codes).

&nbsp;
