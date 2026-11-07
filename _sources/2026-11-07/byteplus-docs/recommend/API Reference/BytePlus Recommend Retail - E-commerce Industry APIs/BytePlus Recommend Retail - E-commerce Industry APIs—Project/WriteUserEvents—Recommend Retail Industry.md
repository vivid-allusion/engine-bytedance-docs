---
title: "WriteUserEvents—Recommend Retail Industry"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/reference-retail_writeuserevents"
---

The WriteUserEvents API enables the seamless uploading of real\-time UserEvent data in the Retail/E\-commerce industry specifically for BytePlus Recommend.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Duplication is not supported when processing real\-time data. Ensure that the UserEvent data is deduplicated before importing.</div>


For more information on BytePlus Recommend token authentication, refer [here](https://docs.byteplus.com/en/recommend/reference/api_token_authentication).

<span id="a1abe13f"></span>
# Limitations

The following limitations apply to WriteUserEvents API:


* Each request can upload no more than 2,000 UserEvent data records at a time. If you upload more than 2,000 UserEvent data records in a single request, you will encounter a rejection.

* The result obtained by multiplying QPS by the number of uploads per request must be less than 30,000.


<span id="36c7c3c1"></span>
# HTTP request


|**URL** |https://rec\-ap\-singapore\-1.byteplusapi.com/data/api/retail/${tenant}/user_event |
|---|---|
|**Method** |POST |


<span id="d5e9f3b3"></span>
# Request parameters

The topics below details the parameters required for the WriteUserEvents API.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Not all request parameters are included in the following table. For a complete list, refer to <a href="https://docs.byteplus.com/recommend/reference/api_token_authentication">HTTP header parameters</a>.</div>


<span id="144f0eac"></span>
## Query

The following table details the query parameters required for the WriteUserEvents API:


|**Query String Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|method |String |Yes |Write |*  |


<span id="1dad2339"></span>
## Body

The following table details the body parameters required for the WriteUserEvents API:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|user_events |Array of Objects |Yes |*  |This is a list of UserEvent data intended for upload on the platform. The UserEvent list can contain a maximum of 2000 entries. If you exceed this limit, your request will be rejected. |
|extra |Object |No |*  |This field is used to pack key\-value pairs.<br><br>For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |


<span id="c641276d"></span>
### **User_events**

This field refers to a list of UserEvents data to be uploaded on the platform. It contains the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|user_id |String |Yes |1457789 |The unique identifier for the user. |
|event_type |String |Yes |purchase |The UserEvent type. The accepted values are:<br><br><br>* impression<br><br>* click<br><br>* add\-to\-cart<br><br>* remove\-from\-cart<br><br>* add\-to\-favorites<br><br>* remove\-from\-favorites<br><br>* purchase<br><br>* search<br><br>* stay\-detail\-page<br><br><br>For more information on the event_types and their requirements, refer to the [API Proto definitions](https://docs.byteplus.com/recommend/samples/retail_api_proto_definitions).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This field is only for the event type, the actual scene is kept separately.</div><br> |
|event_timestamp |Int64 |Yes |1623681888 |The timestamp when the event happened. |
|scene |Object |*  |*  |The scene where the event happened |
|product_id |String |No |632461 |The unique identifier for the product. This parameter should be empty if the event_type is "search", and otherwise it is required. |
|device |Object |*  |*  |The device proto. |
|context |Object |*  |*  |The context for this event. |
|attribution_token |String |No |eyJpc3MiOiJuaW5naGFvLm5ldCIsImV4cCI6IjE0Mzg5NTU0NDUiLCJuYW1lIjoid2FuZ2hhbyIsImFkbWluIjp0cnVlfQz |The identifier used to gather all the relevant events within one user session. |
|rec_info |String |No |CiRiMjYyYjM1YS0xOTk1LTQ5YmMtOGNkNS1mZTVmYTczN2FkNDASJAobcmVjZW50X2hvdF9jbGlja3NfcmV0cmlldmVyFQAAAAAYDxoKCgNjdHIdog58PBoKCgNjdnIdANK2OCIHMjcyNTgwMg== |BytePlus Recommend will provide this parameter value. It contains detailed algorithm information. For more information on ways to improve recommendation performance, refer [here](https://docs.byteplus.com/recommend/resources/ways_to_improve_recommendation_performance). |
|traffic_source |String |No |Self |The source of the directed traffic for this UserEvent. The accepted values are:<br><br><br>* Self—Self\-generated traffic<br><br>* BytePlus—BytePlus\-generated traffic<br><br>* Other—Other system\-generated traffic<br><br><br>For more information on ways to improve recommendation performance, refer [here](https://docs.byteplus.com/recommend/resources/ways_to_improve_recommendation_performance). |
|purchase_count |Int32 |No |20 |When event_type is "purchase", this parameter value must be more than 0. |
|detail_page_stay_time |Int32 |No |10 |The duration spent on the detail page. The value of this parameter depends on `event_type`. If the `event_type` is stay\-detail\-page, the parameter value must be more than 0. |
|extra |Object |No |*  |This field is used to pack key\-value pairs. For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |


<span id="8f482714"></span>
#### **Scene**

This field details the scene where the event happened. It contains the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|scene_name |String |Yes |Details page |The unique identifier for the UserEvent scene. The accepted values include:<br><br><br>* Home page<br><br>* Search page<br><br>* Details page<br><br><br>It is strongly recommended that you split the scene if possible. For more information on effective and efficient data synchronization, refer [here](https://docs.byteplus.com/recommend/resources/effective_and_efficient_data_synchronization). |
|page_number |Int32 |No |1 |The page number.<br><br>It can refer to:<br><br><br>* the page number that the content is found on.<br><br>* the number of times that users swipe the screen before seeing the content.<br><br><br>The default value is 0, which indicates that all content fits into a single page. |
|offset |Int32 |No |10 |The content's position within the page itself. |


<span id="83c6fc1c"></span>
#### **Device**

The device proto. It contains the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|platform |String |Yes |app |The platform used by the user. The accepted values are:<br><br><br>* app<br><br>* desktop\-web<br><br>* mobile\-web<br><br>* other |
|os_type |String |No |Android |The OS of the platform used by the user. The accepted values are:<br><br><br>* Android<br><br>* iOS<br><br>* Windows<br><br>* Other |
|app_version |String |No |9.2.0 |Your application version. |
|device_model |String |No |Huawei\-mate 30 |The user's device model. The accepted values include:<br><br><br>* iPhone 10<br><br>* Pixel 4 |
|device_brand |String |No |Huawei |The user's device brand. The accepted values include:<br><br><br>* Samsung |
|os_version |String |No |10 |The operating system version of the user's device. |
|browser_type |String |No |Firefox |The type of browser. The accepted values include:<br><br><br>* Firefox<br><br>* Chrome |
|user_agent |String |No |Chrome |The UserAgent for the browser. The accepted values include:<br><br><br>* Mozilla<br><br>* AppleWebKit<br><br>* Chrome<br><br>* Huawei Browser<br><br>* Mobile Safari |
|network |String |No |3G |The user's network. The accepted values are:<br><br><br>* 2G<br><br>* 3G<br><br>* 4G<br><br>* 5G<br><br>* Wifi<br><br>* Other |


<span id="b370acd6"></span>
#### **Context**

The context for this event. It contains the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|query |String |No |iPad |This parameter is required if the event_type is "search". It is also required when the purchase or impression event occurs after the search event. |
|root_product_id |String |No |441356 |The main product_id on the "related to this product" page. |


<span id="059af517"></span>
### Extra

This field is used to pack key\-value pairs. It contains the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|newKey |String |*  |*  |*  |
|New Value |String |*  |*  |*  |


<span id="0ce09166"></span>
# Response parameters

The following tables details the response parameters for the WriteUserEvents API:

<span id="23f9a029"></span>
## Default


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|status |Object |*  |This field defines an error model. It contains two types of data: error code and error message. |
|errors |Array of Objects |*  |This field is populated when the statusis an error code: 1001. |


<span id="3189251b"></span>
## **Status**

The `status` defines an error model. Each `status` message contains two types of data: error code and error message.


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|code |Int32 |0 |You should look at this response parameter to determine if your API request was successful or not. The accepted values include:<br><br><br>* 0: it indicates that the calling is successful.<br><br>* 4xx: it indicates user error.<br><br>* 5xx: it indicates server error.<br><br>* 1xxx: it indicates error relating to Import calls.<br><br>* 2xxx: it indicates errors relating to Predict calls. |
|message |String |An unexpected value XXX is included in the XXX field, only ["xx", "yy", "zz"] can be accepted. |Provides a detailed error message on the reasons why your API request was unsuccessful. |


<span id="4b976a87"></span>
# Samples

The following section details the sample codes for the WriteUserEvents API.

<span id="fb01f45e"></span>
## Sample request

The following is a sample request for the API.

```JSON
curl --request POST \
     --url 'https://rec-ap-singapore-1.byteplusapi.com/data/api/retail/retail_demo/user_event?method=write' \
     --header 'Accept: application/json' \
     --header 'Content-Type: application/json' \
     --header 'Request-Id:12313208' \
     --header 'Tenant-Id:d7c5963593798b5263858b028f589' \
     --header 'Tenant-Nonce:1683629026' \
     --header 'Tenant-Ts:1683629026' \
     --header 'Tenant-Signature:3d4617f9323c76222e8b1f04f19c5556dc6d78ff883441a005a811f3ac411b6e' \
     --data '{
     "user_events": [
          {
               "scene": {
                    "scene_name": "product detail page",
                    "page_number": 2,
                    "offset": 10
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
               "context": {
                    "query": "iPad",
                    "root_product_id": "441356"
               },
               "user_id": "1457789",
               "event_type": "purchase",
               "event_timestamp": 1623681888,
               "product_id": "632461",
               "attribution_token": "eyJpc3MiOiJuaW5naGFvLm5ldCIsImV4cCI6IjE0Mzg5NTU0NDUiLCJuYW1lIjoid2FuZ2hhbyIsImFkbWluIjp0cnVlfQ",
               "rec_info": "CiRiMjYyYjM1YS0xOTk1LTQ5YmMtOGNkNS1mZTVmYTczN2FkNDASJAobcmVjZW50X2hvdF9jbGlja3NfcmV0cmlldmVyFQAAAAAYDxoKCgNjdHIdog58PBoKCgNjdnIdANK2OCIHMjcyNTgwMg==",
               "traffic_source": "self",
               "purchase_count": 5,
               "detail_page_stay_time": 10,
               "extra": {
                    "custom_field": "value"
               }
          }
     ],
     "extra": {
          "additionalProp": "additionalVal"
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
    "message": "data is empty; errID:840491090 logID:2023040410222823C6F3CD6EBABB4EAA6C"
  }
}
```


The following is **failed** sample response if the data entries exceed 2,000.

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
      "message": "in the 'purchase_count' field, non-zero field is zero, when `event_type` field is in [purchase]",
      "user_event": {
        "user_id": "1457789",
        "event_type": "purchase",
        "event_timestamp": "1623681888",
        "scene": {
          "scene_name": "product detail page",
          "page_number": 2,
          "offset": 10
        },
        "product_id": "632461",
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
        "context": {
          "query": "iPad",
          "root_product_id": "441356"
        },
        "attribution_token": "eyJpc3MiOiJuaW5naGFvLm5ldCIsImV4cCI6IjE0Mzg5NTU0NDUiLCJuYW1lIjoid2FuZ2hhbyIsImFkbWluIjp0cnVlfQ",
        "rec_info": "CiRiMjYyYjM1YS0xOTk1LTQ5YmMtOGNkNS1mZTVmYTczN2FkNDASJAobcmVjZW50X2hvdF9jbGlja3NfcmV0cmlldmVyFQAAAAAYDxoKCgNjdHIdog58PBoKCgNjdnIdANK2OCIHMjcyNTgwMg==",
        "traffic_source": "self",
        "detail_page_stay_time": 10,
        "extra": {
          "custom_field": "value"
        }
      }
    }
  ]
}
```


<span id="9398e94b"></span>
# Error codes

For more information on the API error codes, refer to [BytePlus Recommend shared error and status codes](https://docs.byteplus.com/recommend/reference/shared_error_and_status_codes).
