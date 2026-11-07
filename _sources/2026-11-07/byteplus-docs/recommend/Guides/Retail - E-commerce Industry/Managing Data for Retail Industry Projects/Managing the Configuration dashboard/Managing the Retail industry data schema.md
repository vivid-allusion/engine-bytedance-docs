---
title: "Managing the Retail industry data schema"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/docs-managing_the_schema"
---

You can use the BytePlus Recommend Console to define your data schemas. In Trial mode, you can modify the data schema as much as you required. However, once your data is imported in Live mode, the defined schema cannot be modified. If needed, users can create another project with a different schema.

We have provided pre\-defined data fields configured for businesses in the retail and e\-commerce industries. It is highly recommended for users to fulfill the data field requirements to optimize model training efficiency and recommendation accuracy.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">There are no differences in the data schema configuration process between the Trial and Live mode.</div>


<span id="75fd9205"></span>
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

<span id="e14cc74c"></span>
# Adding custom data schemas

You can modify the schema list by adding a custom field if required.

**To add a custom data schema:** 


1. Sign in to [BytePlus Recommend](https://console.byteplus.com/recommend/home).

2. Click on the project you want to modify.

3. Click the edit icon.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8278ed53bb354050b3ca6a6aa94d5226~tplv-goo7wpa0wc-image.image" width="864px" />   </div>
   

   The Edit Schema screen appears.

4. Click **Add custom field**.

   A new field appears.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3e76157c1b074bd6aaab38bbb29bfe9a~tplv-goo7wpa0wc-image.image" width="864px" />   </div>
   

5. Enter the following field details: **Field name**, **Type**, and **Description**.

6. Click **Save schema**.

7. (Optional) If you want to delete the field, click the delete icon.

   The new custom field is saved.


<span id="d374f7af"></span>
# Selecting the schema fields

You can select the schema fields to be included in your data schema list.

**Selecting the schema fields:** 


1. Sign in to [BytePlus Recommend](https://console.byteplus.com/recommend/home).

2. Click on the project you want to modify.

3. Click the edit icon.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8278ed53bb354050b3ca6a6aa94d5226~tplv-goo7wpa0wc-image.image" width="864px" />   </div>
   

   The Edit Schema screen appears.

4. Check the box next to the schema field that you want to include in your list.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Checking the top box allows you to select all the schema fields listed.   </div>
   

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/29cb5bca85074bd4a82a51b147155b04~tplv-goo7wpa0wc-image.image" width="864px" />   </div>
   

5. Click on **User**, **Product**, and **User Events** to modify the schema list within each field.

6. Click **Save Schema**.

   The updated schema list is saved.


<span id="f5e911ef"></span>
# Data schema list

There are three data schema categories that you must fill in:


* **User**: User refers to one of the users that you provide your services.

* **Product**: Product refers to one of the items in your catalog.

* **User Events**: User Events refers to the interaction between your users and the products on your platform.


<span id="ec113fcb"></span>
## Default User data schema fields

The BytePlus Recommend console provides you with a default User data schema list. You can manage the schema list as required.


|**Field Name** |**Requirement** |**Priority** |**Description** |
|---|---|---|---|
|user_id |Required |P0 |The unique identifier for the user. The user_id must remain consistent when used in other data imports like UserEvents or Predict.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you plan to encrypt the user_id and substitute it with a hashed value, ensure that you use the identical encrypted value in other parameters.</div><br><br><br>If you plan to encrypt the user_id and substitute it with a hashed value, ensure that you use the identical encrypted value in other parameters. |
|tags |Optional |P1 |The tags for the user. You should include as many tags as possible for the user, even if it has low coverage or might be inaccurate. Some accepted values include:<br><br><br>* new users.<br><br>* low purchasing power.<br><br>* bargain seeker. |
|language |Optional |P2 |The language(s) set by this user. |
|registration_timestamp |Optional |P2 |The timestamp when the user registered or activated an account. |
|activation_channel |Optional |P2 |The channel where the user was acquired.<br><br>Some accepted values include:<br><br><br>* AppStore<br><br>* GoogleAds<br><br>* FacebookAds |
|country |Optional |P2 |The default country set by user, which may differ from their live location. |
|province |Optional |P2 |The default province set by user, which may differ from their live location. |
|city |Optional |P2 |The default city set by user, which may differ from their live location. |
|district |Optional |P2 |The default district set by user, which may differ from their live location. |
|membership_level |Optional |P2 |The user's membership level.<br><br>Some accepted values include:<br><br><br>* silver<br><br>* elite<br><br>* 4<br><br>* 5 |
|gender |Optional |P2 |The user's gender. Some accepted values are:<br><br><br>* Male<br><br>* Female<br><br>* Other |
|age |Optional |P2 |The user's age. The accepted values can be an estimated value or a range. |


<span id="4e9f7b39"></span>
## Default Product data schema fields

The BytePlus Recommend console provides you with a default Product data schema list. You can manage the schema list as required.


|**Field Name** |**Requirement** |**Priority** |**Description** |
|---|---|---|---|
|product_id |Required |P0 |The unique identifier for the product.<br><br>Some accepted values are:<br><br><br>* Series_id.<br><br>* Entity_id.<br><br>* Other unique identifier. |
|is_recommendable |Required |P0 |This field is used to determine whether the product should be recommended to users. The accepted values are as follows:<br><br><br>* True—The product should be recommended to users.<br><br>* False—The product should not be recommended to users.<br><br><br>Even if a product is not recommended to your users, it is important to submit this parameter to us. Users may have interacted with this product in the past, and providing this information enables us to deliver more accurate recommendations. |
|current_price |Required |P0 |The current/displayed/discounted price of the product. Ensure that the value is rounded to 2.d.p. and is a non\-negative value. |
|original_price |Optional |P1 |The original price of the product. Ensure that the value is rounded to 2.d.p. and is a non\-negative value. |
|publish_timestamp |Optional |P1 |The time when the product is put on sale. |
|categories |Optional |P1 |The categories that the product belongs to. The category value is a JSON serialized string.<br><br>**Format requirements:** <br><br><br>* JSON serialised string<br><br>* Depth starts from 1, in consecutive positive integers<br><br>* `Category_nodes` should not contain empty values. If an empty value exists, replace it with `null` .<br><br>* Only one `id_or_name` key\-value pair is allowed under each `category_nodes` |
|tags |Optional |P1 |The product's internal tags. Format it into a JSON serialized string.<br><br>Some accepted values include:<br><br><br>* New Product.<br><br>* Summer Product. |
|title |Optional |P1 |The product title. You can use the text name of the product or the title on the HTML page. |
|brands |Optional |P1 |The brands that the product belongs to. You should sort the brands by their `brand_depth` in ascending order. |
|user_rating |Optional |P2 |The rating given by the users. The value has to be positive. |
|sold_count |Optional |P2 |The number of sales of the product if it is a paid product. The value has to be positive. |
|product_group_id |Optional |P2 |The ID of the group/unit for products with common characteristics |
|display_cover_multimedia_url |Optional |P2 |The URL of the cover multimedia for the product. Format into a JSON serialized string. |
|comment_count |Optional |P2 |The number of comments for this product. The value has to be positive. |
|source |Optional |P2 |The source of the product. Some accepted values are:<br><br><br>* Self<br><br>* Third\-party<br><br>* Other |
|seller_id |Optional |P2 |The unique identifier for the seller. |
|seller_level |Optional |P2 |The seller's tier/level. Some accepted values include:<br><br><br>* gold<br><br>* silver |
|seller_rating |Optional |P2 |The seller's rating given by the customers. The value range should be between 0.0 and 5.0. The value has to be positive. |


<span id="b4c44c1c"></span>
## Default User Events data schema fields

The BytePlus Recommend console provides you with a default User Events data schema list. You can manage the schema list as required.


|**Field Name** |**Sub\-Field Name** |**Requirement** |**Requirement Criteria** |**Priority** |**Description** |
|---|---|---|---|---|---|
|user_id | |Required |Value: true |P0 |The unique identifier for the user. |
|event_type<br><br>The UserEvent type. The accepted values are:<br><br><br>* impression<br><br>* click<br><br>* purchase<br><br>* add\-to\-cart<br><br>* remove\-from\-cart<br><br>* checkout<br><br>* add\-to\-favorites<br><br>* remove\-from\-favorites<br><br>* search<br><br><br>You can modify the event_types if needed. |impression |Required |Value: true |P0 |When user views the product. It can be from client side (preferred) or server side.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If multiple products are viewed at one time, import them as separate user events</div><br> |
||click |Required |Value: true |P0 |When users click on the product. |
||purchase |Required |Value: true |P0 |When users purchase the product. |
||add\-to\-cart |Optional | |P0 |When users add the product to their cart. |
||add\-to\-favorites |Optional | |P0 |When user adds the product to their favorites. |
||checkout |Optional | |P0 |When users make an immediate purchase of the product. This is applicable to "express checkout" or "buy now" scenarios. |
||remove\-from\-cart |Optional | |P0 |When users remove the product from their cart. |
||remove\-from\-favorites |Optional | |P0 |When users remove the product from their favorites. |
||search |Optional | |P0 |When user performs a search. |
|event_timestamp | |Required |Value: true |P0 |The timestamp when the event happened. |
|scene_name | |Conditionally required. |Required when the `event_type` value is the following:<br><br><br>* Impression<br><br>* Click |P0 |The unique identifier for the UserEvent scene. Some accepted values include:<br><br><br>* Home page<br><br>* Search page<br><br>* Details page |
|product_id | |Conditionally required. |Required when the `event_type` value is the following:<br><br><br>* impression<br><br>* click<br><br>* add\-to\-cart<br><br>* remove\-from\-cart<br><br>* add\-to\-favorites<br><br>* remove\-from\-favorites<br><br>* purchase<br><br>* checkout |P0 |The unique identifier for the product. This parameter should only be empty if the event_type is "search". |
|purchase_count | |Conditionally required. |Required when the `event_type` value is `purchase`. |P1 |The final number of products purchased in the record. This parameter value must be more than 0. |
|paid_price | |Conditionally required. |Required when the `event_type` value is `purchase`. |P1 |The final amount paid by the user. This parameter value must be more than 0. The value must match the value of the `currency`used. |
|parent_product_id | |Conditionally required. |Required when the `event_type` value is `product_detail_page`. |P1 |The unique ID of the root product during a User Event. Recommended to be provided if the user viewed/clicked on the product from a product detail page. |
|query | |Conditionally required. |Required when the `event_type` value is `search`. |P1 |The search query. It is also required when the purchase or impression event occurs after the search event. |
|page_number | |Optional |range: \>=0 |P1 |The page number.<br><br>It can refer to:<br><br><br>* the page number that the content is found on.<br><br>* the number of times that users swipe the screen before seeing the content.<br><br><br>The default value is 0, which indicates that all content fits into a single page. |
|offset | |Optional |range: \>=0 |P1 |The content's position within the page itself. An integer value starting from 1. |
|platform | |Optional | |P1 |The platform used by the user. Some accepted values are:<br><br><br>* app<br><br>* desktop\-web<br><br>* mobile\-web<br><br>* other |
|os_type | |Optional | |P1 |The user's operating system. |
|os_version | |Optional | |P1 |The version of user's operating system. |
|app_version | |Optional | |P1 |The version of user's application. |
|network | |Optional | |P1 |The user's network. |
|device_model | |Optional | |P1 |The user's device model. |
|attribution_token | |Optional | |P1 |The identifier used to gather all the relevant events within one user session. |
|traffic_source | |Optional | |P2 |The source of the directed traffic for this UserEvent. The accepted values are:<br><br><br>* Self—Self\-generated traffic<br><br>* BytePlus—BytePlus\-generated traffic<br><br>* Other—Other system\-generated traffic |
|currency | |Optional | |P2 |The currency used in the transaction record. Recommended to provide for `purchase` event type. It is also suggested to standardize the currency to USD across multiple countries/regions. |
|country | |Optional | |P2 |The country where the user event took place. |
|province | |Optional | |P2 |The province where the user event took place. |
|city | |Optional | |P2 |The city where the user event took place. |
|district | |Optional | |P2 |The district where the user event took place. |
