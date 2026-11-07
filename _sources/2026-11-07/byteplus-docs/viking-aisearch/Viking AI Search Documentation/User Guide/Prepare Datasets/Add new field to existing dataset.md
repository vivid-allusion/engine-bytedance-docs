---
title: "Add new field to existing dataset"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Add_new_field_to_existing_dataset"
---

*Viking AI Search is a Large\-Language\-Model\-AI\-based enterprise search product. It uses multimodal semantic understanding from large language models, combined with ByteDance's experience in information retrieval, to provide a ready\-to\-use platform for building and integrating end\-to\-end multimodal search and recommendation capabilities.* 


---



If you've already created and configured a dataset, but your business now needs a new field — for example, a new attribute your team wants to search or filter on, or a behavior type you haven't tracked before — you don't need to recreate the dataset. This article covers three related tasks:


* Adding a field to an existing **item dataset**.

* Adding a field to an existing **user event (behavior) dataset**.

* Defining a **new event ** **type** so the platform knows what a raw behavior value (like `"fav"` or `"buy_now"`) means.



---



<span id="7b31bcd9"></span>
# Add a field to an item dataset

<span id="70a981be"></span>
## Step 1: Open the dataset


1. In the left navigation bar, select Datasets.


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/0a14887223974728922bcf2493e6dd79) </span>

&nbsp;


&nbsp;

2. Select the **Item dataset** tab. 

3. Find the dataset you want to update and select View.


&nbsp;

<span id="41f3e143"></span>
## Step 2: Add the field


1. On the dataset details page, in the Data configuration tab, select ** Edit schema.** 


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/aa8c486720ed45c58183ff8510093529) </span>


2. At the bottom of the field list, select  **+ Add field**

3. In the new row, enter a **Field** ** name** (for example, `device_os`).


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/cbe9e2d6250c488c9addee34da4bf2f6) </span>


4. Select a **Data** ** type** from the dropdown — for example `string`, `int`, `float`, `bool`, `array<string>`, or `array<int32>`

5. Select a **Field** ** attribute** if this field plays a specific role the platform should know about — for example **Item ID, Title, Body content, Image URL,**  or **Category**. Leave this blank if the field doesn't need a special role.

6. Select **Complete** to save the schema change. The new field is added to the dataset and synced to every app this dataset is linked to.


<span id="62376751"></span>
## Step 3: Turn on search, filtering, or autocomplete for new field 

Adding a field to the dataset does not automatically make it searchable, filterable, or usable for autocomplete. Those settings are configured separately, per app, because the same dataset can be used differently by different apps.


1. Open the app the dataset is linked to.

2. In the left navigation bar, select **Data configuration**.

3. Click **Edit schema** and find the field you just added.


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/d7199c97ab5a4da79b633eba0e6bd578) </span>


4. Turn on the relevant option for your use case


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/da7e251d3b2744fdb4cbe35d055bb97c) </span>


|<div style="text-align: top"><br><strong>Option</strong></div><br> |<div style="text-align: top"><br><strong>What it does</strong></div><br> |
|---|---|
|<div style="text-align: top"><br>Used for search</div><br> |<div style="text-align: top"><br>Makes a text field's content matchable in keyword and semantic search.</div><br> |
|<div style="text-align: top"><br>Used for image search</div><br> |<div style="text-align: top"><br>Makes an image\-link field usable for image\-based search.</div><br> |
|<div style="text-align: top"><br>Filterable/Faceting</div><br> |<div style="text-align: top"><br>The field can be used to filter or facet search and recommendation results.</div><br> |
|<div style="text-align: top"><br>Autocomplete</div><br> |<div style="text-align: top"><br>Uses the field's values as suggestions in the search box.</div><br> |


&nbsp;

<span id="37705640"></span>
# Add a field to a user event (behavior) dataset

The steps are the same pattern as an item dataset, but with a different set of field attributes.

<span id="a3481d20"></span>
## Step 1: Open the dataset


1. In the left navigation bar, select **Datasets**.

2. Select the **User event dataset** tab, then select **View** on the dataset you want to update. 


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/05bbb25143654f3b81d163bf970a2497) </span>

&nbsp;

<span id="d5971c77"></span>
## Step 2: Add the field


3. Select **Edit schema**, then select  **+ Add field**.


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/ec068f720bd6463f9d2395ffb7eda036) </span>


4. Enter a **Field** ** name** (for example, `user_id` or `event_scene`) and choose a **Data** ** type**. Use `string` for most ID\-style fields and `int64` for millisecond timestamps.

5. If the field represents a core concept the platform needs to recognize, select the matching **Field attribute** — for example **User ID** for a user identifier, so the platform knows this field has a specific role. Otherwise leave it blank.

6. Select **Complete** to save.


&nbsp;

<span id="1b113131"></span>
# Add new event (behavior) type

If your behavior data includes multiple kinds of user interactions (impressions, clicks, purchases, and so on), you must map each raw value to a meaning the platform understands before it can be used in recommendations.


1. On the user event dataset's overview page, select **Manage event types**.


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/8701351b119541c9b7d391782b5ad069) </span>


&nbsp;

2. In the panel that opens, review the raw event values the platform detected from your imported data (for example, `Product View (Impression)`,`Product Click`, `Complete Purchase`).


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/225d49b43b2644cfbcc381cc48b0bc00" width="580px" /></div>



&nbsp;

3. For each raw value, select a meaning from the dropdown: 



|<div style="text-align: top"><br><strong>Meaning</strong></div><br> |<div style="text-align: top"><br><strong>Typical use</strong></div><br> |
|---|---|
|<div style="text-align: top"><br>Exposure</div><br> |<div style="text-align: top"><br>The item was shown to the user (a view or impression).</div><br> |
|<div style="text-align: top"><br>Click</div><br> |<div style="text-align: top"><br>The user clicked or tapped the item.</div><br> |
|<div style="text-align: top"><br>Favourite</div><br> |<div style="text-align: top"><br>The user favorited or bookmarked the item.</div><br> |
|<div style="text-align: top"><br>Share</div><br> |<div style="text-align: top"><br>The user shared the item.</div><br> |
|<div style="text-align: top"><br>Like</div><br> |<div style="text-align: top"><br>The user liked the item.</div><br> |
|<div style="text-align: top"><br>Add to cart</div><br> |<div style="text-align: top"><br>The user added the item to a cart.</div><br> |
|<div style="text-align: top"><br>Place order</div><br> |<div style="text-align: top"><br>The user started checkout.</div><br> |
|<div style="text-align: top"><br>Purchase</div><br> |<div style="text-align: top"><br>The user completed a purchase.</div><br> |
|<div style="text-align: top"><br>Custom user event</div><br> |<div style="text-align: top"><br>Any behavior that doesn't fit the categories above.</div><br> |



4. If a raw value from your data isn't listed yet, select  **+ Add event type**, enter the raw value, and choose its meaning (or **Custom user event** if none of the presets fit).

5. Make sure you have defined all events. Don't leave any event type as "Undefined."

6. Select **OK** to save.



---



<span id="e879733c"></span>
# FAQ


* **Do I need to re\-import my data after adding a field?**  

   * Existing rows likely won't retroactively populate the new field for historical data. Re\-import or backfill data if the new field is required. 

* **Can I change a field's attribute after creating it?**  

   * Field attribute, field name, field type, event type cannot be changed after saving. Ensure accuracy before saving configuration.
