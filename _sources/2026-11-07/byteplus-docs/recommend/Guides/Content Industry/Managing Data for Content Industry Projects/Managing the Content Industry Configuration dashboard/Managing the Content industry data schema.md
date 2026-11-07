---
title: "Managing the Content industry data schema"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/docs-managing_the_content_industry_data_schema"
---

You can use the BytePlus Recommend Console to define your data schemas. In Trial mode, you can modify the data schema as much as you required. However, once your data is imported in Live mode, the defined schema cannot be modified. If needed, users can create another project with a different schema.

We have provided pre\-defined that are configured for businesses in the media and entertainment industry. It is highly recommended for users to fulfill the data field requirements to optimise model training efficiency and recommendation accuracy.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">There are no differences in the data schema configuration process between the Trial and Live mode.</div>


<span id="98aa859c"></span>
# Data schema field categories

The data schema fields are categorized into the following: **Requirement** and **Priority**.


|**Categories** |**Fields** |**Description** |
|---|---|---|
|Requirement |Required |Mandatory field to be filled. |
||Conditional |Fields that are required with the condition of a certain event type. |
||Optional |Good to have but not required. |
|Priority |P0 |This field is mandatory and must be uploaded. Failure to provide this field hinders the entire process. |
||P1 |These fields play a crucial role in model training and feature engineering. It is conditionally required or highly recommended to include these fields for better results. |
||P2 |These fields are optional but can potentially enhance the model training outcome. |


You can read 'Required' fields first to check the mandatory requirements. Then you can check 'Conditional' fields to determine if these fields are required under my condition, and if you find conditionally required ones, you should check 'Priority' to determine how important this field is. Lastly, you can check 'Optional' fields with the order of priority.

A user can't save a schema list that lacks the required conditional fields for specific event types.

<span id="5c73f5df"></span>
# Adding custom data schemas

You can modify the schema list by adding a custom field if required.

**To add a custom data schema:** 


1. Sign in to [BytePlus Recommend](https://console.byteplus.com/recommend/home).

2. Click on the project you want to modify.

3. Click the edit icon.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/de94283e7f304735b4be948a1582eda5~tplv-goo7wpa0wc-image.image) </span>

   The Edit Schema screen appears.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1182046d52894546a4b91eb34c2ab0b9~tplv-goo7wpa0wc-image.image) </span>

4. Click **Add custom field**.

   A new field appears.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e42e99394f234cab823d08b9269c6f1a~tplv-goo7wpa0wc-image.image) </span>

5. Enter the following field details: **Field name**, **Type**, and **Description**.

6. Click **Save schema**.

7. (Optional) If you want to delete the field, click the delete icon.

   The new custom field is saved.


<span id="9b8b11ee"></span>
# Selecting the schema fields

You can select the schema fields to be included in your data schema list.

**Selecting the schema fields:** 


1. Sign in to [BytePlus Recommend](https://console.byteplus.com/recommend/home).

2. Click on the project you want to modify.

3. Click the edit icon.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/de94283e7f304735b4be948a1582eda5~tplv-goo7wpa0wc-image.image" width="864px" />   </div>
   

   The Edit Schema screen appears.

4. Check the box next to the schema field that you want to include in your list.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Checking the top box allows you to select all the schema fields listed.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/49e78d931bcf44ef90465e35545367df~tplv-goo7wpa0wc-image.image) </span>

5. Click on **User**, **Content**, and **User Events** to modify the schema list within each field.

6. Click **Save Schema**.

   The updated schema list is saved.


<span id="d5c25f11"></span>
# Data schema list

There are three data schema categories that you must fill in:


* **User**: User refers to one of the users that you provide your services.

* **Content**: Content refers to one of the content your platform offers.

* **User Events**: User Events refers to the interaction between your users and the content on your platform.


<span id="69ba6644"></span>
## Default User data schema fields

The BytePlus Recommend console provides you with a default User data schema list. You can manage the schema list as required.


|**Field Name** |**Requirement** |**Priority** |**Description** |
|---|---|---|---|
|user_id |Required |P0 |The unique identifier for the user. The user_id must remain consistent when used in other data imports like UserEvents or Predict.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you plan to encrypt the user_id and substitute it with a hashed value, ensure that you use the identical encrypted value in other parameters.</div><br><br><br>If you plan to encrypt the user_id and substitute it with a hashed value, ensure that you use the identical encrypted value in other parameters. |
|tags |Optional |P1 |The tags for the user. You should include as many tags as possible for the user, even if it has low coverage or might be inaccurate. Some accepted values include:<br><br><br>* new users.<br><br>* low purchasing power.<br><br>* bargain seeker. |
|language |Optional |P2 |The language(s) set by this user. |
|registration_timestamp |Optional |P2 |The timestamp when the user registered or activated an account. |
|subscriber_type |Optional |P2 |The user's subscription tier. For example, whether the user is a paying customer or not. |
|membership_level |Optional |P2 |The user's membership level.<br><br>Some accepted values include:<br><br><br>* silver<br><br>* elite<br><br>* 4<br><br>* 5 |
|country |Optional |P2 |The default country set by user, which may differ from their live location. |
|province |Optional |P2 |The default province set by user, which may differ from their live location. |
|city |Optional |P2 |The default city set by user, which may differ from their live location. |
|district |Optional |P2 |The default district set by user, which may differ from their live location. |
|gender |Optional |P2 |The user's gender. Some accepted values are:<br><br><br>* Male<br><br>* Female<br><br>* Other |
|age |Optional |P2 |The user's age. The accepted values can be an estimated value or a range. |


<span id="a8c4e571"></span>
## Default Content data schema fields

The BytePlus Recommend console provides you with a default Content data schema list. You can manage the schema list as required.


|**Field Name** |**Requirement** |**Priority** |**Description** |
|---|---|---|---|
|content_id |Required |P0 |The unique identifier for a piece of content. The content_id can be the series_id/entity_id/video_id/ or any other type of content identifier. |
|content_type |Required |P0 |The content type. The accepted values are:<br><br><br>* picture<br><br>* GIF<br><br>* video<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the <code>content_type</code> is video, ensure that the <code>video_duration</code> parameter has a value of more than 0.   </div><br>   <br><br>* text<br><br>* other |
|is_recommendable |Required |P0 |This field is used to determine whether the content should be recommended to users. The accepted values are as follows:<br><br><br>* True—The content should be recommended to users.<br><br>* False—The content should not be recommended to users.<br><br><br>Even if the content is not recommended to your users, it is important to submit this parameter to us. Users may have interacted with this content in the past, and providing this information enables us to deliver more accurate recommendations. |
|language |Optional |P1 |The content's language. |
|content_title |Optional |P1 |The content title. |
|categories |Optional |P1 |The categories that the product belongs to. The category value is a JSON serialized string.<br><br>**Format requirements:** <br><br><br>* JSON serialised string<br><br>* Depth starts from 1, in consecutive positive integers<br><br>* `Category_nodes` should not contain empty values. If an empty value exists, replace it with `null` .<br><br>* Only one `id_or_name` key\-value pair is allowed under each `category_nodes` |
|tags |Optional |P1 |The product's internal tags. Format it into a JSON serialized string.<br><br>Some accepted values include:<br><br><br>* New.<br><br>* Trending. |
|collection_id |Optional |P1 |The collection ID to which the content belongs. |
|publish_timestamp |Optional |P1 |The time when the product is put on sale. |
|content_owner_id |Optional |P1 |The content creator or publisher's user_id. |
|video_duration |Optional |P1 |If the `content_type` is video, enter the video length in milliseconds. |
|description |Optional |P2 |The detailed description of the content. |
|linked_product_id |Optional |P2 |The product ID of the products sold through the content. |
|video_urls |Optional |P2 |The URL of the video. Format into a JSON serialized string. |
|image_urls |Optional |P2 |The URL of the image. Format into a JSON serialized string. |
|user_rating |Optional |P2 |The rating of the content. It has to be a positive value. |
|is_paid_content |Optional |P2 |Whether users need to pay to access the content, for example, subscribe to the platform before being granted access to the content. The accepted values are as follows:<br><br><br>* 1—If it is paid content.<br><br>* 0—If it is free content. |
|source |Optional |P2 |The source of the recommendation.<br><br>The accepted values are:<br><br><br>* Self—indicates that the recommendation came from the caller's own engine.<br><br>* Other—indicates that the recommendation came from a third\-party engine. |
|current_price |Optional |P2 |This parameter is only applicable if the value of `is_paid_content` is 1. Enter the current price of the content in cents, if discounted.<br><br>For example, $121.00 = 12100. |
|original_price |Optional |P2 |This parameter is only applicable if the value of `is_paid_content` is 1. Enter the price of the content in cents.<br><br>For example, $123.00 = 12300. |


<span id="b44e696e"></span>
## Default UserEvents data schema fields

The BytePlus Recommend console provides you with a default UserEvents data schema list. You can manage the schema list as required.


|**Field Name** |**Requirement** |**Priority** |**Description** |
|---|---|---|---|
|user_id |Required |P0 |The unique user identifier. |
|content_id |Required |P0 |The unique identifier for a piece of content. The content_id can be the series_id/entity_id/video_id/ or any other type of content identifier. This field should be empty if the event_type is "search", and otherwise it is required. |
|event_type |Required |P0 |The UserEvent type. The accepted values are:<br><br><br>* impression<br><br>* click<br><br>* stay<br><br>* like<br><br>* share<br><br>* comment<br><br>* follow<br><br>* favorite<br><br>* search<br><br>* cart<br><br>* checkout<br><br>* purchase |
|event_timestamp |Required |P0 |The timestamp when the event occurred. |
|scene_name |Required |P0 |The unique identifier of a UserEvent scene. Values include the home page, search page, details page, and so on. Be as specific as possible. |
|stay_duration |Optional |P1 |The duration of time the user spent on the content in milliseconds. |
|parent_content_id |Optional |P1 |The unique identifier of the parent content, if any. The parent content refers to the content whose details page contains the recommended content that the user has seen or clicked on. |
|query |Optional |P1 |This parameter is required if the event_type is `search`. |
|content_owner_id |Optional |P1 |The user_id of the content owner. Recommended for the `follow` event_type. |
|purchase_count |Optional |P1 |The final number recorded in the purchase data. Recommended for the `purchase` event_type. |
|paid_price |Optional |P1 |The final amount paid by the user. Required for the `purchase` event_type. The value must match the `currency` value provided. |
|page_number |Optional |P1 |This parameter can be the following definitions:<br><br><br>* the page number that the content is found on.<br><br>* the number of times that users swipe the screen before seeing the content. |
|offset |Optional |P1 |The content's position within the page itself. |
|platform |Optional |P1 |The user's platform.<br><br>Some accepted values include:<br><br><br>* app<br><br>* desktop_web<br><br>* mobile_web<br><br>* others |
|os_type |Optional |P1 |The OS of the platform used by the user.<br><br>Some accepted values are:<br><br><br>* iOS<br><br>* Android<br><br>* Windows<br><br>* Other |
|os_version |Optional |P1 |The user's device's operating system version. |
|app_version |Optional |P1 |Your application version when the user accessed the content. |
|network |Optional |P1 |The user's network.<br><br>Some accepted values are:<br><br><br>* 2G<br><br>* 3G<br><br>* 4G<br><br>* 5G<br><br>* WIFI<br><br>* Other |
|device_model |Optional |P1 |The user's device model. |
|attribution_token |Optional |P1 |The identifier used to gather all the relevant events within one user session. |
|traffic_source |Optional |P2 |The source of the directed traffic for this UserEvent.<br><br>Some accepted values are:<br><br><br>* Self—Self\-generated traffic<br><br>* BytePlus—BytePlus\-generated traffic<br><br>* Other—Other system\-generated traffic |
|currency |Optional |P2 |The currency used and recorded in the transaction record. Recommended to provide for the `purchase`event_type. |
|country |Optional |P2 |The country where the UserEvent took place. |
|province |Optional |P2 |The province where the UserEvent took place. |
|city |Optional |P2 |The city where the UserEvent took place. |
|district |Optional |P2 |The district where the UserEvent took place. |
