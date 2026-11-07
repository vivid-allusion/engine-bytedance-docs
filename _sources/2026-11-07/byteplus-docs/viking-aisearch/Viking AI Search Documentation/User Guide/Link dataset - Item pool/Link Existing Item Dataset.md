---
title: "Link Existing Item Dataset"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Link_Existing_Item_Dataset"
---

*To experience more Viking AI Search capabilities, click to go to: * [Viking AI Search engine, integrated enterprise search and recommendation intelligent engine](https://www.volcengine.com/product/AI-Search-Rec)


---



You can associate an existing item dataset with a new application.

<span id="06acac7d"></span>
# **Navigation**

Go to **Application Management** \> **Data Configuration** to access the item dataset management interface. Depending on the application's current state, click the corresponding **Link Dataset** button.


<columns>
<columnsItem zoneid="SIPXDEYS6M">

&nbsp;

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/2d11d4e543c9443fa20135b04912d607) </span>



</columnsItem>
<columnsItem zoneid="gXzM4r1nst">

&nbsp;

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/9860e3f198ff4a5f9c06883b1b7a9c36) </span>



</columnsItem>
</columns>


<span id="7402ce23"></span>
# Configuration Steps

<span id="c94f9996"></span>
## Step 1: Configure data fields

Based on the uploaded data, the system has automatically detected and pre\-filled field names, field descriptions, field attributes, and field search strategies (such as whether a field is searchable, filterable, usable for search completion, or usable for image\-to\-image search). To adjust these settings according to your specific requirements, refer to [Fields Data Configuration](https://docs.byteplus.com/docs/viking-aisearch/92268#0f5287ce)to review and fine\-tune the configuration, ensuring that search behavior aligns with your business objectives.

&nbsp;

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/58e42fdd292c4043acbee12809d6f04d) </span>

&nbsp;

<span id="43de5f63"></span>
## Step 2: Configure display settings

Configure the display style for items. This configuration is used for preview purposes within the platform only and will not be applied to API responses.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/55b41f72d0c940ceaa3c9442a0605e7f) </span>

&nbsp;

&nbsp;

<span id="e51341f8"></span>
## Step 3: Configure the Application Item Pool

Define the scope of items available for search and recommendation (the item pool). You can set filter conditions to restrict which items are included — for example, filtering by item category, price range, or publish date. For more information, see[initial configuration of application item scope (pre-filter)](https://docs.byteplus.com/docs/viking-aisearch/98548).


&nbsp;


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/1e82112d7182423eb72e2b0d70ba07c3) </span>

<span id="899d176a"></span>
## Step 4: Complete

Once the item dataset is associated, it will be automatically linked to the current application.


---



<span id="7c70419c"></span>
# Unlink item dataset

Before switching to a different data source for an application, or before deleting an item dataset that is currently in use, you must first remove the association between the dataset and the application.


1. In **Application Management** \> **Data Configuration**, go to the **Item Datasets** tab.

2. Locate the item dataset you want to unlink, and click the **Unlink** button below the dataset description.



---



<span id="1a9600b5"></span>
# **Import Item Data**

After the dataset is ready, you can use the following methods to import additional data or update field values:


* **Import jsonl files in the console: ** Suitable for importing and updating small batches of test data, see [Import using JSONL Files](https://docs.byteplus.com/docs/viking-aisearch/Import_JSONL_Files_using_Console)

* **Bulk import/update via API: ** Suitable for the initial full production data build or batch field value updates, see [Batch Import Item Data](https://docs.byteplus.com/docs/viking-aisearch/Batch_Import_Item_Data)

* **Real\-time import/update via API:**  Suitable for real\-time additions or changes to customer product/content libraries in production, syncing the latest data to Viking AI Search recommendations or search candidates, see [Import and Update Item Data in Real Time](https://docs.byteplus.com/docs/viking-aisearch/92214)


&nbsp;

*To experience more Viking AI Search capabilities, click to visit: * [Viking AI Search engine, integrated enterprise search and recommendation intelligent engine](https://www.volcengine.com/product/AI-Search-Rec)
