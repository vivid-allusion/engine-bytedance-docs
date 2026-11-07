---
title: "Create User Event Dataset"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Create_User_Behavior_Dataset"
---

<span id="4412307f"></span>
# Introduction to User Behavior Data

To improve long\-term recommendation performance and provide users with personalized capabilities for new generative recommendations, we offer a feature for uploading user behavior data. By leveraging rich, fine\-grained behavior data — combined with user intent, behavior sequences, and contextual conversation history — to deliver superior end\-to\-end recommendation results, we recommend utilizing this feature. This will enhance long\-term recommendations in specific scenarios, such as:


* **E\-commerce Platforms:**  By combining short\-term behaviors (e.g., adding to favorites, adding to cart, placing orders) with long\-term habits (e.g., preferred categories, price ranges), the system can infer a user's true interests to achieve personalized recommendations and boost sales conversion.

* **Information / Content Platforms:**  Where user behavior tends to be unstructured and topics are diverse, the system can analyze interactions (e.g., browsing, liking, commenting, sharing, dwell time). The generative recommendation system extracts behavior trajectories across different timeframes and content domains, providing the LLM with a more semantic behavioral context for more refined and personalized content delivery.


&nbsp;

When using recommendation features, uploading both **item data** and **behavior data** is essential. Both data types can be configured for use across multiple applications simultaneously. While a single application supports multiple item datasets, **it can only be configured with one behavior dataset.** 

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">Before configuring a behavior dataset within an application for a specific app, you must first complete the configuration of the <strong>item dataset</strong> in that app.</div>


The following sections detail the data preparation requirements and upload methods for user behavior data.

<span id="5265cc35"></span>
## Data Preparation

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">The field names provided here are <strong>for illustrative purposes only</strong>. When uploading the 5 mandatory fields, you may use your own data schema and the pre\-defined field names from your existing records.</div>


When defining a behavior table, there are **five mandatory categories** of fields. Their meanings are as follows:


|<div style="text-align: center"><br><strong>Field meaning</strong></div><br> |<div style="text-align: center"><br><strong>Sample field name</strong></div><br> |<div style="text-align: center"><br><strong>Required</strong></div><br> |<div style="text-align: center"><br><strong>Supported data types</strong></div><br> |<div style="text-align: center"><br><strong>Description</strong></div><br> |
|---|---|---|---|---|
|<div style="text-align: center"><br>Item ID</div><br> |<div style="text-align: center"><br> item_id</div><br> |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>string, int32, int64</div><br> |<div style="text-align: center"><br>Unique identifier of the item which user interacted with</div><br> |
|<div style="text-align: center"><br>User ID</div><br> |<div style="text-align: center"><br>user_id</div><br> |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>string, int32, int64</div><br> |<div style="text-align: center"><br>Unique identifier of the user</div><br> |
|<div style="text-align: center"><br>Behavior type</div><br> |<div style="text-align: center"><br>event_type</div><br> |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>int32, int64, string</div><br> |<div style="text-align: center"><br>Action labels used to record user behavior</div><br><br><br><div style="text-align: center"><br>(such as: view, click, like, collect, add_to_cart, purchase, etc.)</div><br> |
|<div style="text-align: center"><br>Time when the action occurred</div><br> |<div style="text-align: center"><br>event_timestamp</div><br> |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>int64</div><br> |<div style="text-align: center"><br>Action time in timestamp format (milliseconds)</div><br> |
|<div style="text-align: center"><br>Scenario where the action occurred</div><br> |<div style="text-align: center"><br>scene</div><br> |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>string, int32, int64</div><br> |<div style="text-align: center"><br>Description of where the user action occurs or the functional scenario</div><br><br><br><div style="text-align: center"><br>(e.g., homepage, search, detail, feed)</div><br> |


In addition to the mandatory fields above, you can configure **custom fields** based on your business needs to enrich the contextual information of individual behaviors. The system will automatically parse and utilize these custom fields to help you build a more comprehensive and refined user behavior analysis model. For example, you can use a `duration` field to record a user's dwell time on a specific page, a `query` field to capture search keywords, or `device_type` and `platform` fields to distinguish behavior characteristics across different devices and operating systems.


|<div style="text-align: center"><br><strong>Sample field meaning</strong></div><br> |<div style="text-align: center"><br><strong>Description</strong></div><br> |
|---|---|
|<div style="text-align: center"><br>Duration of stay</div><br> |Length of stay, applicable to browsing behavior |
|<div style="text-align: center"><br>Search term</div><br> |If the behavior occurs in a search context, record the search keywords |
|<div style="text-align: center"><br>User device</div><br> |Type of user device (e.g., mobile, pc, tablet) |
|<div style="text-align: center"><br>User system</div><br> |Operating system or platform, such as iOS, Android, Web |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="warning">Please ensure that the data type for the same field remains consistent globally. Avoid changing data formats or types when reporting the same field at different times, as this may lead to data parsing failures or errors.</div>


In the left navigation bar of the console, select **`Datasets`** ** ** and choose the **`User event dataset`** tab, then click **`Create dataset`** button.

<span id="4c3844d8"></span>
## Data Upload

<span id="c64d9661"></span>
### Step 1: Upload Sample Data

You can upload user behavior data by uploading a **JSONL file** (maximum file size 10 MB) or by directly **pasting JSON formatted data**. You do not need to upload all your data at once during the initial setup; you only need to ensure that the data uploaded during dataset creation meets the following requirements:


* All **5 mandatory fields ** are included.

* The **schema structure** of the uploaded data is complete.

* The **enumerated values** for data types are fully represented.


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/abddcd12f20741b1bb630b874a3a3324) </span>

&nbsp;

Below is an example of the JSON format:

```JSON
[{
    "user_id": "user134",
    "item_id": "1235",
    "event_id": "41231",
    "event_type": "Exposure",
    "event_timestamp": 1678886400000,
    "event_scene": "home",
    "device_os": "Android"
},
{
    "user_id": "user134",
    "item_id": "1235",
    "event_id": "41234",
    "event_type": "Add to Cart",
    "event_timestamp": 1678886520000,
    "event_scene": "product_detail_page",
    "device_os": "IOS"
},
{
    "user_id": "user134",
    "item_id": "1235",
    "event_id": "41236",
    "event_type": "Purchase",
    "event_timestamp": 1678886580000,
    "event_scene": "shopping_cart",
    "device_os": "Android"
}]
```


&nbsp;

When uploading a JSONL file, you can either select it from your local folders or drag and drop the file directly into the area for automatic parsing (file size must be within **10 MB**). 

&nbsp;

Alternatively, you can choose to upload by **pasting JSON code**.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/892c2517e0d34369b719689f5e5dc1eb) </span>

&nbsp;

Once completed, click **`Next: Configure fields`** ** ** in the bottom right. After the model performs the initial field identification, you will proceed to the Field Configuration stage.

&nbsp;

<span id="a91a8c62"></span>
### Step 2: Field Configuration


1. After the preliminary identification, the model will automatically generate field attributes and descriptions for this dataset. You can modify it if anything is not accurate.


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/92c78a15905745e68a6ecd8766f89a5e) </span>

&nbsp;


&nbsp;

2. Click **`Add field`** to enter the name, type, attributes and description for a new field. You can manually enter the name and description, while the type and attributes can be selected from the dropdown menu.


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/9eebed74c9aa4f39b0bfb398a73fd87e) </span>

&nbsp;

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="warning">Different field attributes have different requirements for field types. During configuration, please first choose the field type that matches your data, then select the field attributes you wish to configure. You cannot select attributes until a type is defined. Hover over the field type to see tooltip showing its corresponding data type.</div>



&nbsp;

3. After selecting the field types, you select the field attributes:


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/3858aa76748d4348a8c52f2cce035766) </span>

&nbsp;

The following table lists the data type requirements and meanings for mandatory fields in a behavior dataset:


|<div style="text-align: center"><br><strong>Field name</strong></div><br> |<div style="text-align: center"><br><strong>Required</strong></div><br> |<div style="text-align: center"><br><strong>Supported data types</strong></div><br> |<div style="text-align: center"><br><strong>Behavior description</strong></div><br> |
|---|---|---|---|
|<div style="text-align: center"><br>Item ID</div><br> |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>string, int32, int64</div><br> |<div style="text-align: center"><br>Unique identifier of the item interacted with by the user</div><br> |
|<div style="text-align: center"><br>User ID</div><br> |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>string, int32, int64</div><br> |<div style="text-align: center"><br>Unique identifier of the user or users</div><br> |
|<div style="text-align: center"><br>Action type</div><br> |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>int32, int64, string</div><br> |<div style="text-align: center"><br>Action name recording user behavior</div><br><br><br><div style="text-align: center"><br>(e.g., view, click, like, collect, add_to_cart, purchase, etc.)</div><br> |
|<div style="text-align: center"><br>Time when the action occurred</div><br> |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>int64</div><br> |<div style="text-align: center"><br>Action time, timestamp format (milliseconds)</div><br> |
|<div style="text-align: center"><br>Behavior scenario</div><br> |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>string, int32, int64</div><br> |<div style="text-align: center"><br>Description of where the user action occurs or the functional scenario</div><br><br><br><div style="text-align: center"><br>(e.g., homepage, search, detail, feed, etc.)</div><br> |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">If the previously uploaded data does not match the schema configuration, it will be discarded. If mandatory fields are missing, clicking "Complete" will trigger the missing field to be highlighted in red, requiring you to configure them.</div>


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/bf6b27d0c5b8421ebf63c2d9306f7798) </span>

&nbsp;

<span id="8b823c8e"></span>
### Step 3: Behavior Type Enumeration Configuration

Since profile extraction, modeling, and recommendation results rely heavily on the understanding of behavior types, you must configure the enumerations for the `event_type` field.


1. Click the **Next Step: Confirm Required Fields.** 

2. The system will automatically retrieve behavior type enumerations based on your uploaded data. You can also manually customize or modify these enumerations and their meanings. 

   **Every enumeration value must have a defined meaning**; otherwise, subsequent extraction and recommendation processes cannot proceed.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>



1. <div data-tips="true" data-tips-type="default">Meanings can be repeated, but enumeration values must be unique.</div>


2. <div data-tips="true" data-tips-type="default">The "Exposure" type must be configured.</div>



<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/33a222a36b6341eb82a9add1032b20d7) </span>

<span id="05419ca4"></span>
### Step 4: Create Dataset


1. Click the `Complete` button to complete the dataset creation.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="warning">After creation, you are only allowed to add new behavior types or modify field meanings. </div>


<div data-tips="true" data-tips-type="warning">You <strong>cannot modify</strong> existing behavior type enumeration values or saved field attribute configurations.</div>


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/cf7bd298164c40e78e21203116e2a134) </span>

&nbsp;

<span id="4ee47e96"></span>
### Step 5: Link Application

For more details, please see [Prerequisites and setup](https://docs.byteplus.com/docs/393/92202)

&nbsp;

<span id="07f51d46"></span>
## View Dataset

After creating the behavior dataset, you can find it in the dataset list. Enter the dataset details page to view its basic information, field configuration, and operation history.

Once the behavior dataset is created, you can find it in the **Datasets ** list. Enter the dataset details page to view its basic information, field configurations, and operation history.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/6126b13b25db4b6cabea132204258225) </span>


&nbsp;

1. After successfully creating the behavior dataset, return to the **Datasets** page to see the newly created dataset.

2. In the **Datasets ** list, locate the dataset you wish to view and click the **`View`** button in the "Action" column.


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/ebdb12a614174440b6f574611b3433ed) </span>


&nbsp;

3. **Dataset Details Page:**  Upon entering, you will see the following key tabs:

   * **Configuration**:

      * In this tab, you can view and adjust various configuration parameters of the current dataset.

      * **Please note**: modifications made to the configuration on this page will **not** be automatically applied to datasets already linked and configured in your applications.

   * **Data import**:

      * If you wish to add more data entries to this dataset, you can do so under this tab.

      * For detailed data import procedures and format requirements, please see  [Import and Update Item Data in Real Time](https://docs.byteplus.com/docs/393/92214).

   * **Activity history**:

      * This tab records all key operations performed on this dataset, such as configuration changes and data import tasks, allowing you to track its modification history.

      * You can also access the history directly from the **Datasets ** list page by clicking the `Activity history` button in the "Action" column for the corresponding dataset.


<span id="0b78a7e6"></span>
## Change Behavior Data Configuration

<span id="8eed41bd"></span>
### Add behavioral data field


1. On the **Datasets ** list page, locate the target behavior dataset and click the **`View`** ** **  button in the "Action" column. Go to **Configuration ** tab ** ** then click **`Edit schema`** ** ** button **.** 


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/8bca9538920a4b6cabe6a218fed3b620) </span>


&nbsp;

2. Click `Add field`, then enter the field name, data type, attributes and field description.


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/3dc304c7bf5741138c598a75d94d126a) </span>


&nbsp;

3. After the update, click **`Complete`** to save the changes. Applications associated with this behavior dataset will have the updates synchronized automatically.


&nbsp;

<span id="2ba01fa5"></span>
### Add a new behavior type enumeration


1. On the **Datasets ** list page, locate the target behavior dataset and click the **`View`** ** **  button in the "Action" column. Go to **Configuration ** tab ** ** then click **`Manage Event Types`** ** ** button **.** 


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/05fcfe7bf33a4b46ba3ef868814a5dfe) </span>


&nbsp;

2. Click the "Add Event Type", then enter the enumeration value and its meaning.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/92f3815383e74dfda2b808d36406c6e1" width="296px" /></div>



&nbsp;

3. After the update, click **OK** to save the changes. Applications associated with this behavior dataset will have the updates synchronized automatically.
