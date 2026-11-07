---
title: "WriteContents—Recommend Content Industry"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/reference-content_writecontents"
---

The WriteContents API for BytePlus Recommend enables the uploading of new content data or updating existing content data in the Media/Content industry.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information on BytePlus Recommend token authentication, refer <a href="https://docs.byteplus.com/en/recommend/reference/api_token_authentication">here</a>.</div>


<span id="a4e7df39"></span>
# Limitations

The following limitations apply to WriteContents API:


* Each request can upload no more than 2,000 content data records at a time. If you upload more than 2,000 content data records, you will encounter a rejection.

* The result obtained by multiplying QPS by the number of uploads per request must be less than 30,000.

* Deleting content is not supported.


<span id="36c7c3c1"></span>
# HTTP request

This is the URL and HTTP request method for the WriteContents API.


|**URL** |https://rec\-us\-east\-1.byteplusapi.com/data/api/media/${tenant}/content |
|---|---|
|**Method** |POST |


<span id="d5e9f3b3"></span>
# Request parameters

The topics below details the parameters required for the WriteContents API.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Not all request parameters are included in the following table. For a complete list, refer to <a href="https://docs.byteplus.com/recommend/reference/api_token_authentication">HTTP header parameters</a>.</div>


<span id="0ffea6c2"></span>
## Query

The following table details the query parameters required for the WriteContents API:


|**Query String Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|method |String |Yes |Write |*  |


<span id="5be14b39"></span>
## Body

The following table details the body parameters required for the WriteContents API:


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|content_id |String |Yes |632461 |The unique identifier for a piece of content. The content_id can be the series_id/entity_id/video_id/ or any other type of content identifier. |
|is_recommendable |Int32 |Yes |1 |Determines if the content should be recommended to the user.<br><br>The accepted values are:<br><br><br>* 1—The content should be recommended to users.<br><br>* 0— The content should not be recommended to users.<br><br><br>Even if the content is not recommended to your users, you must submit this parameter to us. Users might have interacted with this content before, and this information allows us to provide more accurate recommendations.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Any changes made to the <code>is_recommendable</code> parameter will take up to 1 hour to be reflected.</div><br> |
|categories |String |Yes |[<br><br>{"category_depth":1,<br><br>"category_nodes": [{"id_or_name":"Movie"}] },<br><br>{"category_depth":2,<br><br>"category_nodes": [{"id_or_name":"Comedy"}] }<br><br>] |The categories that a piece of content belongs to. The category value is a JSON serialized string.<br><br>If the content belongs to 2 different categories, the value should look like this:<br><br>```JSON```<br>```[```<br>``` {"category_depth":1,```<br>```  "category_nodes": [{"id_or_name":"Movie"}] },```<br>``` {"category_depth":2,```<br>```  "category_nodes": [{"id_or_name":"Comedy"},```<br>```                     {"id_or_name":"Action"}] }```<br>```]```<br><br><br>You can also serialize the JSON object to String like the following:<br><br>```JSON```<br>```categories = json.dumps( [```<br>```   {"category_depth":1,```<br>```    "category_nodes": [{"id_or_name":"Movie"}] },```<br>```   {"category_depth":2,```<br>```    "category_nodes": [{"id_or_name":"Comedy"}] }```<br>``` ])```<br> |
|content_title |String |Yes |Video #1 |The content title. |
|content_type |String |Yes |video |The content type. The accepted values are:<br><br><br>* picture<br><br>* GIF<br><br>* video<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the <code>content_type</code> is video, ensure that the <code>video_duration</code> parameter has a value of more than 0.   </div><br>   <br><br>* text<br><br>* other |
|description |String |No |Test video |The content description. |
|content_owner |String |No |testuser#1 |The content creator or publisher's user_id. |
|language |String |No |English |The content's language. |
|tags |Array of Strings |No |New, Trending |The content's internal tags. |
|listing_page_display_tags |Array of Strings |No |Popular, Recommend |The content's tags displayed to the user on the listing page, like the home page or category landing page. |
|detail_page_display_tags |Array of Strings |No |Popular, Recommend |The content's tags displayed to the user on the content\-detail page. |
|listing_page_display_type |String |No |image |The content's listing type, if applicable. The accepted values are:<br><br><br>* image<br><br>* video<br><br>* other |
|cover_multimedia_url |String |No |https://demo.jpg |If there is a value in `listing_page_display_type`, fill this parameter with the cover image's link. |
|user_rating |Double |No |3 |The content's rating given by users. The value range is from 0.0 to 5.0. |
|views_count |Int32 |No |10000 |The content's view count. |
|comments_count |Int32 |No |100 |The content's comment count. |
|likes_count |Int32 |No |1000 |The content's like count. |
|shares_count |Int32 |No |50 |The content's share count. |
|is_paid_content |Int32 |No |1 |Whether users need to pay to access the content, for example, subscribe to the platform before being granted access to the content. The accepted values are as follows:<br><br><br>* 1—If it is paid content.<br><br>* 0—If it is free content. |
|origin_price |Int64 |No |12300 |This parameter is only applicable if the value of `is_paid_content` is 1. Enter the price of the content in cents.<br><br>For example, $123.00 = 12300. |
|current_price |Int64 |No |12100 |This parameter is only applicable if the value of `is_paid_content` is 1. Enter the current price of the content in cents, if discounted.<br><br>For example, $121.00 = 12100. |
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
|video_duration |Int64 |No |2400000 |If the `content_type` is video, enter the video length in milliseconds. |
|publish_timestamp |Int64 |No |1623193487 |The timestamp when the content is published. |
|copyright_start_timestamp |Int64 |No |1623193487 |[For OTT platforms]<br><br>The timestamp when the content is available to users. |
|copyright_end_timestamp |Int64 |No |1623194487 |[For OTT platforms]<br><br>The timestamp when the content is no longer available to users. |
|actors |Array of Strings |No |John Doe |[For OTT platforms]<br><br>The actors within the content. |
|source |String |No |Self |The source of the recommendation.<br><br>The accepted values are:<br><br><br>* Self—indicates that the recommendation came from the caller's own engine.<br><br>* Other—indicates that the recommendation came from a third\-party engine. |
|extra |Object |No |*  |A catch\-all field to pass any additional information.<br><br>You should provide as much information as possible using this field. |


<span id="0ce09166"></span>
# Response parameters

The following tables details the response parameters for the WriteContents API:


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|status |Object |*  |The `status` defines an error model. Each `status` message contains two types of data: error code and error message. |
|errors |Array of Objects |*  |This field is populated when the `status`is an error code: 1001. |


<span id="6c0daa02"></span>
## **Status**

The status defines an error model. Each status message contains two types of data: error code and error message.


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|code |Int32 |0 |You should look at this response parameter to determine if your API request was successful.<br><br><br>* 0: it indicates that the calling is successful.<br><br>* 4xx: it indicates user error.<br><br>* 5xx: it indicates server error.<br><br>* 1xxx: it indicates error relating to Import calls.<br><br>* 2xxx: it indicates errors relating to Predict calls. |
|message |String |An unexpected value XXX is included in the XXX field, only ["xx", "yy", "zz"] can be accepted. |Provides a detailed error message on the reasons why your API request was unsuccessful. |


<span id="0ce6d6f9"></span>
### **Content**

The content proto. It contains the following fields:


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|content_id |String |632461 |The unique identifier for a piece of content. The content_id can be the series_id/entity_id/video_id/ or any other type of content identifier. |
|is_recommendable |Int32 |1 |Determines if the content should be recommended to the user.<br><br>The accepted values are:<br><br><br>* 1—The content should be recommended to users.<br><br>* 0— The content should not be recommended to users.<br><br><br>Even if the content is not recommended to your users, you must submit this parameter to us. Users might have interacted with this content before, and this information allows us to provide more accurate recommendations. |
|categories |String |[<br><br>{"category_depth":1,<br><br>"category_nodes": [{"id_or_name":"Movie"}] },<br><br>{"category_depth":2,<br><br>"category_nodes": [{"id_or_name":"Comedy"}] }<br><br>] |The categories that a piece of content belongs to. The category value is a JSON serialized string.<br><br>If the content belongs to 2 different categories, the value should look like this:<br><br>```JSON```<br>```[```<br>``` {"category_depth":1,```<br>```  "category_nodes": [{"id_or_name":"Movie"}] },```<br>``` {"category_depth":2,```<br>```  "category_nodes": [{"id_or_name":"Comedy"},```<br>```                     {"id_or_name":"Action"}] }```<br>```]```<br><br><br>You can also serialize the JSON object to String like the following:<br><br>```JSON```<br>```categories = json.dumps( [```<br>```   {"category_depth":1,```<br>```    "category_nodes": [{"id_or_name":"Movie"}] },```<br>```   {"category_depth":2,```<br>```    "category_nodes": [{"id_or_name":"Comedy"}] }```<br>``` ])```<br> |
|content_title |String |Video #1 |The content title. |
|content_type |String |video |The content type. The accepted values are:<br><br><br>* picture<br><br>* GIF<br><br>* video<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the <code>content_type</code> is video, ensure that the <code>video_duration</code> parameter has a value of more than 0.</div><br><br><br><br>* text<br><br>* other |
|description |String |Test video |The content description. |
|content_owner |String |testuser#1 |The content creator or publisher's user_id. |
|language |String |English |The content's language. |
|tags |Array of Strings |New, Trending |The content's internal tags. |
|listing_page_display_tags |Array of Strings |Popular, Recommend |The content's tags displayed to the user on the listing page, like the home page or category landing page. |
|detail_page_display_tags |Array of Strings |Popular, Recommend |The content's tags displayed to the user on the content\-detail page. |
|listing_page_display_type |String |image |The content's listing type, if applicable. The accepted values are:<br><br><br>* image<br><br>* video<br><br>* other |
|cover_multimedia_url |String |https://demo.jpg |If there is a value in `listing_page_display_type`, fill this parameter with the cover image's link. |
|user_rating |Double |0 |The content's rating given by users. The value range is from 0.0 to 5.0. |
|views_count |Int32 |10000 |The content's view count. |
|comments_count |Int32 |100 |The content's comment count. |
|likes_count |Int32 |1000 |The content's like count. |
|shares_count |Int32 |50 |The content's share count. |
|is_paid_content |Int32 |1 |Whether users need to pay to access the content, for example, subscribe to the platform before being granted access to the content. The accepted values are as follows:<br><br><br>* 1—If it is paid content.<br><br>* 0—If it is free content. |
|origin_price |Int64 |12300 |This parameter is only applicable if the value of `is_paid_content` is 1. Enter the price of the content in cents.<br><br>For example, $123.00 = 12300. |
|current_price |Int64 |12100 |This parameter is only applicable if the value of `is_paid_content` is 1. Enter the current price of the content in cents, if discounted.<br><br>For example, $121.00 = 12100. |
|publish_region |String |US |The region where the content is published. |
|available_region |Array of Strings |US, Singapore, India |The region(s) where the content is available for viewing. |
|entity_id |String |1 |[For the OTT platforms]<br><br>The entity's ID. |
|entity_name |String |Friends |[For the OTT platforms]<br><br>If the content is a television show with multiple seasons, input the show's entity ID as the parameter value. |
|series_id |String |11 |[For OTT platforms]<br><br>If the content is a television show with multiple seasons, input the season's ID as the parameter value. |
|series_index |Int32 |1 |[For OTT platforms]<br><br>If the content is a television show with multiple seasons, input the season's number as the parameter value. |
|series_name |String |Friends Season 1 |[For OTT platforms]<br><br>The name of the season. |
|series_count |Int32 |10 |[For OTT platforms]<br><br>The total number of seasons the television series has. |
|video_id |String |111 |[For OTT platforms]<br><br>The video ID in the television series. |
|video_index |Int32 |6 |[For OTT platforms]<br><br>The video episode within the television series. |
|video_name |String |The One With Ross' New Girlfriend |[For OTT platforms]<br><br>The name of the episode. |
|video_count |Int32 |10 |[For OTT platforms]<br><br>The total number of episodes within the season. |
|video_type |String |series, movie, reality show |[For OTT platforms]<br><br>The video type. |
|video_duration |Int64 |2400000 |If the `content_type` is video, enter the video length in milliseconds. |
|publish_timestamp |Int64 |1623193487 |The timestamp when the content is published. |
|copyright_start_timestamp |Int64 |1623193487 |[For OTT platforms]<br><br>The timestamp when the content is available to users. |
|copyright_end_timestamp |Int64 |1623194487 |[For OTT platforms]<br><br>The timestamp when the content is no longer available to users. |
|actors |Array of Strings |John Doe |[For OTT platforms]<br><br>The actors within the content. |
|source |String |Self |The source of the recommendation.<br><br>The accepted values are:<br><br><br>* Self—indicates that the recommendation came from the caller's own engine.<br><br>* Other—indicates that the recommendation came from a third\-party engine. |
|extra |Object |*  |A catch\-all field to pass any additional information.<br><br>You should provide as much information as possible using this field. |


<span id="ed90ff97"></span>
# Samples

The following section details the sample codes for the WriteContents API.

<span id="fb01f45e"></span>
## Sample request

The following is a sample request for the API.

```JSON
curl --request POST \
     --url 'https://rec-us-east-1.byteplusapi.com/data/api/media/media_demo/content?method=write' \
     --header 'Accept: application/json' \
     --header 'Content-Type: application/json' \
     --header 'Request-Id:12313208' \
     --header 'Tenant-Id:d7c5963593798b5263858b028f589' \
     --header 'Tenant-Nonce:1683634542' \
     --header 'Tenant-Ts:1683634542' \
     --header 'Tenant-Signature:ade6c5d76b6c2e146c88c9535d3c4f0b2f3b4b6716613cb73b0417eabb816bf8' \
     --data '{
     "contents": [
          {
               "content_id": "123456",
               "is_recommendable": 1,
               "categories": "[{\"category_depth\":1,\"category_nodes\":[{\"id_or_name\":\"Movie\"}]},{\"category_depth\":2,\"category_nodes\":[{\"id_or_name\":\" Comedy\"}]}]",
               "content_title": "Video#1",
               "content_type": "video",
               "description": "This is a test video",
               "content_owner": "testuser#1",
               "language": "English",
               "tags": ["New", "Trending"],
               "listing_page_display_tags": ["popular", "recommend"],
               "detail_page_display_tags": ["popular", "recommend"],
               "listing_page_display_type": "image",
               "cover_multimedia_url": "https://images-na.ssl-images-amazon.com/images/I/81WmojBxvbL._AC_UL1500_.jpg",
               "user_rating": 3.0,
               "views_count": 10000,
               "comments_count": 100,
               "likes_count": 1000,
               "shares_count": 50,
               "is_paid_content": 1,
               "origin_price": 12300,
               "current_price": 12100,
               "publish_region": "US",
               "available_region": ["Singapore", "India", "US"],
               "entity_id": "1",
               "entity_name": "Friends",
               "series_id": "11",
               "series_index": 1,
               "series_name": "Friends Season 1",
               "series_count": 10,
               "video_id": "111",
               "video_index": 6,
               "video_name": "The One With Ross New Girlfriend",
               "video_count": 10,
               "video_type": "series",
               "video_duration": 7200000,
               "publish_timestamp": 1647570563,
               "copyright_start_timestamp": 1647570563,
               "copyright_end_timestamp": 1647670563,
               "actors": ["Rachel Green", "Ross Geller"],
               "source": "self",
               "extra": {
                   "key": "value"
               }
          }
     ],
     "extra": {
         "extra_key": "extra_value"
     }
}'
```


<span id="de55caff"></span>
## Sample responses

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
      "content": {
        "is_recommendable": 1,
        "categories": "[{\"category_depth\":1,\"category_nodes\":[{\"id_or_name\":\"Movie\"}]},{\"category_depth\":2,\"category_nodes\":[{\"id_or_name\":\" Comedy\"}]}]",
        "content_title": "Video#1",
        "content_type": "video",
        "description": "This is a test video",
        "content_owner": "testuser#1",
        "language": "English",
        "tags": [
          "New",
          "Trending"
        ],
        "listing_page_display_tags": [
          "popular",
          "recommend"
        ],
        "detail_page_display_tags": [
          "popular",
          "recommend"
        ],
        "listing_page_display_type": "image",
        "cover_multimedia_url": "https://images-na.ssl-images-amazon.com/images/I/81WmojBxvbL._AC_UL1500_.jpg",
        "user_rating": 3,
        "views_count": 10000,
        "comments_count": 100,
        "likes_count": 1000,
        "shares_count": 50,
        "is_paid_content": 1,
        "origin_price": "12300",
        "current_price": "12100",
        "publish_region": "US",
        "available_region": [
          "Singapore",
          "India",
          "US"
        ],
        "entity_id": "1",
        "entity_name": "Friends",
        "series_id": "11",
        "series_index": 1,
        "series_name": "Friends Season 1",
        "series_count": 10,
        "video_id": "111",
        "video_index": 6,
        "video_name": "The One With Ross New Girlfriend",
        "video_count": 10,
        "video_type": "series",
        "video_duration": "7200000",
        "publish_timestamp": "1647570563",
        "copyright_start_timestamp": "1647570563",
        "copyright_end_timestamp": "1647670563",
        "actors": [
          "Rachel Green",
          "Ross Geller"
        ],
        "source": "self",
        "extra": {
          "key": "value"
        }
      }
    }
  ]
}
```


<span id="9398e94b"></span>
# Error codes

For more information on the API error codes, refer to [BytePlus Recommend shared error and status codes](https://docs.byteplus.com/recommend/reference/shared_error_and_status_codes).
