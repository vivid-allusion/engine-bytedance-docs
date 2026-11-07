---
title: "Predict—Recommend SaaS Content Industry"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/reference-content_saas_predict"
---

The Predict API for BytePlus Recommend SaaS empowers the updating and ranking of content lists in the Media/Content industry. User data takes approximately 24 hours to take effect, while content data influences the results within just 30 minutes. By leveraging UserEvent data, the API enhances recommendation outcomes, delivering improved user experiences tailored to individual preferences.

<span id="36c7c3c1"></span>
# HTTP request

This is the URL and HTTP request method for the Predict API.


|**URL** |https://rec\-api\-sg1.recplusapi.com/ContentSaaS/Predict |
|---|---|
|**Method** |POST |


<span id="d5e9f3b3"></span>
# Request parameters

The topics below details the parameters required for the Predict API.

<span id="b9094dc1"></span>
## Metadata

The following table details the metadata parameters required for the Predict API:


|**Header Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Tenant\-Id |String |Yes |3000001813 |Your BytePlus account's ID. For more information on retrieving Recommend Tenant IDs, refer [here](https://docs.byteplus.com/recommend/docs/content_standard_getting_started). |
|Request\-id |String |Yes |84kduxkls74lcdj73jdu3 |The client assigns the request id, and it should be unique for each request. No specific format is required for the request\-id, but it is advisable to keep it reasonably short.<br><br>For more information on request\-id generation code samples, refer [here](https://docs.byteplus.com/recommend/reference/api_token_authentication). |
|Other Auth Header |*  |Yes |*  |**Recommend Standard**<br><br>BytePlus Recommend SaaS Standard uses Access Key/Secret Key (AK/SK) for Byteplus Standard header authentication. The process of constructing these headers can be complex, so it is recommended to use the SDK for easier access and implementation.<br><br>For more information on using the AK/SK authentication, refer [here](https://docs.byteplus.com/en/recommend/reference/api_authentication#9e904017).<br><br>**Recommend Premium**<br><br>BytePlus Recommend SaaS Premium uses token header authentication.<br><br>For more information on using the SDK token authentication, refer [here](https://docs.byteplus.com/en/recommend/reference/api_token_authentication). |


<span id="6756869f"></span>
## Body

The following table details the body parameters required for the Predict API:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|project_id |String |Yes |807247981 |The unique identifier for the recommendation project. |
|model_id |String |Yes |100000 |The unique identifier for the recommendation model used. |
|user_id |String |Yes |1457789 |The unique identifier for the user. The value is the same as `User.user_id`. |
|size |Int32 |Yes |20 |The maximum number of pieces of content returned.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The actual number of pieces of content returned is the minimum of the following numbers:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">size</div><br><br><br>* <div data-tips="true" data-tips-type="tip">length(context.candidate_content_ids)</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Total number of content with <code>is_recommendable</code>=1</div><br> |
|scene |Object |Yes |*  |The recommendation scene information. |
|content_context |Object |Yes |*  |The context of the current Predict request. |
|extra |Object |No |*  |An extra parameter field to include any additional information not entered above. |


<span id="d21d77f5"></span>
### **Scene**

Scene refers to the location where the user interaction event happened. The scene proto contains the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|scene_name |String |Yes |home |The name of the scene the UserEvent occurred in. Some scenes include the home page, search page, details page, and many more. |
|page_number |Int32 |No |1 |The page number.<br><br>This field can refer to:<br><br><br>* the page number that the content is found on.<br><br>* the number of times that users swipe the screen before seeing the content.<br><br><br>The default value is 0, which indicates that all content fits into a single page. |
|offset |Int32 |No |10 |The content's position within the page itself. |


<span id="d07e72b2"></span>
### **Content_context**

PredictRequest.Context contains the context of a Predict API request. Its proto contains the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|root_content |Object |Yes |*  |The parent content information, if any. The parent content refers to the content whose details page contains the recommended content the user has seen or clicked on. |
|device |Object |Yes |app |The platform used to access the content. The accepted values are:<br><br><br>* app<br><br>* desktop\-web<br><br>* mobile\-web<br><br>* other |
|candidate_contents |Array of Objects |No |*  |The list of candidates for recommendation. If this field is empty, all contents are candidates. |


<span id="b87d4885"></span>
#### **Root_content**

The parent content information, if any. The parent content refers to the content whose details page contains the recommended content the user has seen or clicked on. Its proto contains the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|content_id |String |Yes |632461 |The unique identifier for a piece of content. The content_id can be the series_id/entity_id/video_id/ or any other type of content identifier. |
|is_recommendable |Int32 |Yes |1 |Determines if the content should be recommended to the user.<br><br>The accepted values are:<br><br><br>* 1—The content should be recommended to users.<br><br>* 0— The content should not be recommended to users.<br><br><br>Even if the content is not recommended to your users, you must submit this parameter to us. Users might have interacted with this content before, and this information allows us to provide more accurate recommendations. |
|categories |String |Yes |[<br><br>{"category_depth":1,<br><br>"category_nodes": [{"id_or_name":"Movie"}] },<br><br>{"category_depth":2,<br><br>"category_nodes": [{"id_or_name":"Comedy"}] }<br><br>] |The categories that a piece of content belongs to. The category value is a JSON serialized string.<br><br>If the content belongs to 2 different categories, the value should look like this:<br><br>```JSON```<br>```[```<br>``` {"category_depth":1,```<br>```  "category_nodes": [{"id_or_name":"Movie"}] },```<br>``` {"category_depth":2,```<br>```  "category_nodes": [{"id_or_name":"Comedy"},```<br>```                     {"id_or_name":"Action"}] }```<br>```]```<br><br><br>You can also serialize the JSON object to String like the following:<br><br>```Python```<br>```categories = json.dumps( [```<br>```   {"category_depth":1,```<br>```    "category_nodes": [{"id_or_name":"Movie"}] },```<br>```   {"category_depth":2,```<br>```    "category_nodes": [{"id_or_name":"Comedy"}] }```<br>``` ])```<br> |
|content_type |String |Yes |video |The content type. The accepted values are:<br><br><br>* picture<br><br>* GIF<br><br>* video<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the <code>content_type</code> is video, ensure that the <code>video_duration</code> parameter has a value of more than 0.</div><br><br><br><br>* text<br><br>* other |
|video_duration |Int32 |*  |2400000 |If the `content_type` is video, enter the video length in milliseconds. |
|content_title |String |No |Video #1 |The content title. |
|description |String |No |Test video |The content description. |
|content_owner |String |No |359938082141597 |The content creator or publisher's user_id. |
|content_owner_followers |Int32 |No |1000 |The number of followers the content owner has. |
|content_owner_rating |Float |No |3.5 |The rating of the content owner, if any. |
|content_owner_name |String |No |testuser#1 |The name of the content owner. |
|collection_id |String |No |1234 |Enter the collection ID if the content belongs to any collection. |
|tags |String |No |New, Trending |The content's internal tags. |
|topic_tags |String |No |Political, Latest |Enter the tags of the topic if the content belongs to any topic. |
|image_urls |String |No |https://demo.jpg |Enter the url to the image file, if any. |
|detail_pic_num |Int32 |No |1 |The number of images displayed on the detail page. |
|video_urls |String |No |https://test_video.mov |Enter the url to the video file, if any. |
|user_rating |Float |No |3.5 |The content's rating given by users. The value range is from 0.0\-5.0. |
|views_count |Int32 |No |10000 |The content's view count. |
|comments_count |Int32 |No |100 |The content's comment count. |
|likes_count |Int32 |No |10 |The content's like count. |
|shares_count |Int32 |No |50 |The content's share count. |
|save_count |Int32 |No |50 |The content's save count. |
|current_price |Int32 |Yes |12100 |This parameter is only applicable if the value of is_paid_content is 1. Enter the current price of the content in cents, if discounted.<br><br>For example, $121.00 = 12100. |
|original_price |Int32 |No |12300 |This parameter is only applicable if the value of is_paid_content is 1. Enter the price of the content in cents.<br><br>For example, $123.00 = 12300. |
|available_location |String |No |Cafe 101 |The location where the content is available for viewing. |
|publish_timestamp |Int32 |No |1623193487 |The timestamp when the content is published. |
|update_timestamp |Int32 |No |1623193487 |The timestamp when the content is updated. |
|copyright_start_timestamp |Int32 |No |1623193487 |The timestamp when the content is available to users. |
|copyright_end_timestamp |Int32 |No |1623194487 |The timestamp when the content is no longer available to users. |
|is_paid_content |Boolean |No |True |Whether users need to pay to access the content, for example, subscribe to the platform before being granted access to the content. The accepted values are as follows:<br><br><br>* True—If it is paid content.<br><br>* False—If it is free content. |
|language |String |No |English |The languages used in the content. |
|related_content_ids |String |No |12345678 |If your platform provides the "Related Content" section, enter the list of related content IDs. |
|sold_count |Int32 |No |100 |If the content requires payment, provide the number of purchases. |
|source |String |No |Self |The source of the recommendation.<br><br>The accepted values are:<br><br><br>* Self—indicates that the recommendation came from the caller's own engine.<br><br>* Other—indicates that the recommendation came from a third\-party engine. |


<span id="3e7fc9f9"></span>
#### **Device**

The platform used to access the content. It contains the following fields:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|platform |String |Yes |App |The platform used to access the content. The accepted values are:<br><br><br>* app<br><br>* desktop\-web<br><br>* mobile\-web<br><br>* other |
|os_type |String |No |Android |The OS of the platform used by the user. The accepted values are:<br><br><br>* iOS<br><br>* Android<br><br>* Windows<br><br>* Other |
|app_version |String |No |9.2.0 |Your application version when the user accessed the content. |
|device_model |String |No |iPhone X |The user's device model. |
|device_brand |String |No |Apple |The user's device brand. |
|os_version |String |No |10 |The user's device's operating system version. |
|browser_type |String |No |Chrome |The browser used to access the content. |
|user_agent |String |No |Safari |The UserAgent for the browser. |
|network |String |No |4G |The user's network. The accepted values are:<br><br><br>* 2G<br><br>* 3G<br><br>* 4G<br><br>* 5G<br><br>* WIFI<br><br>* Other |


<span id="c490f0e2"></span>
#### Candidate_contents

The list of candidates for recommendation. If this field is empty, all contents are candidates.


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|content_id |String |Yes |632461 |The unique identifier for a piece of content. The content_id can be the series_id/entity_id/video_id/ or any other type of content identifier. |
|is_recommendable |Int32 |Yes |1 |Determines if the content should be recommended to the user.<br><br>The accepted values are:<br><br><br>* 1—The content should be recommended to users.<br><br>* 0— The content should not be recommended to users.<br><br><br>Even if the content is not recommended to your users, you must submit this parameter to us. Users might have interacted with this content before, and this information allows us to provide more accurate recommendations. |
|categories |String |Yes |[<br><br>{"category_depth":1,<br><br>"category_nodes": [{"id_or_name":"Movie"}] },<br><br>{"category_depth":2,<br><br>"category_nodes": [{"id_or_name":"Comedy"}] }<br><br>] |The categories that a piece of content belongs to. The category value is a JSON serialized string.<br><br>If the content belongs to 2 different categories, the value should look like this:<br><br>```JSON```<br>```[```<br>``` {"category_depth":1,```<br>```  "category_nodes": [{"id_or_name":"Movie"}] },```<br>``` {"category_depth":2,```<br>```  "category_nodes": [{"id_or_name":"Comedy"},```<br>```                     {"id_or_name":"Action"}] }```<br>```]```<br><br><br>You can also serialize the JSON object to String like the following:<br><br>```Python```<br>```categories = json.dumps( [```<br>```   {"category_depth":1,```<br>```    "category_nodes": [{"id_or_name":"Movie"}] },```<br>```   {"category_depth":2,```<br>```    "category_nodes": [{"id_or_name":"Comedy"}] }```<br>``` ])```<br> |
|content_type |String |Yes |video |The content type. The accepted values are:<br><br><br>* picture<br><br>* GIF<br><br>* video<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the <code>content_type</code> is video, ensure that the <code>video_duration</code> parameter has a value of more than 0.</div><br><br><br><br>* text<br><br>* other |
|video_duration |Int32 |No |2400000 |If the `content_type` is video, enter the video length in milliseconds. |
|content_title |String |No |Video #1 |The content title. |
|description |String |No |Test video |The content description. |
|content_owner |String |No |1234567 |The user ID of the account that created the content or the video publisher. |
|content_owner_followers |Int32 |No |1000 |The number of followers the content owner has. |
|content_owner_rating |Float |No |3.5 |The rating of the content owner, if any. |
|content_owner_name |String |No |testuser#1 |The content owner's name. |
|collection_id |String |No |1234 |The collection ID of the content, if applicable. |
|tags |Array of Strings |No |New, Trending |The content's internal tags. |
|topic_tags |String |No |Political |The content's topic tags, if applicable. |
|image_urls |String |No |https://demo.jpg |The image file's URL. |
|detail_pic_num |Int32 |No |1 |The number of images displayed on the details page. |
|video_urls |String |No |https://test_video.mov |The video file's URL. |
|user_rating |Float |No |0.0 |The content's rating given by users. The value range is from 0.0\-5.0. |
|views_count |Int32 |No |10000 |The content's view count. |
|comments_count |Int32 |No |100 |The content's comment count. |
|likes_count |Int32 |No |1000 |The content's like count. |
|shares_count |Int32 |No |50 |The content's share count. |
|save_count |Int32 |No |50 |The content's save count. |
|current_price |Int32 |Yes |12100 |This parameter is only applicable if the value of is_paid_content is 1. Enter the current price of the content in cents, if discounted.<br><br>For example, $121.00 = 12100. |
|original_price |Int32 |No |12300 |This parameter is only applicable if the value of is_paid_content is 1. Enter the price of the content in cents.<br><br>For example, $123.00 = 12300. |
|available_location |String |No |Cafe 101 |The location where the content is available for viewing. |
|publish_timestamp |Int32 |No |1623193487 |The timestamp when the content is published. |
|update_timestamp |Int32 |No |1623193487 |The timestamp when the content is updated. |
|copyright_start_timestamp |Int32 |No |1623193487 |The timestamp when the content is available to users. |
|copyright_end_timestamp |Int32 |No |1623194487 |The timestamp when the content is no longer available to users. |
|is_paid_content |Boolean |No |True |Whether the content requires payment or a subscription to access. The accepted values are as follows:<br><br><br>* True—If it is paid content.<br><br>* False—If it is free content. |
|language |String |No |English |The languages used in the content. |
|related_content_ids |String |No |12345678 |If your platform provides the "Related Content" section, enter the list of related content IDs. |
|sold_count |Int32 |No |100 |If the content requires payment, provide the number of purchases. |
|source |String |No |Self |The source of the recommendation.<br><br>The accepted values are:<br><br><br>* Self—indicates that the recommendation came from the caller's own engine.<br><br>* Other—indicates that the recommendation came from a third\-party engine. |


<span id="0ce09166"></span>
# Response parameters

The following tables details the response parameters for the Predict API:


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|status |Object |*  |The `status` defines an error model. Each `status` message contains two types of data: error code and error message. |
|request_id |String |*  |The same request ID as `PredictRequest.Request.id`. |
|content_value |Object |*  |The Predict call result. |


<span id="9ae6633f"></span>
## Content_value


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|response_contents |Array of Objects |*  |The predicted content list. |
|extra |Object |*  |A catch\-all field that returns any additional information, typically for debugging. |


<span id="f72bcc0f"></span>
### Response_contents


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|content_id |String |*  |The content's ID. This is the same as `Content.content_id`. |
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
     --url https://rec-api-sg1.recplusapi.com/ContentSaaS/Predict \
     --header 'Tenant-Id: 3000001813' \
     --header 'Request-Id: 221b7634-0a4c-497c-b268-e4b2f9b475b8' \
     --header 'accept: application/json' \
     --header 'content-type: application/json' \
     --data '
{
  "project_id": "807247981",
  "model_id": "100001",
  "user_id": "1457789",
  "size": 20,
  "scene": {
    "scene_name": "home_page",
    "page_number": 1,
    "offset": 10
  },
  "content_context": {
    "root_content": {
      "content_id": "7324310"
    },
    "device": {
      "platform": "app",
      "os_type": "android",
      "app_version": "V9.0.8",
      "device_model": "iPhone10",
      "device_brand": "Samsung",
      "os_version": "14.4.2",
      "browser_type": "chrome",
      "user_agent": "mock_user_agent",
      "network": "4g"
    },
    "candidate_contents": [
      {
        "content_id": "6324610"
      },
      {
        "content_id": "6324611"
      },
      {
        "content_id": "6324612"
      },
      {
        "content_id": "6324613"
      }
    ]
  },
  "extra": {
    "extra_key": "extra_value"
  }
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
  },
  "request_id": "221b7634-0a4c-497c-b268-e4b2f9b475b8",
  "content_value": {
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
        "content_id": "product_id_3",
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

```JSON
{ 
  "status": { 
    "code": 400, 
    "message": "unmarshal request body fail, plz make sure path is correct. path:/ContentSaaS/Predict, targetReqType:*saas.PredictRequest; errID:852940573 logID:202304041027049278AA2F7CA2A95A785F" 
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


<span id="01345d64"></span>
# Error codes

For more information on the API error codes, refer to [BytePlus Recommend shared error and status codes](https://docs.byteplus.com/recommend/reference/shared_error_and_status_codes).
