---
title: "WriteUserEvents—Recommend Content Industry"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/reference-content_writeuserevents"
---

Call WriteUserEvents to upload real\-time UserEvent data in the Media/Content industry.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information on BytePlus Recommend token authentication, refer <a href="https://docs.byteplus.com/en/recommend/reference/api_token_authentication">here</a>.</div>


<span id="382634fb"></span>
# Limitations

The following limitations apply to WriteUserEvents API:


* Each request can upload no more than 2,000 UserEvent data records at a time. If you upload more than 2,000 UserEvent data records, you will encounter a rejection.

* The result obtained by multiplying QPS by the number of uploads per request must be less than 30,000.


<span id="20e4f21b"></span>
# HTTP request

This is the URL and HTTP request method for the WriteUserEvents API.


|**URL** |https://rec\-us\-east\-1.byteplusapi.com/data/api/media/${tenant}/user_event |
|---|---|
|**Method** |POST |


<span id="840b3737"></span>
# Request parameters

The topics below details the parameters required for the WriteUserEvents API.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Not all request parameters are included in the following table. For a complete list, refer to <a href="https://docs.byteplus.com/recommend/reference/api_token_authentication">HTTP header parameters</a>.</div>


<span id="2636c2da"></span>
## Query

The following table details the query parameters required for the WriteUserEvents API:


|**Query String Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|method |String |Yes |Write |*  |


<span id="fb777e27"></span>
## Body

The following table details the body parameters required for the WriteUserEvents API:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|user_id |String |Yes |1457789 |The unique user identifier. |
|event_type |String |Yes |impression |The UserEvent type. The accepted values are:<br><br><br>* impression<br><br>* click<br><br>* play<br><br>* playover<br><br>* like<br><br>* comment<br><br>* purchase<br><br>* add\-to\-cart<br><br>* remove\-from\-cart<br><br>* add\-to\-favorites<br><br>* remove\-from\-favorites<br><br>* search<br><br>* stay\-detail\-page<br><br><br>For more information on the event_types and their requirements, refer to the[ API Proto definitions](https://docs.byteplus.com/recommend/samples/content_api_proto_definitions). |
|event_timestamp |Int64 |Yes |1623681888 |The timestamp when the event occurred. |
|content_id |String |Yes |632461 |The unique identifier for a piece of content. The content_id can be the series_id/entity_id/video_id/ or any other type of content identifier. This field should be empty if the event_type is "search", and otherwise it is required. |
|traffic_source |String |No |Self |The source of the directed traffic for this UserEvent. The accepted values are:<br><br><br>* Self—Self\-generated traffic<br><br>* BytePlus—BytePlus\-generated traffic<br><br>* Other—Other system\-generated traffic |
|request_id |String |No |67a9fcf74a82fdc55a26ab4ee12a7b96890407fc0042f8cc014e07a4a560a9ac |A request ID provided by BytePlus. This ID will match the UserEvent with the same request_ID when calling the BytePlus Predict API. |
|rec_info |String |No |CiRiMjYyYjM1YS0xOTk1LTQ5YmMtOGNkNS1mZTVmYTczN2FkNDASJAobcmVjZW50X2hvdF9jbGlja3NfcmV0cmlldmVyFQAAAAAYDxoKCgNjdHIdog58PBoKCgNjdnIdANK2OCIHMjcyNTgwMg== |BytePlus will provide this parameter value. It contains detailed algorithm information. |
|attribution_token |String |No |eyJpc3MiOiJuaW5naGFvLm5ldCIsImV4cCI6IjE0Mzg5NTU0NDUiLCJuYW1lIjoid2FuZ2hhbyIsImFkbWluIjp0cnVlfQ |The identifier used to gather all the relevant events within one user session. |
|scene_name |String |No |Home Page |The unique identifier of a UserEvent scene. Values include the home page, search page, details page, and so on. |
|page_number |Int32 |No |2 |This parameter can be the following definitions:<br><br><br>* the page number that the content is found on.<br><br>* the number of times that users swipe the screen before seeing the content. |
|offset |Int32 |No |10 |The content's position within the page itself. |
|play_type |String |No |0 |The form in which the user plays the content:<br><br><br>* 0: Plays from the start.<br><br>* 1: Continue where the user stopped.<br><br>* 2: Trial play. |
|play_duration |Int64 |No |6000 |The user's watch duration in milliseconds, if the content is a video.<br><br>For example, 6 seconds = 6000ms. |
|start_time |Int32 |No |150 |The starting point of the user's watch duration in seconds, if the content is a video.<br><br>For example, "0" if the user starts watching the video from the beginning, "150" if the user starts watching the video from the 2min 30s mark, and so on |
|end_time |Int32 |No |300 |The ending point of the user's watch duration in seconds, if the content is a video.<br><br>For example, "300" if the user stops watching the video at the 5min mark. |
|entity_id |String |No |1 |[For OTT platforms]<br><br>If the content is a television show with multiple seasons, input the show's entity ID as the parameter value. |
|series_id |String |No |11 |[For OTT platforms]<br><br>If the content is a television show with multiple seasons, input the season's ID as the parameter value. |
|video_id |String |No |111 |[For OTT platforms]<br><br>The video ID within the series. |
|parent_consent_id |String |No |630000 |The unique identifier of the parent content, if any. The parent content refers to the content whose details page contains the recommended content that the user has seen or clicked on. |
|detail_stay_time |Int32 |No |10 |The duration spent on the detail page in seconds. The value of this parameter depends on `event_type`. If the `event_type` is stay\-detail\-page, the parameter value must be more than 0. |
|query |String |No |comedy |This parameter is required if the `event_type`is search. |
|device |String |Yes |app |The platform used to access the content. The accepted values are:<br><br><br>* app<br><br>* desktop\-web<br><br>* mobile\-web<br><br>* other |
|os_type |String |No |Android |The OS of the platform used by the user. The accepted values are:<br><br><br>* iOS<br><br>* Android<br><br>* Windows<br><br>* Other |
|app_version |String |No |9.2.0 |Your application version when the user accessed the content. |
|device_model |String |No |iPhone X |The user's device model. |
|device_brand |String |No |Apple |The user's device brand. |
|os_version |String |No |10 |The user's device's operating system version. |
|browser_type |String |No |Chrome |The browser used to access the content. |
|user_agent |String |No |Safari |The UserAgent for the browser. |
|network |String |No |4G |The user's network. The accepted values are:<br><br><br>* 2G<br><br>* 3G<br><br>* 4G<br><br>* 5G<br><br>* WIFI<br><br>* Other |
|extra |Object |No |*  |An extra parameter field to include any additional information not entered above. |


<span id="0ce09166"></span>
# Response parameters

The following tables details the response parameters for the WriteUserEvents API:


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|status |Object |*  |The `status` defines an error model. Each `status` message contains two types of data: error code and error message. |
|errors |Array of Objects |*  |This field is populated when the `status`is an error code: 1001. |


<span id="04ae0ab7"></span>
## **Status**

The Status defines an error model. Each Status message contains two types of data: error code and error message.


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|code |Int32 |0 |You should look at this response parameter to determine if your API request was successful.<br><br><br>* 0: it indicates that the calling is successful.<br><br>* 4xx: it indicates user error.<br><br>* 5xx: it indicates server error.<br><br>* 1xxx: it indicates error relating to Import calls.<br><br>* 2xxx: it indicates errors relating to Predict calls. |
|message |String |An unexpected value XXX is included in the XXX field, only ["xx", "yy", "zz"] can be accepted. |Provides a detailed error message on the reasons why your API request was unsuccessful. |


<span id="91f6fe21"></span>
### User_event

The UserEvent proto details. It contains the following fields:


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|user_id |String |1457789 |The unique user identifier. |
|event_type |String |impression |The UserEvent type. The accepted values are:<br><br><br>* impression<br><br>* click<br><br>* play<br><br>* playover<br><br>* like<br><br>* comment<br><br>* purchase<br><br>* add\-to\-cart<br><br>* remove\-from\-cart<br><br>* add\-to\-favorites<br><br>* remove\-from\-favorites<br><br>* search<br><br>* stay\-detail\-page<br><br><br>For more information on the event_types and their requirements, refer to the[ API Proto definitions](https://docs.byteplus.com/recommend/samples/content_api_proto_definitions). |
|event_timestamp |Int64 |1623681888 |The timestamp when the event occurred. |
|content_id |String |632461 |The unique identifier for a piece of content. The content_id can be the series_id/entity_id/video_id/ or any other type of content identifier. This field should be empty if event_type is "search", and otherwise it is required. |
|traffic_source |String |Self |The source of the directed traffic for this UserEvent. The accepted values are:<br><br><br>* Self—Self\-generated traffic<br><br>* BytePlus—BytePlus\-generated traffic<br><br>* Other—Other system\-generated traffic |
|request_id |String |67a9fcf74a82fdc55a26ab4ee12a7b96890407fc0042f8cc014e07a4a560a9ac |A request ID provided by BytePlus. This ID will match the UserEvent with the same request_ID when calling the BytePlus Predict API. |
|rec_info |String |CiRiMjYyYjM1YS0xOTk1LTQ5YmMtOGNkNS1mZTVmYTczN2FkNDASJAobcmVjZW50X2hvdF9jbGlja3NfcmV0cmlldmVyFQAAAAAYDxoKCgNjdHIdog58PBoKCgNjdnIdANK2OCIHMjcyNTgwMg== |BytePlus will provide this parameter value. It contains detailed algorithm information. |
|attribution_token |String |eyJpc3MiOiJuaW5naGFvLm5ldCIsImV4cCI6IjE0Mzg5NTU0NDUiLCJuYW1lIjoid2FuZ2hhbyIsImFkbWluIjp0cnVlfQ |The identifier used to gather all the relevant events within one user session. |
|scene_name |String |Home Page |The unique identifier of a UserEvent scene. Values include the home page, search page, details page, and so on. |
|page_number |Int32 |2 |This parameter can be the following definitions:<br><br><br>* the page number that the content is found on.<br><br>* the number of times that users swipe the screen before seeing the content. |
|offset |Int32 |10 |The content's position within the page itself. |
|play_type |String |0 |The form in which the user plays the content:<br><br><br>* 0: Plays from the start.<br><br>* 1: Continue where the user stopped.<br><br>* 2: Trial play. |
|play_duration |Int64 |6000 |The user's watch duration in milliseconds, if the content is a video.<br><br>For example, 6 seconds = 6000ms. |
|start_time |Int32 |150 |The starting point of the user's watch duration in seconds, if the content is a video.<br><br>For example, "0" if the user starts watching the video from the beginning, "150" if the user starts watching the video from the 2min 30s mark, and so on. |
|end_time |Int32 |300 |The ending point of the user's watch duration in seconds, if the content is a video.<br><br>For example, "300" if the user stops watching the video at the 5min mark. |
|entity_id |String |1 |[For OTT platforms]<br><br>If the content is a television show with multiple seasons, input the show's entity ID as the parameter value. |
|series_id |String |11 |[For OTT platforms]<br><br>If the content is a television show with multiple seasons, input the season's ID as the parameter value. |
|video_id |String |111 |[For OTT platforms]<br><br>The video ID within the series. |
|parent_consent_id |String |630000 |The unique identifier of the parent content, if any. The parent content refers to the content whose details page contains the recommended content that the user has seen or clicked on. |
|detail_stay_time |Int32 |10 |The duration spent on the detail page. The value of this parameter depends on event_type. If the event_type is stay\-detail\-page, the parameter value must be more than 0. |
|query |String |comedy |This parameter is required if the`event_type` is "search". |
|device |String |app |The platform used to access the content. The accepted values are:<br><br><br>* app<br><br>* desktop\-web<br><br>* mobile\-web<br><br>* other |
|os_type |String |Android |The OS of the platform used by the user. The accepted values are:<br><br><br>* iOS<br><br>* Android<br><br>* Windows<br><br>* Other |
|app_version |String |9.2.0 |Your application version when the user accessed the content. |
|device_model |String |iPhone X |The user's device model. |
|device_brand |String |Apple |The user's device brand. |
|os_version |String |10 |The user's device's operating system version. |
|browser_type |String |Chrome |The browser used to access the content. |
|user_agent |String |Safari |The UserAgent for the browser. |
|network |String |4G |The user's network. The accepted values are:<br><br><br>* 2G<br><br>* 3G<br><br>* 4G<br><br>* 5G<br><br>* WIFI<br><br>* Other |
|extra |Object |*  |An extra parameter field to include any additional information not entered above. |


<span id="ed90ff97"></span>
# Samples

The following section details the sample codes for the WriteUserEvents API.

<span id="fb01f45e"></span>
## Sample request

The following is a sample request for the API with the `event_type`as `impression`.

```JSON
curl --request POST \
     --url 'https://rec-us-east-1.byteplusapi.com/data/api/media/media_demo/user_event?method=write' \
     --header 'Accept: application/json' \
     --header 'Content-Type: application/json' \
     --header 'Request-Id:12313208' \
     --header 'Tenant-Id:d7c5963593798b5263858b028f589' \
     --header 'Tenant-Nonce:1683634755' \
     --header 'Tenant-Ts:1683634755' \
     --header 'Tenant-Signature:7b2681d710c3dcd743abdb309974e0f1c0b219806cb2f018188af066b3c814db' \
     --data '{
     "user_events": [
          {
              "user_id": "1457789",
              "event_type": "impression",
              "event_timestamp": 1623681888,
              "content_id": "632461",
              "traffic_source": "self",
              "request_id": "abc123",
              "rec_info": "CiRiMjYyYjM1YS0xOTk1LTQ5YmMtOGNkNS1mZTVmYTczN2FkNDASJAobcmVjZW50X2hvdF9jbGlja3NfcmV0cmlldmVyFQAAAAAYDxoKCgNjdHIdog58PBoKCgNjdnIdANK2OCIHMjcyNTgwMg==",
              "attribution_token": "eyJpc3MiOiJuaW5naGFvLm5ldCIsImV4cCI6IjE0Mzg5NTU0NDUiLCJuYW1lIjoid2FuZ2hhbyIsImFkbWluIjp0cnVlfQ",
              "scene_name": "home",
              "page_number": 2,
              "offset": 10,
              "play_type": "0",
              "play_duration": 600000,
              "start_time": 150,
              "end_time": 300,
              "entity_id": "1",
              "series_id": "11",
              "video_id": "111",
              "parent_content_id": "123",
              "detail_stay_time": 10,
              "query": "comedy",
              "device": "app",
              "os_type": "android",
              "app_version": "9.2.0",
              "device_model": "huawei-mate30",
              "device_brand": "huawei",
              "os_version": "10",
              "browser_type": "chrome",
              "user_agent": "Mozilla/5.0 (Linux; Android 10; TAS-AN00; HMSCore 5.3.0.312) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.106 HuaweiBrowser/11.0.8.303 Mobile Safari/537.36",
              "network": "4g",
              "extra": {
                 "extra_key": "extra_value"
             }
          }
     ],
     "extra": {
         "extra_key": "extra_value"
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
      "user_event": {
        "event_type": "impression",
        "event_timestamp": "1623681888",
        "content_id": "632461",
        "traffic_source": "self",
        "request_id": "abc123",
        "rec_info": "CiRiMjYyYjM1YS0xOTk1LTQ5YmMtOGNkNS1mZTVmYTczN2FkNDASJAobcmVjZW50X2hvdF9jbGlja3NfcmV0cmlldmVyFQAAAAAYDxoKCgNjdHIdog58PBoKCgNjdnIdANK2OCIHMjcyNTgwMg==",
        "attribution_token": "eyJpc3MiOiJuaW5naGFvLm5ldCIsImV4cCI6IjE0Mzg5NTU0NDUiLCJuYW1lIjoid2FuZ2hhbyIsImFkbWluIjp0cnVlfQ",
        "scene_name": "home",
        "page_number": 2,
        "offset": 10,
        "play_type": "0",
        "play_duration": "600000",
        "start_time": 150,
        "end_time": 300,
        "entity_id": "1",
        "series_id": "11",
        "video_id": "111",
        "parent_content_id": "123",
        "detail_stay_time": 10,
        "query": "comedy",
        "device": "app",
        "os_type": "android",
        "app_version": "9.2.0",
        "device_model": "huawei-mate30",
        "device_brand": "huawei",
        "os_version": "10",
        "browser_type": "chrome",
        "user_agent": "Mozilla/5.0 (Linux; Android 10; TAS-AN00; HMSCore 5.3.0.312) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.106 HuaweiBrowser/11.0.8.303 Mobile Safari/537.36",
        "network": "4g"
      }
    }
  ]
}
```


<span id="9398e94b"></span>
# Error codes

For more information on the API error codes, refer to [BytePlus Recommend shared error and status codes](https://docs.byteplus.com/recommend/reference/shared_error_and_status_codes).
