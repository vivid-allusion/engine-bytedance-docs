---
title: "Predict—Recommend Content Industry"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/reference-content_predict"
---

The Predict API for BytePlus Recommend empowers the updating and ranking of content lists in the Media/Content industry. User data takes approximately 24 hours to take effect, while content data influences the results within just 30 minutes. By leveraging UserEvent data, the API enhances recommendation outcomes, delivering improved user experiences tailored to individual preferences.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information on BytePlus Recommend token authentication, refer <a href="https://docs.byteplus.com/en/recommend/reference/api_token_authentication">here</a>.</div>


<span id="36c7c3c1"></span>
# HTTP request

This is the URL and HTTP request method for the Predict API.


|**URL** |https://rec\-us\-east\-1.byteplusapi.com/predict/api/media/${tenant}/$ |
|---|---|
|**Method** |POST |


<span id="d5e9f3b3"></span>
# Request parameters

The topics below details the parameters required for the Predict API.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Not all request parameters are included in the following table. For a complete list, refer to <a href="https://docs.byteplus.com/recommend/reference/api_token_authentication">HTTP header parameters</a>.</div>


<span id="1dad2339"></span>
## Body

The following table details the body parameters required for the Predict API:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|user_id |String |Yes |1457789 |The unique identifier for the user. The value is the same as `User.user_id`. |
|size |Int32 |Yes |20 |The maximum number of pieces of content returned.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The actual number of pieces of content returned is the minimum of the following numbers:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">size</div><br><br><br>* <div data-tips="true" data-tips-type="tip">length(context.candidate_content_ids)</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Total number of content with is_recommendable=1</div><br> |
|scene |Object |Yes |*  |The recommendation scene information. |
|context |Object |Yes |*  |The context of the current Predict request. |
|extra |Object |No |*  |An extra parameter field to include any additional information not entered above. |


<span id="d5969633"></span>
### **Scene**

Scene refers to the location where the user interaction event happened. The scene proto contains the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|scene_name |String |Yes |home |The name of the scene the UserEvent occurred in. The value is the same as `UserEvent.scene_name`. |
|page_number |Int32 |No |1 |The page number.<br><br>This field can refer to:<br><br><br>* the page number that the content is found on.<br><br>* the number of times that users swipe the screen before seeing the content.<br><br><br>The default value is 0, which indicates that all content fits into a single page. |
|offset |Int32 |No |10 |The content's position within the page itself. |


<span id="b22e6771"></span>
### **Context**

PredictRequest.Context contains the context of a Predict API request. Its proto contains the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|root_content |Object |Yes |*  |The parent content information, if any. The parent content refers to the content whose details page contains the recommended content the user has seen or clicked on.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This field is only required for the content details page.</div><br> |
|candidate_content_ids |Array of Strings |No |*  |The list of candidates for recommendation. If this field is empty, all contents are candidates. |
|device |String |Yes |app |The platform used to access the content. The accepted values are:<br><br><br>* app<br><br>* desktop\-web<br><br>* mobile\-web<br><br>* other |
|os_type |String |No |Android |The OS of the platform used by the user. The accepted values are:<br><br><br>* iOS<br><br>* Android<br><br>* Windows<br><br>* Other |
|app_version |String |No |9.2.0 |Your application version when the user accessed the content. |
|device_model |String |No |iPhone X |The user's device model. |
|device_brand |String |No |Apple |The user's device brand. |
|os_version |String |No |10 |The user's device's operating system version. |
|browser_type |String |No |Chrome |The browser used to access the content. |
|user_agent |String |No |Safari |The UserAgent for the browser. |
|network |String |No |4G |The user's network. The accepted values are:<br><br><br>* 2G<br><br>* 3G<br><br>* 4G<br><br>* 5G<br><br>* WIFI<br><br>* Other |


<span id="c7c74533"></span>
#### **Root_content**

The parent content information, if any. The parent content refers to the content whose details page contains the recommended content the user has seen or clicked on. Its proto contains the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|content_id |String |Yes |632461 |The unique identifier for a piece of content. The content_id can be the series_id/entity_id/video_id/ or any other type of content identifier. |
|is_recommendable |Int32 |Yes |1 |Determines if the content should be recommended to the user.<br><br>The accepted values are:<br><br><br>* 1—The content should be recommended to users.<br><br>* 0— The content should not be recommended to users.<br><br><br>Even if the content is not recommended to your users, you must submit this parameter to us. Users might have interacted with this content before, and this information allows us to provide more accurate recommendations. |
|categories |String |Yes |[<br><br>{"category_depth":1,<br><br>"category_nodes": [{"id_or_name":"Movie"}] },<br><br>{"category_depth":2,<br><br>"category_nodes": [{"id_or_name":"Comedy"}] }<br><br>] |The categories that a piece of content belongs to. The category value is a JSON serialized string.<br><br>If the content belongs to 2 different categories, the value should look like this:<br><br>```JSON```<br>```[```<br>``` {"category_depth":1,```<br>```  "category_nodes": [{"id_or_name":"Movie"}] },```<br>``` {"category_depth":2,```<br>```  "category_nodes": [{"id_or_name":"Comedy"},```<br>```                     {"id_or_name":"Action"}] }```<br>```]```<br><br><br>You can also serialize the JSON object to String like the following:<br><br>```Python```<br>```categories = json.dumps( [```<br>```   {"category_depth":1,```<br>```    "category_nodes": [{"id_or_name":"Movie"}] },```<br>```   {"category_depth":2,```<br>```    "category_nodes": [{"id_or_name":"Comedy"}] }```<br>``` ])```<br> |
|content_title |String |Yes |Video #1 |The content title. |
|content_type |String |Yes |video |The content type. The accepted values are:<br><br><br>* picture<br><br>* GIF<br><br>* video<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the <code>content_type</code> is video, ensure that the <code>video_duration</code> parameter has a value of more than 0.</div><br><br><br><br>* text<br><br>* other |
|description |String |No |Test video |The content description. |
|content_owner |String |No |testuser#1 |The content creator or publisher's user_id. |
|language |String |No |English |The content's language. |
|tags |Array of Strings |No |New, Trending |The content's internal tags. |
|listing_page_display_tags |Array of Strings |No |Popular, Recommend |The content's tags displayed to the user on the listing page, like the home page or category landing page. |
|detail_page_display_tags |Array of Strings |No |Popular, Recommend |The content's tags displayed to the user on the content\-detail page. |
|listing_page_display_type |String |No |image |The content's listing type, if applicable. The accepted values are:<br><br><br>* image<br><br>* video<br><br>* other |
|cover_multimedia_url |String |No |https://demo.jpg |If there is a value in listing_page_display_type, fill this parameter with the cover image's link. |
|user_rating |Double |No |3 |The content's rating given by users. The value range is from 0.0 to 5.0. |
|views_count |Int32 |No |10000 |The content's view count. |
|comments_count |Int32 |No |100 |The content's comment count. |
|likes_count |Int32 |No |1000 |The content's like count. |
|shares_count |Int32 |No |50 |The content's share count. |
|is_paid_content |Int32 |No |1 |Whether users need to pay to access the content, for example, subscribe to the platform before being granted access to the content. The accepted values are as follows:<br><br><br>* 1—If it is paid content.<br><br>* 0—If it is free content. |
|origin_price |Int64 |No |12300 |This parameter is only applicable if the value of is_paid_content is 1. Enter the price of the content in cents.<br><br>For example, $123.00 = 12300. |
|current_price |Int64 |No |12100 |This parameter is only applicable if the value of is_paid_content is 1. Enter the current price of the content in cents, if discounted.<br><br>For example, $121.00 = 12100. |
|publish_region |String |No |US |The region where the content is published. |
|available_region |Array of Strings |No |US, Singapore, India |The region(s) where the content is available for viewing. |
|entity_id |String |No |1 |[For the OTT platforms]<br><br>The entity's ID. |
|entity_name |String |No |Friends |[For the OTT platforms]<br><br>If the content is a television show with multiple seasons, input the show's entity ID as the parameter value. |
|series_id |String |No |11 |[For OTT platforms]<br><br>If the content is a television show with multiple seasons, input the season's ID as the parameter value. |
|series_index |Int32 |No |1 |[For OTT platforms]<br><br>If the content is a television show with multiple seasons, input the season's number as the parameter value. |
|series_name |String |No |Friends Season 1 |[For OTT platforms]<br><br>The name of the season. |
|series_count |Int32 |No |10 |[For OTT platforms]<br><br>The total number of seasons the television series has. |
|video_id |String |No |111 |[For OTT platforms]<br><br>The video ID in the television series. |
|video_index |Int32 |No |6 |[For OTT platforms]<br><br>The video episode within the television series. |
|video_name |String |No |The One With Ross' New Girlfriend |[For OTT platforms]<br><br>The name of the episode. |
|video_count |Int32 |No |10 |[For OTT platforms]<br><br>The total number of episodes within the season. |
|video_type |String |No |series, movie, reality show |[For OTT platforms]<br><br>The video type. |
|video_duration |Int64 |No |2400000 |If the content_type is video, enter the video length in milliseconds. |
|publish_timestamp |Int64 |No |1623193487 |The timestamp when the content is published. |
|copyright_start_timestamp |Int64 |No |1623193487 |[For OTT platforms]<br><br>The timestamp when the content is available to users. |
|copyright_end_timestamp |Int64 |No |1623194487 |[For OTT platforms]<br><br>The timestamp when the content is no longer available to users. |
|actors |Array of Strings |No |John Doe |[For OTT platforms]<br><br>The actors within the content. |
|source |String |No |Self |The source of the recommendation.<br><br>The accepted values are:<br><br><br>* Self—indicates that the recommendation came from the caller's own engine.<br><br>* Other—indicates that the recommendation came from a third\-party engine. |
|extra |Object |No |*  |An extra parameter field to include any additional information not entered above. |


<span id="0ce09166"></span>
# Response parameters

The following tables details the response parameters for the Predict API:


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|status |Object |*  |The Status defines an error model. Each Status message contains two types of data: error code and error message. |
|request_id |String |*  |This field has the same value as `PredictRequest.Request_id`. |
|value |Object |*  |The Predict call result. |


<span id="98d44720"></span>
## **Status**

The Status defines an error model. Each Status message contains two types of data: error code and error message.


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|code |Int32 |0 |You should look at this response parameter to determine if your API request was successful.<br><br><br>* 0: it indicates that the calling is successful.<br><br>* 4xx: it indicates user error.<br><br>* 5xx: it indicates server error.<br><br>* 1xxx: it indicates error relating to Import calls.<br><br>* 2xxx: it indicates errors relating to Predict calls. |
|message |String |An unexpected value XXX is included in the XXX field, only ["xx", "yy", "zz"] can be accepted. |Provides a detailed error message on the reasons why your API request was unsuccessful. |


<span id="4f3b99d0"></span>
## Value

This parameter contains the following fields:


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|response_contents |Array of Objects |*  |The list of predicted contents. |
|extra |Object |*  |This is a field for additional debug information. |


<span id="b7370516"></span>
### **Response_contents**

This parameter contains the following fields:


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|content_id |String |*  |The unique identifier for the content.<br><br>The value is consistent with `Content.content_id`. |
|rank |Int32 |*  |The content's recommendation ranking. |
|pctr |Double |*  |The predicted Click\-Through Rate (CTR). |
|pcvr |Double |*  |The predicted Conversion Rate (CVR). |
|rec_info |String |*  |The strategy used for this particular recommendation result. |
|extra |Object |*  |A catch\-all field that returns any additional information, typically for debugging. |


<span id="ed90ff97"></span>
# Samples

The following section details the sample codes for the Predict API.

<span id="fb01f45e"></span>
## Sample request

The following is a sample request for the API.

```JSON
curl --request POST \
     --url https://rec-us-east-1.byteplusapi.com/predict/api/media/media_demo/home \
     --header 'Accept: application/json' \
     --header 'Request-Id: 221b7634-0a4c-497c-b268-e4b2f9b475b8' \
     --header 'Content-Type: application/json' \
     --header 'Tenant-Id:d7c5963593798b5263858b028f589' \
     --header 'Tenant-Nonce:1683634974' \
     --header 'Tenant-Ts:1683634974' \
     --header 'Tenant-Signature:a90bc19fecb71efabe928e6965ba75888e46c4cae5902ccae6c0d57b544e7c3b' \
     --data '{
     "user_id": "123",
     "size": 3,
     "scene": {
          "scene_name": "home",
          "page_number": 1,
          "offset": 0
     },
     "context": {
         "root_content": {
               "content_id": "123456"
         },
         "candidate_content_ids": ["1234", "2345", "4567"],
         "device": "app",
         "os_type": "android",
         "app_version": "9.2.0",
         "device_model": "huawei-mate30",
         "device_brand": "huawei",
         "os_version": "10",
         "browser_type": "chrome",
         "user_agent": "Mozilla/5.0 (Linux; Android 10; TAS-AN00; HMSCore 5.3.0.312) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.106 HuaweiBrowser/11.0.8.303 Mobile Safari/537.36",
         "network": "4g"
     },
     "extra": {
         "custom_field": "value"
     }
}'
```


<span id="de55caff"></span>
## Sample response

The following is a **successful** sample response.

```JSON
{
  "status": {
    "message": "OK",
    "success": true
  },
  "request_id": "221b7634-0a4c-497c-b268-e4b2f9b475b8",
  "value": {
    "response_contents": [
      {
        "content_id": "content_id_1",
        "rank": 1,
        "pctr": 0.3,
        "pcvr": 0.6,
        "rec_info": "CggxMjgzMTAwMRITCgp2aWtpbmdfY3RyFVDOFb4YABITCgp2aWtpbmdfY3ZyFZAESr4YHxIaChFyZWNlbnRfa=",
        "extra": {
          "category": "cate_1"
        }
      },
      {
        "content_id": "content_id_2",
        "rank": 2,
        "pctr": 0.15,
        "pcvr": 0.32,
        "rec_info": "3ZyFZAESr4YHxIaChFyZWNlbnRfaCggxMjgzMTAwMRITCgp2aWtpbmdfY3RyFVDOFb4YABITCgp2aWtpbmdfY=",
        "extra": {
          "category": "cate_1"
        }
      },
      {
        "content_id": "content_id_3",
        "rank": 1,
        "pctr": 0.09,
        "pcvr": 0.43,
        "rec_info": "MjgzMTAwMRITCgp2aWtpbmd3ZyFZAESr4YHxIaChFyZWNlbnRfaCggxfY3RyFVDOFb4YABITCgp2aWtpbmdfY=",
        "extra": {
          "category": "cate_2"
        }
      }
    ]
  }
}
```


The following is a **failed** sample response.

<span id="9398e94b"></span>
### ```JSON

{

"status": {

"code": 400,

"message": "unmarshal request body fail, plz make sure path is correct. path:/api/media/media_demo/home, targetReqType:\*media.PredictRequest; errID:852940573 logID:202304041027049278AA2F7CA2A95A785F"

}

}

```Plain Text

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


<span id="01345d64"></span>
# Error codes

For more information on the API error codes, refer to [BytePlus Recommend shared error and status codes](https://docs.byteplus.com/recommend/reference/shared_error_and_status_codes).
