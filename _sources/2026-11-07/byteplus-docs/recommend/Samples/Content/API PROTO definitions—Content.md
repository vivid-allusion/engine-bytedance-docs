---
title: "API PROTO definitions—Content"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/samples-content_api_proto_definitions"
---

This reference guide contains the API PROTO definitions for the Content Industry saas.proto and the scalar value types used in the .proto file.

<span id="saas.proto"></span>
# saas.proto

This section documents the PROTO definitions for saas.proto.

<span id="AckServerImpressionsRequest"></span>
## AckServerImpressionsRequest

The request proto for the AckServerImpressions API contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|project_id |string | |Required.<br><br>The unique identifier for the recommendation project. |
|model_id |string | |Required.<br><br>The unique identifier for the recommendation model used. |
|predict_request_id |string | |Required.<br><br>The unique identifier for the API request.<br><br>The value should be same as PredictRequest.request_id. |
|user_id |string | |Required.<br><br>The unique identifier for the user.<br><br>The value should be same as PredictRequest.user_id. |
|traffic_source |string | |Required.<br><br>The source of the recommendation.<br><br>The accepted values are:<br><br><br>* self—indicates that the recommendation came from the caller's own engine.<br><br>* byteplus—indicates that the recommendation came from BytePlus.<br><br>* other—indicates that the recommendation came from a third\-party engine. |
|scene |Scene | |Required.<br><br>The recommendation scene information.<br><br>Ensure that this is as close to UserEvent.scene as possible. |
|altered_contents |AckServerImpressionsRequest.AlteredContent |repeated |Required.<br><br>The list of altered contents. |
|extra |AckServerImpressionsRequest.ExtraEntry |repeated |Optional.<br><br>A catch\-all field to pass any additional information.<br><br>You should provide as much information as possible using this field. |


<span id="AckServerImpressionsRequest.AlteredContent"></span>
## AckServerImpressionsRequest.AlteredContent

AckServerImpressionsRequest.AlteredContent contains information about a piece of content that has been altered in the recommendation result. Its proto contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|content_id |string | |Required.<br><br>The unique identifier for the content.<br><br>The value is same as Content.content_id. |
|altered_reason |string | |Required.<br><br>The content's final state.<br><br>The accepted values are:<br><br><br>* kept—indicates that the content was included in the actual impression.<br><br>* filtered—indicates that the content was filtered out of the actual impression by your platform's logic.<br><br>* inserted—indicates that the content was inserted into the actual impression by your platform's logic. |
|rank |int32 | |Required.<br><br>The content's final recommendation ranking.<br><br>If the value is unset or 0, it is assumed that the content is filtered out from the actual impression. |
|content_id_hash |int64 | |Internal.<br><br>The content ID hash.<br><br>If content_id is a number, the value of content_id_hash is the same as content_id. If content_id is not a number, the value of content_id_hash is fnv(content_id). |
|extra |AckServerImpressionsRequest.AlteredContent.ExtraEntry |repeated |Optional.<br><br>A catch\-all field to pass any additional information.<br><br>You should provide as much information as possible using this field. |


<span id="AckServerImpressionsRequest.AlteredContent.ExtraEntry"></span>
## AckServerImpressionsRequest.AlteredContent.ExtraEntry

AckServerImpressionsRequest.AlteredContent.ExtraEntry contains additional information for altered content in an AckServerImpressions API request. Its proto contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|key |string | |Key. |
|value |string | |Value. |


<span id="AckServerImpressionsRequest.ExtraEntry"></span>
## AckServerImpressionsRequest.ExtraEntry

AckServerImpressionsRequest.ExtraEntry contains additional information for an AckServerImpressions API request. Its proto contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|key |string | |Key. |
|value |string | |Value. |


<span id="AckServerImpressionsResponse"></span>
## AckServerImpressionsResponse

The response message for the AckServerImpressions API contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|status |Status | |Output only.<br><br>The API call response status. |


<span id="Content"></span>
## Content

The content proto contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|content_id |string | |Required.<br><br>The unique identifier for the content, which can be one of the following:<br><br><br>* series_id<br><br>* entity_id<br><br>* video_id<br><br>* other unique identifiers<br><br><br>For example, "12345678", "146582662088489399", and so on. |
|is_recommendable |int32 | |Required.<br><br>Whether the content is recommendable.<br><br>The accepted values are:<br><br><br>* 1—indicates that the content is recommendable and can be returned in the recommendation result<br><br>* 0—indicates that the content is not recommendable<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Even if the content is not recommendable, you should still send the content's information to BytePlus Recommend. Given that users may still interact with these content, such as viewing its details page, the content information provides strong signals about the user's preference.</div><br> |
|categories |string | |Required.<br><br>The content category.<br><br>The order of its depth should be ascending. For example, if a piece of content is categorized as "Movie \> Comedy", the JSON array looks like the following:<br><br>```JSON```<br>```[```<br>``` {"category_depth":1,```<br>``` "category_nodes": [{"id_or_name":"Movie"}] },```<br>``` {"category_depth":2,```<br>``` "category_nodes": [{"id_or_name":"Comedy"}] }```<br>```]```<br>``````<br><br><br>If a piece of content belongs to two different categories, "Movie \> Comedy" and "Movie \> Action", the JSON array looks like the following:<br><br>```JSON```<br>```[```<br>``` {"category_depth":1,```<br>``` "category_nodes": [{"id_or_name":"Movie"}] },```<br>``` {"category_depth":2,```<br>``` "category_nodes": [{"id_or_name":"Comedy"},```<br>``` {"id_or_name":"Action"}] }```<br>```]```<br><br><br>However, the values should be formatted as a serialized string containing the JSON array. Serialization can be carried out in a number of different ways. For example, in Python:<br><br>```Python```<br>```categories = json.dumps( [```<br>``` {"category_depth":1,```<br>``` "category_nodes": [{"id_or_name":"Movie"}] },```<br>``` {"category_depth":2,```<br>``` "category_nodes": [{"id_or_name":"Comedy"}] }```<br>```])```<br> |
|content_type |string | |Required.<br><br>The type of content.<br><br>The accepted values are:<br><br><br>* picture<br><br>* gif<br><br>* video<br><br>* text<br><br>* other<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the content_type is video, video_duration must be non\-zero.</div><br> |
|video_duration |int32 | |Depends on content_type. Required for videos.<br><br>The video duration in milliseconds.<br><br>For example, "1200000". |
|content_title |string | |Optional.<br><br>The content title.<br><br>For example, "Video #1", "Titanic clip", and so on. |
|description |string | |Optional.<br><br>The content description. |
|content_owner |string | |Optional.<br><br>The user who created or published the content.<br><br>For example, "1234567", "359938082141597", "665DEA957EBFB34D41B1F1D80E4B5F89", and so on. |
|content_owner_followers |int32 | |Optional.<br><br>The number of followers that the content owner has.<br><br>For example, "0", "1000", "1000000", and so on. |
|content_owner_rating |float | |Optional.<br><br>The content owner's rating, if any.<br><br>For example, "3.5", "98.0", and so on. |
|content_owner_name |string | |Optional.<br><br>The content owner's name.<br><br>For example, "testuser#1". |
|collection_id |string | |Optional.<br><br>The unique identifier for the content's collection, if the content belongs to a collection.<br><br>For example, "1234". |
|tags |string | |Optional.<br><br>The content's internal tags.<br><br>The values should be formatted as a serialized string containing the JSON array. For example, "["New", "Trending"]". |
|topic_tags |string | |Optional.<br><br>The content's topic tags, if any.<br><br>The values should be formatted as a serialized string containing the JSON array. For example, "["Political", "Latest"]". |
|image_urls |string | |Optional.<br><br>The URL for the image file.<br><br>The values should be formatted as a serialized string containing the JSON array. |
|detail_pic_num |int32 | |Optional.<br><br>The number of images displayed on the details page.<br><br>For example, "1", "5", and so on. |
|video_urls |string | |Optional.<br><br>The URL for the video file.<br><br>The values should be formatted as a serialized string containing the JSON array. |
|user_rating |float | |Optional.<br><br>The content rating given by the users.<br><br>The value is normalized to [0.0, 5.0], which is the accepted value range. |
|views_count |int32 | |Optional.<br><br>The number of views for the content.<br><br>For example, "10000". |
|comments_count |int32 | |Optional.<br><br>The number of comments for the content.<br><br>For example, "100". |
|likes_count |int32 | |Optional.<br><br>The number of likes for the content.<br><br>For example, "10". |
|shares_count |int32 | |Optional.<br><br>The number of shares for the content.<br><br>For example, "50". |
|save_count |int32 | |Optional.<br><br>The number of saves for the content.<br><br>For example, "50". |
|current_price |int32 | |Required.<br><br>The current price in cents, if the content is paid content.<br><br>For example, $100.12 should be "10012". |
|original_price |int32 | |Optional.<br><br>The original price in cents, if the content is paid content.<br><br>For example, $100.12 should be "10012". |
|available_location |string | |Optional.<br><br>The content's location tags.<br><br>The values should be formatted as a serialized string containing the JSON array. For example, "["Cafe 101"]". |
|publish_timestamp |int32 | |Optional.<br><br>The timestamp when the content is published for viewing.<br><br>For example, "1623193487". |
|update_timestamp |int32 | |Optional.<br><br>The timestamp when any content information, such as categories, description, and so on, is updated.<br><br>For example, "1623193487". |
|copyright_start_timestamp |int32 | |Optional.<br><br>The timestamp when the content can be shown to users.<br><br>For example, "1623193487". |
|copyright_end_timestamp |int32 | |Optional.<br><br>The timestamp when the content stops being available to users.<br><br>For example, "1623193487". |
|is_paid_content |bool | |Optional.<br><br>Whether the content requires payment or a subscription to view. |
|language |string | |Optional.<br><br>The languages used in the content.<br><br>For example, "English", "Chinese", and so on. |
|related_content_ids |string | |Optional.<br><br>The unique identifier for related content, if your platform provides "Related Content" recommendations.<br><br>The values should be formatted as a serialized string containing the JSON array. For example, "["12345678","12345679"]". |
|sold_count |int32 | |Optional.<br><br>The number of content purchases, if the content requires payment.<br><br>For example, "100". |
|source |string | |Optional.<br><br>The source of the content.<br><br>The accepted values are:<br><br><br>* self<br><br>* thirdparty<br><br>* other |


<span id="DataError"></span>
## DataError

DataError contains a summary of error messages returned in a Write API response. Its proto contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|message |string | |Output only.<br><br>The detailed error message, which should be in English.<br><br>For example, "An unexpected value XXX is included in the XXX field. Only ["xx", "yy", "zz"] can be accepted." |
|data |string | |Output only.<br><br>The specific abnormal data. |


<span id="Device"></span>
## Device

The device proto contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|platform |string | |Required.<br><br>The platform used by the user.<br><br>The accepted values are:<br><br><br>* app<br><br>* desktop\-web<br><br>* mobile\-web<br><br>* other |
|os_type |string | |Optional.<br><br>The operating system used by the user.<br><br>The accepted values are:<br><br><br>* android<br><br>* ios<br><br>* windows<br><br>* other |
|app_version |string | |Optional.<br><br>The application version.<br><br>For example, "V9.0.8". |
|device_model |string | |Optional.<br><br>The device model used by the user.<br><br>For example, "iPhone 10", "Pixel 4". |
|device_brand |string | |Optional.<br><br>The brand of the device used by the user.<br><br>For example, "Samsung". |
|os_version |string | |Optional.<br><br>The operating system version used by the user.<br><br>For example, "14.4.2". |
|browser_type |string | |Optional.<br><br>The type of browser used by the user.<br><br>For example, "Chrome", "Firefox", and so on. |
|user_agent |string | |Optional.<br><br>The UserAgent for the browser. |
|network |string | |Optional.<br><br>The network used by the user.<br><br>The accepted values are:<br><br><br>* 2g<br><br>* 3g<br><br>* 4g<br><br>* 5g<br><br>* wifi<br><br>* other |


<span id="PredictRequest"></span>
## PredictRequest

The request proto for the Predict API contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|project_id |string | |Required.<br><br>The unique identifier for the recommendation project. |
|model_id |string | |Required.<br><br>The unique identifier for the recommendation model used. |
|user_id |string | |Required.<br><br>The unique identifier for the user.<br><br>The value is same as User.user_id. |
|size |int32 | |Required.<br><br>The maximum number of pieces of content returned.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><em>The actual number of pieces of content returned is the minimum of the following numbers:</em></div><br><br><br><br>* <div data-tips="true" data-tips-type="tip"><em>size</em></div><br><br><br>* <div data-tips="true" data-tips-type="tip"><em>length(context.candidate_content_ids)</em></div><br><br><br>* <div data-tips="true" data-tips-type="tip"><em>Total number of content with is_recommendable=1</em></div><br> |
|scene |Scene | |Optional.<br><br>The recommendation scene information. |
|context |PredictRequest.Context | |Optional.<br><br>The context of the current Predict request. |
|extra |PredictRequest.ExtraEntry |repeated |Optional.<br><br>A catch\-all field to pass any additional information.<br><br>You should provide as much information as possible using this field. |


<span id="PredictRequest.Context"></span>
## PredictRequest.Context

PredictRequest.Context contains the context of a Predict API request. Its proto contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|root_content |Content | |Optional.<br><br>The parent content information, if any. The parent content refers to the content whose details page contains the recommended content that the user has seen or clicked on.<br><br>This field is only required for the content details page. |
|device |Device | |Optional.<br><br>The device information.<br><br>Ensure that the value is as close to UserEvent.device as possible. |
|candidate_contents |Content |repeated |Optional.<br><br>The list of candidates for recommendation.<br><br>If this field is empty, all content are candidates. |


<span id="PredictRequest.ExtraEntry"></span>
## PredictRequest.ExtraEntry

PredictRequest.ExtraEntry contains additional information for a Predict API request. Its proto contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|key |string | |Key. |
|value |string | |Value. |


<span id="PredictResponse"></span>
## PredictResponse

The response message for the Predict API contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|status |Status | |Output only.<br><br>The API call response status. |
|request_id |string | |Output only.<br><br>The unique identifier for the API request.<br><br>The value is same as PredictRequest.request_id. |
|content_value |PredictResult | |Output only.<br><br>The API result.<br><br>This field is only populated when PredictResponse.status.code is 0. |


<span id="PredictResult"></span>
## PredictResult

PredictResult contains a single Predict API call result. Its proto contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|response_contents |PredictResult.ResponseContent |repeated |Output only.<br><br>The list of predicted content. |
|extra |PredictResult.ExtraEntry |repeated |Output only.<br><br>A catch\-all field that returns any additional information, typically for debugging. |


<span id="PredictResult.ExtraEntry"></span>
## PredictResult.ExtraEntry

PredictResult.ExtraEntry contains additional information for a Predict API call result. Its proto contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|key |string | |Key. |
|value |string | |Value. |


<span id="PredictResult.ResponseContent"></span>
## PredictResult.ResponseContent

PredictResult.ResponseContent contains the content information of a single recommendation in a Predict API call result. Its proto contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|content_id |string | |Output only.<br><br>The unique identifier for the content.<br><br>The value is consistent with Content.content_id. |
|rank |int32 | |Output only.<br><br>The content's recommendation ranking. |
|pctr |double | |Output only.<br><br>The predicted Click\-Through Rate (CTR). |
|pcvr |double | |Output only.<br><br>The predicted Conversion Rate (CVR). |
|rec_info |string | |Output only.<br><br>The strategy used for this particular recommendation result. |
|extra |PredictResult.ResponseContent.ExtraEntry |repeated |Output only.<br><br>A catch\-all field that returns any additional information, typically for debugging. |


<span id="PredictResult.ResponseContent.ExtraEntry"></span>
## PredictResult.ResponseContent.ExtraEntry

PredictResult.ResponseContent.ExtraEntry contains additional information for a Predict API call result response. Its proto contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|key |string | |Key. |
|value |string | |Value. |


<span id="Scene"></span>
## Scene

Scene refers to the location where the user interaction event happened. The scene proto contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|scene_name |string | |Required.<br><br>The unique identifier for the scene.<br><br>For example, "home_page", "search_page", "details_page", and so on.<br><br>The value is determined by the scene specified during model training.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">It is strongly recommended that you use one recommendation model per scene if possible</div><br> |
|page_number |int32 | |Optional.<br><br>The page number.<br><br>This field can refer to:<br><br><br>* the page number that the content is found on.<br><br>* the number of times that users swipe the screen before seeing the content.<br><br><br>The default value is 0, which indicates that all content fits into a single page. |
|offset |int32 | |Optional.<br><br>The content's position within the page itself. |


<span id="Status"></span>
## Status

Status defines a logical error model. The status proto contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|code |int32 | |Output only.<br><br>The response code, which could be a success code or an error code. Users should expect this field for all responses.<br><br>The possible values are:<br><br><br>* 0—indicates that the request is successfully returned.<br><br>* xxx—3\-digit error codes, which align with standard HTTP error codes. For example, 4xx indicates user error while 5xx indicates server error.<br><br>* 2xxx—indicates errors related to Predict calls.<br><br><br>For more information, refer to [Error codes](https://docs.byteplus.com/recommend/resources/error-codes). |
|message |string | |Output only.<br><br>The detailed error message. |


<span id="User"></span>
## User

The user proto contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|user_id |string | |Required.<br><br>The unique identifier for the user.<br><br>For example, "1234567", "359938082141597", "665DEA957EBFB34D41B1F1D80E4B5F89", and so on.<br><br>The value of user_id is often the device ID or member ID.<br><br>Consistency is required for each user across different UserEvents, PredictRequest, and so on.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If you want to encrypt user_id and use the hashed value in this field, ensure that the hashed value is consistent for each user.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If users often switch between a login/logout status on your platform, the same user may be recorded with different IDs (member versus visitor). To ensure consistency, we recommend using an immutable ID like device ID.</div><br> |
|user_id_type |string | |Optional.<br><br>The type of user ID.<br><br>For example, "email", "phone number", "facebook", "system_generated", and so on. |
|gender |string | |Optional.<br><br>The user's gender.<br><br>The accepted values are:<br><br><br>* male<br><br>* female<br><br>* other |
|age |string | |Optional.<br><br>The user's age.<br><br>The value can be a single value (estimate) or a range. For example, "23", "18\-25", "0\-15", "50\-100", and so on. |
|tags |string | |Optional.<br><br>The user's tags.<br><br>The values should be formatted as a serialized string containing the JSON array. For example, "["new users", "high buying power"]".<br><br>You should fill in this field as much as possible even if the tags have low coverage or are slightly inaccurate. |
|language |string | |Optional.<br><br>The primary language used by the user.<br><br>For example, "Chinese", "English", and so on. |
|subscriber_type |string | |Optional.<br><br>Whether the user is a subscriber.<br><br>The accepted values are:<br><br><br>* free<br><br>* subscribed<br><br>* other |
|network |string | |Optional.<br><br>The network used by the user.<br><br>The accepted values are:<br><br><br>* 2g<br><br>* 3g<br><br>* 4g<br><br>* 5g<br><br>* wifi<br><br>* other |
|platform |string | |Optional.<br><br>The platform used by the user.<br><br>The accepted values are:<br><br><br>* app<br><br>* desktop\-web<br><br>* mobile\-web<br><br>* other |
|os_type |string | |Optional.<br><br>The operating system used by the user.<br><br>The accepted values are:<br><br><br>* android<br><br>* ios<br><br>* windows<br><br>* other |
|app_version |string | |Optional.<br><br>The application version of user's device.<br><br>For example, "V9.0.8", "V9.0.9", and so on. |
|device_model |string | |Optional.<br><br>The device model used by the user.<br><br>For example, "iPhone 10", "Pixel 4". |
|os_version |string | |Optional.<br><br>The operating system version used by the user.<br><br>For example, "14.4.2", "14.4.3", and so on. |
|membership_level |string | |Optional.<br><br>The user's membership level.<br><br>For example, "silver", "elite", "4", "5", and so on. |
|registration_timestamp |int32 | |Optional.<br><br>The timestamp when the user registered to your platform.<br><br>For example, "1623593487". |
|update_timestamp |int32 | |Optional.<br><br>The timestamp when any user information, such as username, name, date of birth, and so on, is updated.<br><br>For example, "1623593487". |
|last_login_timestamp |int32 | |Optional.<br><br>The timestamp of the user's last login.<br><br>For example, "1623593487". |
|country |string | |Optional.<br><br>The user's country.<br><br>For example, "USA", "UK", and so on. |
|province |string | |Optional.<br><br>The user's province.<br><br>For example, "Texas", "Alaska", and so on. |
|city |string | |Optional.<br><br>The user's city.<br><br>For example, "Kirkland". |
|district |string | |Optional.<br><br>The user's district. For example,<br><br>"King County". |
|area |string | |Optional.<br><br>The user's area.<br><br>For example, "Neighborhood #1". |


<span id="UserEvent"></span>
## UserEvent

The user event proto contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|user_id |string | |Required.<br><br>The unique identifier for the user.<br><br>For more information, refer to User.user_id. |
|event_type |string | |Required.<br><br>The type of user event.<br><br>The accepted values are:<br><br><br>* impression<br><br>* click<br><br>* auto_play<br><br>* manual_play<br><br>* playover<br><br>* like<br><br>* share<br><br>* follow<br><br>* comment<br><br>* purchase<br><br>* add\-to\-cart<br><br>* add\-to\-favorites<br><br>* search<br><br>* stay\-detail\-page<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This field is for the type of user event, which is separate from the actual scene.</div><br><br><br>Some of these event_types are required.<br><br><br>* **impression**—Required. When a piece of content is seen by a user. The impression can be counted based on the client side or server side. The client side is preferred.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">content_id must be filled.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">scene_name must be filled.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If multiple pieces of content are seen by a user together, each content should be sent as separate user events.</div><br><br><br><br>**click**—Required. When a user clicks on a piece of content.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">content_id must be filled.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">scene_name must be filled.</div><br><br><br>* **auto_play**—Optional. When a video plays automatically, if the content is a video.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">content_id must be filled.</div><br><br><br><br>* **manual_play**—Optional. When a user plays the video manually, if the content is a video.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">content_id must be filled.</div><br><br><br><br>* **playover**—Optional. When a user completes the video, if the content is a video.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">content_id must be filled.</div><br><br><br><br>* **like**—Optional. When a user likes a piece of content.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">content_id must be filled.</div><br><br><br><br>* **share**—Optional. When a user shares a piece of content.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">content_id must be filled.</div><br><br><br><br>* **follow**—Optional. When a user follows a piece of content.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">content_id must be filled.</div><br><br><br><br>* **comment**—Optional. When a user leaves a comment on a piece of content.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">content_id must be filled.</div><br><br><br><br>* **purchase**—Required. When a user completes a purchase of a piece of content.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">content_id must be filled.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If one order contains multiple pieces of content, each content should be sent as separate user events.</div><br><br><br>* **add\-to\-cart**—Optional. When a user adds a piece of content to the shopping cart.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">content_id must be filled.</div><br><br><br><br>* **add\-to\-favorites**—Optional. When a user adds a piece of content to the favorite list.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">content_id must be filled.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you do not have a favorite list feature on your platform, you can enter "like" event data directly without the "add\-to\-favorites" event.</div><br><br><br>* **search**—Optional. When a user searches for content.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">content_id must be filled.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">query must be filled.</div><br><br><br>* *stay\-detail\-page*—Optional. When a user stays on a content detail page.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">content_id must be filled.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">detail_stay_time must be a value more than 0.</div><br> |
|event_timestamp |int32 | |Required.<br><br>The timestamp when the event happened. |
|content_id |string | |Depends on event_type. Required for all types of user events except for search events.<br><br>The unique identifier for the content.<br><br>The field should be empty for search events. |
|traffic_source |string | |Optional.<br><br>The source of the recommendation leading to the user event.<br><br>The accepted values are:<br><br><br>* self—indicates that the recommendation came from the caller's own engine.<br><br>* byteplus—indicates that the recommendation came from BytePlus.<br><br>* other—indicates that the recommendation came from a third\-party engine. |
|request_id |string | |Optional.<br><br>The unique identifier for the API request.<br><br>For example, "67a9fcf74a82fdc55a26ab4ee12a7b96890407fc0042f8cc014<br><br>e07a4a560a9ac".<br><br>The value will be provided by BytePlus, in order to match the user event with the request_id when the Predict API is called. |
|rec_info |string | |Optional.<br><br>The identifier for the BytePlus Recommend strategy and model used to produce the recommendation.<br><br>For example, "CiRiMjYyYjM1YS0xOTk1LTQ5YmMtOGNkNS1mZTVm<br><br>YTczN2FkNDASJAobcmVjZW50X2hvdF9jbGlja3NfcmV0cmlldmVyFQ<br><br>AAAAAYDxoKCgNjdHIdog58PBoKCgNjdnIdANK2OCIHMjcyNTgwMg<br><br>==".<br><br>The value will be provided by BytePlus, which contains detailed algorithm information from BytePlus. |
|attribution_token |string | |Optional.<br><br>The identifier used to hook all relevant user events in a user session.<br><br>For example, "eyJpc3MiOiJuaW5naGFvLm5ldCIsImV4cCI6IjE0Mzg5NTU0NDUiLCJu<br><br>YW1lIjoid2FuZ2hhbyIsImFkbWluIjp0cnVlfQ". |
|scene_name |string | |Depends on event_type. Required for impression and click events. Optional for all other types of user events.<br><br>The unique identifier for the scene.<br><br>For example, "home_page", "search_page", "content_detail_page", and so on.<br><br>It is strongly recommended that you use one recommendation model per scene if possible. |
|page_number |int32 | |Optional.<br><br>The page number.<br><br>This field can refer to:<br><br><br>* the page number that the content is found on.<br><br>* the number of times that users swipe the screen before seeing the content.<br><br><br>The default value is 0, which indicates that all content fits into a single page. |
|offset |int32 | |Optional.<br><br>The content's position within the page itself.<br><br>For example, "1", "10", and so on. |
|play_duration |int32 | |Optional.<br><br>The user's watch duration in milliseconds, if the content is a video.<br><br>For example, "150000". |
|video_duration |int32 | |Optional.<br><br>The video duration in milliseconds, if the content is a video.<br><br>For example, "1200000". |
|start_time |int32 | |Optional.<br><br>The starting point of the user's watch duration in milliseconds, if the content is a video.<br><br>For example, "0" if the user starts watching the video from the beginning, "150000" if the user starts watching the video from the 2min 30s mark, and so on. |
|end_time |int32 | |Optional.<br><br>The ending point of the user's watch duration in milliseconds, if the content is a video.<br><br>For example, "300000" if the user stops watching the video at the 5min mark. |
|parent_content_id |string | |Optional.<br><br>The unique identifier of the parent content, if any. The parent content refers to the content whose details page contains the recommended content that the user has seen or clicked on. |
|content_owner_id |string | |Optional.<br><br>The unique identifier for the content owner.<br><br>For example, "1234". |
|detail_stay_time |int32 | |Depends on event_type.<br><br>The user's stay duration on the content's details page in seconds.<br><br>If the event_type is stay\-detail\-page, the value of detail_stay_time must be non\-zero. |
|dislike_type |string | |Optional.<br><br>The type of dislike, if your platform supports dislike as a user event.<br><br>For example, "content_id", "content_owner_id", "tag", and so on. |
|dislike_value |string | |Optional.<br><br>The number of dislikes, if your platform supports dislike as a user event. |
|query |string | |Depends on event_type. Required for search events.<br><br>The user's search query.<br><br>This field should also be filled when the type of user event is a purchase or impression event that follows a search event. |
|platform |string | |Optional.<br><br>The platform used by the user.<br><br>The accepted values are:<br><br><br>* app<br><br>* desktop\-web<br><br>* mobile\-web<br><br>* other |
|os_type |string | |Optional.<br><br>The operating system used by the user.<br><br>The accepted values are:<br><br><br>* android<br><br>* ios<br><br>* windows<br><br>* other |
|app_version |string | |Optional.<br><br>The application version of user's device.<br><br>For example, "V9.0.8", "V9.0.9", and so on. |
|device_model |string | |Optional.<br><br>The device model used by the user.<br><br>For example, "iPhone 10", "Pixel 4". |
|os_version |string | |Optional.<br><br>The operating system version used by the user.<br><br>For example, "14.4.2", "14.4.3", and so on. |
|network |string | |Optional.<br><br>The network used by the user.<br><br>The accepted values are:<br><br><br>* 2g<br><br>* 3g<br><br>* 4g<br><br>* 5g<br><br>* wifi<br><br>* other |
|country |string | |Optional.<br><br>The user's country.<br><br>For example, "USA", "UK", and so on. |
|province |string | |Optional.<br><br>The user's province.<br><br>For example, "Texas", "Alaska", and so on. |
|city |string | |Optional.<br><br>The user's city.<br><br>For example, "Kirkland". |
|district |string | |Optional.<br><br>The user's district. For example,<br><br>"King County". |
|area |string | |Optional.<br><br>The user's area.<br><br>For example, "Neighborhood #1". |


<span id="WriteDataRequest"></span>
## WriteDataRequest

The request proto for the Write APIs contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|project_id |string | |Required.<br><br>The unique identifier for the recommendation project. |
|stage |string | |Required.<br><br>The data import stage, corresponding to stages in the Recommendation Console.<br><br>The possible values are:<br><br><br>* trial—indicates the test data/pre\-synchronization stage, where data is only used for testing.<br><br>* production—indicates the historical data synchronization stage, where data is used to train the model.<br><br>* incrementalRealtime—indicates the incremental real\-time data synchronization stage, where data is used to update the model in real\-time.<br><br>* incrementalDaily—indicates the incremental daily data synchronization stage, where data is used to update the model daily. |
|data |string |repeated |Required.<br><br>An array where each element is a JSON serialized string of data representing one data record. For example, to send data using the Write APIs, the following JSON array should be serialized into a string:<br><br>```JSON```<br>```[```<br>``` {```<br>``` "user_id": "1457789",```<br>``` "user_id_type": "system_generated",```<br>``` "gender": "male",```<br>``` "age": "23",```<br>``` "tags": "[\"new user\",\"low purchasing power\",\"bargain seeker\"]",```<br>``` "language": "English",```<br>``` "subscriber_type": "free",```<br>``` "network": "4g",```<br>``` "platform": "app",```<br>``` "os_type": "ios",```<br>``` "app_version": "1.0.1",```<br>``` "device_model": "iPhone10",```<br>``` "os_version": "14.4.2",```<br>``` "membership_level": "silver",```<br>``` "registration_timestamp": 1659958007,```<br>``` "update_timestamp": 1659958007,```<br>``` "last_login_timestamp": 1659958207,```<br>``` "country": "USA",```<br>``` "province": "Texas",```<br>``` "city": "Kirkland",```<br>``` "district": "King County",```<br>``` "area": "Neighborhood #1"```<br>``` },```<br>``` {```<br>``` "user_id": "1457790",```<br>``` "user_id_type": "system_generated",```<br>``` "gender": "female",```<br>``` "age": "20-40",```<br>``` "tags": "[\"new user\"]",```<br>``` "language": "English",```<br>``` "subscriber_type": "free",```<br>``` "network": "wifi",```<br>``` "platform": "app",```<br>``` "os_type": "android",```<br>``` "app_version": "2.1.3",```<br>``` "device_model": "Huawei-Mate30",```<br>``` "os_version": "14.4.3",```<br>``` "membership_level": "silver",```<br>``` "registration_timestamp": 1659957007,```<br>``` "update_timestamp": 1659957007,```<br>``` "last_login_timestamp": 1659957207,```<br>``` "country": "USA",```<br>``` "province": "Texas",```<br>``` "city": "Kirkland",```<br>``` "district": "King County",```<br>``` "area": "Neighborhood #2"```<br>``` }```<br>```]```<br> |
|extra |WriteDataRequest.ExtraEntry |repeated |Optional.<br><br>A catch\-all field to pass any additional information.<br><br>You should provide as much information as possible using this field. |


<span id="WriteDataRequest.ExtraEntry"></span>
## WriteDataRequest.ExtraEntry

WriteDataRequest.ExtraEntry contains additional information for a Write API request. Its proto contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|key |string | |Key. |
|value |string | |Value. |


<span id="WriteResponse"></span>
## WriteResponse

The response message for the Write APIs contains the following fields:


|**Field** |**Type** |**Label** |**Description** |
|---|---|---|---|
|status |Status | |Output only.<br><br>The API call response status.<br><br>If status.code is 0, it indicates that no exception occurred during execution and the full data import has been successful. |
|errors |DataError |repeated |Output only.<br><br>The summary of error messages for when the data import fails.<br><br>This field contains a value when status.code is 1206. Even if this field contains no value, the data import is unsuccessful when status.code is not 0. |


<span id="BytePlusSaasService"></span>
## BytePlusSaasService

The BytePlus Recommend SaaS service contains the following APIs:


|**Method Name** |**Request Type** |**Response Type** |**Description** |
|---|---|---|---|
|WriteUsers |WriteDataRequest |WriteResponse |Batch writes User information up to 2,000 data entries in a single request. Exceeding 2,000 entries in a request results in a rejection.<br><br>You can use this method to upload new data or to update existing data. |
|WriteContents |WriteDataRequest |WriteResponse |Batch writes Content information up to 2,000 data entries in a single request. Exceeding 2,000 entries in a request results in a rejection.<br><br>You can use this method to upload new data or to update existing data. |
|WriteUserEvents |WriteDataRequest |WriteResponse |Batch writes UserEvent information up to 2,000 data entries in a single request. Exceeding 2,000 entries in a request results in a rejection.<br><br>You can use this method to upload new data only. The method does not support updating existing data. |
|Predict |PredictRequest |PredictResponse |Gets the ranked list of content.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Any incremental User data will take effect in 24 hours. Any incremental Content data will take effect in 30 minutes. Depending on how the incremental UserEvent data is imported (in real\-time or in batch), it will be fed into the model and take effect afterwards.</div><br> |
|AckServerImpressions |AckServerImpressionsRequest |AckServerImpressionsResponse |Sends back to the server the actual content shown to the user, which may differ from the list of content in the PredictResponse.<br><br>For example, the Predict API returns a list of items [1, 2, 3, 4], but your platform logic has filtered content 3 because it has been sold out and inserted content 10 before content 2 based on a promotion rule. The AckServerImpressionsRequest will look like the following:<br><br>```Plain```<br>```[```<br>``` {id:1, altered_reason: "kept", rank:1},```<br>``` {id:10, altered_reason: "inserted", rank:2},```<br>``` {id:2, altered_reason: "kept", rank:3},```<br>``` {id:4, altered_reason: "kept", rank:4},```<br>``` {id:3, altered_reason: "filtered", rank:0},```<br>```]</pre]```<br> |


<span id="Methods with HTTP bindings"></span>
### Methods with HTTP bindings

The BytePlus Recommend APIs have the following HTTP bindings:


|**Method Name** |**Method** |**Path** |**Body** |
|---|---|---|---|
|WriteUsers |POST |/ContentSaaS/WriteUsers |*  |
|WriteContents |POST |/ContentSaaS/WriteContents |*  |
|WriteUserEvents |POST |/ContentSaaS/WriteUserEvents |*  |
|Predict |POST |/ContentSaaS/Predict |*  |
|AckServerImpressions |POST |/ContentSaaS/AckServerImpressions |*  |


<span id="Scalar value types"></span>
# Scalar value types

This section documents the scalar value types specified in the .proto file and their corresponding types in various programming languages:


| **.proto Type** |**Notes** |**C++ Type** |**Java Type** |**Python Type** |**Go Type** |**C# Type** |**PHP Type** |**Ruby Type** |
|---|---|---|---|---|---|---|---|---|
|double |*  |double |double |float |float64 |double |float |Float |
|float |*  |float |float |float |float32 |float |float |Float |
|int32 |Uses variable\-length encoding. Inefficient for encoding negative numbers. If your field is likely to have negative values, use sint32 instead. |int32 |int |int |int32 |int |integer |Bignum or Fixnum (as required) |
|int64 |Uses variable\-length encoding. Inefficient for encoding negative numbers. If your field is likely to have negative values, use sint64 instead. |int64 |long |int/long |int64 |long |integer/<br><br>string |Bignum |
|uint32 |Uses variable\-length encoding. |uint32 |int |int/long |uint32 |uint |integer |Bignum or Fixnum (as required) |
|uint64 |Uses variable\-length encoding. |uint64 |long |int/long |uint64 |ulong |integer/<br><br>string |Bignum or Fixnum (as required) |
|sint32 |Uses variable\-length encoding. Signed int value. Encodes negative numbers more efficiently than regular int32. |int32 |int |int |int32 |int |integer |Bignum or Fixnum (as required) |
|sint64 |Uses variable\-length encoding. Signed int value. Encodes negative numbers more efficiently than regular int64. |int64 |long |int/long |int64 |long |integer/<br><br>string |Bignum |
|fixed32 |Always four bytes. More efficient than uint32 if values are often greater than 2^28. |uint32 |int |int |uint32 |uint |integer |Bignum or Fixnum (as required) |
|fixed64 |Always eight bytes. More efficient than uint64 if values are often greater than 2^56. |uint64 |long |int/long |uint64 |ulong |integer/<br><br>string |Bignum |
|sfixed32 |Always four bytes. |int32 |int |int |int32 |int |integer |Bignum or Fixnum (as required) |
|sfixed64 |Always eight bytes. |int64 |long |int/long |int64 |long |integer/<br><br>string |Bignum |
|bool |*  |bool |boolean |boolean |bool |bool |boolean |TrueClass/<br><br>FalseClass |
|string |Must always contain UTF\-8 encoded or 7\-bit ASCII text. |string |String |str/<br><br>unicode |string |string |string |String (UTF\-8) |
|bytes |May contain any arbitrary sequence of bytes. |string |ByteString |str |[]byte |ByteString |string |String (ASCII\-8BIT) |
