---
title: "Create and Link Item Dataset"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Create_an_Application_and_Link_Item_Datasets"
---

*Want to explore more Viking AI Search capabilities? Visit: * [Viking AI Search engine, integrated enterprise search and recommendation intelligent engine](https://www.volcengine.com/product/AI-Search-Rec)


---



You can create an item dataset directly within an application and have it automatically associated with that application.

<span id="6ea35dc5"></span>
# **Navigation**

Go to **Application Management** \> **Data Configuration** to access the item dataset management interface. Depending on the application's current state, click the corresponding **Create Dataset** button.


<columns>
<columnsItem zoneid="RyRZOBOHcm">

<div style="text-align: center">
<strong>No dataset linked</strong></div>


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/ff42ccc73100414da99c00167d247141) </span>



</columnsItem>
<columnsItem zoneid="UTfvyOxg3H">

<div style="text-align: center">
<strong>Dataset linked</strong></div>


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/d5a06af332bf46ff8d344b3c2cc5db11) </span>

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/e27ed7c28cac4f82b03858a5b28d202a) </span>



</columnsItem>
</columns>


&nbsp;

<span id="4f5c4f2b"></span>
# Configuration steps

<span id="8d62a1ce"></span>
## Step 1: Upload data sample

For instructions on uploading sample data, adding fields, and removing fields, refer to [Create Item Dataset - Image & Text Data](https://docs.byteplus.com/docs/viking-aisearch/Create_item_dataset_image_text), [Create Item Dataset - Video Data](https://docs.byteplus.com/docs/viking-aisearch/92224).


<columns>
<columnsItem zoneid="L3Y8ILM7YE">

&nbsp;

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/7f580f330b8f4c56b4530d04afe26de8) </span>



</columnsItem>
<columnsItem zoneid="w9rIS1Diad">

&nbsp;

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/eb5da3858f3f4f889cf05087cd26bf12) </span>



</columnsItem>
</columns>


&nbsp;

<span id="1d70d464"></span>
## Step 2: Configure data fields

Based on the uploaded sample data, the system automatically detects and pre\-fills field names, field descriptions, field attributes, and field search strategies (such as whether a field is searchable, filterable, usable for search completion, or usable for image\-to\-image search). To adjust these settings according to your specific requirements, refer to [Fields Data Configuration](https://docs.byteplus.com/docs/viking-aisearch/92268#0f5287ce)to review and fine\-tune the configuration, ensuring that search behavior aligns with your business objectives.

<div style="text-align: center">
</div>


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/2d63916bdd4e4f7482e064755e6f9621) </span>

<span id="46a409fe"></span>
## Step 3: Configure display style

Configure the display style for items. This configuration is used for preview purposes within the platform only and will not be applied to API responses.

<div style="text-align: center">
</div>


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/cbfafac4d06c4c20a5467d7982ed6adf) </span>

<span id="7814a2f7"></span>
## Step 4: Configure the Application Item Scope

Define the scope of items available for search and recommendation (the item pool). You can set filter conditions to restrict which items are included — for example, filtering by item category, price range, or publish date. For more information, see [Initial Configuration of Item Pool](https://docs.byteplus.com/docs/viking-aisearch/98548).


&nbsp;


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/d4288dd985774fd29dcbdcb15c434cfa) </span>

<span id="ac976104"></span>
## Step 5: Complete configuration

Once the item dataset is created, it will be automatically associated with the current application.


---



<span id="7fcd887e"></span>
# Unlink Item Dataset

Before switching to a different data source for an application, or before deleting an item dataset that is currently in use, you must first remove the link between the dataset and the application.


1. In **Application Management** \> **Data Configuration**, go to the **Item Datasets** tab.

2. Locate the item dataset you want to unlink, and click the ** Unlink** button below the dataset description.



---



<span id="1a9600b5"></span>
# Import item data

After creating a dataset, you can use the following methods to import additional data or update field values:


* **Import JSONL files through the console: ** Use this when you need to import and update small batches of test data. See [Import using JSONL Files](https://docs.byteplus.com/docs/viking-aisearch/Import_JSONL_Files_using_Console)

* **Batch import/update item data via API:**  Use this when you need to build full\-scale production data initially, or perform batch field value updates. See [Batch Import Item Data](https://docs.byteplus.com/docs/viking-aisearch/Batch_Import_Item_Data)

* **Real\-time import/update item data via API:**  Use this when you need to synchronize the latest data for new or changed items in the production environment's customer products/content library to the AI Search engine's Recommendation or Search candidates. See [Import and Update Item Data in Real Time](https://docs.byteplus.com/docs/viking-aisearch/Import_and_Update_Item_Data_in_Real_Time)


&nbsp;

&nbsp;

*To experience more Viking AI Search capabilities, Click to visit: * [Viking AI Search engine, integrated enterprise search and recommendation intelligent engine](https://www.volcengine.com/product/AI-Search-Rec)
