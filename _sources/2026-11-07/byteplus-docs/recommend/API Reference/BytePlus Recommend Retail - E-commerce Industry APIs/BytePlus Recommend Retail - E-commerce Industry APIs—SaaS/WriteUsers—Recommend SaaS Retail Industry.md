---
title: "WriteUsers—Recommend SaaS Retail Industry"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/reference-retail_saas_writeusers"
---

The WriteUsers API, specifically designed for Recommend SaaS in the Retail/E\-commerce industry, allows you to efficiently upload new user data or update existing user information.

<span id="a1abe13f"></span>
# Limitations

The following limitations apply to WriteUsers API:


* Each request can update no more than 2,000 user data records at a time. If you upload more than 2,000 user data records in a single request, you will encounter a rejection.

* The result obtained by multiplying QPS by the number of uploads per request must be less than 30,000.


<span id="36c7c3c1"></span>
# HTTP request


|**URL** |https://rec\-api\-sg1.recplusapi.com/RetailSaaS/WriteUsers |
|---|---|
|**Method** |POST |


<span id="b2cde28c"></span>
# Request parameters

The topics below details the parameters required for the WriteUsers API.

<span id="ec195085"></span>
## Header


|**Header Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Tenant\-Id |String |Yes |3000001813 |Your BytePlus account's ID. For more information on retrieving Recommend Tenant IDs, refer [here](https://docs.byteplus.com/recommend/docs/retail_standard_getting_started). |
|Request\-id |String |Yes |84kduxkls74lcdj73jdu3 |The client assigns the request id, and it should be unique for each request. No specific format is required for the request\-id, but it is advisable to keep it reasonably short.<br><br>For more information on request\-id generation code samples, refer [here](https://docs.byteplus.com/recommend/reference/api_token_authentication). |
|Other Auth Header |*  |Yes |*  |**Recommend Standard**<br><br>BytePlus Recommend SaaS Standard uses Access Key/Secret Key (AK/SK) for Byteplus Standard header authentication. The process of constructing these headers can be complex, so it is recommended to use the SDK for easier access and implementation.<br><br>For more information on using the AK/SK authentication, refer [here](https://docs.byteplus.com/en/recommend/reference/api_authentication#9e904017).<br><br>**Recommend Premium**<br><br>BytePlus Recommend SaaS Premium uses token header authentication.<br><br>For more information on using the SDK token authentication, refer [here](https://docs.byteplus.com/en/recommend/reference/api_token_authentication). |


<span id="1dad2339"></span>
## Body

The following table details the body parameters required for the WriteUsers API.


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|project_id |String |Yes |851467130 |The unique identifier for the Recommend project. |
|stage |String |Yes |production |The data import stage corresponds to the stages in the BytePlus Recommend Console. Accepted values for this stage include:<br><br><br>* production: this indicates the historical data synchronization stage, where the data is used for training the model.<br><br>* incremental_sync_streaming: this indicates the incremental real\-time data synchronization stage, where data is used to update the model in real\-time. |
|data |Array of Strings |Yes |*  |The user data is an array of data records, where each record follows the Schema defined in your SaaS platform and contains field names and types that are consistent with the Schema. Each element in the array represents one data record and is serialized as a JSON string. To send data using the Write APIs, the JSON array should be serialized into a string and included in the API request.<br><br>```JSON```<br>```[```<br>``` {```<br>```   "user_id": "1457789",```<br>```   "gender": "male",```<br>```   "age": "23",```<br>```   "tags": "[\"new user\",\"low purchasing power\",\"bargain seeker\"]",```<br>```   "activation_channel": "AppStore",```<br>```   "membership_level": "silver",```<br>```   "registration_timestamp": 1623593487,```<br>```   "city": "Kirkland",```<br>```   "country": "USA",```<br>```   "district": "King County",```<br>```   "province": "Texas",```<br>```   "language": "English"```<br>``` },```<br>```{```<br>```   "user_id": "1457790",```<br>```   "gender": "female",```<br>```   "age": "20-40",```<br>```   "tags": "[\"new user\"]",```<br>```   "activation_channel": "AppStore",```<br>```   "membership_level": "silver",```<br>```   "registration_timestamp": 1623593490,```<br>```   "city": "Kirkland",```<br>```   "country": "USA",```<br>```   "district": "King County",```<br>```   "province": "Texas",```<br>```   "language": "English"```<br>``` }```<br>```]```<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The data format should match the data schema submitted through the BytePlus Recommend platform.</div><br> |
|extra |Map<String, String\> |No |*  |A catch\-all field to pass any additional information. You should provide as much information as possible using this field. |


<span id="b925110b"></span>
### Extra

This is a field for additional information. It contains the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|newkey |String |*  |*  |*  |
|New Value |String |*  |*  |*  |


<span id="0ce09166"></span>
# Response parameters

The following tables details the response parameters for the WriteUsers API:


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|status |Object |*  |The status defines an error model. It contains two types of data: error code and error message. |
|errors |Array of Objects |*  |This field is populated when the status is an error code: 1001. |


<span id="beb68e9e"></span>
## **Status**

The `status` defines an error model. Each `status` message contains two types of data: error code and error message.


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|code |Int32 |0 |You should look at this response parameter to determine if your API request was successful or not. The accepted values include:<br><br><br>* 0: it indicates that the calling is successful.<br><br>* 4xx: it indicates user error.<br><br>* 5xx: it indicates server error.<br><br>* 1xxx: it indicates error relating to Import calls.<br><br>* 2xxx: it indicates errors relating to Predict calls. |
|message |String |An unexpected value XXX is included in the XXX field, only ["xx", "yy", "zz"] can be accepted. |Provides a detailed error message on the reasons why your API request was unsuccessful. |


<span id="ed90ff97"></span>
# Samples

The following section details the sample codes for the WriteUsers API.

<span id="fb01f45e"></span>
## Sample request

The following is a sample request for the API.

```JSON
curl --request POST \
     --url https://rec-api-sg1.recplusapi.com/RetailSaaS/WriteUsers \
     --header 'Tenant-Id: 3000001813' \
     --header 'Request-Id:12313208' \
     --header 'accept: application/json' \
     --header 'content-type: application/json' \
     --data '
{
  "project_id": "851467130",
  "stage": "production",
  "data": [
    "{\"user_id\":\"14577890\",\"gender\":\"male\",\"age\":\"23\",\"tags\":\"[\\\"new user\\\",\\\"low purchasing power\\\",\\\"bargain seeker\\\"]\",\"activation_channel\":\"AppStore\",\"membership_level\":\"silver\",\"registration_timestamp\":1623593487,\"city\":\"Kirkland\",\"country\":\"USA\",\"district\":\"King County\",\"province\":\"Texas\",\"language\":\"English\"}"
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
      "data": "{\"user_id\":\"\",\"gender\":\"male\",\"activation_channel\":\"AppStore\",\"membership_level\":\"silver\",\"registration_timestamp\":1623593487,\"age\":\"23\",\"tags\":\"[\\\"new user\\\",\\\"low purchasing power\\\",\\\"bargain seeker\\\"]\",\"city\":\"Kirkland\",\"country\":\"USA\",\"district\":\"King County\",\"province\":\"Texas\",\"language\":\"English\"}"
    }
  ]
}
```


<span id="9398e94b"></span>
# Error codes

For more information on the API error codes, refer to [BytePlus Recommend shared error and status codes](https://docs.byteplus.com/recommend/reference/shared_error_and_status_codes).
