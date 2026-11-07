---
title: "WriteContents—Recommend SaaS Content Industry"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/reference-content_saas_writecontents"
---

The WriteContents API for BytePlus Recommend SaaS enables the uploading of new content data or updating existing content data in the Media/Content industry.

<span id="2e421388"></span>
# Limitations

The following limitations apply to WriteContents API:


* Each request can upload no more than 2,000 content data records at a time. If you upload more than 2,000 content data records in a single request, you will encounter a rejection.

* The result obtained by multiplying QPS by the number of uploads per request must be less than 30,000.


<span id="36c7c3c1"></span>
# HTTP request

This is the URL and HTTP request method for the WriteContents API.


|**URL** |https://rec\-api\-sg1.recplusapi.com/ContentSaaS/WriteContents |
|---|---|
|**Method** |POST |


<span id="d5e9f3b3"></span>
# Request parameters

The topics below details the parameters required for the WriteContents API.

<span id="df2272f4"></span>
## Header

The following table details the metadata parameters required for the WriteContents API:


|**Header Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Tenant\-Id |String |Yes |3000001813 |Your BytePlus account's ID. For more information on retrieving Recommend Tenant IDs, refer [here](https://docs.byteplus.com/recommend/docs/content_standard_getting_started). |
|Request\-id |String |Yes |84kduxkls74lcdj73jdu3 |The client assigns the request id, and it should be unique for each request. No specific format is required for the request\-id, but it is advisable to keep it reasonably short.<br><br>For more information on request\-id generation code samples, refer [here](https://docs.byteplus.com/recommend/reference/api_token_authentication). |
|Other Auth Header |*  |Yes |*  |**Recommend Standard**<br><br>BytePlus Recommend SaaS Standard uses Access Key/Secret Key (AK/SK) for Byteplus Standard header authentication. The process of constructing these headers can be complex, so it is recommended to use the SDK for easier access and implementation.<br><br>For more information on using the AK/SK authentication, refer [here](https://docs.byteplus.com/en/recommend/reference/api_authentication#9e904017).<br><br>**Recommend Premium**<br><br>BytePlus Recommend SaaS Premium uses token header authentication.<br><br>For more information on using the SDK token authentication, refer [here](https://docs.byteplus.com/en/recommend/reference/api_token_authentication). |


<span id="144f0eac"></span>
## Body

The following table details the body parameters required for the WriteContents API:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|project_id |String |Yes |807247981 |The unique identifier for the recommendation project. |
|stage |String |Yes |production |The data import stage corresponds to the stages in the BytePlus Recommend Console. Accepted values for this stage include:<br><br><br>* production: this indicates the historical data synchronization stage, where the data is used for training the model.<br><br>* incremental_sync_streaming: this indicates the incremental real\-time data synchronization stage, where data is used to update the model in real\-time. |
|data |Array of Strings |Yes |*  |This is an array of content data where the field names and field types align with the Schema defined in the BytePlus Recommend Console. Each element in the array represents a single data record and is serialized as a JSON string. When using the Write APIs to send data, you should serialize the following JSON array into a string:<br><br>```JSON```<br>```[```<br>``` {```<br>```   "content_id": "632461",```<br>```   "is_recommendable": 1,```<br>```   "categories": "[{\"category_depth\":1,\"category_nodes\":[{\"id_or_name\":\"Movie\"}]},{\"category_depth\":2,\"category_nodes\":[{\"id_or_name\":\"Comedy\"}]}]",```<br>```   "content_type": "video",```<br>```   "video_duration": 1200000,```<br>```   "content_title": "Green Book Movie Explanation",```<br>```   "description": "A brief summary of the main content of the Green Book movie",```<br>```   "content_owner": "1457789",```<br>```   "collection_id": "1342",```<br>```   "tags": "[\"New\",\"Trending\"]",```<br>```   "image_urls": "[\"https://images-na.ssl-images-amazon.com/images/I/81WmojBxvbL._AC_UL1500.jpg\"]",```<br>```   "video_urls": "[\"https://test_video.mov\"]",```<br>```   "user_rating": 4.9,```<br>```   "current_price": 130.05,```<br>```   "original_price": 160.05,```<br>```   "publish_timestamp": 1660035734,```<br>```   "is_paid_content": true,```<br>```   "language": "English",```<br>```   "linked_product_id": "[\"632462\",\"632463\"]",```<br>```   "source": "self"```<br>``` }```<br>```]```<br> |
|extra |Map<String, String\> |No |*  |A catch\-all field to pass any additional information.<br><br>You should provide as much information as possible using this field. |


<span id="0ce09166"></span>
# Response parameters

The following tables details the response parameters for the WriteContents API:


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|status |Object |*  |The status defines an error model. Each status message contains two types of data: error code and error message. |
|errors |Array of Objects |*  |This field is populated when the status is an error code: 1001. |


<span id="ba98dcea"></span>
## **Status**

The `status` defines an error model. Each `status` message contains two types of data: error code and error message.


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|code |Int32 |0 |You should look at this response parameter to determine if your API request was successful or not. The accepted values are:<br><br><br>* 0: it indicates that the calling is successful.<br><br>* 4xx: it indicates user error.<br><br>* 5xx: it indicates server error.<br><br>* 1xxx: it indicates error relating to Import calls.<br><br>* 2xxx: it indicates errors relating to Predict calls. |
|message |String |An unexpected value XXX is included in the XXX field, only ["xx", "yy", "zz"] can be accepted. |Provides a detailed error message on the reasons why your API request was unsuccessful. |


<span id="ed90ff97"></span>
# Samples

The following section details the sample codes for the WriteContents API.

<span id="fb01f45e"></span>
## Sample request

The following is a sample request for the API.

```JSON
curl --request POST \
     --url https://rec-api-sg1.recplusapi.com/ContentSaaS/WriteContents \
     --header 'Tenant-Id: 3000001813' \
     --header 'Request-Id:12313207' \
     --header 'accept: application/json' \
     --header 'content-type: application/json' \
     --data '
{
  "project_id": "807247981",
  "stage": "production",
  "data": [
    "{\"content_id\": \"632461\", \"is_recommendable\": 1, \"categories\": \"[{\\\"category_depth\\\":1,\\\"category_nodes\\\":[{\\\"id_or_name\\\":\\\"Movie\\\"}]},{\\\"category_depth\\\":2,\\\"category_nodes\\\":[{\\\"id_or_name\\\":\\\"Comedy\\\"}]}]\", \"content_type\": \"video\", \"video_duration\": 1200000, \"content_title\": \"Green Book Movie Explanation\", \"description\": \"A brief summary of the main content of the Green Book movie\", \"content_owner\": \"1457789\", \"collection_id\": \"1342\", \"tags\": \"[\\\"New\\\",\\\"Trending\\\"]\", \"image_urls\": \"[\\\"https://images-na.ssl-images-amazon.com/images/I/81WmojBxvbL._AC_UL1500.jpg\\\"]\", \"video_urls\": \"[\\\"https://test_video.mov\\\"]\", \"user_rating\": 4.9, \"current_price\": 130.05, \"original_price\": 160.05, \"publish_timestamp\": 1660035734, \"is_paid_content\": true, \"language\": \"English\", \"linked_product_id\": \"[\\\"632462\\\",\\\"632463\\\"]\", \"source\": \"self\"}"
  ]
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


The following is a failed sample response.

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
      "message": "in the 'content_id' field, required field is empty",
      "data": "{\"content_id\": \"\", \"is_recommendable\": 1, \"categories\": \"[{\\\"category_depth\\\":1,\\\"category_nodes\\\":[{\\\"id_or_name\\\":\\\"Movie\\\"}]},{\\\"category_depth\\\":2,\\\"category_nodes\\\":[{\\\"id_or_name\\\":\\\"Comedy\\\"}]}]\", \"content_type\": \"video\", \"video_duration\": 1200000, \"content_title\": \"Green Book Movie Explanation\", \"description\": \"A brief summary of the main content of the Green Book movie\", \"content_owner\": \"1457789\", \"collection_id\": \"1342\", \"tags\": \"[\\\"New\\\",\\\"Trending\\\"]\", \"image_urls\": \"[\\\"https://images-na.ssl-images-amazon.com/images/I/81WmojBxvbL._AC_UL1500.jpg\\\"]\", \"video_urls\": \"[\\\"https://test_video.mov\\\"]\", \"user_rating\": 4.9, \"current_price\": 130.05, \"original_price\": 160.05, \"publish_timestamp\": 1660035734, \"is_paid_content\": true, \"language\": \"English\", \"linked_product_id\": \"[\\\"632462\\\",\\\"632463\\\"]\", \"source\": \"self\"}"
    }
  ]
}
```


<span id="9398e94b"></span>
# Error codes

For more information on the API error codes, refer to [BytePlus Recommend shared error and status codes](https://docs.byteplus.com/recommend/reference/shared_error_and_status_codes).
