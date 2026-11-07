---
title: "WriteUserEvents—Recommend SaaS Retail Industry"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/reference-retail_saas_writeuserevents"
---

The WriteUserEvents API enables the seamless uploading of real\-time UserEvent data in the Retail/E\-commerce industry specifically for BytePlus Recommend SaaS.

<span id="a1abe13f"></span>
# Limitations

The following limitations apply to WriteUserEvents API:


* Each request can upload no more than 2,000 UserEvent data records at a time. If you upload more than 2,000 UserEvent data records in a single request, you will encounter a rejection.

* The result obtained by multiplying QPS by the number of uploads per request must be less than 30,000.


<span id="36c7c3c1"></span>
# HTTP request


|**URL** |https://rec\-api\-sg1.recplusapi.com/RetailSaaS/WriteUserEvents |
|---|---|
|**Method** |POST |


<span id="d5e9f3b3"></span>
# Request parameters

The topics below details the parameters required for the WriteUserEvents API.

<span id="df2272f4"></span>
## Header


|**Header Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Tenant\-Id |String |Yes |3000001813 |Your BytePlus account's ID. For more information on retrieving Recommend Tenant IDs, refer [here](https://docs.byteplus.com/recommend/docs/retail_standard_getting_started). |
|Request\-id |String |Yes |84kduxkls74lcdj73jdu3 |The client assigns the request id, and it should be unique for each request. No specific format is required for the request\-id, but it is advisable to keep it reasonably short.<br><br>For more information on request\-id generation code samples, refer [here](https://docs.byteplus.com/recommend/reference/api_token_authentication). |
|Other Auth Header |*  |Yes |*  |**Recommend Standard**<br><br>BytePlus Recommend SaaS Standard uses Access Key/Secret Key (AK/SK) for Byteplus Standard header authentication. The process of constructing these headers can be complex, so it is recommended to use the SDK for easier access and implementation.<br><br>For more information on using the AK/SK authentication, refer [here](https://docs.byteplus.com/en/recommend/reference/api_authentication#9e904017).<br><br>**Recommend Premium**<br><br>BytePlus Recommend SaaS Premium uses token header authentication.<br><br>For more information on using the SDK token authentication, refer [here](https://docs.byteplus.com/en/recommend/reference/api_token_authentication). |


<span id="1dad2339"></span>
## Body

The following table details the body parameters required for the WriteUserEvents API.


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|project_id |String |Yes |851467130 |The unique identifier for the Recommend project. |
|stage |String |Yes |production |The data import stage corresponds to the stages in the BytePlus Recommend Console. Accepted values for this stage include:<br><br><br>* production: this indicates the historical data synchronization stage, where the data is used for training the model.<br><br>* incremental_sync_streaming: this indicates the incremental real\-time data synchronization stage, where data is used to update the model in real\-time. |
|data |Array of Strings |Yes |*  |This is an array of UserEvent data where the field names and field types align with the Schema defined in the BytePlus Recommend Console. Each element in the array represents a single data record and is serialized as a JSON string. When using the Write APIs to send data, you should serialize the following JSON array into a string:<br><br>```JSON```<br>```[```<br>``` {```<br>```   "user_id": "1457789",```<br>```   "event_type": "click",```<br>```   "event_timestamp": 1640657087,```<br>```   "scene_name": "product detail page",```<br>```   "page_number": 2,```<br>```   "offset": 10,```<br>```   "product_id": "632461",```<br>```   "platform": "app",```<br>```   "os_type": "android",```<br>```   "app_version": "9.2.0",```<br>```   "device_model": "huawei-mate30",```<br>```   "os_version": "10",```<br>```   "network": "3g",```<br>```   "query": "iPad",```<br>```   "parent_product_id": "441356",```<br>```   "attribution_token": "eyJpc3MiOiJuaW5naGFvLm5ldCIsImV4cCI6IjE0Mzg5NTU0NDUiLCJuYW1lIjoid2FuZ2hhbyIsImFkbWluIjp0cnVlfQ",```<br>```   "traffic_source": "self",```<br>```   "purchase_count": 20,```<br>```   "paid_price": 100.12,```<br>```   "currency": "USD",```<br>```   "city": "Kirkland",```<br>```   "country": "USA",```<br>```   "district": "King County",```<br>```   "province": "Texas"```<br>``` }```<br>```]```<br> |
|extra |Map<String, String\> |No |*  |This is a field for additional information. You should provide as much information as possible. |


<span id="bf57b5c3"></span>
### Extra

This is a field for additional information. It contains the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|newkey |String |*  |*  |*  |
|New Value |String |*  |*  |*  |


<span id="0ce09166"></span>
# Response parameters

The following tables details the response parameters for the WriteUserEvents API.


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|status |Object |*  |This field defines an error model. It contains two types of data: error code and error message. |
|errors |Array of Objects |*  |This field is populated when the statusis an error code: 1001. |


<span id="af5704dc"></span>
## **Status**

The `status` defines an error model. Each `status` message contains two types of data: error code and error message.


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|code |Int32 |0 |You should look at this response parameter to determine if your API request was successful or not. The accepted values include:<br><br><br>* 0: it indicates that the calling is successful.<br><br>* 4xx: it indicates user error.<br><br>* 5xx: it indicates server error.<br><br>* 1xxx: it indicates error relating to Import calls.<br><br>* 2xxx: it indicates errors relating to Predict calls. |
|message |String |An unexpected value XXX is included in the XXX field, only ["xx", "yy", "zz"] can be accepted. |Provides a detailed error message on the reasons why your API request was unsuccessful. |


<span id="ed90ff97"></span>
# Samples

The following section details the sample codes for the WriteUserEvents API.

<span id="fb01f45e"></span>
## Sample request

The following is a sample request for the API.

```JSON
curl --request POST \
     --url https://rec-api-sg1.recplusapi.com/RetailSaaS/WriteUserEvents \
     --header 'Tenant-Id: 3000001813' \
     --header 'Request-Id:12313207' \
     --header 'accept: application/json' \
     --header 'content-type: application/json' \
     --data '
{
  "project_id": "851467130",
  "stage": "production",
  "data": [
    "{\"user_id\": \"1457789\", \"event_type\": \"click\", \"event_timestamp\": 1686643067, \"scene_name\": \"product detail page\", \"page_number\": 2, \"offset\": 10, \"product_id\": \"632461\", \"platform\": \"app\", \"os_type\": \"android\", \"app_version\": \"9.2.0\", \"device_model\": \"huawei-mate30\", \"os_version\": \"10\", \"network\": \"3g\", \"query\": \"iPad\", \"parent_product_id\": \"441356\", \"attribution_token\": \"eyJpc3MiOiJuaW5naGFvLm5ldCIsImV4cCI6IjE0Mzg5NTU0NDUiLCJuYW1lIjoid2FuZ2hhbyIsImFkbWluIjp0cnVlfQ\", \"traffic_source\": \"self\", \"purchase_count\": 20, \"paid_price\": 100.12, \"currency\": \"USD\", \"city\": \"Kirkland\", \"country\": \"USA\", \"district\": \"King County\", \"province\": \"Texas\"}"
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
      "message": "in the 'user_id' field, required field is empty",
      "data": "{\"device_os_version\":\"10\",\"device_browser_type\":\"chrome\",\"context_query\":\"iPad\",\"traffic_source\":\"self\",\"user_id\":\"\",\"product_id\":\"632461\",\"device_os_type\":\"android\",\"device_app_version\":\"9.2.0\",\"detail_page_stay_time\":10,\"rec_info\":\"CiRiMjYyYjM1YS0xOTk1LTQ5YmMtOGNkNS1mZTVmYTczN2FkNDASJAobcmVjZW50X2hvdF9jbGlja3NfcmV0cmlldmVyFQAAAAAYDxoKCgNjdHIdog58PBoKCgNjdnIdANK2OCIHMjcyNTgwMg==\",\"purchase_count\":20,\"event_type\":\"purchase\",\"event_timestamp\":1683605111,\"scene\":\"product detail page\",\"device_network\":\"3g\",\"device_device_model\":\"huawei-mate30\",\"device_user_agent\":\"Mozilla/5.0 (Linux; Android 10; TAS-AN00; HMSCore 5.3.0.312) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.106 HuaweiBrowser/11.0.8.303 Mobile Safari/537.36\",\"context_root_product_id\":\"441356\",\"attribution_token\":\"eyJpc3MiOiJuaW5naGFvLm5ldCIsImV4cCI6IjE0Mzg5NTU0NDUiLCJuYW1lIjoid2FuZ2hhbyIsImFkbWluIjp0cnVlfQ\",\"scene_page_number\":2,\"scene_offset\":10,\"device_platform\":\"app\",\"device_device_brand\":\"huawei\"}"
    }
  ]
}
```


<span id="9398e94b"></span>
# Error codes

For more information on the API error codes, refer to [BytePlus Recommend shared error and status codes](https://docs.byteplus.com/recommend/reference/shared_error_and_status_codes).
