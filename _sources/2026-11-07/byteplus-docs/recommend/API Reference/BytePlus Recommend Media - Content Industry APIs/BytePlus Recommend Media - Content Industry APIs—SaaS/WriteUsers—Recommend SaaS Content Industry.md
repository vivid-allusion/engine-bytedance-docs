---
title: "WriteUsers—Recommend SaaS Content Industry"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/reference-content_saas_writeusers"
---

The WriteUsers API for BytePlus Recommend SaaS facilitates the uploading of new user data or updating existing user data in the Media/Content industry.

<span id="82655cb9"></span>
# Limitations

The following limitations apply to WriteUsers API:


* Each request can upload no more than 2,000 user data records at a time. If you upload more than 2,000 user data records in a single request, you will encounter a rejection.

* The result obtained by multiplying QPS by the number of uploads per request must be less than 30,000.


<span id="36c7c3c1"></span>
# HTTP request

This is the URL and HTTP request method for the WriteUsers API.


|**URL** |https://rec\-api\-sg1.recplusapi.com/ContentSaaS/WriteUsers |
|---|---|
|**Method** |POST |


<span id="d5e9f3b3"></span>
# Request parameters

The topics below details the parameters required for the WriteUsers API.

<span id="df2272f4"></span>
## Header

The following table details the header parameters required for the WriteUsers API:


|**Header Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Tenant\-Id |String |Yes |3000001813 |Your BytePlus account's ID. For more information on retrieving Recommend Tenant IDs, refer [here](https://docs.byteplus.com/recommend/docs/content_standard_getting_started). |
|Request\-id |String |Yes |84kduxkls74lcdj73jdu3 |The client assigns the request id, and it should be unique for each request. No specific format is required for the request\-id, but it is advisable to keep it reasonably short.<br><br>For more information on request\-id generation code samples, refer [here](https://docs.byteplus.com/recommend/reference/api_token_authentication). |
|Other Auth Header |*  |Yes |*  |**Recommend Standard**<br><br>BytePlus Recommend SaaS Standard uses Access Key/Secret Key (AK/SK) for Byteplus Standard header authentication. The process of constructing these headers can be complex, so it is recommended to use the SDK for easier access and implementation.<br><br>For more information on using the AK/SK authentication, refer [here](https://docs.byteplus.com/en/recommend/reference/api_authentication#9e904017).<br><br>**Recommend Premium**<br><br>BytePlus Recommend SaaS Premium uses token header authentication.<br><br>For more information on using the SDK token authentication, refer [here](https://docs.byteplus.com/en/recommend/reference/api_token_authentication). |


<span id="1dad2339"></span>
## Body

The following table details the body parameters required for the WriteUsers API:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|project_id |String |Yes |807247981 |The unique identifier for the recommendation project. |
|stage |String |Yes |production |The data import stage corresponds to the stages in the BytePlus Recommend Console. Accepted values for this stage include:<br><br><br>* production: this indicates the historical data synchronization stage, where the data is used for training the model.<br><br>* incremental_sync_streaming: this indicates the incremental real\-time data synchronization stage, where data is used to update the model in real\-time. |
|data |Array of Strings |Yes |*  |This is an array of user data where the field name and field type adhere to the Schema defined in the BytePlus Recommend Console. Each element in the array is a JSON serialized string representing a single data record. When using the Write APIs, the following JSON array should be serialized into a string:<br><br>```JSON```<br>```[```<br>``` {```<br>```   "user_id": "1457789",```<br>```   "gender": "male",```<br>```   "age": "23",```<br>```   "tags": "[\"new user\",\"low purchasing power\",\"bargain seeker\"]",```<br>```   "language": "English",```<br>```   "subscriber_type": "free",```<br>```   "membership_level": "silver",```<br>```   "registration_timestamp": 1659958007,```<br>```   "country": "USA",```<br>```   "province": "Texas",```<br>```   "city": "Kirkland",```<br>```   "district": "King County"```<br>``` },```<br>``` {```<br>```   "user_id": "1457790",```<br>```   "gender": "female",```<br>```   "age": "20-40",```<br>```   "tags": "[\"new user\"]",```<br>```   "language": "English",```<br>```   "subscriber_type": "free",```<br>```   "membership_level": "silver",```<br>```   "registration_timestamp": 1659957007,```<br>```   "country": "USA",```<br>```   "province": "Texas",```<br>```   "city": "Kirkland",```<br>```   "district": "King County"```<br>``` }```<br>```]```<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The data format should match the data schema submitted through the BytePlus Recommend platform.</div><br> |
|extra |Map<String, String\> |No |*  |A catch\-all field to pass any additional information.<br><br>You should provide as much information as possible using this field. |


<span id="0ce09166"></span>
# Response parameters

The following tables details the response parameters for the WriteUsers API:


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|status |Object |*  |It defines an error model. Each status contains two types of data: error code and error message. |
|errors |Array of Objects |*  |This field is populated when the status is an error code: 1001. |


<span id="4acd1f1a"></span>
## **Status**

The `status` defines an error model. Each `status` message contains two types of data: error code and error message.


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|code |Int32 |0 |You should look at this response parameter to determine if your API request was successful or not. The accepted values are:<br><br><br>* 0: it indicates that the calling is successful.<br><br>* 4xx: it indicates user error.<br><br>* 5xx: it indicates server error.<br><br>* 1xxx: it indicates error relating to Import calls.<br><br>* 2xxx: it indicates errors relating to Predict calls. |
|message |String |An unexpected value XXX is included in the XXX field, only ["xx", "yy", "zz"] can be accepted. |Provides a detailed error message on the reasons why your API request was unsuccessful. |


<span id="ed90ff97"></span>
# Samples

The following section details the sample codes for the WriteUsers API.

<span id="fb01f45e"></span>
## Sample request

The following is a sample request for the API.

```JSON
curl --request POST \
     --url https://rec-api-sg1.recplusapi.com/ContentSaaS/WriteUsers \
     --header 'Tenant-Id: 3000001813' \
     --header 'Request-Id:12313208' \
     --header 'accept: application/json' \
     --header 'content-type: application/json' \
     --data '
{
  "project_id": "807247981",
  "stage": "production",
  "data": [
    "{\"user_id\": \"1457789\", \"gender\": \"male\", \"age\": \"23\", \"tags\": \"[\\\"new user\\\",\\\"low purchasing power\\\",\\\"bargain seeker\\\"]\", \"language\": \"English\", \"subscriber_type\": \"free\", \"membership_level\": \"silver\", \"registration_timestamp\": 1659958007, \"country\": \"USA\", \"province\": \"Texas\", \"city\": \"Kirkland\", \"district\": \"King County\"}"
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
      "message": "in the 'user_id' field, required field is empty",
      "data": "{\"province\":\"Texas\",\"district\":\"King County\",\"os_type\":\"ios\",\"os_version\":\"14.4.2\",\"membership_level\":\"silver\",\"last_login_timestamp\":1659958207,\"area\":\"Neighborhood #1\",\"user_id\":\"\",\"gender\":\"male\",\"language\":\"English\",\"app_version\":\"1.0.1\",\"device_model\":\"iPhone10\",\"user_id_type\":\"system_generated\",\"age\":\"23\",\"platform\":\"app\",\"registration_timestamp\":1659958007,\"update_timestamp\":1659958007,\"country\":\"USA\",\"city\":\"Kirkland\",\"tags\":\"[\\\"new user\\\",\\\"low purchasing power\\\",\\\"bargain seeker\\\"]\",\"subscriber_type\":\"free\",\"network\":\"4g\"}"
    }
  ]
}
```


<span id="9398e94b"></span>
# Error codes

For more information on the API error codes, refer to [BytePlus Recommend shared error and status codes](https://docs.byteplus.com/recommend/reference/shared_error_and_status_codes).
