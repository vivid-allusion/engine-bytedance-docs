---
title: "Create Item Dataset - Image & Text Data"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Create_item_dataset_image_text"
---

To power your platform's search and recommendation features with your own data, you need a structured item dataset. This guide provides step\-by\-step instructions for creating an item dataset specifically for image and text data. You will learn the complete workflow, from uploading sample data and configuring fields to finalizing the dataset for use in your applications.

The method for preparing and creating a dataset depends on the type of data you intend to import. This document focuses on the creation workflow for **Image & Text data**, including data format requirements, field mapping rules, and solutions to common issues. If you wish to create a video dataset, please refer to ** ** [Create Item Dataset - Video Data](https://docs.byteplus.com/docs/393/Create_Item_Dataset_-_Video_Data).

&nbsp;

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">This is a step\-by\-step guide for dataset creation and will require fundamental understanding of the different datasets found in Viking AI Search. </div>


<div data-tips="true" data-tips-type="default">To learn more about the different datasets and its features  — such as basic concepts of item datasets, supported data formats, specific definitions of field types, detailed parameter explanations, or search strategies — refer to the <a href="https://docs.byteplus.com/docs/393/92268">Dataset Introduction</a> instead. </div>


&nbsp;

<span id="2772dc1a"></span>
# Create an Image & Text Dataset

<span id="e8e1742b"></span>
## Step 1: Start dataset configuration

This initial step guides you to the dataset creation page and starts the workflow.


1. In the Viking AI Search console, navigate to the **Datasets** page.

2. Click **Create Dataset**. In the pop\-up window, select **Item Dataset** and click **Create Now** to begin the dataset creation process.


<span id="0b135a7e"></span>
## Step 2: Upload Sample Data

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/bd8f05d2531a4411892d4da9c686ff6b) </span>

&nbsp;

In this step, we will guide you through naming your new Image/Text dataset and uploading a sample file to parse data fields and generate configurations.


1. Enter the **Dataset Name** on the creation page.

2. Select **Image and Text Data** as the Dataset Type.

3. **Upload Data:**  Upload a sample of your data here. This helps the system automatically identify data fields and generate initial configurations. Note that this is only for configuration preview; you can decide later whether to formally add this data to the dataset.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">\*Note   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><strong>Must Include a Unique Identifier:</strong> Each record must contain a unique ID field of type <code>String</code> to serve as the basis for retrieval.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><strong>Consistent Schema Across Records:</strong> Conflicting formats for fields with the same name will result in an error.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><strong>Support for Multi\-level Data Structures:</strong> The system can process nested objects up to 3 levels deep, enabling effective indexing and retrieval of nested attributes.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><strong>Image Data Upload:</strong> You can upload multiple image fields. The field type should be <code>String</code> or <code>Array</code>, and the content should be an image URL (or a list of URLs). Please ensure the URLs are publicly accessible and are not direct download triggers.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><strong>Image Resource Handling:</strong> We support passing images via URL references. Images must be uploaded within specific JSON attributes. We recommend keeping image file sizes under <strong>5MB</strong>.   </div>
   



&nbsp;

The system supports two upload methods. You can click the toggle button below the upload control to choose your preferred method:

   
   <Tabs>
   <Tab zoneid="ze37Wob0BJ" title="Upload JSONL document">
   <TabTitle>Upload JSONL document</TabTitle>
   
   **Upload JSONL file**
   
   Click or drag to upload a **JSONL file**. The file must follow standard JSONL specifications, with each record written on a new line. The file size should not exceed **10 MB**.
   
   The example below demonstrates the required standard JSONL format:
   
   ```JSON
   {"item_id": "product_001", "name": "New Fashion Dress", "price": 299.00, "current_price": 249.00, "description": "Elegant and slim-fit, suitable for all occasions.", "images": ["https://example.com/images/dress_1.jpg", "https://example.com/images/dress_2.jpg"], "category": "Women's Clothing", "key_words": ["dress", "fashion", "elegant", "slim-fit", "women's clothing"]}
   {"item_id": "product_002", "name": "Stylish Windbreaker Jacket", "price": 312.00, "current_price": 300.00, "description": "Perfect for any occasion.", "images": ["https://example.com/images/jacket_1.jpg", "https://example.com/images/jacket_2.jpg"], "category": "Men's Clothing", "key_words": ["fashion", "stylish", "jacket", "men's clothing"]}
   ```
   
   
   
   </Tab>
   <Tab zoneid="iVFz2PPF2U" title="Paste JSON data">
   <TabTitle>Paste JSON data</TabTitle>
   
   **Paste JSON data**
   
   Paste one or more image & text data entries using the JSON Object (or Array of Objects) format. It is recommended to paste fewer than 100 records at a time. You must follow standard JSON formatting during input.
   
   The example below demonstrates the required standard JSON format:
   
   ```JSON
   {
     "item_id": "product_xxx",
     "name": "New Fashion Dress",
     "price": 299.00,
     "current_price": 249.00,
     "description": "Elegant and slim-fit, suitable for various occasions.",
     "images": [
       "https://example.com/images/dress_1.jpg",
       "https://example.com/images/dress_2.jpg"
     ],
     "category": "Women's Clothing",
     "keywords": ["dress", "fashion", "elegant", "slim-fit", "women's clothing"]
   }
   ```
   
   
   
   </Tab>
   </Tabs>
   



&nbsp;

4. After completing the upload or input, click **`Next: Configure Fields`** to proceed to the Data Configuration section.


&nbsp;

<span id="60748fd2"></span>
## Step 3: Add Fields (Optional)

The platform will automatically identify most data fields based on the sample data you uploaded. However, in certain cases, you may wish to add fields manually. The platform provides the following two methods for manual field addition:

&nbsp;

**Method 1**: Click the blue  **`+ Add Field`** button located at the bottom of the field list to add a new field.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/f446f5b8457f420bb0f60fd66baa4d6a) </span>

&nbsp;

**Method 2**: For fields with data types of **Object** or **Object Array**, you can click the  **`+`**  ** button** next to the field name in the corresponding row. This allows you to add the individual nested fields contained within that object (or within the objects of the array) and specify information such as the name and type for these nested fields.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">The platform currently supports nested objects with <strong>a maximum depth of 3 levels</strong>.</div>


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/92fcaf9927ac4e7798a4e3872d54ca35) </span>

&nbsp;

<span id="071b916a"></span>
## Step 4: Delete Fields (Optional)

During the process of configuring your dataset structure, if you find that certain fields are redundant, no longer needed, or were incorrectly identified during initial parsing, you can remove them from the data configuration.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">Deleting a field will remove all of its associated configuration information immediately.</div>



&nbsp;

1. In the field list, locate the field you want to delete. Click the **`delete`** ** button** at the far right of the row for that field to remove it.


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/e08e801cb9254b6ab2e654f84df770a5) </span>

&nbsp;

<span id="ce6ddfdf"></span>
## Step 5: Configure Field Attributes

The system automatically identifies and pre\-fills the dataset description, field names, field types, and field attributes based on the uploaded sample data. Please review these auto\-generated configurations.

In the field list, find the row for the field you wish to configure, click the dropdown menu under the  **"Field Attributes"**  column, and check one or more applicable attributes (such as "Unique Identifier," "Image URL," etc.).

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/8c51f66575f9489aab420e7ae4ba12a1) </span>

&nbsp;

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">Field attributes are used by downstream tasks and <strong>cannot be changed</strong> once configured. Please ensure the accuracy of your attribute settings before saving.</div>



|**Attribute** |**Mandatory?**  |**Supported Field Type(s)**  |**Attribute Description** |
|---|---|---|---|
|**Item ID (unique identifier)**  |Mandatory |String |The unique identifier for a single piece of data, which is the primary key. In search and recommendation scenarios, a different item ID represents a different "candidate".<br><br>A **data schema must contain exactly one unique identifier.** <br><br><br>* Supports upload as a **String** type.<br><br>* Only an outermost, non\-nested field is supported as the unique identifier. |
|**Title** |Optional |String |A field storing the title or name of the item. Applicable to product names, content or article titles, etc.<br><br>It is recommended to upload this information, as it serves as core semantic information for search and personalised recommendations. |
|**Image URL**<br><br> |Optional |String, Array<String\> |This field stores image URLs. After uploading data, the system automatically pulls images and extracts visual features for multimodal understanding. To use URLs for multimodal search, the field must be marked as an Image URL attribute. <br><br>Supports both single string and string array fields. |
|**Image Base64** |Optional |String, Array<String\> |This field stores image Base64 strings (or a list). |
|**Category** |Optional |String |The field stores the category or classification to which the item belongs.<br><br>It is recommended to upload this attribute in product data. Category information serves as a core data feature for search and recommendation, and the conversational assistant uses it to intelligently filter categories based on user queries during the decision\-making process.<br><br>Multiple classification attributes can be uploaded. If your product belongs to multiple categories (e.g., Level 1, Level 2 categories), you can use different fields to upload them. |
|**Publish Time (Date/Time Format)**  |Optional |String |Stores the publish or listing time of the item in date\-time format, used for sorting by newness in search and recommendation. <br><br>Supports the following formats:<br><br><br>* Standard ISO date\-time strings (`YYYY-MM-DDThh:mm:ss+08:00`).<br><br>* Non\-standard date\-time strings (`YYYY-MM-DD hh:mm:ss` or date\-only strings). The system will automatically convert these to standard format. |
|**Publish Time (UNIX Timestamp, Seconds)**  |Optional |Int64 |Item publish time represented by a standard 10\-digit UNIX timestamp, used for freshness ranking in search and recommendation. |
|**Publish Time (UNIX Timestamp, Milliseconds)**  |Optional |Int64 |Item listing time represented by a standard 13\-digit UNIX timestamp, used for freshness ranking in search and recommendation. |
|**Geographical Location \- Longitude** |Optional |Float or String |Longitude and latitude information used to identify the location of an item. Supports configurations for the following field types:<br><br><br>* Single JSON object: `"location":{"lat":"12.709","long":"30.281"}`.<br><br>* JSON object array for multiple locations: `"location":[{"lat":"12.709","long":"30.281"},{...}]`. The system will select the maximum or minimum distance for calculations based on strategies.<br><br><br>&nbsp;<br><br>Supports both Float or String representation (e.g., `"30.281"` or `30.281`). |
|**Geographical Location \- Latitude** |Optional |Float or String ||


<span id="d18e38a1"></span>
## Step 6: Synthesize New Fields with LLM (Optional)

After completing the basic field configuration of your dataset, we offer an advanced feature powered by AI Large Language Models:  **"Synthesize New Fields with LLM."**  This is designed to help you further tap into the potential of your existing data and achieve data enrichment.

This feature can generate entirely new, high\-value text fields based on existing fields in your dataset. Examples include generating image and text descriptions, extracting core keywords, or creating relevant user query lists. These AI\-generated fields are integrated directly into the dataset, effectively enhancing search results and autocomplete performance, thereby improving the overall discoverability and utility of your data.

**Note:**  This is an optional advanced optimization and is **not a mandatory step** for creating a dataset. If you are interested in using AI to automatically enrich your data and want to learn how to enable, configure, and use this feature, please refer to the [Synthesize New Fields using Large Language Models](https://docs.byteplus.com/docs/viking-aisearch/92185) chapter for detailed instructions and explanations.

&nbsp;

<span id="7bf9fa2f"></span>
## Step 7: Create Dataset


1. Before clicking the **`Complete Configuration`** button, you have the option to check **`Save Sample Data`** to include the uploaded sample in your dataset. If checked, the sample file data used during the upload step will be formally stored in this dataset. If left unchecked, the data will only be used for configuration purposes and will not be saved.

2. Click **`Complete Configuration`** to successfully create the dataset.

3. Once the configuration is complete and activated, the system will automatically begin analyzing the semantic information and processing the index.


&nbsp;


---



<span id="f8c22fb6"></span>
# View Dataset

Once the Image & Text dataset is created, you can find it in the **Datasets ** page. On the Dataset Details page, you can view its basic information, field configurations, and operation history.


1. After successfully creating the Image/Text dataset, return to the **Datasets** page to view the newly created item dataset.


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/0994dbb840fd43ebb293d9a468bbe1fe) </span>


&nbsp;

2. In the Dataset List, locate the dataset you wish to view and click the **`View`** button in the "Action" column.



&nbsp;

3. **Dataset Details Page**: Once you enter the details page, you will see several key tabs:

   * **Configuration:**  This tab allows you to view and adjust various configuration parameters for the current dataset.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">Note      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Changes made to the dataset configuration on this page require your manual confirmation and activation before syncing to the item dataset linked to your AI search app and updating the index configuration.      </div>
      

   * **Data preview: ** This tab allows you to check the status of image/text data validation and processing. You can also view the timestamps for data imports and recent updates, as well as preview the data. 

      * For a detailed introduction to data details, please refer to [View Data Details](https://docs.byteplus.com/docs/viking-aisearch/View_Data_Details).

   * **Activity history: ** You can view all key operations performed on the dataset, such as configuration changes and data import tasks. This allows you to track the modification history of the dataset. 

      * In addition to the Dataset Details page, you can also view the history by clicking the **`Activity history`** button in the "Action" column for the corresponding dataset on the Dataset List page.

   * **Import Data:**  On top right corner, you can add more data.

      * For detailed data import procedures and format requirements, please refer to the [Import and Update Item Data in Real Time](https://docs.byteplus.com/docs/viking-aisearch/92214)


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/a8e24e3e4d0342ad8c16230e17f44e3f) </span>

&nbsp;
