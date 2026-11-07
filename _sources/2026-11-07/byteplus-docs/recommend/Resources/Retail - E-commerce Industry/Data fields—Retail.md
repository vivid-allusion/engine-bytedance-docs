---
title: "Data fields—Retail"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/resources-retail_data_fields"
---

This section details the different types of data fields present in BytePlus Recommend.

<span id="2116a8bc"></span>
# User data

This section details the types of User data fields seen in BytePlus Recommend.

<span id="4dfc6234"></span>
## user_id

This is the unique identifier of a user. This ID should be consistent throughout the whole process. This ensures that the recommendation system can collect all the relevant UserEvent occurrences and provide better recommendation results.

<span id="78155f26"></span>
### Generating user_ids

There are two methods of generating a user_id:


* Use the account_id.

* Use the device_id or mobile phone IMEI.


<span id="6df38c8e"></span>
# Product data

This section details the types of Product data fields seen in BytePlus Recommend.

<span id="9fb65319"></span>
## product_id

This is the unique identifier of a product. It is recommended to use numeric values below 32 bits. However, our team also supports string\-type product_ids.

**SPECIAL CASES**

If a product has different SKUs, clients should discuss with the BytePlus team how to better label and upload the product_ids. If clients want the recommendation results at SKU level, the product_id is the same as the sku_id. Otherwise, if clients want the recommendation results at an SPU level, the product_id is the same as the spu_id. It is also highly recommended to synchronize the SKU and SPU ID mapping relationship in the product data using extra data fields.

For example, say there is a phone offered in five colors up for sale on the platform with a spu_id of 123456 and the white model has a sku_id of 12345604. The following scenarios should be of attention:


* If the recommendation scenes on your platform display SPU, clients should enter 123456 as the product_id to the BytePlus team and enter `white:12345604` in the extra data field. The format for this data field should be aligned with the BytePlus team. The BytePlus model will then return 123456 for a user if the model predicts that said user may like this product.

* If the recommendation scenes on your platform display SKU, clients should enter 12345604 as the product_id and `spu_123456` in the extra data field. The format for this data field should be aligned with the BytePlus team. The BytePlus model will return 12345604 if the model predicts that the user will like this product.


<span id="23349c65"></span>
## publish_timestamps

This refers to the exact Unix timestamp in seconds when a product is published, for example 1520327038. This data field is used to track the duration of when the product is live. It is especially important for time\-sensitive products and scenarios like flash\-sale products or live\-streaming shopping.

<span id="020409e4"></span>
### Generating publish_timestamps

If a product publication occurs at 12:30:08 on February 13, 2022, the corresponding timestamp is 1644726608.

<span id="daf05b1b"></span>
## is_recommendable

This indicates whether a product can be recommended to users. There are a few types of products that should not be recommended:


* Banned or blocked products

* Products from sensitive categories

* Sold out or invalid products


<span id="1a489a35"></span>
### Generating is_recommendables

If product A is published on February 9 and sold out on February 11, the product data synchronized to BytePlus on the 9th should be marked with is_recommendable = true. The data from the 11th should be marked is_recommendable = false.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Even if the product is not suggested as recommended, clients should still send this data to the BytePlus team. This is important, as the team can add more information to the recommendation model.</div>


<span id="90d24394"></span>
# UserEvent data

This section details the types of UserEvent data fields seen in BytePlus Recommend.

<span id="745948df"></span>
## root_product_id

When a UserEvent is recorded on the product detail page, there are two types of products present:


* Main product (root_product_id): Parent product.

* Recommended product: Child product.


**EXAMPLE**

A customer looks at a black dress and lands on its product detail page. The black dress is the parent product, and its product_id is the root_product_id. In the "You may also like" section, the BytePlus Recommend team creates algorithms leading to good recommendation results. Thus, it is essential to provide the root_product_id to the team.

<div style="text-align: center">
<img src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/421562d-Picture_1.png" width="299px" /></div>


<span id="dbb7d6ac"></span>
## scene_name

The scene_name refers to the specific location of a platform, for example, the home page or the category page, where the UserEvent occurs. The scene_name is essential when generating recommendation results because it is key to understanding user preferences. Thus, when obtained, the team can gather UserEvent data specific to the scene, and it helps produce more precise recommendation results.

**EXAMPLE**

The UserEvent data on the "You may also like" scene on the home page differs from the UserEvent data for the "You may also like" scene on the product detail page. For the home page, more diverse and personalized products might be recommended. However, recommended products are generally similar to the parent product for the same scene on the product detail page.

<span id="d6fa1932"></span>
### Generating scene_names

The scene_name should contain the following sections, separated by `$##$`:


* A: Business

* B: Page

* C: Page section

   Scene_name = A$##$B$##$C.


For example, the scene_name of the similar products section on the product detail page (PDP) is business1$##$PDP$##$similarProduct.

If a section is empty, leave it blank in the scene_name, as shown here: business1$##$$##$similarProducts.

Clients can give different names to different scenes for easier identification. For example, the similar products section on the product detail page can be renamed as SimilarProducts.

<span id="98b6ab3c"></span>
## traffic_source

A traffic_source refers to the source from which the customer traffic flows once an A/B test starts. There are usually two sources: one uses an in\-house algorithm, and the other uses the BytePlus algorithm. However, clients can employ third\-party algorithms for more comparisons.

When a UserEvent, like a click, occurs, the traffic_source data field is used to determine the source of the traffic in\-flow and the performance. In most scenarios, the impression and click data must include the traffic_source as a data field.

<span id="e37cfb26"></span>
### Generating traffic_source tags

Recommended results that produce any impression or clicks from the in\-house algorithm should be labeled In\-house. Those produced from the BytePlus algorithm should be labeled BytePlus. Any other recommended results should be labeled Others.

**EXAMPLE**

After integrating the BytePlus recommendation model into your app or website, you can split your user traffic into Group A and Group B. Group A uses the in\-house algorithm, while Group B uses the BytePlus algorithm. If user A in Group A impresses or clicks on a product, the UserEvent data should be marked In\-house in the traffic_source field.

<span id="255e58a1"></span>
## event_type

This is used to indicate which type of user behavior is performed. There are only seven types of event_types accepted in BytePlus Recommend:


* **impression**: Refers to the moment the user sees a product. This is the starting point of the user's journey, where a subsequent click or purchase may happen. If the impression data is missing, the recommendation system cannot differentiate between products with an impression compared to those without one. This data is key to providing good recommendation results.

* **click**: When a user clicks on the product and navigates to the product detail page.

* **purchase**: When a user purchases the product.

* **add\-to\-cart** and **remove\-from\-cart**: When the user adds or removes the product from the cart.

* **add\-to\-favorite** and **remove\-from\-favorite**: When the user adds or removes the product from their favorites.

* **search**: When the user searches for a query. After the search results are generated, clients should track the number of impression occurrences with scene_name = search result page.

* **stay\-detail\-page**: The duration of time a user stays on the product detail page. A longer period indicates a stronger preference the user might have towards the product.


<span id="24bff28d"></span>
## event_timestamp

This refers to the exact Unix timestamp in seconds when a UserEvent happens, for example, 1520327038. Do not manually adjust this timestamp to other timezones like UTC\-4; it should always remain in UTC.

<span id="0f60086d"></span>
## Generating event_timestamps

If a UserEvent occurs at 12:30:08 on February 13, 2022, the corresponding timestamp is 1644726608.
